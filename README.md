# Blockly-Desk
## A Blockly-Extention for Franka Emika Desk

Blockly is a visual programming tool developed by Google for enabling people to learn the basics of computer programming. Desk is the visual programming environment provided by Franka Emika for enabling the teach-in of their Panda collaborative robot (short cobot).

Desk is a simplified task-oriented programming environment designed to get you started quickly with the Panda cobot. The basic apps (i.e., configurable software functions designed for different types of robot movements and interoperability with external hardware) provided can arranges in a sequence to produce an assembly workflow. Both user interaction (through tapping) and interaction with external hardware (e.g., via MODBUS) is supported. Panda's strongest point is its simple and intuitive way of teaching movements, which is supported by its intuitive programming environment Desk. 

The Blockly-Desk extension enables Panda programmers to leverage Desk and the existing capabilities of Blockly as well as to add new blocks in connection with the robot's abilities. Robot-specific blocks may be regarded as meta-apps, which can orchestrate existing tasks in Desk as well as the creation of new tasks and the automated configuration of apps provided in Desk.  

## Here's how it's supposed to work

The working principle is that of JavaScript code generation using Blockly and injection into Desk via a so-called bookmarklet (https://en.wikipedia.org/wiki/Bookmarklet). A bookmarklet is a browser bookmark containing JavaScript code, which can be injected into the currently opened website in a browser tab. Since Desk is a web-based application, the bookmarklet technique can also be used to manipulate the HTML elements and events used by Desk to enable the creation, configuration, and orchestration of tasks and apps. Think of it as of a macro-style way of automating some of the tasks one would have to carry out manually and repeatedly for some purpose on a website, such as editing, clicking away unwanted content, or preventing it altogether. This programming style is currently used, for example, to test websites and there are entire test-suites, which build upon this simple code injection and meta-orchestration technique--not to mention the well-known Add Blocker or Mendeley's bookmarking tool (https://www.mendeley.com/reference-management/web-importer#id_3).  

### Writing a Panda program in Blockly

Download blockly-desk.zip, then unzip it, find **your_folder/blockly/demos/code/index.html**, and open it in a browser (currently, only tested in Chrome).

Alternatively, you can use this online Version: http://blockly-desk.comemak.at

Under the menu item "Franka" you'll find a choice of five blocks (disregard the first block called **Precondition** for now):

![alt text](https://raw.githubusercontent.com/comemak/blockly-desk/master/franka_tasks.png)  

There are two **Task** blocks and two **Move** blocks having the following capabilities:
* The first Task block is used to trigger an existing Task created in Desk. Just type in the name of the desired task in the field (case sensitive).
* The second Task block can be used for the same purpose but here you need to define a "pattern" variable containing the name of the task instead of a fixed string. This is useful when varying the task names within a loop, for example. 
* The first Move block will create a new task in Desk, add a **Relative Motion** app to it, and configure it so as to carry out the desired relative motion. By default we configure it to use the end effector (EE) frame of reference.
* The second Move task will use variables for x,y,z. This allows you to programmatically move to places where the arm has never been before! No teach-in required. 

![alt text](https://raw.githubusercontent.com/comemak/blockly-desk/master/blocks.png)

**Note:** The Move blocks will generate new tasks in Desk. Their names will reflect the x,y,z coordinates of the movement. If a task with that name already exists in Desk, then no additional task will be created since it is assumed that it will do the job. This situation will occur whenever you call that same relative move task multiple times in a program or when some other program has already created it. At some point, however, you might need to delete some of the "zombie" tasks from the list for the purpose of restoring the world order.  

### Generating the bookmarklet

Click on the red button on the upper-right side of Blockly. This will generate a link, as shown in the picture below, which you can drag to the bookmarks bar. This is the bookmarklet containing the JavaScript code to be injected into Desk. You can have a look at it by copying its content and pasting it into a code editor, like Notepad++. Save the file using the .js extension for syntax highlighting. 

![alt text](https://raw.githubusercontent.com/comemak/blockly-desk/master/blockly.png)

### Executing the program contained in the bookmarklet

Now open another browser tab and type robot.franke.de (or just switch to it if it's already open). To run the program, the safety button should not be pushed down and the robot should be initialized. Then make sure you are connected to the Internet. This is needed to download the jQuery library on the fly. jQuery is used by the generated code to trigger tasks and actions in Desk. 

The figure below illustrates what will happen when you click on one of the bookmarklets. The JavaScript program generated in Blockly will execute the tasks in a sequence, by loading them and then programmatically clicking on the **RUN** button in Desk by triggering a click event on a specific HTML item. Behind the scenes, a state machine will monitor this button to determine whether the current task has finished before calling another one.

![alt text](https://raw.githubusercontent.com/comemak/blockly-desk/master/desk.png)

### Demo video and conference paper

Here's a demo video showing Panda making some chess moves. Behind the scene a Blockly-generated bookmarklet orchestrates Desk. There are only 2-3 predefined tasks in the list (for opening and closing the gripper and for driving to the A1 position on the board). All other moves are generates dynamically. You can see this in the video whenever the robot is waiting for something--apparently thinking about the next move. During this time, a relative motion task is created automatically in Desk and configured with the parameters of the chess move--all relative to the thought-in A1 position.

Check out the video here: https://drive.google.com/file/d/1y_DA1puLOhRJROA1YBQ5Qt8xgNJ0bcaq/view?usp=sharing

And here is a conference paper describing the approach in more detail: https://github.com/CoMeMak/blockly-desk/raw/master/Blockly-Desk-CIRP-CMS.pdf

### What's next?

If you get it running, Blockly-Desk will enable you to use the full palette of program structures offered in Blockly by default and create blocks of your own. This is described in detail on the Blockly website (https://developers.google.com/blockly/). If you develop a new block, why not share it with the community? Let us know about it somehow! Thanks!

### Safety advice and disclaimer

Using the Panda robot and the Desk environment via the Blockly-Desk extension merely automates some of the tasks the user would need to carry out manually in order to achieve the same results. However, this extension might animate Desk and Panda in ways that may not be evident to you, at least not during the first run of a new program. So please stand by the robot at a safe distance, holding the safety stop button at any time while using the programs (i.e., bookmarklets) generated by Blockly-Desk. You can also use the Developer Tools provided by all modern browsers to monitor the automated execution of the tasks. If you encounter strage behavior by the robot, push the safety stop button first, then reload the Desk page in the browser and, if still necessary, click the task stop button in Desk. 

In any case, the authors of the Blockly-Desk extension will not assume responsibility for anything that may go wrong during this process.
