## Project EQ Database (Sept 28, 2025)</h3>
This is a full export of the Project EQ database used by EQEmu as of 09/28/2025.

### How to Use

#### 1. Install MariaDB (10.x)

* https://dlm.mariadb.com/3277103/MariaDB/mariadb-10.11.4/winx64-packages/mariadb-10.11.4-winx64.msi
* Install it as a service if you prefer (Can set to Manual startup in Windows Services if preferred)
    * Manual startup means it's not consuming RAM when not in use
* Use 4gb buffer and 16kb page (1gb-2gb is fine if you're low on RAM since this is just a personal server)
* Use username "root" or "peq" and remember the password you choose

#### 2. Add MariaDB to Windows path
* Type "```env```" in Windows search to pull up "Edit the system variables"
* Click "Environment Variables" button
* In the lower textarea (System variables), click "Path"
* Under the lower textarea (System variables), click “Edit…”
* Click the "New" button
* Type "```C:\Program Files\MariaDB 10.11\bin\```" or whatever your Maria ```bin``` folder is
* Click "OK" out of everything


#### 3. Create the ProjectEQ database
* Extract this repo folder's .zip anywhere
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
* Create an entry for the MariaDB database "peq" we just created, using the username and password you chose earlier.  Save.

Done.
