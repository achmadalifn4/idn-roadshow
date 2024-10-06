# Linux

# Basic Commands
## Basic Operation Linux
displays the user used
```
whoami
```
displays the currently logged in user
```
who
```
displays the server hostname
```
hostnamectl
```
displays date and time
```
timedatectl
```

## Assesmen Server
displays the operating system
```
cat /etc/os-release 
```
displays the operating system
```
uname
```
displays the server processor
```
lscpu
```
display memory
```
free -h
```
display storage
```
lsblk / df -h
```

# File and Directory Management


## Directory Management
create dirctory
```
mkdir idn
```
enter and exit the directory
```
cd idn
```
displays the contents of the directory
```
ls
```
displays which directory we are in
```
pwd
```
delete directory
```
rmdir idn
```

## File management
create file without content
```
touch idn-roadshow
```
create file with content
```
echo "Hello World" >> idn_roadshow
```
displays the contents of the file
```
cat idn_roadshow
```
displays the first 10 lines of a file
```
head /var/log/syslog
```
displays the last 10 lines of a file
```
tail /var/log/syslog
```
delete file
```
rm idn-roadshow
```
copy file and dirctory
```
cp idn_roadshow ~/sysadmin
```
move or rename file and directory
```
mv idn_roadshow nama_siswa
```

# User and Group Management

## User Management
add new user
```
useradd nama_siswa
```
displays a list of users
```
cat /etc/passwd
```
change user password
```
passwd nama_user
```
modify user
```
usermod -u 10000 rudi
usermod -aG nama_group nama_user
```

## Group Management
create new group
```
groupadd smk
```
displays a list of group
```
cat /etc/group
```
modify group
```
groupmod 
```