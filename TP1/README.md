# TP Docker 1 🐋


🌞 Ajouter votre utilisateur au groupe docker :

si jamais y'a pas le groupe docker : 

```
sudo groupadd docker
```

et quand y'a le groupe kié la :

```
sudo usermod -aG docker $USER
```

du coup ça donne ça à la fin :

```
nepnath@NepUntu:~$ sudo usermod -aG docker nepnath
nepnath@NepUntu:~$ id nepnath
uid=1000(nepnath) gid=1000(nepnath) groupes=1000(nepnath),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),100(users),114(lpadmin),984(docker)
```


🌞 Lancer un conteneur NGINX : 

pour ça on a juste à lancer le conteneur NGINX, si on a pas l'image ça va la dl toute seul comme un grand, et après plus qu'a docker run :

```
nepnath@NepUntu:~$ docker run -d -p 9999:80 nginx
e8ad11cf7342d2d3aad2c1681846c220c3b8e3ec4a57dcf04f3903ca7369d7cf
```

puis après on peux check que le conteneur est bien lancé (par localhost mais j'vais mettre un docker ps pour montrer que ça tourne)
```
nepnath@NepUntu:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
e8ad11cf7342   nginx     "/docker-entrypoint.…"   51 seconds ago   Up 50 seconds   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   gallant_villani
nepnath@NepUntu:~$ ^C
```
