## Fresh, working EQEmu + ProjectEQ Windows server
Files were copied from the official repos at the time some of the resources were pulled offline. This is essentially a plug-and-play archive and guide to installing a working Windows EQEmu server from scratch, exactly as it would have been at that time, with much of the config guesswork taken out of it.

You will need to install 2 support apps (Strawberry Perl, MariaDB).  Other than those, this repo contains everything needed to run the server:  pre-compiled binaries, quests, plugins, server maps, properly formatted config files, etc.

## How to Use:
### Perl
#### Install Strawberry Perl
ProjectEQ scripting currently implements both Perl and Lua scripts made over the years.  Only Perl requires an installation on your machine since Lua is processed directly by the server.

https://strawberryperl.com/download/5.24.4.1/strawberry-perl-5.24.4.1-64bit.msi (or latest)

### Database

#### 1. Install MariaDB (10.x)

* https://dlm.mariadb.com/3277103/MariaDB/mariadb-10.11.4/winx64-packages/mariadb-10.11.4-winx64.msi
* Install it as a service if you prefer (Can set to Manual startup in Windows Services if preferred)
    * Manual startup means it's not consuming RAM when not in use
* Use 4gb buffer and 16kb page (1gb-2gb is fine if you're low on RAM since this is just a personal server)
* Use username "root" or "peq" and remember the password you choose

#### 2. Add MariaDB to Window's path
* Type "```env```" in Windows search to pull up "Edit the system variables"
* Click "Environment Variables" button
* In the lower textarea (System variables), click "Path"
* Under the lower textarea (System variables), click “Edit…”
* Click the "New" button
* Type "```C:\Program Files\MariaDB 10.11\bin\```" or whatever your Maria ```bin``` folder is
* Click "OK" out of everything


#### 3. Create the ProjectEQ database
* Extract the ProjectEQ sql files from the .zip file in `_database-setup/`, to anywhere
* Open a ```cmd``` prompt
* ```cd``` to the extraction folder **(important)**
* type ```mysql -u <username> -p``` using the username you chose when installing MariaDB
* type the password you chose when installing MariaDB
* You'll now be at a MariaDB database prompt, run these commands:
```
CREATE DATABASE peq;
use peq;
source create_all_tables.sql;
```

#### 4. (Optional) Install HeidiSQL
* Popular tool for direct, simple database administration
* https://www.heidisql.com/download.php 
* Create an entry for the MariaDB installation using the username and password you chose earlier.  Save that entry.  You can name it whatever you want like "PEQ"

#### 5. Spire
* This is included in the EQEmu root.  An official EQEmu tool for server and database administration and visualization that you can use alongside or in place of HeidiSQL.  I only use it to look things up (items, npcs, etc.) but it can do quite a bit.
* To use, just run the exe

#### 6. Server Configs
These have been fully set up but you'll need to put in your MariaDB username and password, if different from the defaults, and you'll need to put in your LAN IP address or 127.0.0.1 in place of the 192.168.0.1 placeholder. Where 127.0.0.1 already exists, leave as is (unless you have some reason to change it.) Check both configs in the root folder to make these changes. There is some overlap of data but it's necessary:
* Check ```eqemu_config.json``` (for the server)
* Check ```login.json``` (for the separate loginserver)

#### 7. Client

* Install a RoF2 or Titanium EQ client.
* In your client's `eqhosts.txt` file, set the LoginServer as follows:
    * For RoF2 clients:<br>
    ```
    [LoginServer]
    Host=127.0.0.1:5999
    ```
    * For Titanium clients:<br>
    ```
    [LoginServer]
    Host=127.0.0.1:5998
    ```
* Regardless of which client you use, do not change the 5998 in the server configs from step 6.  That stays 5998 in either case.
* Create a shortcut to the client .exe and change the shortcut's target by adding "patchme" to the end.  This is not special to this installation, but rather to all EQEmu installations.  For example, your Target should say something like:
"C:\games\everquest\client\eqgame.exe patchme"
