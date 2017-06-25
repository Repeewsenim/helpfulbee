# ![helpfulbee](https://user-images.githubusercontent.com/26120940/27520450-d0c8dc9a-59c0-11e7-991d-77f372039381.png)
*Insert description about this project here.* This project is based off of Hartley Brody's [Facebook Messenger Bot Tutorial](https://blog.hartleybrody.com/fb-messenger-bot/).

# Deploying to an Apache Server

You need to have a LA(M)P (Linux, Apache, MySQL, and Python) stack installed on your server. This project doesn't use a database for persistent storage.

## Install and Enable `mod_wsgi`

WSGI (Web Server Gateway Interface) is a specification for interface between web servers and web applications for Python. Install the `mod_wsgi` Apache HTTP server mod that allows Apache to serve Flask applications.

```bash
sudo apt-get install libapache2-mod-wsgi python-dev
```

Enable `mod_wsgi`.

```bash
sudo a2enmod wsgi
```

## Set up a Virtual Environment

`virtualenv` is a tool that will create sandboxed Python execution environments. This will keep the application dependencies separated from the main system.

It can be installed using `pip`.

```bash
sudo pip install virtualenv
```

Create the virtual environment and activate it. `venv` is the name of the virtual environment that will be created.

```bash
virtualenv venv
source venv/bin/activate
```

Next, install the Python dependencies listed in `requirements.txt`. When finished, deactivate the virtual environment with:

```bash
deactivate
```

## Run the Deploy Script

Navigate to the `deploy/` directory and edit the variables at the top of `deploy.sh`. Do **not** include a trailing `/` at the end of the path names.

- `VENV_DIR` is the absolute path to the directory of the virtual environment created.
- `INSTALL_DIR` is the absolute path to the directory where you want the application to be installed to.
- `SERVER_NAME` is the domain name that the application will be served to.
- `SECRET_KEY` is the key used to sign user session cookies. Keep this really secret.

Save and run the script to deploy the application. This will install *Helpful Bee* to the specified deployment directory and configure the Apache server to run the application.

```bash
sudo bash deploy.sh
```

**Warning:** *This will remove everything in `INSTALL_DIR` if it exists. Double check that the variable values are correct before running the script.*