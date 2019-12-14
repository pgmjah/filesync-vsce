# filesync README

FileSync will keep files synchronized between src and dest locations.  It can also clone git repositories before synchronizing, and rename files.

***Note: This has never been run/tested on any Mac/UNIX box. My guess is it will not work, as FileSync uses the Node file System extensively, and I'm sure there are major differences in how the calls should be made.***

## Features

* Clone git repositories
* Rename files
* Keep files synchonized between source/destination directories.
* Simple to configure.

## Extension Settings
* Show FileSync activity in the statusbar.

## FileSync Configuration
* Add file(s) called "fsconfig.json" (see below) to the folders you open, or are part of your workspace.

## fsconfig.json
* You can have multiple fsconfig.json files, the extension will find them in your workspace/folders and load each one.

The FileSync config file is a json object with the following layout:
```javascript
{
	"configs":
	[
		{
			"name":"sample_sync_config",
			"enabled":true,
			"rename":
			[
				{
					"src":"c:/path/to/file/file.ext",
					"name":"new_name.ext"
				}
			],
			"git":
			[
				{
					"src":"https://github.com/gitrepo/gitrepo.git",
					"dest":"c:/clone/to/this/location"
				}
			],
			"sync":
			[
				{
					"src":"c:/some/source/folder",
					"dest":"c:/some/dest/folder",
					"ignore":
					[
						"folder1/relative/to/src",
						"folder2/relative/to/src"
					],
					"bidir":true
				}
			]
		}
	]
}
```
* configs - You can have an array of config blocks, each specifying their own syncing actions.
* name - just an indentifier, has no intrinsic meaning.
* enabled - activate/ignore this block when starting.
* rename - array of objects specifying what files you want renamed before syncing (can be a single object, if just one).
  * src - the file you want to rename.
  * name - what you want the file renamed to.  You can specify '\*' as the filename to just change the extension...like "*.txt_fsync_".
* git - array of git repositories to be cloned into a specified location (can be a single object, if just one).
  * src - location of the git repository.
  * dest - where to clone the src repos into.
* sync - array of objects specifying what directories you want synchronized where (can be a single object, if just one).
  * src - the source directory to syncronize.
  * dest - the destination directory to keep synchronized.
  * ignore - array of relative paths to src to be ignored when syncing (can be a single object, if just one).
  * bidir - bidirectional synchronization...that is, files will be removed from destination if they don't exist in the source.

## Commands
* FileSync: Create a fsconfig.json file - will generate a default config file in the workspace folder you choose.
* FileSync: Toggle synchronizing files/directories - selectively turn on/off synching for various directories.
* FileSync: Start synchronizing files/directories - start all the FileSyncs in loaded fsconfig.json files.
* FileSync: Stop synchronizing files/directories" - stop all the currently running FileSyncs.

## Release Notes

## 1.0.18
* Relative paths should be valid anywhere in config file.

## 1.0.17
* Housekeeping.

## 1.0.16
* Created specific git branch for extension (vsce).

### 1.0.15
* Put back mkdef standalone command.

### 1.0.14
* Messed up "main" in package.json...left as needed for npm...my bad!

### 1.0.13
* Running standalone - added mkdef command to create a default fsconfig.json file.

### 1.0.12
* Added bin to package.json

### 1.0.11
* Removed standalone bat file

### 1.0.10
* Added an 'ignore' section to the fsconfig.json file.  You can put an array of directories which will be skipped when synchronizing (can be a single string, if just one).  ".git" directories are automatically ignored.

### 1.0.9
* Added note about not working on UNIX...**I'm working on it!**

### 1.0.8
* Now watching config files for changes...will automatically update when create/edited/deleted

### 1.0.7
* Cleaned up toggle sync command handling.

### 1.0.6
* Added config setting to show/hide activity in the statusbar.
* Added command to toggle on/off file synching for a particular directory.

### 1.0.5
* Cleaned up start/stop command handling.

### 1.0.4
* Updated this file (readme.md).

### 1.0.3
* Just working on proper extension packaging.

### 1.0.2

### 1.0.1
* Changed default fsconfig.json to use arrays of git/rename instead of single objects.

### 1.0.0

* Initial release of FileSync

