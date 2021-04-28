# Account Management Portal
The purpose of this portal is to allow specific users in BCS to track the outcome of each Recon. With the developement of this portal, it hopes to improve effeciency in tracking all of BCS's privilege accounts in their system.

# Source Files
Currently, the package/directory **app** is hosting the portal/flask application. Next we have the main module ( ***main.py**). This main module is important as it carries the different URLs that the portal implements. We then have the rest of our self-implemented modules that resides in the Mods directory. It consists of:
* **RequestHandler.py** : This is our request handler module that handles all the different request from each URL processed by the portal. It is the main body of all api request from the portal
* **Config.py**: This module holds all configuration information required by the portal. For instance , database configuration, file names etc. If any of these parameters needs changing, the next developer would have to change only this file.
* **db.py**: This handles all the basic database queries, such as SELECT, INSERT. Currently, the portal only handles these 2 main query statements. if require any additional query statements, this module needs to be expanded.
* **logs.py**: This module handles all the logging. All log files produced by this module resides in the **log** directory. Naming convention of all log files follow the **YYYY-MM-DD.txt**. 
* **account.py** This is a simple account class , that creates an account object with the class parameters,account id,device id,account,hostname,ipaddress,device type,network remediation,cyberark remediation,breakglass remediation, uam remediation.

# Getting Started
The Account Management Portal is a Flask application currently running on Python 3. It is currently interacting with a MySQL database. Flask, Python and MySQL needs to be installed in the local machine for the portal to run on in a development(SIT etc) enviroment.
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Installing Python
If you do not have python installed in your SIT enviroment, you can install Python from the Python official website. To make sure Python 3 is installed, open your terminal window and type the `py` and you should expect to see:

### Installing Flask
The next step is to install Flask. For windows, 
```
py -m pip install Flask
```
Make sure you are conneccted to the internet. If not, the package would not be installed.

# Preparing the database

### Installing MySQL and MySQL Workbench
You can install MySQL directly from MySQL website. You will also need a visual database tool to mantain the database during SIT developement. Hence, you would need to install MySQL Workbench as well.

### Configuring an access to a localhost instance
After both has succesfully been installed, you would need to create a localhost instance in MySQL for the portal to interact with it. Open MySQL Workbench. In the setup New Connection Dialogue, Type your database connection credentials.
The credentials would be like the following

* Connection Name: You can name this whatever you like.
* Connection Method: Standard (TCP/IP).
* Hostname: You can use your domain our your cPanel IP address.
* Port: 3306
* Username: Your cPanel username or the user you created for the database.
* Password: cPanel password or the password for the database user that was created.
* Default Schema: This can be left blank.


### Insert Latest Recon data into database
We would need to insert the latest recon data into the database. As of 20 April 2021, the script updatedb.py in **insertdb** directory reads recon_2021.xlsx and upload it into the database.
Any changes in either **naming** or **excel format** of the recon data excel file, would require for certain lines of the script to change respectively. Please take note that this process is only for Network accounts. The schema network_accounts created will only host network accounts recon data. If this portal were to expand to cater to other accounts such as Database accounts, Operating systems etc, new schemas has to be created to host these data. *updatedb.py* script has to expanded as well.

To run script, simply run the command 

```
py updatedb.py
```
Results is expected to be as such:
```

```

### IMPORTANT** : Future recon data insert
Currently, since its only the 1st recon, inserting the recon data is quite straightforward. updatedb.py still applies. However, moving forward, during the next subsequent recons, when doing an insert of data into the database, the script is required to change to take into account, the comparisom between all past recon and the current recon. I have created a new script to do this, **reconupdate.py**

* updaterecon.py summary:
* retrieve all past recon's data 
* read current recon's data excel sheet
* if account is new, insert account into um_privilege_accounts table
* if device is new, insert device into um_devices

For every entry in current recon consolidated excel:
* 1. if it is a new device entry( not found in DB records)
* 2. it is an existing device and account ( found in our DB records)
* 3. if is an existing device but new account entry

For every entry in past recon:
* 1. if it is an existing device, and existing account but not found in new data

Go to Workbench and the 8 respective tables would have been created in network_accounts schema , with all the updated recon data.

# Database Design

* um_privilegeaccounts

id| name 
| :--- | ---: 

* um_devices
id| hostname | ipaddress | devicetype
| :--- | ---: | ---: | ---:



# Creating a virtual Enviroment

After having the database set up on your development local machine, we can start to run the portal. It is recommended to run the FLask Application in a virtual enviroment to keep the dependencies of this project separated from other projects in your local machine. 
To do so, we would need to first reside in the project directory and use this command to start up the virtual enviroment called **venv**.

```
cd ""
py -m venv venv
venv\Scripts\activate
```

Results would be as such

```

```
You would need to install all the libraries in **requirements.txt** before running the Flask Application. Simply run command

```
py -m pip install -r requirements.txt
```

# Running the portal 

To run the portal, simply type in the command flask, and open your internet browser and load http://127.0.0.1:5000/index
```
flask run
```

During development, if any changes are made, to see the new changes, simply stop the flask application with `^C` and re-run the flask application with `flask run`

# Libraries

The Account Management Portal is developed using Flask framework as well as front end open source libraries such as AdminLTE and Chartjs. All CSS/JS scrits from these libraries are already embedded into the static folder. Can refer to their individual websites to learn how to use the respective libraries to create interactive charts for data visualisation.



# Deployment

Add additional notes about how to deploy this on a live system




# Authors

* **Nur Atsirah Binte Kamsir**
![Uploading image.png…]()
