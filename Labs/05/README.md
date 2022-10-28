# Quickstart: Install and use a package with the dotnet CLI

NuGet packages contain compiled binary code that developers make available for other developers to use in their projects. For more information, see What is NuGet. This quickstart describes how to install the popular Newtonsoft.Json NuGet package into a .NET project by using the dotnet add package command.

You refer to installed packages in code with a using <namespace> directive, where <namespace> is often the package name. You can then use the package's API in your project.

# Prerequisites

- The .NET SDK, which provides the dotnet command-line tool. Starting in Visual Studio 2017, the dotnet CLI automatically installs with any .NET or .NET Core related workloads.
  
# Create a project

You can install NuGet packages into a .NET project. For this walkthrough, create a simple .NET console project by using the dotnet CLI, as follows:

1. Create a folder named Nuget.Quickstart for the project.
2. Open a command prompt and switch to the new folder.
3. Create the project by using the following command:
```
  dotnet new console
```
4. Use dotnet run to test the app. You should see the output Hello, World!.

# Add the Newtonsoft.Json NuGet package
1. Use the following command to install the Newtonsoft.json package:
```
 dotnet add package Newtonsoft.Json
```
2. After the command completes, open the Nuget.Quickstart.csproj file in Visual Studio to see the added NuGet package reference:
```
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="13.0.1" />
</ItemGroup>
```

# Use the Newtonsoft.Json API in the app
1. In Visual Studio, open the Program.cs file and add the following line at the top of the file:
```
  using Newtonsoft.Json;
```
 2. Add the following code to replace the Console.WriteLine("Hello, World!"); statement:
 ```
 namespace Nuget.Quickstart
{
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    internal class Program
    {
        static void Main(string[] args)
        {
            Account account = new Account
            {
                Name = "John Doe",
                Email = "john@nuget.org",
                DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
            };

            string json = JsonConvert.SerializeObject(account, Formatting.Indented);
            Console.WriteLine(json);
        }
    }
}
```
3. Save the file, then build and run the app by using the dotnet run command. The output is the JSON representation of the Account object in the code:

```
{
  "Name": "John Doe",
  "Email": "john@nuget.org",
  "DOB": "1980-02-20T00:00:00Z"
}
```
