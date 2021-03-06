---
title: project.json reference
description: project.json reference
keywords: .NET, .NET Core, project.json
author: aL3891
manager: wpickett
ms.date: 07/06/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3aef32bd-ee2a-4e24-80f8-a2b615e0336d
translationtype: Human Translation
ms.sourcegitcommit: 1c9d71e08bdf49f3e15339c6ba83077204f01045
ms.openlocfilehash: 1eca599b0e83a580b618a46b06fe4ce4237a1331

---

# project.json reference

> [!NOTE]
> This topic is preliminary and subject to change in the next release. You can track the status of this issue through our public GitHub issue tracker.

## name
Type: String

The name of the project, used for the assembly name as well as the name of the package. The top level folder name is used if this property is not specified.

For example:

    {
        "name": "MyLibrary"
    }

## version
Type: String

The [Semver](http://semver.org/spec/v1.0.0.html) version of the project, also used for the NuGet package.

For example:

    {
        "version": "1.0.0-*"
    }

## description
Type: String

A longer description of the project. Used in the assembly properties.

For example:

    {
        "description": "This is my library and it's really great!"
    }

## copyright
Type: String

The copyright information for the project. Used in the assembly properties.

For example:

    {
        "copyright": "Fabrikam 2016"
    }

## title
Type: String

The friendly name of the project, can contain spaces and special characters not allowed when using the `name` property. Used in the assembly properties.

For example:

    {
        "title": "My Library"
    }

## entryPoint
Type: String

The entrypoint method for the project. `Main` by default.

For example:

    {
        "entryPoint": "ADifferentMethod"
    }
    
## testRunner
Type: String

The name of the test runner, such as [NUnit](http://nunit.org/) or [xUnit](http://xunit.github.io/), to use with this project. Setting this also marks the project as a test project.

For example:

    {
        "testRunner": "NUnit"
    }

## authors
Type: String[]

An array of strings with the names of the authors of the project.

For example:

    {
        "authors": ["Anne", "Bob"]
    }

## language
Type: String

The (human) language of the project. Corresponds to the "neutral-language" compiler argument.

For example:

    {
        "language": "en-US"
    }

## embedInteropTypes
Type: Boolean

**true** to embed COM interop types in the assembly; otherwise, **false**. 

For example:

    {
        "embedInteropTypes": true
    }

## preprocess
Type: String or String[] with a globbing pattern

Specifies which files are included in preprocessing.

For example:

    {
        "preprocess": "compiler/preprocess/**/*.cs"
    }

## shared
Type: String or String[] with a globbing pattern

Specifies which files are shared, this is used for library export.

For example:

    {
        "shared": "shared/**/*.cs"
    }

## dependencies
Type: Object

An object that defines the package dependencies of the project, each key of this object is the name of a package and each value contains versioning information.

For example:

    "dependencies": {
        "System.Reflection.Metadata": "1.3.0",
        "Microsoft.Extensions.JsonParser.Sources": {
          "type": "build",
          "version": "1.0.0-rc2-20221"
        },
        "Microsoft.Extensions.HashCodeCombiner.Sources": {
          "type": "build",
          "version": "1.1.0-alpha1-21456"
        },
        "Microsoft.Extensions.DependencyModel": "1.0.0-*"
    }

## tools
Type: Object

An object that defines package dependencies that are used as tools for the current project, not as references. Packages defined here are available in scripts that run during the build process, but they are not accessible to the code in the project itself. Tools can for example include code generators or post-build tools that perform tasks related to packing.

For example:

    {
        "tools": {
            "MyObfuscator": "1.2.4"
        }
    }

## scripts
Type: Object

An object that defines scripts run during the build process. Each key in this object identifies where in the build the script is run. Each value is either a string with the script to run or an array of strings containing scripts that will run in order.
The supported events are:
* precompile
* postcompile
* prepublish
* postpublish

For example:

    {
        "scripts": {
            "precompile": "generateCode.cmd"
            "postcompile": [ "obfuscate.cmd", "removeTempFiles.cmd" ]
        }
    }

## buildOptions
Type: Object

An object whose properties control various aspects of compilation. The valid properties are listed below. Can also be specified per target framework as described in the [frameworks section](#frameworks).

For example:

    "buildOptions": {
      "allowUnsafe": true,
      "emitEntryPoint": true
    }

### define
Type: String[]

A list of defines such as "DEBUG" or "TRACE" that can be used in conditional compilation in the code.

For example:

    {
        "buildOptions": {
            "define": ["TEST", "OTHERCONDITION"]
        }
    }

### nowarn
Type: String[]

A list of warnings to ignore.

For example:

    {
        "buildOptions": {
            "nowarn": ["CS0168", "CS0219"]
        }
    }

This ignores the warnings `The variable 'var' is assigned but its value is never used` and `The variable 'var' is assigned but its value is never used`

### additionalArguments
Type: String[]

A list of extra arguments that will be passed to the compiler.

For example:

    {
        "buildOptions": {
            "additionalArguments": ["/parallel", "/nostdlib"]
        }
    }

### warningsAsErrors
Type: Boolean

**true** to treat warnings as errors; otherwise, **false**. The default is **false**.

For example:

    {
        "buildOptions": {
            "warningsAsErrors": true
        }
    }

### allowUnsafe
Type: Boolean

**true** to allow unsafe code in this project; otherwise, **false**. The default is **false**.

For example:

    {
        "buildOptions": {
            "allowUnsafe": true
        }
    }

### emitEntryPoint
Type: Boolean

**true** to create an executable; **false** to produce a `.dll` file. The default is **false**.

For example:

    {
        "buildOptions": {
            "emitEntryPoint": true
        }
    }

### optimize
Type: Boolean

**true** to enable the compiler to optimize the code in this project; otherwise, **false**. The default is **false**.

For example:

    {
        "buildOptions": {
            "optimize": true
        }
    }

### platform
Type: String

The name of the target platform, such as AnyCpu, x86 or x64.

For example:

    {
        "buildOptions": {
            "platform": "x64"
        }
    }

### languageVersion
Type: String

The version of the language used by the compiler: ISO-1, ISO-2, 3, 4, 5, 6, or Default

For example:

    {
        "buildOptions": {
            "languageVersion": "5"
        }
    }

### keyFile
Type: String

The path for the key file used for signing this assembly.

For example:

    {
        "buildOptions": {
            "keyFile": "../keyfile.snk"
        }
    }

### delaySign
Type: Boolean

**true** to delay signing; otherwise, **false**. The default is **false**.

For example:

    {
        "buildOptions": {
            "delaySign": true
        }
    }

### publicSign
Type: Boolean

**true** to enable signing of the resulting assembly; otherwise, **false**. The default is **false**.

For example:

    {
        "buildOptions": {
            "publicSign": true
        }
    }

### debugType
Type: String

Indicates the type of symbol file (PDB file) to generate. The options are "portable" (for .NET Core projects), "full" (the traditional Windows-only PDB files) or "none".

For example:

    {
        "buildOptions": {
            "debugType": "portable"
        }
    }

### xmlDoc
Type: Boolean

**true** to generate XML documentation from triple-slash comments in the source code; otherwise, **false**. The default is **false**.

For example:

    {
        "buildOptions": {
            "xmlDoc": true
        }
    }

### preserveCompilationContext
Type: Boolean

**true** to preserve reference assemblies and other context data to allow for runtime compilation; otherwise, **false**. The default is **false**.

For example:

    {
        "buildOptions": {
            "preserveCompilationContext": true
        }
    }

### outputName
Type: String

Change the name of the output file. 

For example:

    {
        "buildOptions": {
            "outputName": "MyApp"
        }
    }

### compilerName
Type: String

The name of the compiler used for this project. `csc` by default. Currently, `csc` (the C# compiler) or `fsc` (the F# compiler) are supported.
 
For example:

    {
        "compilerName": "fsc"
    }
    
### compile
Type: Object

An object containing properties for compilation configuration.

#### include
Type: String or String[] with a globbing pattern.

Specifies which files to include in the build. The patterns are rooted at the project folder. Defaults to none.

For example:

    {
        "include":["wwwroot", "Views"]
    }

#### exclude
Type: String or String[] with a globbing pattern.

Specifies which files to exclude from the build. The exclude patterns have higher priority than the include patterns, so a file found in both will be excluded. The patterns are rooted at the project folder. Defaults to none.

For example:

    {
        "exclude": ["bin/**", "obj/**"]
    }

#### includeFiles

Type: String or String[] with a globbing pattern.

A list of file paths to include. The paths are rooted at the project folder. This list has a higher priority than the include and exclude globbing patterns, hence a file listed here and in the exclude globbing pattern will still be included. Defaults to none.

For example:

    {
        "includeFiles": []
    }

#### excludeFiles

Type: String or String[] with a globbing pattern.

A list of file paths to exclude. The paths are rooted at the project folder. This list has a higher priority than globbing patterns and the include paths, hence a file found in all will be excluded. Defaults to none.

For example:

    {
        "excludeFiles":[],
    }

#### builtIns

Type: Object

The defaults provided by the system. It can have `include` and `exclude` globbing patterns which are merged with the corresponding values of the `include` and `exclude` properties.

For example:

    {
        "builtIns":{}
    }

#### mappings
Type: Object

Keys to the object represent destination paths in the output layout.

Values are either a string or an object representing the source path of files to include.  The object represtation can have its own `include`, `exclude`, `includeFiles` and `excludeFiles` sections.

String example:

    {
        "mappings": {
            "dest/path": "./src/path"
        }
    }

Object example:

    {
        "mappings": {
            "dest/path":{
                "include":"./src/path"
            }
        }
    }

### embed
Type: Object

An object containing properties for compilation configuration.

#### include
Type: String or String[] with a globbing pattern.

    {
        "include":["wwwroot", "Views"]
    }

#### exclude
Type: String or String[] with a globbing pattern.

Specifies which files to exclude from the build.

For example:

    {
        "exclude": ["bin/**", "obj/**"]
    }

#### includeFiles

Type: String or String[] with a globbing pattern.

    {
        "includeFiles":[],
    }

#### excludeFiles

Type: String or String[] with a globbing pattern.

    {
        "excludeFiles":[],
    }

#### builtIns
Type: Object

    {
        "builtIns":{}
    }

#### mappings
Type: Object

Keys to the object represent destination paths in the output layout.

Values are either a string or an object representing the source path of files to include.  The object represtation can have its own `include`, `exclude`, `includeFiles` and `excludeFiles` sections.

String example:

    {
        "mappings": {
            "dest/path": "./src/path"
        }
    }

Object example:

    {
        "mappings": {
            "dest/path":{
                "include":"./src/path"
            }
        }
    }

### copyToOutput
Type: Object

An object containing properties for compilation configuration.

#### include
Type: String or String[] with a globbing pattern.

    {
        "include":["wwwroot", "Views"]
    }

#### exclude
Type: String or String[] with a globbing pattern.

Specifies which files to exclude from the build.

For example:

    {
        "exclude": ["bin/**", "obj/**"]
    }

#### includeFiles

Type: String or String[] with a globbing pattern.

    {
        "includeFiles":[],
    }

#### excludeFiles

Type: String or String[] with a globbing pattern.

    {
        "excludeFiles":[],
    }

#### builtIns
Type: Object

    {
        "builtIns":{}
    }

#### mappings
Type: Object

Keys to the object represent destination paths in the output layout.

Values are either a string or an object representing the source path of files to include.  The object represtation can have its own `include`, `exclude`, `includeFiles` and `excludeFiles` sections.

String example:

    {
        "mappings": {
            "dest/path": "./src/path"
        }
    }

Object example:

    {
        "mappings": {
            "dest/path":{
                "include":"./src/path"
            }
        }
    }

## publishOptions
Type: Object

An object containing properties for compilation configuration.

### include
Type: String or String[] with a globbing pattern.

    {
        "include":["wwwroot", "Views"]
    }

### exclude
Type: String or String[] with a globbing pattern.

Specifies which files to exclude from the build.

For example:

    {
        "exclude": ["bin/**", "obj/**"]
    }

### includeFiles

Type: String or String[] with a globbing pattern.

    {
        "includeFiles":[],
    }

### excludeFiles

Type: String or String[] with a globbing pattern.

    {
        "excludeFiles":[],
    }

### builtIns
Type: Object

    {
        "builtIns":{}
    }

### mappings
Type: Object

Keys to the object represent destination paths in the output layout.

Values are either a string or an object representing the source path of files to include.  The object represtation can have its own `include`, `exclude`, `includeFiles` and `excludeFiles` sections.

String example:

    {
        "mappings": {
            "dest/path": "./src/path"
        }
    }

Object example:

    {
        "mappings": {
            "dest/path":{
                "include":"./src/path"
            }
        }
    }

## runtimeOptions
Type: Object

Specifies parameters to be provided to the runtime during initialization.

### configProperties
Type: Object

Contains configuration properties to configure the runtime and the framework.

#### System.GC.Server
Type: Boolean

**true** to enable server garbage collection; otherwise, **false**. The default is **false**.

For example:

    {
        "runtimeOptions": {
            "configProperties": {
                "System.GC.Server": true
            }
        }
    }

#### System.GC.Concurrent
Type: Boolean

**true** to enable concurrent garbage collection; otherwise, **false**. The default is **false**.

For example:

    {
        "runtimeOptions": {
            "configProperties": {
                "System.GC.Concurrent": true
            }
        }
    }

#### System.GC.RetainVM
Type: Boolean

**true** to put segments that should be deleted on a standby list for future use instead of releasing them back to the operating system (OS); otherwise, **false**.

For example:

    {
        "runtimeOptions": {
            "configProperties": {
                "System.GC.RetainVM": true
            }
        }
    }

#### System.Threading.ThreadPool.MinThreads
Type: Integer

Overrides the number of minimum threads for the ThreadPool worker pool.

    {
        "runtimeOptions": {
            "configProperties": {
                "System.Threading.ThreadPool.MinThreads": 4
            }
        }
    }

#### System.Threading.ThreadPool.MaxThreads
Type: Integer

Overrides the number of maximum threads for the ThreadPool worker pool.

    {
        "runtimeOptions": {
            "configProperties": {
                "System.Threading.ThreadPool.MaxThreads": 25
            }
        }
    }

### framework
Type: Object

Contains shared framework properties to use when activating the application. The presence of this section indicates that the application is a portable app designed to use a shared redistributable framework.

#### name
Type: String

Name of the shared framework.

    {
        "runtimeOptions": {
            "framework": {
                "name": "Microsoft.DotNetCore"
            }
        }
    }

#### version
Type: String

Version of the shared framework.

    {
        "runtimeOptions": {
            "framework": {
                "version": "1.0.1"
            }
        }
    }

### applyPatches
Type: Boolean

**true** to use the framework from either the same or a higher version that differs only in the `SemVer` patch field. **false** for the host to use only the exact framework version. The default is **true**.

    {
        "runtimeOptions": {
            "applyPatches": false
        }
    }

## packOptions
Type: Object

Defines options pertaining to the packaging of the project output into a NuGet package.

### summary
Type: String

A short description of the project.

For example:

    {
        "packOptions": {
            "summary": "This is my library."
        }
    }

### tags
Type: String[]

An array of strings with tags for the project, used for searching in NuGet.

For example:

    {
        "packOptions": {
            "tags": ["hyperscale", "cats"]
        }
    }

### owners
Type: String[]

An array of strings with the names of the owners of the project.

For example:

    {
        "packOptions": {
            "owners": ["Fabrikam", "Microsoft"]
        }
    }

### releaseNotes
Type: String

Release notes for the project.

For example:

    {
        "packOptions": {
            "releaseNotes": "Initial version, implemented flimflams."
        }
    }

### iconUrl
Type: String

The URL for an icon that will be used in various places such as the package explorer.

For example:

    {
        "packOptions": {
            "iconUrl": "http://www.mylibrary.gov/favicon.ico"
        }
    }

### projectUrl
Type: String

The URL for the homepage of the project.

For example:

    {
        "packOptions": {
            "projectUrl": "http://www.mylibrary.gov"
        }
    }

### licenseUrl
Type: String

The URL for the license the project uses.

For example:

    {
        "packOptions": {
            "licenseUrl": "http://www.mylibrary.gov/licence"
        }
    }

### requireLicenseAcceptance
Type: Boolean

**true** to cause a prompt to accept the package license when installing the package to be shown; otherwise, **false**. Only used for NuGet packages, ignored in other uses. The default is **false**.

For example:

    {
        "packOptions": {
            "requireLicenseAcceptance": true
        }
    }
   
### repository
Type: Object

Contains information about the repository where the project is stored.

#### type
Type: String

Type of the repository. The default value is "git".

For example:

    {
        "packOptions": {
            "repository": {
                "type": "git"
            }
        }
    }

#### url
Type: String

URL of the repository where the project is stored.

For example:

    {
        "packOptions": {
            "repository": {
                "url": "http://github.com/dotnet/corefx"
            }
        }
    }

### files

#### include
Type: String or String[] with a globbing pattern.

    {
        "include":["wwwroot", "Views"]
    }

#### exclude
Type: String or String[] with a globbing pattern.

Specifies which files to exclude from the build.

For example:

    {
        "exclude": ["bin/**", "obj/**"]
    }

#### includeFiles

Type: String or String[] with a globbing pattern.

    {
        "includeFiles":[]
    }

#### excludeFiles

Type: String or String[] with a globbing pattern.

    {
        "excludeFiles":[]
    }

#### builtIns
Type: Object

    {
        "builtIns":{}
    }

#### mappings
Type: Object

Keys to the object represent destination paths in the output layout.

Values are either a string or an object representing the source path of files to include.  The object representation can have its own `include`, `exclude`, `includeFiles` and `excludeFiles` sections. 

String example:

    {
        "mappings": {
            "dest/path": "./src/path"
        }
    }

Object example:

    {
        "mappings": {
            "dest/path":{
                "include":"./src/path"
            }
        }
    }

## analyzerOptions
Type: Object

An object with properties used by code analysers.

For example:

    {
        "analyzerOptions": { }
    }

### languageId
Type: String

The id of the language to analyze. "cs" represents C#, "vb" represents Visual Basic and "fs" represents F#.

For example:

    "analyzerOptions": {
      "languageId": "vb"
      }
    }

## configurations
Type: Object

An object whose properties define different configurations for this project, such as Debug and Release. Each value is an object that can contain a `buildOptions` object with options specific for this configuration.

For example:

    "configurations": {
      "Release": {
        "buildOptions": {
          "allowUnsafe": false
        }
      }
    }

## frameworks
Type: Object

Specifies which frameworks this project supports, such as the .NET Framework or Universal Windows Platform (UWP). Must be a valid Target Framework Moniker (TFM). Each value is an object that can contain information specific to this framework such as `buildOptions`, `analyzerOptions`, `dependencies` as well as the properties in the following sections.

For example:

    "frameworks": {
        "netcoreapp1.0": {
            "buildOptions": {
                "define": ["FOO", "BIZ"]
            }
        }
    }

### dependencies
Type: Object

Dependencies that are specific for this framework. This is useful in scenarios where you cannot simply specify a package-level dependency across all targets. Reasons for this can include one target lacking built-in support that other targets have, or requiring a different version of a dependency than other targets.

For example:

    "frameworks": {
        "netstandard1.5": {
            "dependencies": {
                "Microsoft.Extensions.JsonParser.Sources": "1.0.0-rc2-20221"
            }
        }
    }

### frameworkAssemblies
Type: Object

Similar to dependencies but contains reference to assemblies in the GAC that are not NuGet packages. Can also specify the version to use as well as the dependency type. This is used when targeting .NET Framework and Portable Class Library (PCL) targets. You can only build a project with this specified on Windows.

For example:

    "frameworks": {
        "net451": {
            "frameworkAssemblies": {
                "System.Runtime": {
                    "type": "build",
                    "version": "4.0.0"
                }
            }
        }

### wrappedProject
Type: String

Specifies the location of the dependency project. 

For example:

    "frameworks": {
        "net451": {
            "wrappedProject": "MyProject.csproj"
            }
        }

### bin
Type: Object

An object with a single property, `assembly`, whose value is the assembly path.

For example:

    "frameworks": {
      "netcoreapp1.0": {
         "bin": {
           "assembly" :"c:/otherProject/otherdll.dll"
        }
      }
    }

### imports
Type: String

Specifies other framework profiles that this project is compatible with.

For example:

    "frameworks": {
      "netcoreapp1.0": {
         "imports": "portable-net45+win8"
      }
    }

Will cause other packages targeting `portable-net45+win8` to be usable when targeting `netcoreapp1.0` with the current project.



<!--HONumber=Aug16_HO2-->


