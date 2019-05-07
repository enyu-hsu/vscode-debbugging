# VS Code Debbugging Environment for Python
This is a guide to help you setup the VS Code debugging environment for Python locally and remotely, and is based on VS Code's documents on [debugging](https://code.visualstudio.com/docs/editor/debugging) and [Python debug configuration](https://code.visualstudio.com/docs/python/debugging).

## Install VS Code
You can download VS Code [here](https://code.visualstudio.com/).

## Setup Debugging Configuration for Python
Click on the debug icon in the sidebar.

![debug_icon](images/debug_icon.png)

If you don't have any configuration yet, you will see "No Configurations". Click on the setting icon on the right to create one.

![no_configuration](images/no_configuration.png)

A configuration menu will show up, choose **Python File**.

![python_configuration](images/python_configuration.png)

This will create and open a `launch.json` file with default configuration located in a `.vscode` folder in your workspace (project root folder). You can modify or add custom configurations here. For more configuration options, checkout the [official document](https://code.visualstudio.com/docs/python/debugging#_set-configuration-options).

## Launch versus Attach configuration
In VS Code, there are two ways to perform debugging actions, **Launch** and **Attach**. You may think of **launching** is to start your program in debug mode, and **attaching** is to attach the VS Code debugger to an **already** running process.

You may choose the way you prefer by setting the `"request"` argument to `"launch"` or `"attach"` in `launch.json`.

## Launching a Program in Debug Mode
With default configuration, you can launch a Python program locally in debug mode. Simply press `F5` to enter debug mode. The status bar below will turn orange and show the active launch configuration once you successfully enter debug mode.

![debug_mode](images/debug_mode.png)

For other kinds of breakpoints(such as conditional breakpoint, function breakpoint...), checkout [here](https://code.visualstudio.com/docs/editor/debugging#_advanced-breakpoint-topics).
