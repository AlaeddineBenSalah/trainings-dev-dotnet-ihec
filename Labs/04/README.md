# Tutorial: Create a .NET class library using Visual Studio Code

In this tutorial, you create a simple utility library that contains a single string-handling method.
A class library defines types and methods that are called by an application. If the library targets .NET Standard 2.0, it can be called by any .NET implementation (including .NET Framework) that supports .NET Standard 2.0. If the library targets .NET 6, it can be called by any application that targets .NET 6. This tutorial shows how to target .NET 6.
When you create a class library, you can distribute it as a third-party component or as a bundled component with one or more applications.

# Prerequisites

- Visual Studio Code with the C# extension installed. For information about how to install extensions on Visual Studio Code, see VS Code Extension Marketplace.
- The .NET 6 SDK.

# Create a solution

Start by creating a blank solution to put the class library project in. A solution serves as a container for one or more projects. You'll add additional, related projects to the same solution.
1. Start Visual Studio Code.

2. Select File > Open Folder (Open... on macOS) from the main menu

3. In the Open Folder dialog, create a ClassLibraryProjects folder and click Select Folder (Open on macOS).

4. Open the Terminal in Visual Studio Code by selecting View > Terminal from the main menu.

The Terminal opens with the command prompt in the ClassLibraryProjects folder.

5. In the Terminal, enter the following command:
```
dotnet new sln
```
The terminal output looks like the following example:
```
The template "Solution File" was created successfully
```

# Create a class library project

Add a new .NET class library project named "StringLibrary" to the solution.

1. In the terminal, run the following command to create the library project:
```
dotnet new classlib -o StringLibrary
```
The -o or --output command specifies the location to place the generated output.

The terminal output looks like the following example:

```
The template "Class library" was created successfully.
Processing post-creation actions...
Running 'dotnet restore' on StringLibrary\StringLibrary.csproj...
  Determining projects to restore...
  Restored C:\Projects\ClassLibraryProjects\StringLibrary\StringLibrary.csproj (in 328 ms).
Restore succeeded.
```

Run the following command to add the library project to the solution:
```
dotnet sln add StringLibrary/StringLibrary.csproj
```
The terminal output looks like the following example:
```
Project `StringLibrary\StringLibrary.csproj` added to the solution.
```

Check to make sure that the library targets .NET 6. In Explorer, open StringLibrary/StringLibrary.csproj.

The TargetFramework element shows that the project targets .NET 6.0.

```
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net6.0</TargetFramework>
  </PropertyGroup>

</Project>
```
4. Open Class1.cs and replace the code with the following code.
```
namespace UtilityLibraries;

public static class StringLibrary
{
    public static bool StartsWithUpper(this string? str)
    {
        if (string.IsNullOrWhiteSpace(str))
            return false;

        char ch = str[0];
        return char.IsUpper(ch);
    }
}
```
The class library, UtilityLibraries.StringLibrary, contains a method named StartsWithUpper. This method returns a Boolean value that indicates whether the current string instance begins with an uppercase character. The Unicode standard distinguishes uppercase characters from lowercase characters. The Char.IsUpper(Char) method returns true if a character is uppercase.
StartsWithUpper is implemented as an extension method so that you can call it as if it were a member of the String class.

5. Save the file.
6. Run the following command to build the solution and verify that the project compiles without error.
```
dotnet build
```
The terminal output looks like the following example:
```
Microsoft (R) Build Engine version 16.7.0+b89cb5fde for .NET
Copyright (C) Microsoft Corporation. All rights reserved.
  Determining projects to restore...
  All projects are up-to-date for restore.
  StringLibrary -> C:\Projects\ClassLibraryProjects\StringLibrary\bin\Debug\net6.0\StringLibrary.dll
Build succeeded.
    0 Warning(s)
    0 Error(s)
Time Elapsed 00:00:02.78
```

# Add a console app to the solution
Add a console application that uses the class library. The app will prompt the user to enter a string and report whether the string begins with an uppercase character.
1. In the terminal, run the following command to create the console app project:
```
dotnet new console -o ShowCase
```
The terminal output looks like the following example:
```
The template "Console Application" was created successfully.
Processing post-creation actions...
Running 'dotnet restore' on ShowCase\ShowCase.csproj...  
  Determining projects to restore...
  Restored C:\Projects\ClassLibraryProjects\ShowCase\ShowCase.csproj (in 210 ms).
Restore succeeded.
```
2. Run the following command to add the console app project to the solution:
```
dotnet sln add ShowCase/ShowCase.csproj
```

The terminal output looks like the following example:
```
Project `ShowCase\ShowCase.csproj` added to the solution.
```

3. Open ShowCase/Program.cs and replace all of the code with the following code.
```
using UtilityLibraries;

class Program
{
    static void Main(string[] args)
    {
        int row = 0;

        do
        {
            if (row == 0 || row >= 25)
                ResetConsole();

            string? input = Console.ReadLine();
            if (string.IsNullOrEmpty(input)) break;
            Console.WriteLine($"Input: {input}");
            Console.WriteLine("Begins with uppercase? " +
                 $"{(input.StartsWithUpper() ? "Yes" : "No")}");
            Console.WriteLine();
            row += 4;
        } while (true);
        return;

        // Declare a ResetConsole local method
        void ResetConsole()
        {
            if (row > 0)
            {
                Console.WriteLine("Press any key to continue...");
                Console.ReadKey();
            }
            Console.Clear();
            Console.WriteLine($"{Environment.NewLine}Press <Enter> only to exit; otherwise, enter a string and press <Enter>:{Environment.NewLine}");
            row = 3;
        }
    }
}
```
The code uses the row variable to maintain a count of the number of rows of data written to the console window. Whenever it's greater than or equal to 25, the code clears the console window and displays a message to the user.

The program prompts the user to enter a string. It indicates whether the string starts with an uppercase character. If the user presses the Enter key without entering a string, the application ends, and the console window closes.

4. Save your changes.

# Add a project reference

Initially, the new console app project doesn't have access to the class library. To allow it to call methods in the class library, create a project reference to the class library project.

1. Run the following command:
```
dotnet add ShowCase/ShowCase.csproj reference StringLibrary/StringLibrary.csproj
```
The terminal output looks like the following example:
```
Reference `..\StringLibrary\StringLibrary.csproj` added to the project.
```

# Run the app
1. Run the following command in the terminal:
```
dotnet run --project ShowCase/ShowCase.csproj
```
Try out the program by entering strings and pressing Enter, then press Enter to exit.
The terminal output looks like the following example:
``` 
Press <Enter> only to exit; otherwise, enter a string and press <Enter>:

A string that starts with an uppercase letter
Input: A string that starts with an uppercase letter
Begins with uppercase? : Yes

a string that starts with a lowercase letter
Input: a string that starts with a lowercase letter
Begins with uppercase? : No
```


