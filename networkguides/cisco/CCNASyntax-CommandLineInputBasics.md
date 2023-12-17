# CCNA Syntax Exercises Written In Markdown - Part 1 - Getting to know Command Line Input

# Summary 
This exercise dives into the heart of Cisco device management – the command-line interface (CLI). You'll explore its functionalities, including:

- **Command Parser:** Understand how commands are interpreted and executed.
- **Auto-complete:** Learn to utilize this time-saving feature for faster command entry.
- **Keyboard Shortcuts:** Learn efficient navigation techniques within the CLI environment.

Whether you're practicing on GNS3, Packet Tracer, or a real Cisco device, this is a good way to start getting yourself comfortable using the IOS Command Line.

## Starting with basic commands 
Let's begin! Open the console on your device, and you'll see the current hostname displayed. Now on mine its called #R1 via GNS, but for these exercises I am going to use YourDevice> and at the end I will show you how to change it look like my hostname.

**Example** 

```
YourDevice> 
```

- The > prompt signals you're in user **EXEC** mode, the most basic and restricted level of the CLI. It focuses on monitoring, not configuration. Any attempt to modify the device, like with configuration commands, won't be allowed. Let's see an example of this by issuing the following command:

```
YourDevice>configure terminal
```

- You should get a return error that looks like this:
```
% Invalid input detected at '^' marker.
```
- Time to experiment! Remember, user **EXEC** mode focuses on monitoring. Commands for configuration won't work here. But we can still access helpful information. Typing ? will display a list of all valid commands you can use in this mode:
```
YourDevice>?
```
- Enter the ? command to see a list of all valid commands you can use in user EXEC mode. This will display two columns:

- Commands: These are the actual commands you can use in the mode you are. (The router I am using is already in privledged mode but the concept is the same.)
- Descriptions: This column provides a brief explanation of what each command does.

You will also see entries like ---MORE--- indicating additional commands beyond the initial display. Remember, the specific list you see will vary depending on your Cisco device model and what mode you're currently in.

```
  access-enable    Create a temporary Access-List entry
  access-profile   Apply user-profile to interface
  access-template  Create a temporary Access-List entry
  alps             ALPS exec commands
  archive          manage archive files
  audio-prompt     load ivr prompt
  auto             Exec level Automation
  bfe              For manual emergency modes setting
  call             Voice call
  ccm-manager      Call Manager Application exec commands
  cd               Change current directory
  clear            Reset functions
  clock            Manage the system clock
  cns              CNS agents
  configure        Enter configuration mode
  connect          Open a terminal connection
  copy             Copy from one file to another
  crypto           Encryption related commands.
  debug            Debugging functions (see also 'undebug')
  delete           Delete a file
  dir              List files on a filesystem
```

- Time to explore auto-complete and keyboard shortcuts! Let's start with a command I use a lot, which is the *show interfaces* command to give an idea of auto-complete.
```
YourDevice>show interfaces
```

- You should see something like this after issuing the command:
```
FastEthernet0/0 is administratively down, line protocol is down 
  Hardware is AmdFE, address is cc01.c2cd.0000 (bia cc01.c2cd.0000)
  MTU 1500 bytes, BW 100000 Kbit/sec, DLY 100 usec, 
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full-duplex, 100Mb/s, 100BaseTX/FX
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input never, output never, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue: 0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     0 packets input, 0 bytes
     Received 0 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
     0 watchdog
```
Let's practice! Try crafting some valid and invalid examples using the show interface command. Experimenting is a great way to learn the CLI's flow. We'll start with one that definitely will work.
```
YourDevice>Sh Int
```
- Notice anything familar? That when issuing the *sh int* works the same way as *show interfaces*? Now lets try another one.
```
YourDevice>sh i
```
- You sould see something that looks like this in.
```
% Ambiguous command:  "sh I"
```
- Cisco's auto-complete feature is a handy tool for navigating the vast command-line interface (CLI) efficiently. However, it requires a bit more than just a couple of letters to work its magic. While typing *sh i* won't trigger auto-completion, something like *sh int* will work the same as typing *show interfaces*

Take a few minutes to play around and get a feel for what works. You'll be surprised how quickly you will start to be able to shorten commands. 

