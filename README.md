# handy-commands

## Banish .idea from repo

```
find . -name .idea -print0 | xargs -0 git rm -r -f --ignore-unmatch
echo .idea >> .gitignore  
git add .gitignore  
git commit -m '.idea banished!'
git push
```

## Select python version for a virtualenv

`virtualenv -p /usr/local/opt/python@3.7/bin/python3.7 ocrenv`

you can change `python@3.7` assuming you have multiple versions. 


## Alternative python version selection method

```
pyenv install 3.7.9

pyenv local 3.7.9
```

## Set up pipenv

```
pip --version 
pip install --user pipenv 
python -m site --user-base 
export PATH="$PATH:/home/olasimbo/.local/bin" 
source ~/.bashrc
```

## Proper checkout/merge branch

`git checkout dev && git pull` 

then merge `dev` branch into your branch locally 

`git checkout feature/CGP-3 && git merge --no-ff dev`

then do `git push` to update `feature/CGP-3`


## Get server ip

`ipconfig getifaddr en0`

or 

`server_ip = requests.get('http://ipconfig.in/ip').text`


## Add your ssh key to cloud VM authorized keys

```
cat ~/.ssh/id_rsa.pub | sudo ssh -i /path/to/pem_or_key user@ipaddress "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
```
you can then connect to VM directly from VScode remote-ssh or from local terminal


## Using VSCode Remote-SSH with Ubuntu/Linux server

First add Remote-SSH under extension in VSCode, then edit your `.ssh` config file with the following and save it

```
Host *
ServerAliveInterval 30
ServerAliveCountMax 6


Host project-name
    HostName server-ip
    User ubuntu
    IdentityFile /path/to/pem
```
Incase you already copied your local ssh to cloud VM authorized keys, then you can omit IdentityFile (not needed)


## Copy files to server

```
rsync -PrlptD ~/Documents/hor/AnnotatedData/untitled_folder ubuntu@ipaddress:/home/ubuntu/hor/csv_tmp 
rsync -I -PrlptD ~/Documents/hor/json_tmp ubuntu@ipaddress:/home/ubuntu/hor/json_tmp
```

## Creating postgres DB

```
sudo -u postgres psql
create database mydb;
create user myuser with encrypted password 'mypass';
grant all privileges on database mydb to myuser;
```


## Alter Role on DB

```
ALTER USER role SUPERUSER CREATEDB CREATEROLE;
```

## Drop DB

``` 
sudo -u postgres dropdb databasename
```


## Network Issues 

# OCI Linux Server

For issues with making requests to a linux server on OCI, set these options for the ports:

```
sudo firewall-cmd --zone=public --permanent --add-port=5005/tcp 

sudo firewall-cmd --reload
```

# OCI Ubuntu Server

For ubuntu:

```
sudo iptables -I INPUT 6 -p tcp --dport 5010 -j ACCEPT 

sudo netfilter-persistent save
```

or use

```
sudo ufw allow 22
sudo ufw allow your-port
sudo ufw enable
```
First ensure port 22 is opened, open your preferred port (e.g 5010), then enable the firewall (select `y`). 
