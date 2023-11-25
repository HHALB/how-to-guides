# Setting up Directories and Permissions for a Plex Media Server

I created this guide to simplify the process of setting up Plex Media Server on Linux, particularly Arch Linux. However, these instructions are applicable to other Linux distributions as well.

This guide assumes that you have a basic understanding of using the *command-line interface (CLI)* via terminal, even if you're a beginner. I'll strive to explain the commands we'll use to create directories and set permissions for your Plex Media Server in a beginner-friendly manner.

## Setting up Directories 

If you're familiar with creating directories using the terminal, you can skip to the second half of this guide. Otherwise, let's begin by creating directories in your media folder.

Let's first type out:

```
mkdir Media
```

**Note: Some distros such as Ubuntu and Mint setup a media folder during installation.**

Now lets jump into that media folder by typing : 

```
cd Media
```

Nowe lets make some directories for your media by typing : 

```
mkdir Movies
mkdir Shows
mkdir Music
```

Now confirm you have these new folders in your media directory by typing it out:

```
dir
```

You should see the following 

```
Movies
Shows
Music
```

With the directory creation complete, let's proceed to the next step: working with groups.

## Groups

Now that we've created the necessary directories, let's delve into the concept of groups. Groups allow a set of users to share the same permissions for reading, writing, and executing specific resources. In this instance, we'll use groups to grant Plex access the directories we have previously setup and thereby allowing Plex to access / play your files. 

You can get a list of your groups by typing this in the terminal:
```
Groups
```

This is an example of what shows up on my Arch Machine

```
wheel
hhalb
Plex
```


Now that you have verified the groups, it's time to add yourself to the Plex Group. You can do this by typing:

```
sudo usermod -a -G $USER plex
```
**The usermod command is used to modify attributes to already existing accounts on your Linux box.** 

I want to note when executing this command it will affect different files /etc/ folder.

More Spefically, when using this command what you are doing with -a is adding you, the $USER to a secondary group. While using -G is adding you, the $USER to a supplemantry group. 

### Other notes

**It's recommended that you NOT group your root with the Plex Group** 

## Permissions for your Plex Media Server

Now we have taken care of groups lets start setting up the permissions for your Plex Media Server to be able access your folders.

The next command that we will use is the following 

```
sudo chown $USER:plex /media/$USER
```

**The chown command is used to change owners of the directory your plex media server is trying to accesss.**

The next command we will be using is : 
```
sudo chmod 750 /media/$USER
```

**The chmod 750 is setting the permission for you and your group, which is Plex to be able to read and execute your files in the media folder**

sudo setfacl -m g:$USER:rwx /media/$USER/

**This command is utilitizing Active Control Lists. ACLs give more flexibity in permissions than your traditional CHMOD. The -m is to modify permissions, while the g: is to represent our group for accessing plex.**

##Rebooting your Plex Media Server via terminal

Now its time to reboot the Plex Media Server.

We can do this by typing on Arch and Manjaro with
```
systemctl restart plexmediaserver (Arch and Manjaro)
```
Or if you are using a distro such as Ubuntu and Mint you can type: 

```
sudo service plexmediaserver restart
```
## Conclusion 

Now your plex can access your media folders and you can enjoy using Plex to its full potential