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
