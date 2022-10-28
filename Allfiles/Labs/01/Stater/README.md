# Tutorial: Create a .NET console application using Visual Studio Code
This tutorial shows how to create and run a .NET console application by using Visual Studio Code and the .NET CLI. Project tasks, such as creating, compiling, and running a project are done by using the .NET CLI. You can follow this tutorial with a different code editor and run commands in a terminal if you prefer.
## Prerequisites
Visual Studio Code with the C# extension installed. For information about how to install extensions on Visual Studio Code, see VS Code Extension Marketplace.
The .NET 6 SDK.
## Create the app
Create a .NET console app project named "HelloWorld".
1. Start Visual Studio Code.
2. Select File > Open Folder (File > Open... on macOS) from the main menu.
3. In the Open Folder dialog, create a HelloWorld folder and select it. Then click Select Folder (Open on macOS).
   The folder name becomes the project name and the namespace name by default. You'll add code later in the tutorial that assumes the project namespace is HelloWorld.
4. In the Do you trust the authors of the files in this folder? dialog, select Yes, I trust the authors.
5. Open the Terminal in Visual Studio Code by selecting View > Terminal from the main menu.
   The Terminal opens with the command prompt in the HelloWorld folder.
6. In the Terminal, enter the following command:
```
dotnet new console --framework net6.0
```
7. Replace the contents of Program.cs with the following code:
```
namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```
The first time you edit a .cs file, Visual Studio Code prompts you to add the missing assets to build and debug your app. Select Yes, and Visual Studio Code creates a .vscode folder with launch.json and tasks.json files.

## Run the app
Run the following command in the Terminal:
```
dotnet run
```

## Enhance the app
Enhance the application to prompt the user for their name and display it along with the date and time.
1. Open Program.cs.
2. Replace the contents of the Main method in Program.cs, which is the line that calls Console.WriteLine, with the following code:
```
Console.WriteLine("What is your name?");
var name = Console.ReadLine();
var currentDate = DateTime.Now;
Console.WriteLine($"{Environment.NewLine}Hello, {name}, on {currentDate:d} at {currentDate:t}!");
Console.Write($"{Environment.NewLine}Press any key to exit...");
Console.ReadKey(true);
```
3. Save your changes.
4. Run the program again:
```
dotnet run
```
5. Respond to the prompt by entering a name and pressing the Enter key
6. Press any key to exit the program.
