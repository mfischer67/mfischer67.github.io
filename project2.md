# Project 2 - Docker Project
### System Administration
### Madison Fischer

## Methodology

I used this source for installing WordPress: https://www.hostinger.com/tutorials/run-docker-wordpress
I used this source to look up IP address: https://www.linuxtrainingacademy.com/determine-public-ip-address-command-line-curl/

We installed docker and docker compose in class via the Powerpoint Slides 

### Installing WordPress 

Once docker and docker compose are installed, you first need to check you are on the right version with the command `docker compose -version`

Then once you've checked the version, you make a directory called 'wordpress' with the command `mkdir wordpress`

Then you have to cd into the wordpress directory with the command `cd wordpress`

After that, I chose to use VS Code to create my .yml file, then I inserted the info that I got from my source into the .yml file. I did change the port number from 8000 to 8080 because of some issues I was having with port 80000

Then to finish the installation of wordpress, I put in the command `docker compose up -d` which finished the install of wordpress 

* I ran into some issues of the port 8080 not connection properly, I asked Codi and I found out that i had to use my ip address instead of localhost in the URL

Then I had to run the link http://10.10.1.111:8080/ to open WordPress. 

Then I entered my credentials and made a username and password

Then I was on the main WordPress website 

![Main Page](/mainWordpresspage.png)

![Successful Login](/successful login of wordpress page.png)
