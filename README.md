# Blockly-Desk
## A Blockly-Extention for Franka Emika Desk

Blockly is a visual programming tool developed by Google for enabling people to learn the basics of computer programming. Desk is the visual programming environment provided by Franka Emika for enabling the teach-in of their Panda collaborative robot (short cobot).

Desk is a simplified task-oriented programming environment designed to get you started quickly with the Panda cobot. The basic apps (i.e., configurable software functions designed for different types of robot movements and interoperability with external hardware) provided can arranges in a sequence to produce an assembly workflow. Both user interaction (through tapping) and interaction with external hardware (e.g., via MODBUS) is supported. Panda's strongest point is its simple and intuitive way of teaching movements, which is supported by its intuitive programming environment Desk. 

The Blockly-Desk extension enables Panda programmers to leverage Desk and the existing capabilities of Blockly as well as to add new blocks in connection with the robot's abilities. Robot-specific blocks may be regarded as meta-apps, which can orchestrate existing tasks in Desk as well as the creation of new tasks and the automated configuration of apps provided in Desk. 

The working principle is that of JavaScript code generation using Blockly and injection into Desk via a so-called bookmarklet (https://en.wikipedia.org/wiki/Bookmarklet). A bookmarklet is a browser bookmark containing JavaScript code, which can be injected into the currently opened webside in a browser tab. Since Desk is a web-based application, the bookmarklet technique can also be used to manipulate the HTML elements and events used by Desk to enable the creation, configuration, and orchestration of tasks and apps. Think of is as of a macro-style way of automating some of the tasks one would have to carry out manually and repeatedly for some purpose on a website, such as editing, clicking away unwanted content, or priventing it alltogether. This programming style is currently used, for example, to test websites and there are entire test-suites, which build upon this simple code injection and meta-orchestration technique--not to mention the well-known Add Blocker or Mendeley's bookmarking tool (https://www.mendeley.com/reference-management/web-importer#id_3).   

## Here's how it's supposed to work

### Writing a Panda program in Blockly

Download blockly-desk.zip, then unzip it, find **your_folder/blockly/demos/code/index.html**, and open it in a browser (currently, only tested in Chrome).

Under the menu item "Franka" you'll find a choice of five blocks (disregard the first block called **Precondition** for now):

![alt text](https://raw.githubusercontent.com/comemak/blockly-desk/master/franka_tasks.png)  

There are two **Task** blocks and two **Move** blocks having the following capabilities:
* The first Task block is used to trigger an existing Task created in Desk. Just type in the name of the desired task in the field (case sensitive--I think).
* The second Task block can be used for the same purpose but here you need to define a "pattern" variable containing the name of the task instead of a fixed string. This is useful when varying the task names within a loop, for example. 
* The first Move block will creat a new task in Desk, add a **Relative Motion** app to it, and configure it so as to carry out the desired relative motion. By default we configure it to use the end effector (EE) frame of reference.
* The second Move task will use variables for x,y,z. This allows you to programatically move to places where the arm has never been before! No teach-in required. 

**Note:** The Move blocks will generate new tasks in Desk. Their names will reflect the x,y,z coordinates of the movement. If a task with that name already exists in Desk, then no additional task will be created since it is assumed that it will do the job. This situation will occur whenever you call that same relative move task multiple times in a program or when some other program has already created it. At some point, however, you might need to delete some of the "zombie" tasks from the list for the purpose of restoring the world order.  

### Generating the bookmarklet

Click on the red button on the upper-right side of Blockly. This will generate a link, as shown in the picture below, which you can drag to the bookmarks bar. This is the bookmarklet containing the JavaScript code to be injected into Desk. You can have a look at it by copying its content and pasting it into a code editor, like Notepad++. Save the file using the .js extension for syntax highlighting. 

![alt text](https://raw.githubusercontent.com/comemak/blockly-desk/master/blockly.png)

### Executing the program contained in the bookmarklet

Now open another browser tab and type robot.franke.de (or just switch to it if it's already open). To run the program, the safety button should not be pushed down and the robot should be initialized. Then make sure you are connected to the Internet. This is needed to download the jQuery library on the fly. jQuery is used by the generated code to trigger tasks and actions in Desk. 

The figure below illustrates what will happen when you click on one of the bookmarklets. The JavaScript program generated in Blockly will execute the tasks in a sequence, by loading them and then programatically clicking on the **RUN** button in Desk by triggering a click event on a specific HTML item. Behind the scenes, a state machine will monitor this button to determine whether the current task has finished before calling another one.

![alt text](https://raw.githubusercontent.com/comemak/blockly-desk/master/desk.png)

### What's next?

If you get it running, Blockly-Desk will enable you to use the full palette of program structures offered in Blockly by default and create blocks of your own. This is described in detail on the Blockly website (https://developers.google.com/blockly/). If you develop a new block, why not share it with the community? You can do it using JSFiddle (https://jsfiddle.net/), for example, and then let us know somehow about it.

### A closing word


