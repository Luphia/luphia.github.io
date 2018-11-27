

```shell
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib -y
```

```shell
sudo -i -u postgres
sudo passwd postgres
su postgres
```

```shell
createuser --interactive
createdb mydb
```

```shell
psql
alter user harry with encrypted password 'potter';
grant all privileges on database mydb to harry;
```
