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
very useful in case of project backup

