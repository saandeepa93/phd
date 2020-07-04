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

## **Pytorch**

 1. To reshape the pytorch tensor. DONOT convert the pytorch to numpy and then reshape. Instead, reshape with `permute` and then convert to numpy if required. Doing the former messes up the data representation.