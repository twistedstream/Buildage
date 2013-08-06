# Buildage #
The easy build and packager for C# projects.

This collection of MSBuild scripts (bundled with [MSBuildTasks](https://github.com/loresoft/msbuildtasks)) will make it easy to have a command-line build script up and running in no time that builds your source code, runs unit tests, and generates NuGet packages.

Buildage performs the following build steps:
* Generates a common **AssemblyInfo** file for your solution from a core set of metadata
* Compiles your solution(s)
* Runs test assemblies written in [NUnit](http://nunit.org)
* Creates [NuGet](http://nuget.org) packages

## Getting Started ##

**NOTE:** These instructions assume your project code is in a [Git](http://git-scm.com/) repository and you have a root-level directory in your repo called `build` that can contain your build scripts.

* Add the **Buildage** project repo as a git submodule to your repo in your `build` directory:

```    
C:\YourRepo> git submodule add https://github.com/twistedstream/Buildage.git build/Buildage
``` 

* Copy the `Input.targets` file from `samples` to your `build` directory and customize it to match your solution:

```
C:\YourRepo> cp .\build\Buildage\samples\Input.targets .\build
C:\YourRepo> notepad .\build\Input.targets
```

* You can generate NuGet packages in one of two ways, and both require a special file with a `.nuspec.template` extension.  This file is what Buildage uses to generate a final `.nuspec` file at build time to be used with the `nuget pack` command.  Buildage will automatically find any `.nuspec.template` file anywhere in your source directory path (specified via the `Input_SourceDirPath` property in the `Input.targets` file) and generate a package in your build output directy path (specified by `Input_OutputDirPath`).
  * The first method Buildage uses to generate NuGet packages is to use both a Visual Studio project and a `.nuspec` file as the source for the `nuget pack` command.  Much of the package metadata is sourced from the project, but the big advantage is the automatic detection of binaries and NuGet dependencies.  The `.nuspec` file can then provide additional NuGet-specific metadata.  For more information on using Visual Studio project files and `.nuspec` files together as a package source, see the [NuGet documentation](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package).
  * The second method is to only use the `.nuspec` file, which is useful in more complex scenarios or when there's no relevant Visual Studio project to source from.
* To generate a NuGet package that uses a Visual Studio project as its primary input, copy the `MyProject.nuspec.template` file from `samples` to your project's directory, rename it to match your project name, and customize it to match your project:

```
C:\YourRepo> cp .\build\Buildage\samples\MyProject.nuspec.template .\src\MyActualProject\MyActualProject.nuspec.template
C:\YourRepo> notepad .\src\MyActualProject\MyActualProject.nuspec.template
```

* To generate a NuGet packages that does't use a Visual Studio project as its primary input, do the same as above, but copy the template file to whatever directory under your source root where you're going to generate your .nuspec.  You also need to manually specify the `<id>`, `<title>`, and `<description>` values in the `.nuspec.template` file instead of using the NuGet replacement tokens (ex: `$id$`):

```xml
<package>
  <metadata>
    <id>Your.ID</id> <!-- was $id$ -->
    <title>Your Title</title> <!-- was $title$ -->
    <description>Your description</description> <!-- was $description$ -->
    ...
```

* Copy the `build.cmd` file from `samples` to your root directory:

```
C:\YourRepo> cp .\build\Buildage\samples\build.cmd .\build.cmd
```

* Generate your initial `CommonAssemblyInfo.cs` file:

```
C:\YourRepo> .\build.cmd GenAssemblyInfo
```

* Open your Visual Studio solution and add the generated `CommonAssemblyInfo.cs` file as a [linked file](http://support.microsoft.com/kb/306234?wa=wsignin1.0) to each project.  No need to add it to source control as it can easily be regenerated.  See a step below for actually adding it to your `.gitignore` file.
* Remove any attributes from the standard `AssemblyInfo.cs` files in each project that duplicate what's in `CommonAssemblyInfo.cs`.  For the most part, only the following should be necessary:

```cs
[assembly: AssemblyTitle("YourAssmbly")]
[assembly: AssemblyDescription("YourAssembly description.")]
[assembly: Guid("your-assembly-guid")]
```

* Add the following lines to your `.gitignore` file

```
CommonAssemblyInfo.cs
/build/out
```

* Run your build!

```
C:\YourRepo> .\build.cmd
```

The resulting output files (ex: NuGet packages) will be in the `build\out` directory.

## Questions? ##
[@twistedstream](http://twitter.com/twistedstream)
