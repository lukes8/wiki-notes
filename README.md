# wiki-notes

Windows Useful Commands
---- 
Remove all folders inc. subfolders without prompt
```
rmdir /Q /S foldername
```
Remove all files via wildcard quite quickly, great for large files
```
del /F /Q /S *.* > NUL
```
Copy whole folder structure without files excluding three folders target, .idea, .git
```
robocopy SourceFolder DestFolder /e /xf * /xd "target" /xd ".idea" /xd ".git" /log:log_robocopy.txt
```
**Tip:** 
very useful in case of project backup, you can exclude other big folders like node_modules etc.

Copy all .yml files in folders including sub-folder structure except empty ones
```
robocopy SourceFolder DestFolder /s *.yml /xd "target" /xd ".idea" /xd ".git" /log:log_robocopy.txt
```

Open an Windows Explorer in current path on command line
```
start .
```

Maven Useful Commands
---- 
The maven goal that only makes JAR package from compiled java sources
```
mvn jar:jar
```
The maven goal that makes only WAR package from compiled java sources
```
mvn war:war
```
The maven phase that makes all first phases ending with package ie. compile, test, jar
```
mvn package
```
The maven goal that makes only installation of the package to the maven local .repository (and then accessible as dependency for other projects or modules)
```
mvn install:install
```
Process resources, package into JAR file and finally install it to the maven local .repository
```
mvn resources:resources jar:jar install:install
```
**Tip:** 
very useful if you have just some updated resources and want to build your BIG app simply and faster ie. except of compile and test goals

Process resources, package into WAR file and finally install it to the maven local .repository
```
mvn resources:resources war:war install:install
```
**Note:** 
the resources can be usually JAR libraries of 3th party, resources on the classpath (yml, config, properties etc.). 

Skip javadoc generation during build
```
mvn clean install -Dmaven.javadoc.skip=true
```

Packages all needed files (inc. copying webapp resources) into WAR file and finally install it to the maven local .repository
```
mvn war:war install:install
```
**Tip:**
very useful if you have updated only some javascripts or other frontend stuffs and want to build your BIG app simply and faster ie. except of compile and test goals


Clean the release property and backup files eg. pom.xml.releaseBackup, release.properties
```
mvn release:clean
```

Preparation phase for release when it checks staging area (if exists no modified files)
Checks last version from maven-metadata.xml on jFrog to ensure that we are now on correct version (consistency check)
Create release version from snapshot ie. modify version in project pom.xml from 1.1.42-SNAPSHOT to 1.1.42
Create tag as release version ie. 1.1.42
Create another development version (snapshot) ie. modify version in project pom.xml from 1.1.42 to 1.1.43-SNAPSHOT
```
mvn release:prepare
```

Checkout from SCM URL as remote repository on tagged release version ie. 1.1.42
Deploy/Push the jars or ears to jFrog specified on local settings.xml
```
mvn release:perform
```
**Tips:**
tag is basically something like branch but only mark or naming for specified commit so then you can checkout on this tag much more easier way than on commit specified by its number

Checkout from SCM URL as remote repository on tagged release version ie. 1.1.42
Deploy/Push the jars or ears to jFrog specified on passed settings.xml, we might need to access under different user due to privilegies (jFrog has some permissions to approach for specified users)
```
mvn release:perform -s /path/explicit-settings.xml
```


IntelliJ IDEA Tips & Tricks
---- 
The Multiple Cursors
Caret cloning 
```
The commands are issued by pressing Ctrl , then pressing it again and not releasing. While still holding Ctrl, you can press ↑ and ↓ arrows to clone cursor to the line above or bellow.
```

Multiple Cursors
```
When holding Alt + Shift, clicking on a location creates a new cursor on that location in addition to all the already existing cursors.
```

Select All occurrences
```
Ctrl + Shift + Alt + J
```
Add occurrence (good alternative for Select All occurrences)
```
Alt + J
```

Power Shell Tips & Tricks
---- 
Get-Date and Set-Date feature
```
Set the date in simple way
Set-Date "09/04/2021"   

Returns current set date
Get-Date    

Set the date with current time
set-date -date ("09/04/2021 " + (Get-Date).ToString("hh:mm:ss"));

```

Sync time clock
```
Resync the clock of machine to current date time
W32tm /resync /force;

```
Note: you might need to have admin privilegies for set of date or resync feature
you can 

Execution policy
```
Returns if your machine has osme restrictions policies in setup
Get-ExecutionPolicy

```

Sample script with usage Date and resync (your_script.ps1)
```
"--------------START SCRIPT";

set-date -date ("09/04/2021 " + (Get-Date).ToString("hh:mm:ss"));

"Date was updated and now it's waiting 30s before sync!";
Start-Sleep -s 30;

W32tm /resync /force;

"Clock was sync to current date time!";

"--------------END SCRIPT";

```

You can use above script and call under cmd batch file if you encouter on problem with running of script (policies etc.)
```
@echo off
powershell.exe -noprofile -executionpolicy bypass %MY_SCRIPTS%\your_script.ps1
timeout 10
```
Note: don't forget set up your user environment property where your scripts are located ie. MY_SCRIPTS or you can ignore it
