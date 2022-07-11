# Getting started.
## Pre-requisites
Flash jetbot image onto Heribertbert, follow the instructions here: https://www.waveshare.com/wiki/JetBot_AI_Kit
GitHub Jetbot repository.  
Important link to the master jetbot repository from Waveshare.  
https://github.com/waveshare/jetbot 

## 1. Accessing Heribert-bert’s local file on another pc 

Use IP address of Heribertbert and port 8888 to connect it using an external PC 

- http://(ip address of heribertbert):8888 

(ip address of Heribertbert is shown on the small OLED screen at the back of Heribertbert) 

Example: 

- http://192.168.0.150:8888 

## 2. Clone our project into Heribertbert 

choose a suitable location and "git clone https://mygit.th-deg.de/zt17086/jetson-self-driving-toy-car.git"  

## 3. Building the jetbot from "setup.py"

After cloning the directory from gitlab, change directory into the the newly cloned directory and enter the jetbot folder. There run terminal (or change directory to /jetbot from terminal). There run the command 
- "sudo python3 setup.py install"

This will run the necessarry installation of the dependencies that are of use to us. 

## 4. Important folders to us 
notebooks -> Here are where the tutorials along with best trained paths by our group is stored.  

## (OPTIONAL) To begin training on your own PC instead
Link miniconda setup: https://timoast.github.io/blog/installing-pytorch/ 
Link to pytroch setup: https://pytorch.org/get-started/locally/ 
1. First Anaconda or miniconda must be installed. 
2. Second install pytorch
3. Download dataset from Heribertbert and unpack on main PC
4. Start conda environment and start jupyter notebooks.
5. Run "train_model" in notebooks.