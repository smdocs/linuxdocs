strace notes
====================

1. Debugging shared library issues.

Here is an example to see what specif version of shared libraries are being loaded when there is an issue with a specific program.
```bash
 # Find all the libraries loaded using strace, put all the output in a log file.
 $ strace -f -o /tmp/problems.log ~/clones/iruby/bin/iruby notebook
 
 # Rungrep -v ENOENT is because it looks everywhere in my LD_LIBRARY_PATH so it fails to 
 # find libzmq a bunch of times.
 grep libzmq.so /tmp/problems.log | grep -v ENOENT
```
