# mkdir
#mkdir #linux #bash

To create several folders at once *curly braces* are to be used:
```bash
mkdir {folder1,folder2,folder3}
```

To create subfolder with parent folders `-p` argument is to be used (taking into consideration that parent folders didn't exist):
```bash
mkdir -p folder1/subfolder1/subsubfolder1
```

To create multiple subfolders:
```bash
mkdir -p folder1/{subf1,subf2,subf3}
```