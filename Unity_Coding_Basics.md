## Basics of coding in Unity

    using System.Collections;
    using System.Collections.Generic;
    using UnityEngine;
    
    public class NewBehaviourScript : MonoBehaviour
    {
        // Start is called before the first frame update
        void Start()
        {
            
        }
    
        // Update is called once per frame
        void Update()
        {
            
        }
    }


### Libraries
Libraries, also called namespaces, are collections of related classes and functions that you can use in your code. In Unity, the most common library you'll use is the UnityEngine namespace, which provides access to many of Unity's built-in functions and classes. You can include a library by adding a using statement at the top of your code file, like this:

    using UnityEngine;
    
This allows you to use any class or function within the UnityEngine namespace without needing to fully qualify its name.


### MonoBehaviour
In Unity, MonoBehaviour is a special class that serves as the base class for most scripts that control the behavior of game objects. MonoBehaviour provides several built-in functions and variables that allow you to interact with the game object that the script is attached to, as well as the Unity engine as a whole.

    public  class  MyScript : MonoBehaviour

 - Component Attachment: To use a script in Unity, you typically need to
   attach it to a game object as a component. When you attach a
   MonoBehaviour script to a game object, it gains access to all of the
   features provided by the MonoBehaviour class. 
- Built-in Functions: MonoBehaviour provides several built-in functions that are called
   automatically by the Unity engine at specific times. For example, the
   Start function is called once when the game object is first created,
   while the Update function is called every frame. You can override
   these functions to add custom behavior to your script. 
- Variables: MonoBehaviour provides several built-in variables that allow you to
   interact with the game object and the Unity engine. For example, the
   transform variable provides access to the game object's position,
   rotation, and scale, while the gameObject variable provides a
   reference to the game object itself. 
-  Lifecycle Management: MonoBehaviour provides several functions that allow you to manage the
   lifecycle of a game object. For example, the Destroy function can be
   used to destroy a game object, while the Instantiate function can be
   used to create a new game object from a prefab.

### Variables
Variables are used to store data in your code. In C#, you can declare a variable by specifying its data type, followed by its name. For example, you might declare an integer variable like this:

    int myNumber = 5;

 - int: A whole number variable that can be positive, negative, or zero.
   Examples include health, score, or number of lives.
   
 -  float: A decimal number variable that can be positive, negative, or
   zero. Examples include speed, gravity, or jump height.
   
-   bool: A boolean variable that can be either true or false. Examples
   include isGrounded, isJumping, or isAlive.
   
-   string: A sequence of characters that represent text. Examples
   include playerName, dialogue, or levelName.
   
 -  Vector2 and Vector3: Variables that represent a direction or position
   in 2D or 3D space, respectively. Examples include playerPosition,
   enemyDirection, or bulletVelocity.
   
-   GameObject: A variable that holds a reference to a Unity game object.
   Examples include player, enemy, or powerup.
   
-   Transform: A variable that holds a reference to the transform
   component of a game object. Examples include playerTransform,
   enemyTransform, or powerupTransform.

### Start and Update Functions

These are two special functions that are included in every Unity script. The Start function is called once when the script is first enabled, while the Update function is called every frame. You can use these functions to initialize variables, update game object positions, and respond to user input.

    void Start() 
    { 
	    // This code runs once when the script is first enabled 
	    Debug.Log("Hello, world!"); 
    } 

    void Update() 
    { 
	    // This code runs every frame 
	    transform.Rotate(Vector3.up, Time.deltaTime * 10.0f); 
    }

In the Start method, we've added a simple log message using Unity's Debug.Log function. This message will be printed to the console once when the script is first enabled.

In the Update method, we've added some code to rotate the game object around its Y-axis. This code uses the transform.Rotate function to apply a rotation to the game object's transform component every frame. The rotation is based on the Time.deltaTime variable, which ensures that the rotation speed remains constant regardless of the frame rate.

There are also some more special functions such as Awake and FixedUpdate, which we'll go more into detail later on. 

### Methods
Methods are functions that perform a specific task in your code. In C#, you can declare a method by specifying its return type (if it has one), followed by its name and any parameters it takes. For example, you might declare a method like this:

    void  MyMethod() 
    { 
    // Code to execute when the method is called 
    }
    
This creates a new void method named "MyMethod" that takes an integer parameter named "myParameter". When the method is called, it will execute the code inside its curly braces.

### Comments
Comments are text that are added to a script but are ignored by the compiler. They are used to explain what a piece of code does, provide context or reminders to the script's author, or to temporarily disable a piece of code. In C#, you can create a single-line comment by starting the line with two forward slashes (//), or a multi-line comment by enclosing the comment text in /* and */

    // This is a comment

    /*
    This
    is
    a
    long
    comment
    */


## Example

    using UnityEngine;
    
    public class PlayerController : MonoBehaviour
    {
        // Variables
        public float speed = 10.0f;
        public float jumpForce = 5.0f;
        private Rigidbody rb;
    
        // Start function
        void Start()
        {
            // Get a reference to the Rigidbody component
            rb = GetComponent<Rigidbody>();
        }
    
        // Update function
        void Update()
        {
            // Move the player left/right using the horizontal axis
            float moveHorizontal = Input.GetAxis("Horizontal");
            Vector3 movement = new Vector3(moveHorizontal, 0.0f, 0.0f);
            rb.AddForce(movement * speed);
    
            // Jump the player when the space bar is pressed
            if (Input.GetKeyDown(KeyCode.Space))
            {
                Jump();
            }
        }
    
        // Custom method
        void Jump()
        {
            Vector3 jumpVector = new Vector3(0.0f, jumpForce, 0.0f);
            rb.AddForce(jumpVector, ForceMode.Impulse);
        }
    }

This script defines a player controller in Unity, which can be attached to a player game object. Here's an explanation of each part of the script:

1.  `using UnityEngine;`: This line tells the compiler to include the Unity engine libraries, which provide access to Unity's built-in functions and classes.
    
2.  `public class PlayerController : MonoBehaviour`: This line defines a new class called `PlayerController`, which inherits from the `MonoBehaviour` base class. This means that our class can be used as a script component in Unity, and will have access to all of the built-in functions and variables provided by `MonoBehaviour`.
    
3.  `public float speed = 10.0f;`: This line defines a public float variable called `speed`, which has a default value of `10.0f`. This variable determines how fast the player can move left and right.
    
4.  `public float jumpForce = 5.0f;`: This line defines a public float variable called `jumpForce`, which has a default value of `5.0f`. This variable determines how high the player can jump.
    
5.  `private Rigidbody rb;`: This line defines a private variable called `rb`, which holds a reference to the `Rigidbody` component attached to the player game object.
    
6.  `void Start()`: This line defines an override of the `Start` function, which is called once when the script is first enabled. In this function, we get a reference to the `Rigidbody` component by calling the `GetComponent` function and storing the result in the `rb` variable.
    
7.  `void Update()`: This line defines an override of the `Update` function, which is called every frame by Unity's engine. In this function, we move the player left and right based on the horizontal input axis (`Input.GetAxis("Horizontal")`), which returns a value between -1 and 1. We then create a new `Vector3` variable called `movement` to represent the player's movement direction, and use the `AddForce` function on the `rb` variable to move the player in that direction at the specified speed. We also check if the space bar is pressed (`Input.GetKeyDown(KeyCode.Space)`), and if it is, we call the `Jump` function.
    
8.  `void Jump()`: This line defines a custom method called `Jump`, which is called when the player jumps. In this function, we create a new `Vector3` variable called `jumpVector` to represent the force
