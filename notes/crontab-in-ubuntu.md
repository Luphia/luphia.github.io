```shell
crontab -l > mycron
echo "00 09 * * 1-5 echo hello" >> mycron
crontab mycron
service cron restart
rm mycron
```
