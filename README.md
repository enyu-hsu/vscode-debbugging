# VS Code Debbugging Environment for Python
This is a guide to help you setup the VS Code debugging environment for Python locally and remotely, and is based on VS Code's documents on [debugging](https://code.visualstudio.com/docs/editor/debugging) and [Python debug configuration](https://code.visualstudio.com/docs/python/debugging).

## Install VS Code
You can download VS Code [here](https://code.visualstudio.com/).

## Setup debugging configuration for Python
Click on the debug icon in the sidebar.

![](images/debug_icon.png)

If you don't have any configuration yet, you will see "No Configurations". Click on the setting icon to create one.

![](images/no_configuration.png)

A configuration menu will then show up, choose **Python File**.

![](images/python_configuration.png)

This will create and open a `launch.json` file with default configuration located in a `.vscode` folder in your workspace (project root folder). You can modify or add custom configurations here. For more configuration options, checkout the [VS Code document](https://code.visualstudio.com/docs/python/debugging#_set-configuration-options).

<img src="images/launch_json.png" width="400" height="250">

## Launch versus Attach configuration
In VS Code, there are two ways to perform debugging actions, **Launch** and **Attach**. You may think of **launching** is to start your program in debug mode, and **attaching** is to attach the VS Code debugger to an **already** running process.

You may choose the way you prefer by setting the `"request"` argument to `"launch"` or `"attach"` in `launch.json`.

## Launching a program in debug mode
With default configuration, you can launch a Python program locally in debug mode. Simply press `F5` to enter debug mode. The status bar below will turn orange and show the active launch configuration once you successfully enter debug mode.

![](images/debug_mode.png)

The debug toolbar will also show up for you to perform debug actions.

![](images/debug_toolbar.png)

### Breakpoints
Breakpoints could be set by clicking on the **editor margin** or pressing `F9` on the current line. You may also call `breakpoint()` at any place in your Python code to pause the debugger.

![](images/breakpoint.png)

You can have more control of the breakpoints in Debug view's **BREAKPOINTS** section.

![](images/breakpoint_section.png)

For advanced breakpoints such as conditional breakpoints, inline breakpoints or function breakpoints, checkout [VS Code document](https://code.visualstudio.com/docs/editor/debugging#_advanced-breakpoint-topics).

### Data inspection
Variables can be inspected in the **VARIABLES** section, and variables can be modified with the **Set Value** action by right clicking on the variables. Note that the variable values are relative to the selected stack frame in the **CALL STACK** section.

![](images/variables.png)

You can also add variables or **expressions** to the **WATCH** section.

![](images/watch.png)

## Remote debugging
VS Code's remote debugging feature allows you to step through codes on a remote computer, and it's not nessesarily to install VS Code on the remote computer.

Below are the steps to remote debug using VS Code:
- For both computers
  1. Contains **identical** source code
  2. Install `ptvsd` using one of the command below
      ```
      conda install -c conda-forge ptvsd
      conda install -c conda-forge/label/gcc7 ptvsd
      python -m pip install --upgrade ptvsd
      ```
- Remote computer
  1. In the source code, add the following codes. Change `'1.2.3.4'` to your remote computer's private IP address if available (if you use a public address, you may see a "Cannot assign requested address" error), and specify the port number you would like to use.
      ```python
      import ptvsd

      # Allow other computers to attach to ptvsd at this IP address and port.
      ptvsd.enable_attach(address=('1.2.3.4', 3000), redirect_output=True)

      # Pause the program until a remote debugger is attached
      ptvsd.wait_for_attach()
      ```
  2. Launch the remote process through ptvsd
      ```
      python -m ptvsd --host 1.2.3.4 --port 3000 --wait debug.py
      ```
  This starts the script `debug.py` using `python`, with the remote computer's private IP address `1.2.3.4` listening on port `3000`. The program will be paused until the debugger attaches.
- Local computer
  1. Add the commented lines of the codes that were added to the remote computer. Adding these lines ensures that the code on both computers matches line by line.
      ```python
      #import ptvsd

      # Allow other computers to attach to ptvsd at this IP address and port.
      #ptvsd.enable_attach(address=('1.2.3.4', 3000), redirect_output=True)

      # Pause the program until a remote debugger is attached
      #ptvsd.wait_for_attach()
      ```
  2. Open `launch.json` and add the following configuration to the array in `"configuration"`.
      ```json
      {
          "name": "Python Attach (Remote Debug 192.168.34.156)",
          "type": "python",
          "request": "attach",
          "pathMappings": [
              {
                  "localRoot": "${workspaceFolder}",  // You may also manually specify the directory containing your source code.
                  "remoteRoot": "~/hello" // Linux example; adjust as necessary for your OS and situation.
              }
          ],
          "port": 3000,                   // Set to the remote port.
          "host": "1.2.3.4"               // Set to your remote host's public IP address.
      }
      ```
