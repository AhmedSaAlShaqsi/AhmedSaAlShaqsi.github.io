We are going to build a wordpress in a docker:

# Installations:
First of all we will need to install Docker desktop, and here is the installation link: https://docs.docker.com/engine/install/. After installing you will need to get the docker-compose.yml file, and there are actually a lot of resources to get this file from one of them is docker hub website and then search for the wordpress, scroll down and you will find the .yml file, here is the link for it:https://hub.docker.com/_/wordpress.
# Running docker:
After getting the .yml file it is better to place it in a specific file:
 ```bash
 mkdir my_wordpress
 cd my_wordpress
 ```
 after that place the docker-compose.yml file in it.
 To run the docker compose write this command:
 ```bash
 docker-compose up -d
 ```
 and then go to you browser and type "localhost:port," in the port section write the port that you specified in the .yml file.
 **Setting up the wordpress in the web:**
 ![installing worpress](https://www.google.com/url?sa=i&url=https%3A%2F%2Fmarkheath.net%2Fpost%2Finstall-wordpress-docker-compose&psig=AOvVaw3DtvW_N7fhlOG_uceZ4_uR&ust=1731995360470000&source=images&cd=vfe&opi=89978449&ved=**0CBQQjRxqFwoTCLiL69WX5YkDFQAAAAAdAAAAABAE**)
 
Click in the language that you want and click install.
After that there will be a section to add a username and a password do it.
And there you go there is your wordpress!
 