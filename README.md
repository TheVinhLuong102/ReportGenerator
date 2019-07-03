<h1 align="center">

<img src="https://raw.githubusercontent.com/danielpalme/ReportGenerator/master/docs/resources/logo_512.png" alt="ReportGenerator" width="256"/>
<br/>
ReportGenerator
</h1>

<b align="center">Powerful code coverage visualization</b>
<div align="center">

[![GitHub license](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://raw.githubusercontent.com/danielpalme/ReportGenerator/master/LICENSE.txt)
[![Build Status](https://dev.azure.com/danielpalme/ReportGenerator/_apis/build/status/danielpalme.ReportGenerator?branchName=master)](https://dev.azure.com/danielpalme/ReportGenerator/_build/latest?definitionId=3&branchName=master)
![Coverage](https://img.shields.io/azure-devops/coverage/danielpalme/ReportGenerator/3.svg)

</div>

*ReportGenerator* converts coverage reports generated by OpenCover, dotCover, Visual Studio, NCover, Cobertura, JaCoCo, Clover, gcov or lcov into human readable reports in various formats.

The reports do not only show the coverage quota, but also include the source code and visualize which lines have been covered.

*ReportGenerator* supports merging several reports into one.

<div align="center">

![Input and output](https://danielpalme.github.io/ReportGenerator/resources/input_output.png)

</div>

## Getting started
*ReportGenerator* is a commandline tool which works with full .NET Framework and .NET Core.  
Use the online [configuration tool](https://danielpalme.github.io/ReportGenerator/usage.html) to get started quickly.

### Install the package matching your platform and needs

|**Package**|**Platforms**|**Installation/Usage**|
|:----------|:------------|:---------------------|
|[ReportGenerator](https://www.nuget.org/packages/ReportGenerator)<br/><br/>[![Nuget](https://img.shields.io/nuget/v/ReportGenerator.svg)![Nuget](https://img.shields.io/nuget/dt/ReportGenerator.svg)](https://www.nuget.org/packages/ReportGenerator)|.NET Core 2.0<br/>.NET Framework 4.7|Use this package if your project is based on *.NET Framework* or *.NET Core* and you want to use *ReportGenerator* via the command line or a build script.<br/><br/>**Usage**<br/>```$(UserProfile)\.nuget\packages\reportgenerator\x.y.z\tools\net47\ReportGenerator.exe [options]```<br/><br/>```dotnet $(UserProfile).nuget\packages\reportgenerator\x.y.z\tools\netcoreapp2.1\ReportGenerator.dll [options]```|
|[dotnet-reportgenerator-cli](https://www.nuget.org/packages/dotnet-reportgenerator-cli)<br/><br/>[![Nuget](https://img.shields.io/nuget/v/dotnet-reportgenerator-cli.svg)![Nuget](https://img.shields.io/nuget/dt/dotnet-reportgenerator-cli.svg)](https://www.nuget.org/packages/dotnet-reportgenerator-cli)|.NET Core 2.0|Use this package if your project is based on *.NET Core* and you want to use *ReportGenerator* as a 'DotnetCliTool'.<br/><br/>**Installation**<br/>Add `<DotNetCliToolReference Include="dotnet-reportgenerator-cli" Version="x.y.z" />` to your project file.<br/><br/>**Usage**<br/>```dotnet reportgenerator [options]```|
|[dotnet-reportgenerator-globaltool](https://www.nuget.org/packages/dotnet-reportgenerator-globaltool)<br/><br/>[![Nuget](https://img.shields.io/nuget/v/dotnet-reportgenerator-globaltool.svg)![Nuget](https://img.shields.io/nuget/dt/dotnet-reportgenerator-globaltool.svg)](https://www.nuget.org/packages/dotnet-reportgenerator-globaltool)|.NET Core 2.1|Use this package if your project is based on *.NET Core* and you want to use *ReportGenerator* as a (global) 'DotnetTool'.<br/><br/>**Installation**<br/>```dotnet tool install -g dotnet-reportgenerator-globaltool```<br/>```dotnet tool install dotnet-reportgenerator-globaltool --tool-path tools```<br/><br/>**Usage**<br/>```reportgenerator [options]```<br/>```tools\reportgenerator.exe [options]```|
|[ReportGenerator.Core](https://www.nuget.org/packages/ReportGenerator.Core)<br/><br/>[![Nuget](https://img.shields.io/nuget/v/ReportGenerator.Core.svg)![Nuget](https://img.shields.io/nuget/dt/ReportGenerator.Core.svg)](https://www.nuget.org/packages/ReportGenerator.Core)|.NET Standard 2.0|Use this package if you want to write a custom **plugin** for *ReportGenerator* or if you want to call/execute *ReportGenerator* within your code base.<br/><br/>**Plugin development**<br/>[Custom reports](https://github.com/danielpalme/ReportGenerator/wiki/Custom-reports)<br/>[Custom history storage](https://github.com/danielpalme/ReportGenerator/wiki/Custom-history-storage)|
|[Azure DevOps extension](https://marketplace.visualstudio.com/items?itemName=Palmmedia.reportgenerator)<br/><br/>[![Visual Studio Marketplace Version](https://img.shields.io/visual-studio-marketplace/v/Palmmedia.reportgenerator.svg)![Visual Studio Marketplace Installs - Azure DevOps Extension](https://img.shields.io/visual-studio-marketplace/azure-devops/installs/total/Palmmedia.reportgenerator.svg)](https://marketplace.visualstudio.com/items?itemName=Palmmedia.reportgenerator)|.NET Core 2.1| Add the Azure DevOps extension to your build pipeline.<br />[Learn more](https://github.com/danielpalme/ReportGenerator/wiki/Integration#azure-devops-extension)|

### Usage / Command line parameters
```
Parameters:
    ["]-reports:<report>[;<report>][;<report>]["]
    ["]-targetdir:<target directory>["]
    [["]-reporttypes:<Html|HtmlSummary|...>[;<Html|HtmlSummary|...>]["]]
    [["]-sourcedirs:<directory>[;<directory>][;<directory>]["]]
    [["]-historydir:<history directory>["]]
    [["]-plugins:<plugin>[;<plugin>][;<plugin>]["]]
    [["]-assemblyfilters:<(+|-)filter>[;<(+|-)filter>][;<(+|-)filter>]["]]
    [["]-classfilters:<(+|-)filter>[;<(+|-)filter>][;<(+|-)filter>]["]]
    [["]-filefilters:<(+|-)filter>[;<(+|-)filter>][;<(+|-)filter>]["]]
    [["]-verbosity:<Verbose|Info|Warning|Error|Off>["]]
    [["]-tag:<tag>["]]

Explanations:
   Reports:            The coverage reports that should be parsed (separated by semicolon).
                       Globbing is supported.
   Target directory:   The directory where the generated report should be saved.
   Report types:       The output formats and scope (separated by semicolon).
                       Values: Badges, Cobertura, CsvSummary, Html, HtmlChart, HtmlInline,
                       HtmlInline_AzurePipelines, HtmlInline_AzurePipelines_Dark, HtmlSummary, Latex, 
                       LatexSummary, MHtml, PngChart, SonarQube, TeamCitySummary, TextSummary, Xml, XmlSummary
   Source directories: Optional directories which contain the corresponding source code (separated by semicolon).
                       The source directories are used if coverage report contains classes without path information.
   History directory:  Optional directory for storing persistent coverage information.
                       Can be used in future reports to show coverage evolution.
   Plugins:            Optional plugin files for custom reports or custom history storage (separated by semicolon). 
   Assembly filters:   Optional list of assemblies that should be included or excluded in the report.
   Class filters:      Optional list of classes that should be included or excluded in the report.
   File filters:       Optional list of files that should be included or excluded in the report.
                       Exclusion filters take precedence over inclusion filters.                      
                       Wildcards are allowed.
   Verbosity:          The verbosity level of the log messages.
                       Values: Verbose, Info, Warning, Error, Off
   Tag:                Optional tag or build version.

Default values:
   -reporttypes:Html
   -assemblyfilters:+*
   -classfilters:+*
   -filefilters:+*
   -verbosity:Verbose

Examples:
   "-reports:coverage.xml" "-targetdir:C:\report"
   "-reports:target\*\*.xml" "-targetdir:C:\report" -reporttypes:Latex;HtmlSummary -tag:v1.4.5
   "-reports:coverage1.xml;coverage2.xml" "-targetdir:report" "-sourcedirs:C:\MyProject" -plugins:CustomReports.dll
   "-reports:coverage.xml" "-targetdir:C:\report" "-assemblyfilters:+Included;-Excluded.*"
```

**MSBuild**  
A MSBuild task also exists:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project DefaultTargets="Coverage" xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ToolsVersion="4.0">
  <ItemGroup>
    <PackageReference Include="ReportGenerator" Version="x.y.z" />
  </ItemGroup>
  <Target Name="Coverage">
    <ItemGroup>
      <CoverageFiles Include="OpenCover.xml" />
    </ItemGroup>
    <ReportGenerator ReportFiles="@(CoverageFiles)" TargetDirectory="report" ReportTypes="Html;Latex" HistoryDirectory="history" Plugins="CustomReports.dll" AssemblyFilters="+Include;-Excluded" VerbosityLevel="Verbose" />
  </Target>
</Project>
```

## Supported input and output file formats
*ReportGenerator* supports several input and output formats.  
The wiki explains the different [output formats](https://github.com/danielpalme/ReportGenerator/wiki/Output-formats) or you can download [sample reports](https://danielpalme.github.io/ReportGenerator/resources/SampleReports.zip) of all formats.  
If you need a custom format, you can create a [plugin](https://github.com/danielpalme/ReportGenerator/wiki/Custom-reports).

| **Input formats** | **Output formats** |
|:------------------|:-------------------|
| <ul><li>[OpenCover](https://github.com/OpenCover/opencover) ([Nuget](https://www.nuget.org/packages/OpenCover))<br/>OpenCover format is also generated by [coverlet](https://github.com/tonerdo/coverlet/) and [altcover](https://github.com/SteveGilham/altcover)</li><li>[dotCover](https://www.jetbrains.com/dotcover/help/dotCover__Console_Runner_Commands.html) ([Nuget](https://www.nuget.org/packages/JetBrains.dotCover.CommandLineTools/), /ReportType=DetailedXML)</li><li>Visual Studio ([vstest.console.exe](https://github.com/danielpalme/ReportGenerator/wiki/Visual-Studio-Coverage-Tools#vstestconsoleexe), [CodeCoverage.exe](https://github.com/danielpalme/ReportGenerator/wiki/Visual-Studio-Coverage-Tools#codecoverageexe))</li><li>[NCover](https://www.ncover.com/info/download) (tested version 1.5.8, other versions may not work)</li><li>[Cobertura](https://github.com/cobertura/cobertura)</li><li>[JaCoCo](https://www.jacoco.org/jacoco/index.html)</li><li>[Clover](https://openclover.org/)</li><li>Mono ([mprof-report](https://www.mono-project.com/docs/debug+profile/profile/profiler/#analyzing-the-profile-data))</li><li>[gcov](https://gcc.gnu.org/onlinedocs/gcc/Gcov.html)</li><li>[lcov](https://github.com/linux-test-project/lcov)</li></ul> | <ul><li>HTML, HTMLSummary, HTMLInline, HtmlInline_AzurePipelines, HtmlInline_AzurePipelines_Dark, HTMLChart, [MHTML](https://en.wikipedia.org/wiki/MHTML)</li><li>Cobertura</li><li>[SonarQube](https://docs.sonarqube.org/latest/analysis/generic-test)</li><li>XML, XMLSummary</li><li>Latex, LatexSummary</li><li>TextSummary</li><li>CsvSummary</li><li>PngChart</li><li>Badges</li><li>[Custom reports](https://github.com/danielpalme/ReportGenerator/wiki/Custom-reports)</li></ul><br /><br /> |

### Screenshots
The screenshots show two snippets of the generated reports:
![Screenshot 1](https://danielpalme.github.io/ReportGenerator/resources/screenshot1.png)
![Screenshot 2](https://danielpalme.github.io/ReportGenerator/resources/screenshot2.png)

**Badges**  
Badges in SVG and PNG format can be generated if `-reporttypes:Badges` is used:

![Sample badge](https://danielpalme.github.io/ReportGenerator/resources/badge.svg)

## Resources

### Links
* https://www.palmmedia.de/Blog/2017/12/6/reportgenerator-new-release-with-risk-hotspots-analysis
* https://www.palmmedia.de/Blog/2016/11/6/reportgenerator-new-release-with-enhanced-html-report-and-cobertura-support
* https://www.palmmedia.de/Blog/2015/1/27/reportgenerator-new-beta-with-historytrend-charts
* https://www.palmmedia.de/Blog/2012/4/29/reportgenerator-new-release-with-more-advanced-report-preprocessing

### Download statistics
![Nuget](https://img.shields.io/nuget/dt/ReportGenerator.svg?label=ReportGenerator%40nuget)
![Nuget](https://img.shields.io/nuget/dt/dotnet-reportgenerator-cli.svg?label=dotnet-reportgenerator-cli%40nuget)
![Nuget](https://img.shields.io/nuget/dt/dotnet-reportgenerator-globaltool.svg?label=dotnet-reportgenerator-globaltool%40nuget)
![Nuget](https://img.shields.io/nuget/dt/ReportGenerator.Core.svg?label=ReportGenerator.Core%40nuget)

![Visual Studio Marketplace Installs - Azure DevOps Extension](https://img.shields.io/visual-studio-marketplace/azure-devops/installs/total/Palmmedia.reportgenerator.svg?label=Azure%20DevOps)
![GitHub All Releases](https://img.shields.io/github/downloads/danielpalme/ReportGenerator/total.svg?label=GitHub)
![Chocolatey](https://img.shields.io/chocolatey/dt/reportgenerator.portable.svg?label=Chocolatey)

## Contact

Author: Daniel Palme  
Blog: [www.palmmedia.de](https://www.palmmedia.de)  
Twitter: [@danielpalme](https://twitter.com/danielpalme)  
