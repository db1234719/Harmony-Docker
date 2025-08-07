# Harmony-Docker

A repository focused on Docker Compose YAML files that *just work* as intended (and are reproducible), so you can enjoy self-hosting more!

> **Fun Fact:**  
> When I was creating this repository, I installed an Arch Linux virtual machine inside my Arch Linux machine just to test things out. It’s a personal preference, but I highly recommend Arch — it’s minimal and way more stable than people think. :)

> **Caution:**  
> - IPs used are **examples**  
> - Passwords should be **much more secure**  
> - Please follow our **file structure** for the best experience  

---

## Harmony Files List

If you want to host a media server, use this stack:  
[**Harmony-Media**](#harmony-media)

If you’re interested in hosting a website, use this stack:  
[**Harmony-Web**](#harmony-web) *(in progress)*

If you’d like to host other useful self-hosting services, use this stack:  
[**Harmony-Sync**](#harmony-sync) *(in progress)*

---

### Harmony-Media

We’re using **Jellyfin** as the main component to host and stream media because it has excellent media support and — unlike Plex — it's free and open-source.

For organizing the media library, we use two components from the Servarr stack: **Sonarr** and **Radarr**. Their job is to rename and sort media files so Jellyfin displays the library the way it’s intended.

Just read the `.yaml` files — they include instructions for the Docker side. After you set that up, come back here to continue.

---

### Before We Continue — You Need This

We assume you're on Linux, using a non-root user with `sudo` privileges.

#### Install required packages

**Arch Linux:**
```bash
sudo pacman -S git docker docker-compose
```

**Ubuntu:**
```bash
sudo apt install git docker docker-compose
```

#### Clone the repository:
```bash
git clone https://github.com/db1234719/Harmony-Docker.git
```

#### Make sure Docker is running:
```bash
sudo systemctl enable docker.service --now
```

#### Start a stack:
Replace `<STACK>` with one of: `Media`, `Web`, or `Sync` (case-sensitive).
```bash
sudo docker compose -f ~/Harmony-Docker/Harmony-<STACK>.yaml up
```

---

### Recommended File Structure

To keep your media organized and clean, use this layout:

```
home
└── user
    └── data
        └── media
            ├── movies
            └── shows
```

Create it like this:
```bash
mkdir -p ~/data/media/movies ~/data/media/shows
```

Give proper permissions:
```bash
sudo groupadd media -g 321 && sudo useradd abc -u 111 -g media
```

Then assign ownership:
```bash
sudo chown abc:media ~/data -R && sudo chmod 775 ~/data -R
```

---

### Pro Tip

To check your **local IP address**, run:
```bash
ip a
```

---

## Initial Setup Steps (First-Time Only)

### Jellyfin

Open a browser and go to:
```
http://192.168.1.2:8096
```

You’ll see a language selection screen — choose **English** for consistency.

Then create your **Admin** account:
- Username: `admin`
- Password: `secret` *(choose a stronger one, this is a demo)*

Next, you’ll be asked to set up your **media libraries**. Use paths like:
- `/data/media/movies` for **Movies**
- `/data/media/shows` for **TV Shows**

We recommend enabling:
- `Enable real-time monitoring`  
- `Import metadata from path names`

Leave **metadata language** as English, and keep the "Allow remote connections" enabled for access. Done — Jellyfin is ready.

---

### Sonarr

Go to:
```
http://192.168.1.2:8989
```

Set authentication:
- Auth method: `Forms`
- Require auth: `Enabled`
- Username: `admin`
- Password: `secret`

Then go to:
- **Settings > Media Management**
  - Enable **advanced settings**
  - Turn on **Rename Episodes**
  - Enable **Unmonitor deleted episodes**

Under **Permissions**:
- Set permissions: `Enabled`
- Folder chmod: `775`
- Group chown: `321`

Then under **Root Folders**:
- Add: `/data/media/shows`

Done — Sonarr is ready.

---

### Radarr

Same setup as Sonarr. Only difference:
- Use `/data/media/movies` as the root folder  
Because **Radarr is for movies**, while Sonarr is for TV shows.

---

## 🎉 Done!

You now have a fully working self-hosted media server.

I skipped some advanced things and included only the essentials. Hopefully, this helps you enjoy what you've created — clean, simple, and powerful.
