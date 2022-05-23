# Basic linux terminal commands
## File management
### Change directory
```
cd PATH
```
e.g.
```
cd /home/user
```
Go up a directory
```
cd ../
```
Go to your home directory
```
cd ~
```
or
```
cd
```
Go to root directory
```
cd /
```
### List the content of directory
```
ls
```
list even hidden content (or dot-files like .example)
```
ls -a
```
### Make new directory
```
mkdir YOUR_DIRECTORY_NAME
```
e.g.
```
mkdir Example
```
### Remove a directory (must be empty)
```
rmdir YOUR_DIRECTORY_NAME
```
e.g.
```
rmdir Example
```

### Make new file 
```
touch PATH_AND_NAME
```
e.g. ( makes file called example.txt in current directory, also extension like txt is optional and can be anything)
```
touch ./example.txt
```
### Remove a file
```
rm PATH_TO_FILE
```
e.g. (./ means in current directory)
```
rm ./example.txt
```
remove directory which is not empty (this will also remove all of its content)
-r flag stands for recursive (to recursively remove everything from that directory)
-f flag stands for force (ignore any warnings)

```
rm -rf PATH_TO_DIR
```
### Move or rename a file
```
mv PATH_TO_FILE_TO_MOVE PATH_WHERE_TO_MOVE
```
e.g. ( moves file up a directory )
```
mv ./example.txt ../
```
rename a file
```
mv YOUR_FILE NEW_NAME
```
e.g.
```
mv ./example.txt ./new_example.txt 
```
### Copy file or directory
```
cp PATH_WHAT_TO_COPY PATH_WHERE_TO_COPY
```
e.g. ( copies file up a directory )
```
cp ./example.py ../
```
