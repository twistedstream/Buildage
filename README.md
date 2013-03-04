#Buildage
The easy build and packager for C# projects.

This collection of MSBuild scripts (bundled with [MSBuildTasks](http://nuget.org/packages/MSBuildTasks)) will make it easy to have a command-line build script up and running in no time that builds your source code, runs unit tests, and generates a final NuGet package.

##Getting Started

NOTE: These instructions assume you have a root-level build directory in your project called "build".

1. Add the Buildage project as a git submodule to your project in your build directory:
    
    C:\YourProject> git submodule add https://github.com/twistedstream/Buildage.git build\Buildage
    
2. Copy the MyProject.nuspec.template.sample file to your build directory and rename it to {your project}.nuspec.template:

    C:\YourProject> cp .\build\Buildage\MyProject.nuspec.template.sample .\{your project}.nuspec.template

3. Modify the {your project}.nuspec.template file to match your project.
4. Copy the Input.targets.sample file to your build directory and rename it to Input.targets:

    C:\YourProject> cp .\build\Buildage\Input.targets.sample .\build\Input.targets

5. Modify the Input.targets file to match your project.
6. Copy the build.cmd.sample file to your project root directory and rename it to build.cmd:

    C:\YourProject> cp .\build\Buildage\build.cmd.sample .\build.cmd

7. Generate your initial set of AssemblyInfo.buildage.cs files:

    C:\YourProject> .\build.cmd GenAssemblyInfos

8. Open your Visual Studio solution and add the generated AssemblyInfo.buildage.cs files for each project.  No need to add these files to source control as they can easily be regenerated.
9. Remove the duplicate attributes from the standard AssemblyInfo.cs files in each project.
10. Run your build:

    C:\YourProject> .\build.cmd

11. Examine the build output files and the final resulting package in the build\out directory.
12. Optionally add the following lines to your .gitignore file

    AssemblyInfo.buildage.cs
    /build/out
