# TP Docker 1 🐋


### 🌞 Ajouter votre utilisateur au groupe docker :

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


### 🌞 Lancer un conteneur NGINX : 

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

### 🌞 Lance un conteneur Python, avec un shell / 🌞 Installe des libs Python

vu que j'ai la flemme de faire 120 000 entrée dans le readme je vais compacter les truc de pip que avec un pip install (comme ça sa montre que ça marche)

```
nepnath@NepUntu:~/nginx$ docker run -it python bash
root@f9c9cca5d68e:/# pip install aioconsole 
Collecting aioconsole
  Downloading aioconsole-0.8.1-py3-none-any.whl.metadata (46 kB)
Downloading aioconsole-0.8.1-py3-none-any.whl (43 kB)
Installing collected packages: aioconsole
Successfully installed aioconsole-0.8.1
```


##  II. Images

### 🌞 Lancez un conteneur à partir de l'image Python 

```
docker run -it python bash
```

```
nepnath@NepUntu:~$ docker run -it python bash
root@9ccc1d86432b:/# python3 --version
Python 3.13.1
```

j'ai fais tout le bordel d'image mais j'ai oublié de noter les étapes dans le README du coup je met le produit de fin (quand on run l'image) pour montrer que ça run bien.

```
nepnath@NepUntu:~/appkkdocker$ docker run python_app:version_de_ouf 
Cet exemple d'application est vraiment naze 👎
```

truc à noter c'est que linux ça aime pas 'pip' (pcq ça peux faire du kk avec l'os) du coup au lieu de faire un 'pip install' pour installer le package 'emoji' on peux juste installer le package après avec python : 

```
RUN apt install -y python3 python3-emoji
```

## III. Docker compose

### 🌞 Lancez les deux conteneurs avec docker compose / 🌞 Vérifier que les deux conteneurs tournent

```
nepnath@NepUntu:~/Docker TP1/Compose_test$ docker compose up -d
WARN[0000] /home/nepnath/Docker TP1/Compose_test/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 2/2
 ✔ Container compose_test-conteneur_nul-1        Started                                             0.2s 
 ✔ Container compose_test-conteneur_flopesque-1  S...                                                0.2s 
nepnath@NepUntu:~/Docker TP1/Compose_test$ docker ps
CONTAINER ID   IMAGE     COMMAND        CREATED          STATUS         PORTS     NAMES
76d3582eb0e3   debian    "sleep 9999"   32 seconds ago   Up 4 seconds             compose_test-conteneur_nul-1
489768a0f946   debian    "sleep 9999"   32 seconds ago   Up 4 seconds             compose_test-conteneur_flopesque-1
nepnath@NepUntu:~/Docker TP1/Compose_test$ 
```


### 🌞 Pop un shell dans le conteneur conteneur_nul

on suppose que j'ai lançé le compose et que j'ai donc mes deux conteneur de lancés.

```
docker exec -it {ID} bash
```

```
apt update && apt install -y iputils-ping
```

```
ping conteneur_flopesque / conteneur nul 
```


