# Tutorial: Publish a .NET console application using Visual Studio Code

This tutorial shows how to publish a console app so that other users can run it. Publishing creates the set of files that are needed to run an application. To deploy the files, copy them to the target machine.
The .NET CLI is used to publish the app, so you can follow this tutorial with a code editor other than Visual Studio Code if you prefer.

# Prerequisites
This tutorial works with the console app that you create in Create a .NET console application using Visual Studio Code.

#Publish the app

1. Start Visual Studio Code.
2. Open the HelloWorld project folder that you created in Create a .NET console application using Visual Studio Code.
3. Choose View > Terminal from the main menu.
The terminal opens in the HelloWorld folder.
4. Run the following command:
```
dotnet publish --configuration Release
```
The default build configuration is Debug, so this command specifies the Release build configuration. The output from the Release build configuration has minimal symbolic debug information and is fully optimized.

The command output is similar to the following example:
```
Microsoft (R) Build Engine version 16.7.0+b89cb5fde for .NET
Copyright (C) Microsoft Corporation. All rights reserved.
  Determining projects to restore...
  All projects are up-to-date for restore.
  HelloWorld -> C:\Projects\HelloWorld\bin\Release\net6.0\HelloWorld.dll
  HelloWorld -> C:\Projects\HelloWorld\bin\Release\net6.0\publish\
```

# Inspect the files
By default, the publishing process creates a framework-dependent deployment, which is a type of deployment where the published application runs on a machine that has the .NET runtime installed. To run the published app you can use the executable file or run the dotnet HelloWorld.dll command from a command prompt.

In the following steps, you'll look at the files created by the publish process.
1. Select the Explorer in the left navigation bar.
2. Expand bin/Release/net6.0/publish.

![image](https://user-images.githubusercontent.com/79606006/198721637-06126b92-cb54-4e5c-add7-46d777c5a00e.png)

As the image shows, the published output includes the following files:
- HelloWorld.deps.json
This is the application's runtime dependencies file. It defines the .NET components and the libraries (including the dynamic link library that contains your application) needed to run the app.
- HelloWorld.dll
This is the framework-dependent deployment version of the application. To run this dynamic link library, enter dotnet HelloWorld.dll at a command prompt. This method of running the app works on any platform that has the .NET runtime installed.
- HelloWorld.exe (HelloWorld on Linux, not created on macOS.)
This is the framework-dependent executable version of the application. The file is operating-system-specific.
- HelloWorld.pdb (optional for deployment)
This is the debug symbols file. You aren't required to deploy this file along with your application, although you should save it in the event that you need to debug the published version of your application.
- HelloWorld.runtimeconfig.json
This is the application's runtime configuration file. It identifies the version of .NET that your application was built to run on. You can also add configuration options to it.

# Run the published app
1. In Explorer, right-click the publish folder (Ctrl-click on macOS), and select Open in Terminal.

![image](https://user-images.githubusercontent.com/79606006/198722030-2df38336-4ae9-4041-bacc-299abb5c0bd2.png)

2. On Windows or Linux, run the app by using the executable.
- On Windows, enter .\HelloWorld.exe and press Enter.
- On Linux, enter ./HelloWorld and press Enter.
- Enter a name in response to the prompt, and press any key to exit.
3. On any platform, run the app by using the dotnet command:
- Enter dotnet HelloWorld.dll and press Enter.
- Enter a name in response to the prompt, and press any key to exit
