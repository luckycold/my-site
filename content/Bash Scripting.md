---
{"tags":["Programming","CheatSheet"],"publish":true,"PassFrontmatter":true}
---


- All scripts start with:
	- #!/bin/bash
- echo outputs what is in front of it.
- If statements are structured like so:
```bash
#!/bin/bash

count=100
# -eq stands for Equals
if [ $count -eq 100 ]
then
	echo Count is 100
else
	echo Count is not 100
fi
```
Or
```shell
#!/bin/bash
clear
# -e stands for if a file exists
# -x if file exists AND is executable
if [ -e /home/lucky/error.txt]
	then
	echo "File exist"
	else
	echo "File does not exist"
fi
```
- Loops are structured like so:
```shell
#!/bin/bash
for i in 1 2 3 4 5
do
echo "Welcome $i times"
done
```
Or
```shell
#!/bin/bash

for i in dog jeff bob
do
echo $i
done
```
Or
```shell
#!/bin/bash
# Numbers 1-5
for i in {1..5}
do
echo Number $1
done
```