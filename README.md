# Harmony-Docker
A repository with focus on Docker Compose yaml files that just works as intended (and is reproducable) so you enjoy Self-Hosting more!

Fun Fact: when i was creating this repository i installed and Archlinux virtual machine inside my Archlinux machine to just test things out and it's a personal thing but i recommend Archlinux cause it's minimal and a lot more stable that you think! :)

## Harmony Files List
If you want to Host a Media server use this stack:
[Harmony-Media](#Harmony-Media)

if you are interested in Hosting a Website use this stack:
[Harmony-Web](#Harmony-Web)

if you liketo Host diffrent usefull stuff that is essential use this stack:
[Harmony-Sync](#Harmony-Sync)

### Harmony-Media
We have used Jellyfin as the main component to host our media to the world cause it has great media support and does everything we want and unlike plex it's free and open-source!
For Organizing our media library however we will use two piece of component from Servarr stack named Sonarr, Radarr which all it does is rename files to what the Jellyfin desire to show the library as intended!

Please just read the yaml files there is instruction on how to do the docker side.
After you did the docker part you may come back here to continue :)

### Befor we Continue you need this
First installing the essentials and repository:
(we assume you are on linux and have a user other than root with sudo capabilities)

Installing requierd packages
Arch:
```
sudo pacman -S git docker docker-compose
```
Ubuntu:
```
sudo apt install git docker docker-compose
```

Cloning the repository
```
git clone https://github.com/db1234719/Harmony-Docker.git
```

Make sure docker is running
```
sudo systemctl enable docker.service --start-now
```

For every stack you want you should run this command:
(Change the STACK to the Stack you want: Media, Web, Sync (is cases senstive))
```
sudo docker compose up -f ~/Harmony-Docker/Harmony-<STACK>.yaml
```

Now you will want to use this file structure for a simple and clean look for your media like this:
```
home
-- user
----- data
-------- media
----------- movies
----------- shows
```
you have to do this commands:
```
mkdir ~/data ~/data/media ~/data/media/movies ~/data/media/shows
```

A tip for some people first time
To know your Local IP use this command:
```
ip a
```


Because it's the first time you have started all of them we will do the first time setups one by one:

#### Jellyfin
Open up a modern browser and paste your IP in the search bar with the port of your service which is Jellyfin:
(IPs used are examples)

192.168.1.2:8096

Now you will see this:
<img width="887" height="481" alt="jellyfin first page" src="https://github.com/user-attachments/assets/46396489-d248-436d-910d-0719453081a7" />
Which wants you to choose a language we will use English for conssistancy and versatility
After that click on Next

Now you will need to create the Admin user of Jellyfin server (Choose a strong password please and it's case senstive!)
first the username: admin
then the password: secret (don't use this it's a tutorial)
and the repeat of password: secret
<img width="887" height="709" alt="jellyfin first time user creation" src="https://github.com/user-attachments/assets/ad6d6732-b008-49d7-8301-a3982707d7b8" />
Then you click next

Now it needs your media library which we recommend a lot that you use a good structure like this tutorial:
We will

