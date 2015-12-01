# rcon

rcon is a lightweight resource virtualization tool for linux processes.

## usage
```
 ./rcon --help
Usage: rcon [options] --user username --command "yes >> /dev/null"
    --cpu VAL
      default: 30 (%)
    --mem VAL
      default: 512 (MiB)
    --read VAL
      defualt: 10485760 (Byte/sec)
    --write VAL
      defualt: 10485760 (Byte/sec)
    --group VAL
      defualt: rcon
    --dev VAL
      default: 202:0
    --version
```

## cpu example

limitting cpu 10%

- command
```
sudo ./rcon --user matsumotory --command "yes >> /dev/null" --cpu 10
```

- cpu usage
```
  PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND
23941 matsumot  20   0 98.5m  604  520 R  9.6  0.0   0:00.63 yes
```

## io example

limitting write io 1MByte/sec

- command
```
sudo ./rcon --user matsumotory --command "dd if=/dev/zero of=tempfile bs=1M count=1000 oflag=direct" --write 1024000
```

- io usage
```
  TID  PRIO  USER     DISK READ  DISK WRITE  SWAPIN     IO>    COMMAND
24676 be/4 matsumot    0.00 B/s  995.77 K/s  0.00 % 99.99 % dd if=/dev/zero of=tempfile bs=1M count=1000 oflag=direct  
```

- find io dev id(--dev)
```
$ ls -l /dev/xvda | awk '{print $5 $6}' | sed 's/,/:/'
202:0
```
