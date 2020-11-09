## Pandoc
1. Use the below command to generate html or pdf files from your pandoc notes

```
pandoc --to=pdf -o index.pdf test.md
```

## Openface docker commands

1. To check if the openface docker process is running
```
docker ps -a
```

2. Openface docker image test
```
docker images -a
```

3. Run openface docker image
```
docker run -it --rm --name openface algebr/openface
```

* `-it` interactive
* `--rm` remove instance after killing the process
* `--name` name of the image file manually assigned

4. run a file to extract features

```
./build/bin/FaceLandmarkImg -f filename
 ```

 5. Copy the files to local from docker
 ```
 docker cp openface:/home/openface-build/processed ~/Projects/
 ```

## Unix commands
1. To login to remote machine with ssh key
```
ssh -i path_to_key username@hostname
```

2. To login to remote machine without ssh key
```
ssh username@hostname
```

2. Copy directory from remote to local machine using SSH
```
scp -r -i /path_to_key /local_path username@ipaddress:/remote_path
```

3. Count the number of files in the directory.
```
ls | wc -l
```

4. Delete empty directories recursively
```bash
find . -type d -empty -delete
```

5. Use rsync to copy files from remote to local
```bash
rsync -av -e ssh --include='*/' --include='00*.jpg' --exclude='*' saandeepaath@gaivi2.cse.usf.edu:/data/scanavan1/gaivi_data/BP4D/Sequences/ ./bp4d
```

## **Pytorch**

 1. To reshape the pytorch tensor. DONOT convert the pytorch to numpy and then reshape. Instead, reshape with `permute` and then convert to numpy if required. Doing the former messes up the data representation.


## **Important VAe links**
* To understand disentanglement: [link](https://towardsdatascience.com/disentangling-disentanglement-in-deep-learning-d405005c0741)
* Purpose of Reparametrization: [link](https://towardsdatascience.com/reparameterization-trick-126062cfd3c3)
*