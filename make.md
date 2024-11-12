```make
$target: $depend_file1 $depend_file2
    g++ -o main $depend_file1 $depend_file2

depend_file1: 
    g++ -c depend_file1.cc

depend_file2: 
    g++ -c depend_file2.cc
```
