# DODGER-GAME-OOP
Coursework Report: Dodger Game Application
Object-Oriented Programming - Python App

Student Name: [Your Name]
Student ID: [Your Student ID]
Course: [Your Course Name]
Instructor: [Your Instructor's Name]
Date: May 6, 2025

1. Introduction
1.1 Purpose and Objectives of the Application
The primary purpose of this coursework is to design and implement a simple "Dodger" game using the principles of Object-Oriented Programming (OOP) in Python, leveraging the Pygame library for graphics and event handling. The objectives of this application are to:

Demonstrate understanding and application of core OOP concepts such as classes, objects, encapsulation, and potentially inheritance (if expanded).
Develop a functional and interactive game where the player controls an entity to avoid incoming obstacles.
Implement game logic for player movement, obstacle generation, collision detection, and scoring.
Utilize the Pygame library for creating a visual game environment and handling user input.
Structure the codebase in a modular and organized manner using classes.
1.2 Brief Overview of Chosen Project
The chosen project is a graphical "Dodger" game where the player controls a rectangular entity at the bottom of the screen. Obstacles (also rectangular) fall from the top of the screen, and the player must move left or right to avoid colliding with them. The game continues, increasing in difficulty over time (potentially through faster obstacle speed or increased spawn rate), until the player collides with an obstacle, at which point the game ends, and the final score is displayed. This project was selected to demonstrate the application of OOP principles in a graphical game development context using Pygame.

2. Problem Definition and Requirements
2.1 Description of the Problem Your Application Solves
The application addresses the problem of providing a simple and engaging arcade-style game where the user can test their reflexes and dodging skills. It offers a basic but interactive gaming experience with visual feedback, score tracking, and a clear win/lose condition. The application serves as a practical example of using Python and Pygame to create a game with user interaction, animation, and basic game mechanics, structured using object-oriented principles.

2.2 Functional and Non-Functional Requirements
Functional Requirements:

Player Control: The application must allow the user to control the horizontal movement of a player entity using keyboard input (left and right arrow keys).
Obstacle Generation: The application must generate obstacles that fall from the top of the screen at random horizontal positions.
Obstacle Movement: The generated obstacles must move downwards towards the bottom of the screen.
Collision Detection: The application must detect collisions between the player entity and the falling obstacles.
Game Over Condition: The game must end when a collision occurs between the player and an obstacle.
Score Tracking: The application must keep track of the player's score, which increases as the player successfully avoids obstacles.
Score Display: The application must display the current score during gameplay and the final score upon game over.
Game Restart: The application should provide a mechanism for the user to restart the game after a game over.
Non-Functional Requirements:

Usability: The game controls should be responsive and intuitive.
Performance: The game should run smoothly at a reasonable frame rate.
Maintainability: The codebase should be well-structured using classes and methods to facilitate future modifications.
Readability: The code should be well-commented and use meaningful variable and function names.
Robustness: The game should handle user input and game events without crashing.
Visual Presentation: The game should have a clear and understandable visual representation of the player, obstacles, and score.
3. Design and Implementation
3.1 Object-Oriented Design Principles Used
The application's design leverages several key object-oriented programming principles:

Encapsulation: Data (attributes like position, size, speed) and the methods that operate on that data are bundled within classes (Player, Obstacle, Game). This keeps the code organized and prevents direct manipulation of internal states from outside the class.
Abstraction: Complex behaviors, such as updating the position of an obstacle or detecting a collision, are encapsulated within methods, providing a simpler interface for the main game loop to interact with these objects.
Class and Object: The game is built around the creation of classes (Player, Obstacle, Game) that serve as blueprints for the game entities. Instances (objects) of these classes are created and managed by the Game class to represent the active elements in the game.
3.2 Class Diagrams and Structure
A simplified class diagram for the application is as follows:

Code snippet

classDiagram
    class Game {
        -screen_width: int
        -screen_height: int
        -screen: Surface
        -player: Player
        -obstacles: list
        -score: int
        -font: Font
        -obstacle_spawn_rate: int
        -obstacle_spawn_counter: int
        -running: bool
        -game_over: bool
        +__init__()
        +spawn_obstacle(): void
        +update_obstacles(): void
        +check_collision(): bool
        +display_score(): void
        +game_over_screen(): bool
        +run(): void
    }
    class Player {
        -size: int
        -x: int
        -y: int
        -speed: int
        +__init__(screen_width: int, screen_height: int)
        +move(keys: list): void
        +draw(screen: Surface): void
        +get_rect(): Rect
    }
    class Obstacle {
        -size: int
        -x: int
        -y: int
        -speed: int
        +__init__(screen_width: int)
        +update(): void
        +draw(screen: Surface): void
        +get_rect(): Rect
    }
    Game --|> Player : has a
    Game --|> Obstacle : has many
Class Structure:

Game Class:

Attributes:
screen_width, screen_height: Dimensions of the game window.
screen: The Pygame Surface representing the game display.
player: An instance of the Player class.
obstacles: A list to store instances of the Obstacle class.
score: An integer to track the player's score.
font: A Pygame Font object for displaying text.
obstacle_spawn_rate, obstacle_spawn_counter: Variables to control obstacle spawning frequency.
running, game_over: Boolean flags to manage the game state.
Methods:
__init__(): Constructor to initialize the game environment, player, and other game variables.
spawn_obstacle(): Creates a new Obstacle object and adds it to the obstacles list.
update_obstacles(): Iterates through the obstacles list, updates their positions, and removes obstacles that have gone off-screen.
check_collision(): Checks for collisions between the player's rectangle and any of the obstacle rectangles.
display_score(): Renders and draws the current score on the screen.
game_over_screen(): Displays the game over message and final score, and handles the restart option.
run(): Contains the main game loop, handling events, updating game state, and drawing objects.
Player Class:

Attributes:
size: The size (width and height) of the player rectangle.
x, y: The current coordinates of the player.
speed: The speed at which the player moves.
Methods:
__init__(screen_width, screen_height): Constructor to initialize the player's size, position (at the bottom center), and speed.
move(keys): Updates the player's x coordinate based on the pressed arrow keys, ensuring the player stays within the screen bounds.
draw(screen): Draws the player rectangle on the given screen surface.
get_rect(): Returns a Pygame Rect object representing the player's current position and size, used for collision detection.
Obstacle Class:

Attributes:
size: The size (width and height) of the obstacle rectangle.
x, y: The current coordinates of the obstacle.
speed: The speed at which the obstacle falls.
Methods:
__init__(screen_width): Constructor to initialize the obstacle's size, a random horizontal x position at the top of the screen (y is initially negative), and its speed.
update(): Updates the obstacle's y coordinate to move it downwards.
draw(screen): Draws the obstacle rectangle on the given screen surface.
get_rect(): Returns a Pygame Rect object representing the obstacle's current position and size, used for collision detection.
3.3 Key Algorithms and Data Structures Implemented
Random Obstacle Generation: The random.randint() function is used in the Obstacle.__init__() method to determine the initial random horizontal position of each new obstacle.
Obstacle Movement: The Obstacle.update() method increments the obstacle's y coordinate in each game loop iteration, creating the falling effect.
Collision Detection: The pygame.Rect.colliderect() method is used in the Game.check_collision() method to efficiently determine if the player's rectangle intersects with any of the obstacle rectangles.
Score Tracking: An integer variable score in the Game class is incremented each time an obstacle successfully passes the player without collision.
Data Structures:
List (obstacles): Used in the Game class to store multiple Obstacle objects that are currently active in the game. This allows for managing and updating multiple falling obstacles simultaneously.
Pygame Rect Objects: Used to represent the player and the obstacles, facilitating easy drawing and collision detection using Pygame's built-in functionalities.
4. Development Process
4.1 Tools and Environment
Operating System: [Your Operating System, e.g., Windows 10, macOS Big Sur, Linux Ubuntu]
Programming Language: Python 3.x
Game Development Library: Pygame (version [Your Pygame Version])
Integrated Development Environment (IDE) / Text Editor: [Your IDE/Text Editor, e.g., PyCharm, VS Code, Sublime Text]
Version Control System (Optional but Recommended): Git with a repository on [e.g., GitHub, GitLab, Bitbucket] was [or was not] used for version control.
4.2 Steps Followed During Development
Project Setup and Pygame Initialization:

Created a new Python project.
Installed the Pygame library.
Initialized Pygame and set up the game window (screen dimensions, caption).
Player Class Implementation:

Created the Player class with its attributes (size, position, speed).
Implemented the __init__() method to initialize the player.
Implemented the move() method to handle player movement based on keyboard input.
Implemented the draw() method to render the player on the screen.
Implemented the get_rect() method to obtain the player's bounding rectangle.
Obstacle Class Implementation:

Created the Obstacle class with its attributes (size, position, speed).
Implemented the __init__() method to initialize the obstacle with a random horizontal position.
Implemented the update() method to make the obstacle move downwards.
Implemented the draw() method to render the obstacle on the screen.
Implemented the get_rect() method to obtain the obstacle's bounding rectangle.
Game Class Implementation:

Created the Game class with its attributes (screen, player, obstacles, score, etc.).
Implemented the __init__() method to initialize the game environment and create the player object.
Implemented the spawn_obstacle() method to create new obstacles at a set interval.
Implemented the update_obstacles() method to move existing obstacles and remove off-screen ones.
Implemented the check_collision() method to detect collisions between the player and obstacles.
Implemented the display_score() method to show the current score.
Implemented the game_over_screen() method to display the game over message and handle restarting.
Implemented the run() method containing the main game loop, which handles events, updates game state, and draws all game elements.
Game Loop and Logic Integration:

Integrated the player movement, obstacle spawning, obstacle movement, collision detection, and score updates within the main game loop in the Game.run() method.
Testing and Debugging:

Ran the game frequently during development to test individual components and the overall game flow.
Debugged any errors or unexpected behavior related to object movement, collision detection, or score tracking.
Ensured smooth frame rate and responsive controls.
Implemented the game over condition and the restart functionality.
Documentation:

Added comments to the code to explain the logic and purpose of different sections.
Prepared this coursework report to document the design, implementation, and testing process.
5. Results and Demonstration
5.1 Application Features
The implemented Dodger game application features:

A graphical window displaying the game environment.
A controllable player entity (a black rectangle) at the bottom of the screen.
Falling obstacle entities (red rectangles) appearing randomly from the top.
Smooth horizontal movement of the player controlled by the left and right arrow keys.
Downward movement of the obstacles.
Accurate detection of collisions between the player and the obstacles.
A game over state that is triggered upon collision.
Real-time tracking and display of the player's score (number of avoided obstacles).
A "Game Over" screen displaying the final score and an option to restart the game by pressing the SPACE key.

Player Control Testing: Verified that the player moves correctly in response to left and right arrow key presses and stays within the screen boundaries.
Obstacle Spawning and Movement Testing: Observed the frequency and randomness of obstacle spawning and ensured they move smoothly downwards.
Collision Detection Testing: Intentionally collided the player with obstacles from different angles and speeds to confirm that the collision is detected reliably and the game over state is triggered.
Score Tracking Testing: Played multiple game sessions, carefully counting the avoided obstacles to ensure the score increments correctly.
Game Over and Restart Testing: Confirmed that the game over screen appears after a collision and that pressing the SPACE key correctly restarts the game, resetting the score and obstacle list.
Performance Testing (Informal): Ensured that the game runs at a reasonable frame rate without significant lag or slowdowns.

6. Conclusion and Future Work
6.1 Summary of Achievements
This coursework successfully implemented a graphical "Dodger" game using object-oriented programming principles in Python with the Pygame library. The application effectively demonstrates the use of classes (Player, Obstacle, Game) to structure the game logic and manage game entities. It provides an interactive experience with player control, obstacle generation and movement, collision detection, and score tracking. The game includes a clear game over condition and a restart mechanism, fulfilling the core requirements of the project.
