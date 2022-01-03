---
link: https://devblogs.microsoft.com/cppblog/vcpkg-artifacts/
author: Marc Goodner
published: 2021-12-06T11:27:00
tags: []
---
# Bootstrap your dev environment with vcpkg artifacts
We are happy to announce a new experience for acquiring artifacts using vcpkg. We define an artifact as a set of packages required for a working development environment. Examples of relevant packages include compilers, linkers, debuggers, build systems, and platform SDKs. With this important change, vcpkg can not only download and build your libraries from source, it can also bootstrap the rest of your environment, acquiring pre-built binary dependencies for your projects.

The experience is in preview and currently focused on embedded developers. We will expand the scope in the future to include any developers targeting Linux, macOS, or Windows.

This post focuses on using vcpkg artifacts at the command line. Check out the [Embedded Development in Visual Studio blogpost](https://devblogs.microsoft.com/cppblog/visual-studio-embedded-development/) for how the capabilities are used there.

Here we are going to show how to acquire vcpkg, then activate artifacts for building an embedded project. Following that we’ll cover specific vcpkg capabilities for finding and using artifacts, then how to create a manifest and add artifacts to it. We will also cover how you can use artifacts of your own that are not part of the default artifact registry.

#### Using vcpkg artifacts

We’ll look at some embedded development scenarios to understand the new artifact capabilities in vcpkg. Embedded development is particularly known for being difficult to get a new developer machine started. Projects often have specific compiler requirements, special debug tools needed, etc. What we will show here is how through using vcpkg with a manifest you can capture these requirements and easily restore an environment for an embedded project. You do not need a device to follow along as we will not show any device interactivity. These steps except where noted are consistent cross platform.

##### Acquire vcpkg

We have also added a new way to acquire vcpkg in a single step without a git clone of the repo. Depending on your platform use one of the following commands to get vcpkg.

Linux/macOS

`. <(curl https://aka.ms/vcpkg-init.sh -L)`

PowerShell

`iex (iwr -useb https://aka.ms/vcpkg-init.ps1)`

CMD Shell

`curl -LO https://aka.ms/vcpkg-init.cmd && .\vcpkg-init.cmd`

##### Clone the example project

The example project is the Azure RTOS getting started repo, so start by cloning that with this command.

`git clone --recursive https://github.com/azure-rtos/getting-started.git`

This repo has many projects within is, each for a specific board. Use the Azure IoT DevKit by switching to that directory.

`cd .\getting-started\MXChip\AZ3166\`

##### vcpkg activate

In the project folder, there is a file vcpkg-configuration.json. This manifest file has recorded the tools you need to build and debug this project. Running the vcpkg activate command will use this file to determine if those tools have been acquired before, acquire them not, then activate them in your environment for use.

`vcpkg activate`

This is a new vcpkg command that works with artifacts. As this is the first time you are using vcpkg for artifacts it acquires the new vcpkg-ce component on demand. The ce in this component name stands for configure environment. This name was chosen as vcpkg will modify your current environment to use the artifacts in the manifest with your C++ projects.

To demonstrate that build the project. To do so generate the CMake configuration, then build the project using the preset provided by CMakePresets.json in the project with the following two commands.

```
cmake --preset arm-gcc-cortex-m4
cmake --build --preset arm-gcc-cortex-m4
```

So, in just a few commands you have installed vcpkg, cloned an embedded project, acquired and activated the necessary tools for building the project, and successfully compiled it.

##### Finding artifacts

There is a vcpkg search command already that finds ports of libraries in the vcpkg registry. We needed a way to distinguish between the existing vcpkg port concept and the new artifacts concept in areas where the commands could mean either. As such we have introduced a new find command that can be used as find port name, or find artifact name. The existing search command is still present with its existing behavior that only returns ports.

Try finding an artifact, like CMake, with the following command.

`vcpkg find artifact cmake`

This will output anything that matches the short name used, currently the below.

```
vcpkg-ce ('configure environment') is experimental and may change at any time.
 Artifact                       Version  Summary
 microsoft:tools/kitware/cmake  3.20.1   Kitware's cmake tool
```

##### Using artifacts

Now that you have found an artifact you want to use, you can with the vcpkg use command. Try this command to use CMake.

```
vcpkg use cmake 
vcpkg-ce ('configure environment') is experimental and may change at any time.
 Artifact                           Version    Status     Dependency  Summary

 microsoft:tools/kitware/cmake      3.20.1     installed              Kitware's cmake tool

Activating individual artifacts
```

Yes, you can activate more than one artifact at a time. The following command activates gcc, cmake, and ninja, a complete C++ build system in one command. Note this is the Arm GCC compiler as that is the only one presently in the registry.

`vcpkg use gcc cmake ninja`

##### Creating your own manifest

The manifest, vcpkg-configuration.json, in the example above was also created with vcpkg. To create a manifest with tools needed for your own use vcpkg new. Make sure to run the subsequent commands in a new directory that is not a subfolder of an existing project.

`vcpkg new`

##### Adding artifacts to your manifest

Now that we have a manifest and found artifacts we want to use with our project it is simple to add them. Note that the add command requires us to specify an artifact as it can also be used to add ports to a manifest.

```
vcpkg add artifact cmake

vcpkg-ce ('configure environment') is experimental and may change at any time.

 Artifact                       Version  Status     Dependency  Summary

 microsoft:tools/kitware/cmake  3.20.1   installed  *           Kitware's cmake tool

Project c:\source\newprj activated
```

Now you can check in vcpkg-configuration.json with your source. Anyone else who uses your project can install vcpkg with a single command, then activate the artifacts in your manifest and reproduce the same results locally.

#### Subsequent use of vcpkg

In the above examples vcpkg was available on the command line after installation. There is a quick way to get it back in new instances of your favorite terminal.

Linux/macOS

`. ~/.vcpkg/vcpkg-init.sh`

PowerShell

`. ~/.vcpkg/vcpkg-init.ps1`

CMD Shell

`%USERPROFILE%\.vcpkg\vcpkg-init.cmd`

#### Removing vcpkg

That was fun, how do you remove vcpkg installed from your system using the instructions above? Simply delete the .vcpkg folder in your home directory. No other changes have been made to your system through installing or using it.

#### Using your own registry

The current artifacts in the default registry are limited to the embedded scenarios we have been developing the tool around which focus on Azure RTOS. In the future this set will expand to desktop development scenarios. The default registry can be found here: [https://github.com/microsoft/vcpkg-ce-catalog](https://github.com/microsoft/vcpkg-ce-catalog). Note that we are not taking pull requests of artifact additions to the default registries at this time.

We fully expect people to have their own artifacts they would like to use, or to provide for others to use.

As an example, what if you want to use a newer Arm compiler? Our example uses the one set by the example Azure RTOS project so that is the only one we put into the registry. In the steps below I will show how I added a new Arm compiler to my own registry. You can follow the same steps, modified for the artifact you need, to create your own registry of artifacts for use with vcpkg.

To create a new Arm gcc artifact metadata file I looked at the existing artifact metadata for the gcc compiler in the vcpkg-ce-catalog repo, [compilers/arm/gcc/ gcc-2020.10.0.yaml](https://github.com/microsoft/vcpkg-ce-catalog/blob/main/compilers/arm/gcc/gcc-2020.10.0.yaml).

On my local machine I copied that file into a folder, myregistry, under the same path for consistency. I then went to Arm’s website to find the latest compilers they provide. I then renamed the metadata file to match, gcc-2021.10.0.yaml. I updated the fields in the file for the version, the artifact urls under install > unzip, and added the sha256 information. Note that Arm only provides md5 sums for their artifacts, this meant I had to download the artifacts manually first to generate my own sha256 sums to use. You can find this file in my personal GitHub repository here, [gcc-2021.10.0.yaml](https://github.com/robotdad/myregistry/blob/main/compilers/arm/gcc/gcc-2021.10.0.yaml).

Now, to test this I created a test folder and created a manifest with vcpkg new. I then opened this manifest and added a registry section pointing to my local folder with the artifact metadata.

```json
{
    "registries": [
      {
        "name": "myregistry",
        "location": "c:/source/myregistry",
        "kind": "artifact"
      }
    ]
}
```
Note that I specified the full path, alias like ~ are not supported.  Now, to find this entry I specified the name as part of the search query.

```vcpkg find artifact myregistry:gcc

vcpkg-ce ('configure environment') is experimental and may change at any time.
Artifact                 Version    Summary
myregistry:compilers/arm/gcc  2021.10.0  GCC compiler for ARM CPUs.
```

Once verified I added it to the manifest in the same way.

```
vcpkg add artifact local:gcc

vcpkg-ce ('configure environment') is experimental and may change at any time.
Artifact                      Version    Status     Dependency Summary
myregistry:compilers/arm/gcc  2021.10.0  installed  *          GCC compiler for ARM CPUs.

Project c:\source\test activated
```

Now my manifest looks like this:

```json
{
  "registries": [
    {
      "name": "myregistry",
      "location": "c:/source/myregistry",
      "kind": "artifact"
    }
  ],
  "requires": {
    "myregistry:compilers/arm/gcc": "* 2021.10.0"
  }
}
```

I wouldn’t want to share a manifest with others where a local path was used for a registry. Network paths are supported which works if I am only sharing internally. Note I had to escape the path in the location field.

```json
"location": "\\\\myshare\\folder\\myregistry",
```

I wanted to share my registry on GitHub to support this post which requires a couple of extra steps. The first extra step is to generate an index file. To do so I ran the following experimental command (this is likely to change in the future).

`vcpkg z-ce regenerate c:/source/myregistry`

This generated an index.yaml for all of the artifact metadata files in the specified location.

To use a registry published in a GitHub repo I needed to specify the endpoint that provides an archive of the repository. This allows vcpkg to acquire all the artifact metadata in a single request. For a GitHub repo this is available at the path /archive/refs/heads/main.zip under the repository. For this example, I published my registry in my personal GitHub account here, [https://github.com/robotdad/myregistry](https://github.com/robotdad/myregistry), the location for that is specified as below in the manifest.

```json
"location": "https://github.com/robotdad/myregistry/archive/refs/heads/main.zip",
```

#### Give us your feedback!

We are very interested in hearing your thoughts on the new artifact capabilities in vcpkg. We have a separate repo for the component that provides those, [vcpkg-ce](https://github.com/microsoft/vcpkg-ce), where you can file any issues you encounter. The comments below are open, or you can find us on Twitter ([@VisualC](https://twitter.com/visualc)), or via email at [visualcpp@microsoft.com](mailto:visualcpp@microsoft.com). As capabilities around artifacts in vcpkg evolve, your thoughts are critical to us for creating an excellent developer experience.

The post [Bootstrap your dev environment with vcpkg artifacts](https://devblogs.microsoft.com/cppblog/vcpkg-artifacts/) appeared first on [C++ Team Blog](https://devblogs.microsoft.com/cppblog).