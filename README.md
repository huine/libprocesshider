# libprocesshider

Hide a process under Linux using the ld preloader.
Based on https://github.com/gianlucaborello/libprocesshider
My version hide all process of an user by his uid under Linux.

Full tutorial available at https://sysdigcloud.com/hiding-linux-processes-for-fun-and-profit/

In short, compile the library:

```
gabriel@[~/libprocesshider]:~> make
gcc -Wall -fPIC -shared -o libprocesshider.so processhider.c -ldl
gabriel@[~/libprocesshider]:~> sudo mv libprocesshider.so /usr/local/lib/
```

Load it with the global dynamic linker

```
root@[~]:~> echo /usr/local/lib/libprocesshider.so >> /etc/ld.so.preload
```

And your process will be off the radar 

```
gabriel@[~]:~> sudo ps aux
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
...

gabriel@[~]:~> sudo lsof -ni
COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAME
...
```
