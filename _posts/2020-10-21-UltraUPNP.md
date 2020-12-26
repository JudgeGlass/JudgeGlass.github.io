---
layout: post
title: "UltraUPnP - An easy way to port forward"
date: 2020-10-21 10:52:00 -0700
comments: true
---

<em>Update 11/12/2020: </em> Added C++ version for fun<br>

Have you ever wanted to host a quick, temperary, game server without logging into your router? With this tool, you
map your computer / server to an external port. This tool allows you to add and remove port mappings on your router
without logging into it. (If you router has it enabled / supports UPnP). Go [here](https://github.com/Zicron-Technologies/UltraUPnP)

<h3>Usage:</h3>
Add port mapping
```bash
java -jar UltraUPnP1.1.0.jar -add -externalPort <INT> -internalPort <INT> -host <STRING> -proto <String: UDP|TCP>
```


Remove port mapping
```bash
java -jar UltraUPnP1.1.0.jar -remove -externalPort <INT> -host <STRING> -proto <String: TCP|UDP>
```

<h3>Library Usage</h3>
```java
public UltraUPnP(String[] args){
        RouterFinder findRouter = new RouterFinder();
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
<h3>Qt/C++</h3>
```c++
/*
Source Code: https://github.com/JudgeGlass/UltraUPnP-CPP
*/
#include <QCoreApplication>
#include <QtNetwork/QNetworkDatagram>
#include <QDebug>
#include <QList>

#include <routerfinder.h>
#include <router.h>
#include <routerargument.h>

int main(int argc, char *argv[])
{
    QCoreApplication a(argc, argv);

    RouterFinder routerFinder;

    if(routerFinder.search()){
        qDebug() << "CONNECTED";
    }else{
        qDebug() << "Could not connect";
        return -1;
    }

    Router *router = new Router(routerFinder.getDescriptorURL());
    qDebug() << "External IP: " << router->getExternalIPAddress();

    QList<RouterArgument> portMappings = router->getPortMappings();
    for(RouterArgument ra: portMappings){
        qInfo() << "<" << ra.getArgName() << ">" << ra.getArgValue() << "</" << ra.getArgName() << ">\n";
    }

    router->portForward(888, 888, "192.168.86.22", router->TCP);
    router->removeMapping(888, "192.168.86.22", router->TCP);

    delete router;
    return a.exec();
}

```
