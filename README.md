# Harmony-Docker
A repository with focus on Docker Compose yaml files that just works as intended (and is reproducable) so you enjoy Self-Hosting more!

Fun Fact: when i was creating this repository i installed and Archlinux virtual machine inside my Archlinux machine to just test things out and it's a personal thing but i recommend Archlinux cause it's minimal and a lot more stable that you think! :)

Caution:
IPs used are examples
Passwords need to be a lot more SECURE
Please use our file structure for the best experience

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
sudo systemctl enable docker.service --now
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
You have to do this commands:
```
mkdir ~/data ~/data/media ~/data/media/movies ~/data/media/shows
```
And give premissions to these users so there won't be any premission confilicts:
```
sudo groupadd media -g 321 && \
sudo useradd abc -u 111 -g media
```
Then after we added that group and user we give them the data folder
```
sudo chown abc:media ~/data -R && \
sudo chmod 775 ~/data -R
```

A tip for some people first time
To know your Local IP use this command:
```
ip a
```

Because it's the first time you have started all of them we will do the first time setups one by one:

#### Jellyfin
Open up a modern browser and paste your IP in the search bar with the port of your service which is Jellyfin:

```
192.168.1.2:8096
```

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
We will add a shows and a movies like below
You click the Add Media Library and add one with type movies and name movies and path the data media movies
<img width="886" height="594" alt="image" src="https://github.com/user-attachments/assets/2a45356f-9170-4732-91ee-d2c4a6c50573" />
And i recommend this option to be turned on so your media be more ready to move whenever you want to a new place!
<img width="807" height="152" alt="image" src="https://github.com/user-attachments/assets/39bf0333-3b24-4f64-9cce-4e61e30d6d09" />

after that we will do the same for shows:
<img width="888" height="592" alt="image" src="https://github.com/user-attachments/assets/faabbae8-408c-4183-89d2-7fdd62642301" />

you will have this as a result after you click ok:
<img width="887" height="566" alt="image" src="https://github.com/user-attachments/assets/573b456b-f0c2-4b7e-8581-babe810d1973" />

Then we click Next and leave the preferred metadata language at English:
<img width="886" height="533" alt="image" src="https://github.com/user-attachments/assets/b59eb690-15f4-4a01-84cc-0b9af86f3e81" />

After thats done and we click Next we have this two options:
<img width="887" height="478" alt="image" src="https://github.com/user-attachments/assets/d38d7cd0-c505-48fa-93ff-f2f38a7c9350" />
Which i recommend do not touch and Please leave the first one enabled cause it's crucial you may lose access to the server if disabled!

And dada
Our work with Jellyfin is done.
<img width="889" height="363" alt="image" src="https://github.com/user-attachments/assets/885653cd-1785-41f6-b2ea-fdd4ead606d2" />

#### sonarr
now we go to sonarr to set it up!
it's at this address:

```
192.168.1.2:8989
```

This will be what we are going to be greeted with which we will set according to picture:
authication methos: forms
authication requierd: enable
username: admin
password: secret
repeat password: secret
<img width="888" height="946" alt="image" src="https://github.com/user-attachments/assets/66b5966c-ac5a-4866-9ba3-7498d3676288" />
And we hit save

Now we will use the left side settings -> media management and turn on the advanced options and rename episodes then we scroll to the bottom and enable unmonitor deleted episodes
<img width="675" height="214" alt="image" src="https://github.com/user-attachments/assets/ba76bd23-5692-459d-b846-a8b62ed8e6c4" />
<img width="669" height="147" alt="image" src="https://github.com/user-attachments/assets/0ff324cd-1390-4a07-9796-dd45a80d0ca4" />


after that at the premission which is very important we will enable set premissions and chmod folder will be on 775 and chown group 321
<img width="656" height="541" alt="image" src="https://github.com/user-attachments/assets/7b95ef8c-5439-4468-81d4-68722a4c72e0" />

Now that those are done we will go at the bottom on root folders and add root folder like this:
(we type the exact path for shows cause it's sonarr)
<img width="876" height="818" alt="image" src="https://github.com/user-attachments/assets/73a4dbc6-8f28-4410-b57d-d88ff914e5b8" />

Then we hit save changes and boom sonarr is done too!
<img width="679" height="60" alt="image" src="https://github.com/user-attachments/assets/a6970fc8-89ea-4bac-ab0b-0f3cc07ad38a" />
