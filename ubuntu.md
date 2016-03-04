#Ubuntu Setup

This is assuming fresh 15.10 install.

1. Install the basics.
```bash
sudo apt-get install python-pip python-dev build-essential 
sudo pip install --upgrade pip 
sudo pip install --upgrade virtualenv 
sudo pip install --upgrade virtualenvwrapper
```

2. Install postgres. [Source](http://tecadmin.net/install-postgresql-server-on-ubuntu/)

Command line.
```bash
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
sudo apt-get update
sudo apt-get install postgresql
sudo su - postgres
psql
```

OPTIONAL STEPS (good for finding port that postgres is running on. Default is 5432.
Postgres:
```postgresql
\conninfo
\q
```

Command line:
```bash
su MAINUSERNAME
(password)
```

3. Install git.

```bash
sudo apt-get install git
```

