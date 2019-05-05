## Stdout vs Stderr
- There are two streams of output for each process: stderr and stdout
```
$ cat *
## Today I Learned

### Categories
- [DevOps](#devops)

### DevOps
- [Different types of NodePort in K8s and Comparision with DockerSwarm](devops/Different_types_of_NodePort_in_K8s_and_Comparision_with_DockerSwarm.md)
cat: devops: Is a directory
cat: misc: Is a directory
```
> Note: It showed content(output) and also the error (Is a directory)

- Output will go to Stdout and __will__ propogate to next process
- Error will go to Stderr and __will not__ propogate to next process
```
$ cat * > output.txt
cat: devops: Is a directory
cat: misc: Is a directory
$ cat output.txt
## Today I Learned

### Categories
- [DevOps](#devops)

### DevOps
- [Different types of NodePort in K8s and Comparision with DockerSwarm](devops/Different_types_of_NodePort_in_K8s_and_Comparision_with_DockerSwarm.md)
```
- We can even control what content to go to what stream
```
$ cat * 2>&1 1>/dev/null
cat: devops: Is a directory
cat: misc: Is a directory
```
> Redirect `stderr` to `stdout` and `stdout` to `null`