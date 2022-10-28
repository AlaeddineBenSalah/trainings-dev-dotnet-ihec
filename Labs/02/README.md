# Tutorial 2: Debug a .NET console application using Visual Studio Code
This tutorial introduces the debugging tools available in Visual Studio Code for working with .NET apps.

## Prerequisites
This tutorial works with the console app that you create in Create a .NET console application using Visual Studio Code.

## Use Debug build configuration
Debug and Release are .NET's built-in build configurations. You use the Debug build configuration for debugging and the Release configuration for the final release distribution.

In the Debug configuration, a program compiles with full symbolic debug information and no optimization. Optimization complicates debugging, because the relationship between source code and generated instructions is more complex. The release configuration of a program has no symbolic debug information and is fully optimized.

By default, Visual Studio Code launch settings use the Debug build configuration, so you don't need to change it before debugging.
1. Start Visual Studio Code.
2. Open the folder of the project that you created in Create a .NET console application using Visual Studio Code.
## Set a breakpoint
A breakpoint temporarily interrupts the execution of the application before the line with the breakpoint is run.
1. Open the Program.cs file.
2. Set a breakpoint on the line that displays the name, date, and time, by clicking in the left margin of the code window. The left margin is to the left of the line numbers. Other ways to set a breakpoint are by pressing F9 or choosing Run > Toggle Breakpoint from the menu while the line of code is selected.

Visual Studio Code indicates the line on which the breakpoint is set by displaying a red dot in the left margin.
!(![image](https://user-images.githubusercontent.com/79606006/198717976-bbd90ed8-5fe9-4cb7-8273-d399af34bf43.png))

## Set up for terminal input
The breakpoint is located after a Console.ReadLine method call. The Debug Console doesn't accept terminal input for a running program. To handle terminal input while debugging, you can use the integrated terminal (one of the Visual Studio Code windows) or an external terminal. For this tutorial, you use the integrated terminal.

1. Open .vscode/launch.json.
2. Change the console setting from internalConsole to integratedTerminal:
```
"console": "integratedTerminal",
```
3. Save your changes.

## Start debugging
1. Open the Debug view by selecting the Debugging icon on the left side menu.
![image](https://user-images.githubusercontent.com/79606006/198718285-f8ba1318-bbac-4563-8821-9bd69bf8ae7b.png)
2. Select the green arrow at the top of the pane, next to .NET Core Launch (console). Other ways to start the program in debugging mode are by pressing F5 or choosing Run > Start Debugging from the menu.
![image](https://user-images.githubusercontent.com/79606006/198718478-42a4bd12-82c0-4f0e-895f-83806dac8790.png)
3. Select the Terminal tab to see the "What is your name?" prompt that the program displays before waiting for a response.
![image](https://user-images.githubusercontent.com/79606006/198718527-748ca99b-5511-4056-aae5-efbaf6941b12.png)

4. Enter a string in the Terminal window in response to the prompt for a name, and then press Enter.

Program execution stops when it reaches the breakpoint and before the Console.WriteLine method runs. The Locals section of the Variables window displays the values of variables that are defined in the currently running method.

![image](https://user-images.githubusercontent.com/79606006/198718586-a42b8b35-7050-4e77-b565-f633446d7802.png)

## Use the Debug Console

The Debug Console window lets you interact with the application you're debugging. You can change the value of variables to see how it affects your program.

1. Select the Debug Console tab.
2. Enter name = "Gracie" at the prompt at the bottom of the Debug Console window and press the Enter key.
![image](https://user-images.githubusercontent.com/79606006/198718711-f8d6fab9-be9e-4627-ab00-f0b8e9140271.png)

3. Enter currentDate = DateTime.Parse("2019-11-16T17:25:00Z").ToUniversalTime() at the bottom of the Debug Console window and press the Enter key.
The Variables window displays the new values of the name and currentDate variables.

4. Continue program execution by selecting the Continue button in the toolbar. Another way to continue is by pressing F5.

![image](https://user-images.githubusercontent.com/79606006/198718812-7bc1a8dd-1610-448f-8428-0dc7685f4aac.png)

5. Select the Terminal tab again.
The values displayed in the console window correspond to the changes you made in the Debug Console.

![image](https://user-images.githubusercontent.com/79606006/198718873-4f8d47d7-f1d0-4808-8c26-56c602ea7254.png)

6. Press any key to exit the application and stop debugging.

## Set a conditional breakpoint
The program displays the string that the user enters. What happens if the user doesn't enter anything? You can test this with a useful debugging feature called a conditional breakpoint

1 Right-click on the red dot that represents the breakpoint. In the context menu, select Edit Breakpoint to open a dialog that lets you enter a conditional expression.

![image](https://user-images.githubusercontent.com/79606006/198719057-e70010f2-4f77-485d-a8ef-cfa44a79612a.png)

2. Select Expression in the drop-down, enter the following conditional expression, and press Enter.
```
String.IsNullOrEmpty(name)
```
![image](https://user-images.githubusercontent.com/79606006/198719163-9d655f2a-cdd9-4c56-91ed-f57fbd568ad1.png)

Each time the breakpoint is hit, the debugger calls the String.IsNullOrEmpty(name) method, and it breaks on this line only if the method call returns true.

Instead of a conditional expression, you can specify a hit count, which interrupts program execution before a statement is run a specified number of times. Another option is to specify a filter condition, which interrupts program execution based on such attributes as a thread identifier, process name, or thread name.

3. Start the program with debugging by pressing F5.

4. In the Terminal tab, press the Enter key when prompted to enter your name.

Because the condition you specified (name is either null or String.Empty) has been satisfied, program execution stops when it reaches the breakpoint and before the Console.WriteLine method runs.

The Variables window shows that the value of the name variable is "", or String.Empty.

5. Confirm the value is an empty string by entering the following statement at the Debug Console prompt and pressing Enter. The result is true.
```
name == String.Empty
``` 
6. Select the Continue button on the toolbar to continue program execution.

7. Select the Terminal tab, and press any key to exit the program and stop debugging.

8. Clear the breakpoint by clicking on the dot in the left margin of the code window. Other ways to clear a breakpoint are by pressing F9 or choosing Run > Toggle Breakpoint from the menu while the line of code is selected.

9. If you get a warning that the breakpoint condition will be lost, select Remove Breakpoint.

## Step through a program

## Use Release build configuration

Once you've tested the Debug version of your application, you should also compile and test the Release version. The Release version incorporates compiler optimizations that can affect the behavior of an application. For example, compiler optimizations that are designed to improve performance can create race conditions in multithreaded applications.

To build and test the Release version of your console application, open the Terminal and run the following command:

```
dotnet run --configuration Release
```
