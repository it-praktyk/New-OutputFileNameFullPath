# New-OutputObject Module

## Description and examples of usage

The PowerShell module intended for preparing PowerShell objects what the next help output filesystem objects, means: files and folders.

Would you like prepare names files/folders name like - where any part in "<>" can be provided directly as a parameter of function

- a folder name like: \<MySuperServer>\<\_>\<DailyReport\>\<_\>\<1\>\<\_\>\<20170508\>

```powershell
New-OutputFolder -OutputFolderNamePrefix MySuperServer -OutputFolderNameMidPart DailyReport -OutputFolderNameSuffix 1 -NamePartsSeparator "_"
```

or

- a file name like: \<SuperImportantFile>\<->\<Generated on server>\<->\<SV004>-\<20170508-123400>.\<pdf>

```powershell
New-OutputFile -OutputFileNamePrefix SuperImportantFile -OutputFileNameMidPart "Generated on server" -OutputFileNameSuffix $(Get-Item env:computername).value -OutputFileNameExtension pdf
```

Functions from the New-OutputObject module do:

- check if prepared path contains chars what are supported by FileSystem PSProvider
- check if the provided parent path exist
- checks if the provided path is writable
- prepares the file/folder name based on the path, prefix, suffix, date etc.
- checks if the file/folder already exist and display dialog with a warning and a question about overwrite decission
- returns the PowerShell object what contains e.g. [System.IO.FileInfo]

Functions from the New-OutputObject don't

- create file/folder (except that used to check if destination - parent path - is writable but that files/folders are not retained).


## Feedbacks and comments

Your comments - preferable via GitHub issues - and  pull requests are welcomed.

The current module version: 0.9.9 - 2017-05-16.  
The history of versions you can find [here](VERSIONS.md).

The module you can download directly from GitHub or  from the [PowerShellGallery](https://www.powershellgallery.com/packages/New-OutputObject/).

## New-OutputObject Cmdlets

### New-OutputFile

#### SYNOPSIS

Function intended for preparing a PowerShell object for output files like reports or logs.

#### DESCRIPTION

Function intended for preparing a PowerShell custom object what contains e.g. file name for output/create files like reports or log. The name is prepared based on prefix, middle name part, suffix, date, etc. with verification if provided path exist and is it writable.

##### Supported options

|ParameterName|DefaultValue|Remarks|
|:---|:---:|:---|
|ParentPath| .\\||
|OutputFileNamePrefix|Output||
|OutputFileNameMidPart|||
|OutputFileNameSuffix|||
|IncludeDateTimePartInOutputFileName|true|||
|DateTimePartInOutputFileName| Get-Date ||
|DateTimePartFormat|yyyyMMdd-HHmmss||
|OutputFileNameExtension|txt||
|NamePartsSeparator|-||
|BreakIfError||If not used for some non critical errors returned object can't be suitable to create file|

##### Returned object contains properties

|Property name|Property type|Remarks|
|--|--|--|
|OutputObjectPath|[\[System.IO.FileInfo\]](https://msdn.microsoft.com/en-us/library/system.io.fileinfo(v=vs.110).aspx)|For an ExitCode=2 OutputObjectPath is equal null|
|OutputFilePath|[\[System.IO.FileInfo\]](https://msdn.microsoft.com/en-us/library/system.io.fileinfo(v=vs.110).aspx)|alias of OutputFilePath|
|ExitCode|[Int]||
|ExitCodeDescription|[String]||

##### Returned exit codes and descriptions

|Exit code|Description|
|:---:|:---|
|  0  |Everything is fine :-)|
|  1  |Provided path \<PATH> doesn't exist|
|  2  |The result name contains unacceptable chars|
|  3  |Provided patch \<PATH> is not writable|
|  4  |The file \<PATH>\\<FILE_NAME> already exist  - can be overwritten|
|  5  |The file \<PATH>\\<FILE_NAME> already exist  - can't be overwritten|

Detailed help and examples for the New-ObjectFile you can find  [here\](Help/New-OutputFile.md)

### New-OutputFolder

#### SYNOPSIS

Function intended for preparing a PowerShell object for output/create folders for reports logs, etc.

#### DESCRIPTION

Function intended for preparing a PowerShell custom object what contains e.g.folder name for output/create folders. The name is prepared based on prefix, middle name part, suffix, date, etc. with verification if provided path exist and is it writable.

##### Supported options

|ParameterName|DefaultValue|Remarks|
|:---|:---:|:---|
|ParentPath| .\\||
|OutputFolderNamePrefix|Output||
|OutputFolderNameMidPart|||
|OutputFolderNameSuffix|||
|IncludeDateTimePartInOutputFolderName|true|||
|DateTimePartInOutputFolderName| Get-Date ||
|DateTimePartFormat|yyyyMMdd||
|NamePartsSeparator|-||
|BreakIfError||If not used for some non critical errors returned object can't be suitable to create Folder|

###### Returned object contains properties

|Property name|Property type|Remarks|
|--|--|--|
|OutputObjectPath|[\[System.IO.DirectoryInfo\]](https://msdn.microsoft.com/en-us/library/system.io.directoryinfo(v=vs.110).aspx)|For an ExitCode=2 OutputObjectPath is equal null|
|OutputFolderPath|[\[System.IO.DirectoryInfo\]](https://msdn.microsoft.com/en-us/library/system.io.directoryinfo(v=vs.110).aspx)|alias of OutputFolderPath|
|ExitCode|[Int]||
|ExitCodeDescription|[String]||

###### Returned exit codes and descriptions

|Exit code|Description|
|:---:|:---|
|  0  |Everything is fine :-)|
|  1  |Provided parent path \<PATH> doesn't exist|
|  2  |The result name contains unacceptable chars|
|  3  |Provided patch \<PATH> is not writable|
|  4  |The folder \<PATH>\\<FOLDER_NAME> already exist  - can be overwritten|
|  5  |The folder \<PATH>\\<FOLDER_NAME> already exist  - can't be overwritten|

Detailed help and examples for the New-ObjectFolder you can find  [here\](Help/New-OutputFolder.md)

### New-OutputObject

The behaviour of the New-OutputObject is determined by the value of parameter ObjectType what can be: File or Folder. Generally it's a main functiot, functions New-OutputFile and New-OutputFolder are only proxy to call the New-OutputObject with selected parameter ObjectType.

## LICENSE

Copyright (c) 2016 Wojciech Sciesinski  
This function is licensed under The MIT License (MIT)  
Full license text: https://opensource.org/licenses/MIT

## TODO

For to do and developments plans please check [TODO.md file](TODO.md).
