---
layout: post
title: "UltraUPnP - An easy way to port forward"
date: 2020-10-21 10:52:00 -0700
comments: true
---

Have you ever wanted to host a quick, temperary, game server without logging into your router? With this tool, you
map your computer / server to an external port. This tool allows you to add and remove port mappings on your router
without logging into it. (If you router has it enabled / supports UPnP). Go [here](https://github.com/Zicron-Technologies/UltraUPnP)

#Usage:
```bash
java -jar UltraUPnP1.0.0.jar -externalPort <INT> -internalPort <INT> -host <STRING> -proto <String: UDP|TCP>
```

#Library Usage
```java
public UltraUPnP(String[] args){
        FindRouter findRouter = new FindRouter();
        Router router = null;
        try {
            if(findRouter.search()){ // Serch for router
                router = new Router(findRouter.getUPNPUrlDescriptor()); // Connect to router
            }else{ return;}

	    router.portForward(7979, 7979, "192.168..86.54", Router.TCP); // Add port mapping
            router.removeMapping(7979, "192.168.86.54", Router.TCP);      // Remove port mapping
            System.out.println("External IP: " + router.getExternalIPAddress()); // Get your external IP
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```
