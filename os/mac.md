## Chetsheet Mac Shortcuts

**process id for a port**
```
# will search the process id for port 8080
lsof -n -i4TCP:8080

# Find a LISTEN port
lsof -i -P | grep LISTEN | grep :5001

# Kill a process
kill -9 processId
```

***find all occupied port in Mac***
```sh
alias all_occupied_ports="netstat -vanp tcp"
alias find_port="lsof -i:8080"
```

# quarantine a file.

```sh
sudo xattr -r -d com.apple.quarantine ~/Tools/path/to/the/folder
```

# Find Wifi Password connected in Mac.

```sh
security find-generic-password -ga "Wifi Name" | grep "password:"
```
