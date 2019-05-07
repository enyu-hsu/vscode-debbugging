# VS Code Debbugging Environment for Python
This is a guide to help you setup the VS Code debugging environment for Python locally and remotely, and is based on VS Code's documents on [debugging](https://code.visualstudio.com/docs/editor/debugging) and [Python debug configuration](https://code.visualstudio.com/docs/python/debugging).

## Install VS Code
You can download [VS Code](https://code.visualstudio.com/) here.

## Setup Debugging Configuration for Python
Click on the debug icon in the sidebar.

![debug_icon](images/debug_icon.png)

If you don't have any configuration yet, you will see "No Configurations". Click on the setting icon on the right to create one.

![no_configuration](images/no_configuration.png)

A configuration menu will show up, choose **Python File**.

![python_configuration](images/python_configuration.png)

This will create and open a `launch.json` file with default configuration located in a `.vscode` folder in your workspace (project root folder). You can modify or add custom configurations here. For more configuration options, checkout the [official document](https://code.visualstudio.com/docs/python/debugging#_set-configuration-options).

## Launching a Program in Debug Mode
With default configuration, you can launch a Python program locally in debug mode. Simply press `F5` to enter debug mode.

For other kinds of breakpoints(such as conditional breakpoint, function breakpoint...), checkout [here](https://code.visualstudio.com/docs/editor/debugging#_advanced-breakpoint-topics).
