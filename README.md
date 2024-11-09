# Monogame Setup Guide

You WILL follow these instructions and install things the way I'm telling you to bc on GOD i'm not answering any questions about Visual Studio.

## Setting up VSCode with C# and Monogame

### Installations

Install the latest versions of the following on your computer:

1. [.NET SDK](https://dotnet.microsoft.com/en-us/download)
2. [Visual Studio Code (VSCode)](https://code.visualstudio.com/)
3. Once you have VSCode installed, click on the "Extensions" tab on the sidebar (looks like a group of squares), and search for and install the "C# Dev Kit".
4. Install the "MonoGame for VSCode" extension.

5. Open a terminal window (either in your terminal of choice, or in VSCode by pressing (`Ctrl + \`)) and type

```
dotnet new -i MonoGame.Template.CSharp
```

and

```
dotnet new -i NUnit3.DotNetNew.Template
```

This will install Monogame as well as NUnit, which we will use for writing unit tests.

## GitHub

If you do not already have a [GitHub](https://github.com/) account, please sign up for one.

Install [GitHub Desktop](https://desktop.github.com/download/), or plain Git if you're nasty. YOU DO NOT NEED TO INSTALL BOTH. (i mean i guess you can. but why would you.)

If you are on a Windows machine, you can download Git [here](https://git-scm.com/download/win). If you are on a Mac, you should be able to open a terminal and type

```
 git --version
```

which will prompt you to install Git if you do not already have it installed.

### Project Setup

---

NOTE: The following is only if you want to create your own test game. For the actual codebase you will just pull down the github repo that [emily](https://github.com/ebrents) will set up.

Create a folder that will store any Monogame projects

```
mkdir Monogame_projects
```

Create a folder where you want to store your project.

```
mkdir {project_name}
```

Navigate in your terminal to that folder.

```
cd {project_name}
```

Run the following commands:

```
 dotnet new sln
 dotnet new mgdesktopgl -o {project_name}
 dotnet sln add {project_name}/{project_name}.csproj
```

Replace `{project_name}` with whatever you want your project will be called.

These commands will create a `{project_name}.sln` file that references the `{project_name}/{project_name}.csproj` file.

Open the `{project_name}.csproj` file in VSCode and replace the contents with the following:

```
<Project Sdk="Microsoft.NET.Sdk">

     <PropertyGroup>
         <OutputType>WinExe</OutputType>
         <!-- Set to "netcoreapp" plus the first 2 digits of your .NET Core SDK version. -->
         <TargetFramework>netcoreapp3.0</TargetFramework>
         <TargetLatestRuntimePatch>true</TargetLatestRuntimePatch>
     </PropertyGroup>

     <ItemGroup>
         <MonoGameContentReference Include="**\*.mgcb" />
     </ItemGroup>

     <ItemGroup>
         <PackageReference Include="MonoGame.Content.Builder" Version="3.7.0.4" />
         <PackageReference Include="MonoGame.Framework.DesktopGL.Core" Version="3.7.0.7" />
     </ItemGroup>

     <!-- Actually cleans your project when you run "dotnet clean" -->
     <Target Name="SpicNSpan"  AfterTargets="Clean">
         <!-- Remove obj folder -->
         <RemoveDir Directories="$(BaseIntermediateOutputPath)" />
         <!-- Remove bin folder -->
         <RemoveDir Directories="$(BaseOutputPath)" />
     </Target>

 </Project
```

### Testing

---

We will need to create unit tests at some point because we are not animals. To do this, create a new folder called `{project_name}Tests` in the folder containing you sln file.

```
mkdir {project_name}.Tests`
```

Navigate into that folder

```
cd {project_name}.Tests`
```

and run the following:

```
 dotnet new nunit
 dotnet add reference ../{project_name}/{project_name}.csproj
```

Navigate back to the folder with your sln file

```
cd ..
```

and run the following

```
 dotnet sln add ./{project_name}.Tests/{project_name}.Tests.csproj
```

Replace the contents of the `{project_name}.Tests.csproj` file with

```
 <Project Sdk="Microsoft.NET.Sdk">

     <PropertyGroup>
         <!-- Set to "netcoreapp" plus the first 2 digits of your .NET Core SDK version. -->
         <TargetFramework>netcoreapp3.0</TargetFramework>
         <TargetLatestRuntimePatch>true</TargetLatestRuntimePatch>
         <IsPackable>false</IsPackable>
     </PropertyGroup>

     <ItemGroup>
         <PackageReference Include="nunit" Version="*" />
         <PackageReference Include="NUnit3TestAdapter" Version="*" />
         <PackageReference Include="Microsoft.NET.Test.Sdk" Version="*" />
     </ItemGroup>

     <ItemGroup>
         <ProjectReference Include="..\MyProject\MyProject.csproj" />
     </ItemGroup>

     <!-- Actually cleans your project when you run "dotnet clean" -->
     <Target Name="SpicNSpan"  AfterTargets="Clean">
         <!-- Remove obj folder -->
         <RemoveDir Directories="$(BaseIntermediateOutputPath)" />
         <!-- Remove bin folder -->
         <RemoveDir Directories="$(BaseOutputPath)" />
     </Target>

 </Project>
```

Now you can start writing unit tests! Aren't you thrilled.

### Using Monogame

---

Now unfortunately we have reached the part of the instructions where I can only really say: "This is the part where you need to learn C#, .NET, and Monogame/XNA." I will provide links to tutorials for these.

- [C# Crash Course](http://rbwhitaker.wikidot.com/c-sharp-tutorials)
- [C# Yellow Book](https://www.robmiles.com/c-yellow-book/)
- [Archived XNA Game Studio documentation](<https://docs.microsoft.com/en-us/previous-versions/windows/xna/bb200104(v=xnagamestudio.41)>)
- [XNA Game Studio educational resources archive](https://github.com/SimonDarksideJ/XNAGameStudio)
- [Getting Started with Monogame](http://rbwhitaker.wikidot.com/monogame-getting-started-tutorials)
- [Monogame Documentation](https://docs.monogame.net/articles/getting_started/index.html)
