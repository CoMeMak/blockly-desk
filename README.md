# Blockly-Desk
Blockly-Extention for Franka Emika Desk

Blockly is a visual programming tool developed by Google for enabling people to learn the basics of computer programming. Desk is the visual programming environment provided by Franka Emika for enabling the teach-in of their Panda collaborative robot (short cobot).

Desk is a simplified task-oriented programming environment designed to get you started quickly with the Panda cobot. The basic apps (i.e., configurable software functions designed for different types of robot movements and interoperability with external hardware) provided can arranges in a sequence to produce an assembly workflow. Both user interaction (through tapping) and interaction with external hardware (e.g., via MODBUS) is supported. Panda's strongest point is its simple and intuitive way of teaching movements, which is supported by its intuitive programming environment Desk. 

The Blockly-Desk extension enables Panda programmers to leverage Desk and the existing capabilities of Blockly as well as to add new blocks in connection with the robot's abilities. Robot-specific blocks may be regarded as meta-apps, which can orchestrate existing tasks in Desk as well as the creation of new tasks and the automated configuration of apps provided in Desk. 

The working principle is that of JavaScript code generation using Blockly and injection into Desk via a so-called bookmarklet (https://en.wikipedia.org/wiki/Bookmarklet). A bookmarklet is a browser bookmark containing JavaScript code, which can be injected into the currently opened webside in a browser tab. Since Desk is a web-based application, the bookmarklet technique can also be used to manipulate the HTML elements and events used by Desk to enable the creation, configuration, and orchestration of tasks and apps. Think of is as of a macro-style way of automating some of the tasks one would have to carry out manually and repeatedly for some purpose on a website, such as editing, clicking away unwanted content, or priventing it alltogether. This programming style is currently used, for example, to test websites and there are entire test-suites, which build upon this simple code injection and meta-orchestration technique--not to mention the well-known Add Blocker or Mendeley's bookmarking tool (https://www.mendeley.com/reference-management/web-importer#id_3).   

Here's how it's supposed to work:

![alt text](https://raw.githubusercontent.com/comemak/blockly-desk/master/desk.png)
