#Buildage
The easy build and packager for C# projects.

This collection of MSBuild scripts (bundled with [MSBuildTasks](https://github.com/loresoft/msbuildtasks)) will make it easy to have a command-line build script up and running in no time that builds your source code, runs unit tests, and generates NuGet packages.

Buildage performs the following build steps:
* Generates a common AssemblyInfo for your solution from a core set of metadata
* Compiles your solution
* Runs unit tests written in [NUnit](http://nunit.org)
* Creates [NuGet](http://nuget.org) packages

##Getting Started

**NOTE:** These instructions assume you have a root-level build directory in your project called `build`.

- [ ] Add the **Buildage** project repo as a git submodule to your repo in your `build` directory:

```    
C:\YourRepo> git submodule add https://github.com/twistedstream/Buildage.git build/Buildage
``` 

- [ ] Copy the `Input.targets` file from `samples` to your `build` directory and customize it to match your solution:

```
C:\YourRepo> cp .\build\Buildage\samples\Input.targets .\build
C:\YourRepo> notepad .\build\Input.targets
```

- [ ] For each project in your solution that you wish to generate a NuGet package for: Copy the `MyProject.nuspec.template` file from `samples` to your project's directory, rename it to match your project name, and customize it to match your project.

```
C:\YourRepo> cp .\build\Buildage\samples\MyProject.nuspec.template .\src\MyActualProject\MyActualProject.nuspec.template
C:\YourRepo> notepad .\src\MyActualProject\MyActualProject.nuspec.template
```

- [ ] Copy the `build.cmd` file from `samples` to your root directory:

```
C:\YourRepo> cp .\build\Buildage\samples\build.cmd .\build.cmd
```

- [ ] Generate your initial `CommonAssemblyInfo.cs` file:

```
C:\YourRepo> .\build.cmd GenAssemblyInfo
```

- [ ] Open your Visual Studio solution and add the generated `CommonAssemblyInfo.cs` file as a [linked file](http://support.microsoft.com/kb/306234?wa=wsignin1.0) to each project.  No need to add it to source control as it can easily be regenerated.
- [ ] Remove any attributes from the standard `AssemblyInfo.cs` files in each project that duplicate what's in `CommonAssemblyInfo.cs`.  For the most part, only following should be necessary:

```cs
[assembly: AssemblyTitle("YourAssmbly")]
[assembly: AssemblyDescription("YourAssembly description.")]
[assembly: Guid("your-assembly-guid")]
```

- [ ] Add the following lines to your `.gitignore` file

```
CommonAssemblyInfo.cs
/build/out
```

- [ ] Run your build!

```
C:\YourRepo> .\build.cmd
```

The resulting output files (ex: NuGet packages) will be in the `build\out` directory.

##Questions?
[@twistedstream](http://twitter.com/twistedstream)
