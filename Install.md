dnf -y install java-17-openjdk-headless.x86_64
firewall-cmd --add-port=9443/tcp
firewall-cmd --add-port=9443/tcp --permanent

useradd blynk
su - blynk
mkdir -p blynk-data/config
crontab -e
----------
@reboot /usr/bin/java -jar $HOME/bin/server-0.41.17.jar -dataFolder $HOME/blynk-data -serverConfig $HOME/blynk-data/config/server.properties -mailConfig $HOME/blynk-data/config/mail.properties > $HOME/blynk.console.log 2>&1
----------
reboot
# look into log for admin pw


[blynk@blynk01 ~]$ cat blynk-data/config/server.properties 
https.port=9443
http.port=9080
initial.energy=0
data.folder=/home/blynk/blynk-data
allowed.administrator.ips=10.0.0.0/8,172.16.0.0/12,192.168.0.0/16
admin.email=chris@bitbull.ch
admin.rootPath=/protected

[blynk@blynk01 ~]$ cat blynk-data/config/mail.properties 
mail.smtp.username=send@bitbull.ch
mail.smtp.port=587
mail.smtp.password=xxx...
mail.smtp.auth=true
mail.smtp.starttls.enable=true
mail.smtp.timeout=120000
mail.smtp.host=mail01.sun.bitbull.ch
mail.smtp.connectiontimeout=30000
