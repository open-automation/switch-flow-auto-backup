# switch-flow-auto-backup
Automatically backup your flows.

## FAB program
To utilize flow auto backup (FAB), you must make a program flow which utilizes the FAB functions. You should not have to modify the FAB functions at all. An example FAB program flow is included in this repository. The example program executes backups once per hour, archiving the returned flows in a heirarchy following the flow grouping in the flow pane.

### Example
You can use the FAB Parent Folders as well as the FAB Flow Name to set a hierarchy path in Switch using ‘Set hierarchy path’:

- [Job.PrivateData:Key="FAB Parent Folder4"]
- [Job.PrivateData:Key="FAB Parent Folder3"]
- [Job.PrivateData:Key="FAB Parent Folder2"]
- [Job.PrivateData:Key="FAB Parent Folder1"]
- [Job.PrivateData:Key="FAB Flow Name"]
- .sflows file

<img src="http://i.imgur.com/xIV5k1w.png" width="400">

Here is an example of results using the example above:

<img src="http://i.imgur.com/q5mtO50.png" width="400">

## FAB functions
### Introduction
This  flow function group will provide archivable .sflow files of every flow on a Switch system, as well as their metadata. One potential use is to back up all .sflow files, and archive them according to Switch flow groups:
- FAB Get Flow Function
- FAB Pack Flow Function
- FAB Flow Group Function

### Usage	
To use the FAB functions the following dataset needs to be set as private data:
FAB Portal Callback - The Portal channel where the packed flows will be delivered once the core functions are complete. You do not have to change this.

- __FAB Flows Path__ - The absolute path to your Switch Server/flows directory.
- __FAB Manifest Path__ - The absolute path to your generic manifest.xml file. 
- __FAB Flow Panes Path__ - The absolute path to Switch Server flowpanes.xml file.
- __FAB Portal Failure Callback__ - _Optional_ - The Portal channel where files that fail are delivered from any part of this flow function group.

Out of the Callback, .sflows will start flowing in. Each of these .sflows is ready for use and contains the following new FAB dataset fields:
- __FAB Flow Name__ - The name of the flow
- __FAB Flow Version__ - The current version of the flow
- __FAB Flow ID__ - The numerical ID of the flow
- __FAB Parent Folder<Number Iteration 1 - 4>__ - The folder names of the flow based on grouping in Switch
 
If any of your flows are password protected, these values will say 'Encrypted'.

#### Failure callback
The optional Failure Callback, will return failed jobs with the following private data keys:
- __FAB Fail Flow__
- __FAB Fail Element__
- __FAB Fail Message__
- __FAB Fail Module__


