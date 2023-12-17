# CCNA Syntax Exercises - Saving Configurations

# Summary 
This tutorial will equip you with the fundamentals to manage your network device's configuration effectively. We'll cover:

- Navigating the two: Demystifying the differences between the running-config (active settings) and the startup-config (persistent configuration).
- Starting Fresh: Learn how to safely erase configuration files, allowing you to start fresh.
- Committing Changes: Secure your adjustments by copying your running-config to the startup-config, making them permanent.

## running-config vs startup-config
- Startup-config: This configuration determines your device's state at bootup and is stored in the non-volatile RAM (NVRAM), persisting even after power cycles.
- Running-config: This is the currently active configuration stored in the device's volatile RAM (RAM). It exists only while the device is powered on and changes are lost upon reboot.
- Short and sweet answer : If you are to reboot the device **without** copying over the **running-config** to **startup-config** your changes will be lost. Let's do an example by issuing the following:
```
R1>enable

R1#configure terminal

R1(config)#hostname Gundam1

```
- We have now changed the hostname to Gundam1. Let's see what happens when we reload the device by issuing the following commands:
```
Gundam1(config)#end

Gundam1#reload
```
*Note* : Some of the newer cisco devices do offer to save your configuration before rebooting for this device. If you are using one of those please type no for the sake of exercise.

- After rebooting your device it should comeback as the following erasing the changing of the hostname change you performed:
```
R1> 
```
- Okay, back to square one! Time to save our configuration with the new hostname Gundam1. Let's peek at the current state of things first with this command: 
```
R1>enable

R1#show running-config
```
- You should get something returned like the following:
```
Building configuration...

Current configuration : 811 bytes
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
- Alright, we are going to compare the hostname in our **running-config** to our hostname in our **startup-config** now. Let's take a peek at that startup-config. Issue the following command:
```
R1#show startup-config
```
- Now you should see the following : 
```

Current configuration : 811 bytes
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
!         
!
!
!
```
- You see it, right? The hostname in **startup-config** matches your **running-config**. To make this change permanent, it's time to commit your first edit and save it. This ensures the new hostname persists even after a reboot. Let's start by editing the running-config with our new hostname by doing these steps:
```
R1#configure terminal

R1(config)#hostname Gundam1
```
- Now your hostname should be the same Gundam1 we set before. Now let's get out of configuration mode and move on to committing the change.
```
Gundam1(config)#end

Gundam1#
```

It's time to save your changes, but first, let's start learning how to erase your startup-config. 
```
Gundam1#erase startup-config
```
You should get this return
```
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm]
```
- Hit enter and let's confirm the startup-config has been erased from the NVRAM.
```
Gundam1#show startup-config
```
- You should see the following: 
```
startup-config is not present
```
- Alright, let's move on by issuing the copy command to make our **running-config** our new **startup-config** 
```
Gundam1#copy running-config startup-config
```
- You should recieve a prompt along these lines
```
Destination filename [startup-config]?
```
- Press enter and you will see the following:
```
Building configuration...

[OK]

Gundam1#
```
- Now let's wrap this up by issuing the reload command and see that new hostname sticks after the reboot. Issue the following command and wait for the device to comeback online:
```
Gundam1#reload

```

The next prompt should say this and you can just hit Enter
```
Proceed with reload? [confirm]
```
- If everything went as planned after the reboot of the device you should see the hostname we set as **Gundam1**. 

```
Gundam1>
```