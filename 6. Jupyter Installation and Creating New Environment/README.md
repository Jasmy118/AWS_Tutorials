# Jupyter Installation and creating New Environment in an EC2 instance(Ubuntu)
## 1.	Create Ubuntu 18 instance.
## 2.	Connect to Ubuntu instance:
- $ ssh -i "JUbuntu_KeyPair.pem" ubuntu@ec2-34-230-57-225.compute-1.amazonaws.com
## 3.	Check if Python/Python3 installed:
- $ python
- $ python3
- $ python3 -V
## 4.	Create python script locally and move to the EC2 created:
- $ scp -i JUbuntu_KeyPair.pem scriptForUbuntu.py ubuntu@ec2-34-230-57-225.compute-1.amazonaws.com:scriptForUbuntu.py
  - ($ scp -i KeyPairName file_to_transfer EC2_Machine : filename_to_show_in_EC2) --> pem file and file to be transferred should be in current working directory.
## 5.	Run the python script in the EC2 created:
- $ python3 scriptForUbuntu.py
## 6.	Check if pip/pip3 installed:
- $ pip3
- $ pip3 -V

If not installed, to install pip3, first we need to do the update.
- $ sudo apt-get update - y   //update command for ubuntu

Install pip:
- $ sudo apt-get install python3-pip

Check pip3 version:
- $ pip3 -V
## 7.	Install Jupyter
- $ sudo pip3 install jupyter

Open jupyter notebook:
- $ jupyter notebook
  - http://127.0.0.1:8888/?token=054c3129833892d71a876aaac59f876b0581380c0f15e05d
  - change 127.0.0.1/local host to IPv4 Public IP of the instance.
  - http://34.230.57.225:8888/?token=054c3129833892d71a876aaac59f876b0581380c0f15e05d

Open the link in browser. Cannot be reached because port is not opened.

Edit Inbound Rules of the Ubuntu instance.
  - Add Rule
    - Type = Custom TCP Rule
    - Port Range = 8888
    - Source = Anywhere, 0.0.0.0/0

Access the link again. If still not accessible:
- CTRL+C to shut down the jupyter notebook server.
- $ jupyter notebook --ip=0.0.0.0 --> associates with all possible IPs

Open jupyter notebook with the new link obtained (after changing IP to the IP of the instance)
## 8.	Select new terminal from the jupyter browser and run python script there.
(Tip: type beginning of file name + tab --> gives full file name)
- $ pwd --> present working directory
- $ ls --> list all files/folders in the pwd
- $ python3 scriptForUbuntu.py

Shut down the terminal and the jupyter will be unavailable. (CTRL+C)
## 9.	NOHUP : Jupyter to work even if we shut down the terminal. Connect to EC2 and follow the below commands:
- $ nohup jupyter notebook --ip=0.0.0.0&
- $ ls --> contains nohup.out

Display the content of a file:
- $ cat nohup.out --> Displays the link to the jupyter notebook

Now JupyterNotebook will work even after closing the prompt
## 10.	Creating a new environment in Jupyter with pew.
Check python3 installation:
- $ python3
- $ pip3 install pew

pew works with python 2.7. So install python 2.7

- $ sudo apt-get update
- $ sudo wget https://www.python.org/ftp/python/2.7.16/Python-2.7.16.tgz --> Download python
- $ sudo tar xzf Python-2.7.16.tgz --> extract the downloaded pack
- $ cd Python-2.7.16
- $ sudo ./configure --enable-optimizations
- $ sudo make altinstall
- $ python2.7 -V
- $ pew

Creating new environment:
- $ pew new jTestEnv
- $ exit --> exits the environment
- $ pew ls --> lists all environments
- $ pew workon jTestEnv
- $ pip3 freeze --> lists all installations
- $ pip3 install pandas
- $ pip3 freeze > jTestEnvFreeze.txt --> lists all installations into a text file
- $ cat jTestEnvFreeze.txt --> display contents

Display the environment name in jupyter home page (Now inside jTestEnv):
- $ pip3 install ipykernel
- $ python3 -m ipykernel install - -user - -name=JasTestEnvironment
  - Refresh the home page and new environment name wil be displayed.

Select JasTestEnvironment and in the new notebook:
- import pandas --> will not give error as pandas is installed in this environment

## 11.	Creating a new environment in jupyter with pew and copying all installations from jTestEnv (environment created in step 10).
Nested environment: An environment inside another environment.
- $ jTestEnv…$ pew new jTestEnvDuplicate
- $ exit --> exits jTestEnvDuplicate and will be in jTestEnv
- $ pew ls
- $ pew rm jTestEnvDuplicate --> removes jTestEnvDuplicate
- $ pew ls

Creating an environment outside jTestEnv:
- $ exit --> exits jTestEnv
- $ pew new jTestEnvDuplicate
- $ ls --> lists files of the directory irrespective of the environments

Display the environment name in jupyter home page (Now inside jTestEnvDuplicate):
- $ pip3 install ipykernel
- $ python3 -m ipykernel install - -user - -name=JasTestEnvironmentDuplicate
  - Refresh the home page and open a new notebook in 'JasTestEnvironmentDuplicate' and import pandas:
- import pandas --> gives error because pandas is not installed in this environment.

Copying installations from 'jTestEnv' (Now in jTestEnvDuplicate):
- $ ls
- $ pip3 install -r jTestEnvFreeze.txt --> computes all the installations in this txt file.

Now import pandas in the previously created notebook and it works.

## 12.	Creating new environment in Jupyter with conda.
Check python3 installation:
- $ python3 -V

Latest conda link:
https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
- $ mkdir tmp --> creates a tmp folder
- $ cd /tmp
- $ curl -O https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh --> downloads anaconda
- $ ls
- $ bash Anaconda3-2019.10-Linux-x86_64.sh (Tip : type bash A+tab -- completes the file name)

After installation:
- $ conda

if it shows, conda command not found open a new terminal.
- $ conda
- $ conda create –name JCondaEnv3 python=3 --> creates new environment
- $ conda activate JCondaEnv3--> To activate the new environment

With conda we can create environment in any version of python.

Displaying the environment created with conda in Jupyter home page:
- $ pip3 install ipykernel
- $ ipython kernel install - -user - -name=JasCondaEnv

Refresh Jupyter home page and new environment name appears. Open a new notebook in this environment and import pandas --> gives error as it is not installed. So install pandas in JCondaEnv3:
- $ conda install pandas

Now import pandas in the note book and it works.

Note: $ conda update  -n base -c defaults conda --> to update conda version
