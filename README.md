# crypt_keeper
A secure API for controlling keys to sensitive databases

## SETUP
Create two empty files:

touch .authenticated_users
touch .authenticated_servers

Install requirements

pip install -r requirements.txt

sudo apt update
sudo apt full-upgrade
sudo apt-get install redis-server supervisor certbot

create certificate:
sudo certbot certonly -d your-api-name.your-domain.com

copy cert in to running folder:
sudo cp /etc/letsencrypt/live/your-api-name.your-domain.com/fullchain.pem .fullchain.pem
sudo cp /etc/letsencrypt/live/your-api-name.your-domain.com/privkey.pem .privkey.pem

modify files:
sudo chmod +x crypt_keeper.py
sudo chown yourname:yourname *.pem

Copy SUPERVISOR_EXAMPLE to /etc/supervisor/conf.d/crypt_keeper.conf
Modify example as necessary.

Create new .env file using the ENV_EXAMPLE as a loose template.  Tailor this to your needs.

Set your one time password seed in the env file.  You can use your own password, or use:

import pyotp
pyotp.random_base32()

WARNING!!!! You will be storing your actual passwords in the .env file.  It is imperative that there is not any remote command prompt left open to this server.

## Adding or Removing Users and Servers

python3 add_remove.py

Welcome to the Crypt Keeper

Which action would you like to perform?:

1) Add Authenticated User
2) Remove Authenticated User
3) Add Allowed Server
4) Remove Allowed Server



Logging 

Find the current random ident
sudo ls /var/log/supervisor/crypt_keeper-std*

STDOUT
sudo tail -f /var/log/supervisor/crypt_keeper-stdout---supervisor-SOMERANDOMIDENT.log

STDERR
sudo tail -f /var/log/supervisor/crypt_keeper-stderr---supervisor-SOMERANDOMIDENT.log