# ZoneMinder Multiport Workaround

### Updated September 23, 2021

---

## Purpose

This workaround is used to bypass the browser monitor stream limitation.



## Nature of the problem

By default modern web browsers limit site streams to 6 at a time causing issues for streaming more than 6 camera feeds in Montage view.



This issue can be bypassed in Firefox by editing the ***\*network.http.max-persistent-connections-per-server\**** setting in **about:config**, however, as ZoneMinder's Montage view tends to function better in Chromium-based browsers, this is not the ideal solution.



## Nature of the solution

Resolve the stream limitation permanently by using **iptables** to redirect streams from port 30,000+ to port 80.



## Commands

Redirect ports 30000+ to port 80

> iptables -t nat -A PREROUTING -p tcp --dport 30000:30200 -j REDIRE CT --to-ports 80

Restart apache

> sudo systemctl restart apache2

Set multi port in ZM: **Options > Network > MIN_STREAMING_PORT**

> 30000

Save the changes to make persistent after reboot

> sudo iptables-save
