#Buildage
The easy build and packager for C# projects.

This collection of MSBuild scripts (bundled with [MSBuildTasks](https://github.com/loresoft/msbuildtasks)) will make it easy to have a command-line build script up and running in no time that builds your source code, runs unit tests, and generates a final NuGet package.

##Getting Started

NOTE: These instructions assume you have a root-level build directory in your project called `build`.

* Add the Buildage project as a git submodule to your project in your `build` directory:

```    
C:\YourProject> git submodule add https://github.com/twistedstream/Buildage.git build/Buildage
``` 

* Copy the `MyProject.nuspec.template.sample` file to your `build` directory and rename it to `{your project}.nuspec.template`:

```
C:\YourProject> cp .\build\Buildage\MyProject.nuspec.template.sample .\build\{your project}.nuspec.template
```

* Modify the `{your project}.nuspec.template` file to match your project.
* Copy the `Input.targets.sample` file to your `build` directory and rename it to `Input.targets`:

```
C:\YourProject> cp .\build\Buildage\Input.targets.sample .\build\Input.targets
```

* Modify the `Input.targets` file to match your project.
* Copy the `build.cmd.sample` file to your project root directory and rename it to `build.cmd`:

```
C:\YourProject> cp .\build\Buildage\build.cmd.sample .\build.cmd
```

* Generate your initial set of `AssemblyInfo.buildage.cs` files:

```
C:\YourProject> .\build.cmd GenAssemblyInfos
```

* Open your Visual Studio solution and add the generated `AssemblyInfo.buildage.cs` files for each project.  No need to add these files to source control as they can easily be regenerated.
* Remove the duplicate attributes from the standard `AssemblyInfo.cs` files in each project.
* Run your build:

```
C:\YourProject> .\build.cmd
```

* Examine the build output files and the final resulting package in the `build\out` directory.
* Optionally add the following lines to your `.gitignore` file

```
AssemblyInfo.buildage.cs
/build/out
```
