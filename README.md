# enshrouded_dedicated toolset

Simple Shell script-set to "Monitor / Backup / Update" Enshrouded dedicated servers.


Server-Side: All the scripts work together to collect realtime informations (every minutes), and once a day backup the server map and upgrade server core files if needed (with SteamCMD). They all need to be placed in the PATH of the "enshrouded user" that runs the server binary (enshrouded_server.exe).


Client-Side: 'enshrd_query' + 'steamquery.py' scripts can be used from any linux manchine to get the server status, infos, and Username(s) that are currently logged in to the server.


### "enshrd_query" and "steamquery.py" :

- Show Server_Query infos (cf. https://developer.valvesoftware.com/wiki/Server_Queries)
- Show Currently connected Username(s)

requires: python3 'pip' for SteamQuery lib install and use, 'ssh access' to the server (preferably with a running agent), 


### "enshrd_steamuser_check" :

- Monitor enshroudedserver.log for [successfull/failed] connection attempts
- maintain a list of currently logged in Usernames
- (Optional) send custom message to telegram channel on [User Login/Logout]

Crontab every minute :
```
*/1 * * * * /usr/local/sbin/enshrd_steamuser_check
```
telegram-alert sample script can be found here :
```
https://raw.githubusercontent.com/zephxs/ncat-ipset-honeypot/master/telegram-send
```


### "enshrd_backupgrade" :

- Auto backup Map files (server 'savegame' folder)
- Auto Update Game Server Files with SteamCMD if Steam Game Repository show a new update

requires: 'enshrd_query' to block process if users are connected

Crontab every day @4h30 AM :
```
30 4 * * * /usr/local/sbin/enshrd_backupgrade
```