## Keyboard Shortcuts 
- This table features handy keyboard shortcuts to navigate the Cisco CLI efficiently. We'll demonstrate a couple by using *show interfaces* command, but the cheat sheet below offers plenty more to explore!

| Keys           | What it does                                               |
|----------------|------------------------------------------------------------| 
| CTRL + A       | Moves The cursor to the first letter.                      |
| CTRL + B       | Moves the cursor back on letter.                           |
| CTRL + C       | Aborts the current command and will exit configuration mode|
| CTRL + D       | Erases a character right of the cursor.                    |
| CTRL + E       | Moves the cursor to end of the command line.               |
| CTRL + F       | Moves the cursor forward a character.                      |
| CTRL + N       | Displays the next command from your history.               |
| CTRL + P       | Displays the previous command from your history.           |
| CTRL + R       | Redisplays the current CLI.                                |
| CTRL + U       | Erases a line.                                             |
| CTRL + W       | Erases a word from the left of the cursor.                 |
| ESC + B        | Moves the cursor back one word.                            |
| ESC + F        | Moves the cursor forward one word.                         |
| Tab            | Will complete a partial command similar to the ones above. |


- Now lets work with the commands above to get started using a couple of examples. 
```
YourDevice>show interfaces
```
- Lets use CTRL + A and it should look like this with S being where the cursor is located. I made the || to display this.
```
YourDevice>S||how Interfaces
```
- Lets use CTRL + D and it should look like this
```
YourDevice>||how Interfaces
```
- Lets use CTRL + F and the cursor should be at the end now.
```
YourDevice>Show Interfaces||
```
- I recommend playing with following commands via the table above to learn how to navivate the CLI. Seeing how we've been using the show interface command a lot lets move on some more commands that use show to get more familar with CLI.

# Show Commands
- The show command is one you should familiarize yourself with due to its extensive options and overall importance. Let's try the following example first.
```
YourDevice>show ip interface brief
```
- Here is an example of what shows up when inputting this command:
```
Interface                  IP-Address      OK? Method Status                Protocol
FastEthernet0/0            172.68.1.110    YES manual up                    up      
FastEthernet0/1            172.16.1.111    YES manual up                    up    
```
- Now lets try show history which show the commands you have used previously
```
YourDevice>show history
```
- Here what I got after my entering:
```
  show interfaces
  conf term
  show ip address brief
  show ip interface brief
  show history
```
- The above are  the previous commands I've used on my setup but Cisco will store up to a 100 commands for you to look back on. Now let's talk about one the most important ones, and this show the running-config, which displays the active configuration for your device. Now lets type in the follow. First, we have to actually go into priviledge mode, but don't worry we aren't actually changing anything yet. We will go more indepth in the next section. Now let's get startted by typing : 
```
YourDevice>Enable
```
- Now we can type out:

```
YourDevice#show running-config
```
- You should get some results that look like this:
```
Building configuration...

Current configuration : 865 bytes
!
version 12.4
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
!
hostname R1
!
boot-start-marker
boot-end-marker
!
!
no aaa new-model
memory-size iomem 5
no ip icmp rate-limit unreachable
!
!
ip cef
no ip domain lookup
!
!
 --More-- 
```
## Getting started with Priviledged Mode 
We've been talking about Cisco CLI's user mode, learning commands and navigating its interface. Now, it's time to unlock even greater control by entering privileged mode.

Privileged mode grants access to advanced configuration options and sensitive commands for managing your network device. Think of it as the captain's chair on the bridge, offering full control over the course. Now let us start by typing:
```
YourDevice>enable
```
- Now you should notice a small change in the CLI. The **>** has now been replaced with a **#**
```
YourDevice# 
```
-Let's do some actual configuration! Let's start with typing the following:
```
YourDevice#configure terminal
```
You should see it another difference now. Notice how (config) has been added?
```
YourDevice(config)#
```
Now lets issue a command to change that **hostname**
```
YourDevice(config)#hostname R1
```
Congrats! You've just changed your configuration if it says the following:
```
R1(config)#
```
Alright, lets wrap this up and get back to **EXEC** mode by issuing:
```
R1(config)#end
```
And then: 
```
R1#exit
```
And that is it! Next we will go a little more in depth with start saving the changes you've just made!