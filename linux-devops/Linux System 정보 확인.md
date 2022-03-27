# Linux System 확인

Linux System 구성정보를 확인하는 명령어 및 사용법을 기술한다.

## 시스템 구성정보 


### 커널 정보 확인

```
uname -a 
```

### CPU 정보 확인 

```
deidecode -t {options}
```

- cpu 
- memrory
- processor 

```
cat /roc/cpuinfo
``` 

### Disk 

```
df -h 
```

### Network

```
lspci | grep -i ether
```

```
ethtool -g eht0
```
