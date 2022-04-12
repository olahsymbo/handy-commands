# notes

## Banish .idea from repo

```
find . -name .idea -print0 | xargs -0 git rm -r -f --ignore-unmatch
echo .idea >> .gitignore  
git add .gitignore  
git commit -m '.idea banished!'
```

## Set version based virtualenv

`virtualenv -p /usr/local/opt/python@3.7/bin/python3.7 ocrenv`


## Set up pipenv

```
pip --version 
pip install --user pipenv 
python -m site --user-base 
export PATH="$PATH:/home/olasimbo/.local/bin" 
source ~/.bashrc
```

## proper checkout

I will suggest you update the dev branch locally `git checkout dev && git pull` then merge `dev` branch into your branch locally `git checkout feature/CGP-3 && git merge --no-ff dev`
then do `git push to update feature/CGP-3`


## copy files to server

```
rsync -PrlptD ~/Documents/hypi/AnnotatedData/untitled_folder ubuntu@51.210.39.109:/home/ubuntu/hypi_services_ocr/ocr_extractor/csv_tmp (edited)
rsync -I -PrlptD ~/Documents/hypi_services_ocr/ocr_extractor/json_tmp ubuntu@51.210.39.109:/home/ubuntu/hypi_services_ocr/ocr_extractor/json_tmp
```

server ip

`ipconfig getifaddr en0`


## Using VSCode with Ubuntu/Linux server

use remote explorer and set this in config file

```
Host *
ServerAliveInterval 30
ServerAliveCountMax 6


Host project-name
    HostName server-ip
    User ubuntu
    IdentityFile path to pem file


## Creating postgres DB

```
sudo -u postgres psql
create database mydb;
create user myuser with encrypted password 'mypass';
grant all privileges on database mydb to myuser;
```
grant all privileges on database mydb to myuser;
