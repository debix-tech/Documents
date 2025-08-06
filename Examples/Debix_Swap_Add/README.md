## 📦 Add a Swap Partition on DEBIX  

### ✅ Step 1: Check Current Memory and Swap Usage  
```shell
free -m 
    total        used        free      shared  buff/cache   available
Mem:         1947        808         368       11         771        1039
Swap:         127         39           88
```

### ✅ Step 2: Create a 1GB Swap File  
```shell
dd if=/dev/zero of=/swapfile1 bs=1024 count=1048576
1048576+0 records in
1048576+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 30.0344 s, 35.8 MB/s
```
**Note**:  
- Creates a **1GB** file `/swapfile1` as new swap space  
- Adjust `count` value for different swap sizes  

### ✅ Step 3: Format as Swap and Set Permissions  
```shell
sudo mkswap /swapfile1
mkswap: /swapfile1: insecure permissions 0644, fix with: chmod 0600 /swapfile1
Setting up swapspace version 1, size = 1024 MiB (1073737728 bytes)
no label, UUID=0845fdc8-a7c2-4e39-9af6-4d6cd00b900c

sudo chmod 600 /swapfile1
```

### ✅ Step 4: Activate Swap File Immediately  
```shell
swapon /swapfile1
swapon: /swapfile1: insecure permissions 0644, 0600 suggested.
```

### ✅ Step 5: Enable Automatic Swap Mount at Boot  
Edit `/etc/fstab` and add:  
```shell
/swapfile1 swap swap defaults 0 0
```

### ✅ Step 6: Optimize Swap Usage Policy  
Edit `/etc/sysctl.conf` and add:  
```shell
vm.swappiness=10
```

### 🔧 Parameter Explanation:  
- `vm.swappiness` range: **0 to 100**  
- Controls kernel's tendency to move memory pages to swap:  

| Value | Behavior                                                                 |
|-------|--------------------------------------------------------------------------|
| 0     | **Avoid swap** unless absolutely necessary (physical memory exhausted)  |
| 10    | Minimal swap usage (prefers caching, uses swap under memory pressure)    |
| 60    | Default: **Balanced** memory caching and swap usage                     |
| 100   | **Aggressively use swap**, moving inactive pages to swap early          |

### ✅ Step 7: Reboot System  
```shell
reboot
```

### ✅ Step 8: Verify New Swap Partition  
```shell
free -m
               total        used        free      shared  buff/cache   available
Mem:         1947         704         891       1         351        1163
Swap:         1151           0        1151
```

✅ **Your system now has a 1GB swap partition that automatically mounts at boot**