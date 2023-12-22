# vim-clone
My CS 246E Project (Creating a VM, a Vim clone). For Academic Integrity Reasons, the codebase will not be displayed in this repository, although could be granted upon request.

# Design
The project is structured on the Model-View-Controller (MVC) architecture, where each component (the model, view and controller) is built to handle a specific area of the applications.

The overall interaction between the three components is minimal; the Controller gets the keyboard input from the users, the Model is responsible for handling all the different logic (like computing the changes to the doc, the cursor position, etc) and the View is responsible for displaying the terminal output to the user. To communicate between each component, the project follows the observer pattern and updates a state object with whatever needs to be communicated. 

For the project, communication only occurs when it is absolutely necessary. For instance, when there is new user input, the Controller notifies the Model, and when the Model is done calculating the logic, it communicates with the View.

### Controller
In regards to each component of the MVC architecture, the simplest of the three in my project is the Controller. There is one class that is responsible for awaiting and getting user input. After receiving input, the Controller notifies the Model of the input for processing. 

### Model
The Model is the central component of my project and is responsible for the logic behind the application. The central class in the middle of my project is the VMModel class, which contains several objects. First, it contains a File Handler object that is responsible for reading the initial text as well as file saving. 

Next, it contains 4 objects of subclasses of the Mode object which are responsible for parsing the user input. Based on the mode, the way that the user input is parsed is different. Each Mode object returns a subclass object of the Action class, which is responsible for making the necessary changes based on the user input. However, the Action objects do not actually manipulate the text themselves or move the cursors. 

For file manipulation and cursor movement, the Model class owns a File object that makes the necessary edits based on the parsed input. The Action objects simply connect the Model to the File. Such a design allows for more decoupling and more customizability. 

 ### View
For the actual display of the text editor, the View utilizes the decorator design pattern, where a class initializes and sets up the basic window, another class prints out the contents of the text file, and a final class displays the Vim-like status bar to the user. The use of this pattern allows for dynamic-time updating while adhering to the Single Responsibility Principle. 

### Example Preview:

![image](https://github.com/richardsha19/vim-clone/assets/113735719/786dd786-3693-4d6e-9f14-23b8f761145d)


