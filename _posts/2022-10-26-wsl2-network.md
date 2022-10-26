---
layout: post
title: "WSL2 Network"
date: 2022-10-26 09:00:00 +0800
categories: Linux
tags: [Linux, WSL2]
---

## How to access server which is hosted on WSL2 ?  
1. Use proxy to forward connection from win10 to wsl2.
    - ``` text
        [powershell] > netsh interface portproxy show all

        # listen address/port -> windows 10 ip/port
        # connect address/port -> wsl2 ip/port
        [powershell] > netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=12345 connectaddress=172.26.68.222 connectport=12345

        # If you regret.
        [powershell] > netsh interface portproxy delete v4tov4 listenport=12345 listenaddress=0.0.0.0
        ```
2. Add related ports to inband rule in firewall.
    1. Settings
    2. Update & Security
    3. Windows Security
    4. Firewall & netowrk protection
    5. Advanced settings
    6. Inband Rules
    7. New Rule
    8. Port
    9. Enter the port you want
    10. Allow the connection
    11. Check all
    12. Enter name, e.g., WSL2 network.
    13. Finish