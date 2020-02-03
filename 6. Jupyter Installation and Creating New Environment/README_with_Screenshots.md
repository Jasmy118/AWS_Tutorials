# Jupyter Installation and creating New Environment in an EC2 instance(Ubuntu)
## 1.	Create Ubuntu 18 instance.
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/1.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/2.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/3.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/4.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/5.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/6.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/7.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/8.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9.jpg)
## 2.	Connect to Ubuntu instance:
- $ ssh -i "JUbuntu_KeyPair.pem" ubuntu@ec2-34-230-57-225.compute-1.amazonaws.com
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9a.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9b.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9c.jpg)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9d.jpg)
## 3.	Check if Python/Python3 installed:
- $ python
- $ python3
- $ python3 -V
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9e.png)
## 4.	Create python script locally and move to the EC2 created:
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9f.png)
- $ scp -i JUbuntu_KeyPair.pem scriptForUbuntu.py ubuntu@ec2-34-230-57-225.compute-1.amazonaws.com:scriptForUbuntu.py
  - ($ scp -i KeyPairName file_to_transfer EC2_Machine : filename_to_show_in_EC2) --> pem file and file to be transferred should be in current working directory.
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9g.png)
## 5.	Run the python script in the EC2 created:
- $ python3 scriptForUbuntu.py
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9h.png)
## 6.	Check if pip/pip3 installed:
- $ pip3
- $ pip3 -V
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9i.png)

If not installed, to install pip3, first we need to do the update.
- $ sudo apt-get update - y   //update command for ubuntu
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9j.png)

Install pip:
- $ sudo apt-get install python3-pip
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9k.png)

Check pip3 version:
- $ pip3 -V
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9l.png)
## 7.	Install Jupyter
- $ sudo pip3 install jupyter
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9m.png)

Open jupyter notebook:
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9n.png)
- $ jupyter notebook
  - http://127.0.0.1:8888/?token=054c3129833892d71a876aaac59f876b0581380c0f15e05d
  - change 127.0.0.1/local host to IPv4 Public IP of the instance.
  - http://34.230.57.225:8888/?token=054c3129833892d71a876aaac59f876b0581380c0f15e05d
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9q.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9r.png)

Open the link in browser. Cannot be reached because port is not opened.
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9o.png)

Edit Inbound Rules of the Ubuntu instance.
  - Add Rule
    - Type = Custom TCP Rule
    - Port Range = 8888
    - Source = Anywhere, 0.0.0.0/0
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9p.png)

Access the link again. If still not accessible:
- CTRL+C to shut down the jupyter notebook server.
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9s.png)
- $ jupyter notebook --ip=0.0.0.0 --> associates with all possible IPs
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9t.png)

Open jupyter notebook with the new link obtained (after changing IP to the IP of the instance)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9u.png)
## 8.	Select new terminal from the jupyter browser and run python script there.
(Tip: type beginning of file name + tab --> gives full file name)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9v.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9w.png)
- $ pwd --> present working directory
- $ ls --> list all files/folders in the pwd
- $ python3 scriptForUbuntu.py
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9x.png)

Shut down the terminal and the jupyter will be unavailable. (CTRL+C)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9y.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9z.png)
## 9.	NOHUP : Jupyter to work even if we shut down the terminal. Connect to EC2 and follow the below commands:
- $ nohup jupyter notebook --ip=0.0.0.0&
- $ ls --> contains nohup.out
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9za.png)

Display the content of a file:
- $ cat nohup.out --> Displays the link to the jupyter notebook
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zb.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zc.png)

Now JupyterNotebook will work even after closing the prompt
## 10.	Creating a new environment in Jupyter with pew.
Check python3 installation:
- $ python3
- $ pip3 install pew
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zd.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9ze.png)

pew works with python 2.7. So install python 2.7

- $ sudo apt-get update
- $ sudo wget https://www.python.org/ftp/python/2.7.16/Python-2.7.16.tgz --> Download python
- $ sudo tar xzf Python-2.7.16.tgz --> extract the downloaded pack
- $ cd Python-2.7.16
- $ sudo ./configure --enable-optimizations
- $ sudo make altinstall
- $ python2.7 -V
- $ pew
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zf.png)

Creating new environment:
- $ pew new jTestEnv
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zg.png)
- $ exit --> exits the environment
- $ pew ls --> lists all environments
- $ pew workon jTestEnv
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zh.png)
- $ pip3 freeze --> lists all installations
- $ pip3 install pandas
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zi.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zj.png)
- $ pip3 freeze > jTestEnvFreeze.txt --> lists all installations into a text file
- $ cat jTestEnvFreeze.txt --> display contents
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zk.png)

Display the environment name in jupyter home page (Now inside jTestEnv):
- $ pip3 install ipykernel
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zl.png)
- $ python3 -m ipykernel install - -user - -name=JasTestEnvironment
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zm.png)
  - Refresh the home page and new environment name wil be displayed.
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zn.png)

Select JasTestEnvironment and in the new notebook:
- import pandas --> will not give error as pandas is installed in this environment
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zo.png)

## 11.	Creating a new environment in jupyter with pew and copying all installations from jTestEnv (environment created in step 10).
Nested environment: An environment inside another environment.
- $ jTestEnv…$ pew new jTestEnvDuplicate
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zp.png)
- $ exit --> exits jTestEnvDuplicate and will be in jTestEnv
- $ pew ls
- $ pew rm jTestEnvDuplicate --> removes jTestEnvDuplicate
- $ pew ls
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zq.png)

Creating an environment outside jTestEnv:
- $ exit --> exits jTestEnv
- $ pew new jTestEnvDuplicate
- $ ls --> lists files of the directory irrespective of the environments
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zr.png)

Display the environment name in jupyter home page (Now inside jTestEnvDuplicate):
- $ pip3 install ipykernel
- $ python3 -m ipykernel install - -user - -name=JasTestEnvironmentDuplicate
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zs.png)
  - Refresh the home page and open a new notebook in 'JasTestEnvironmentDuplicate' and import pandas:
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zt.png)
- import pandas --> gives error because pandas is not installed in this environment.
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zu.png)

Copying installations from 'jTestEnv' (Now in jTestEnvDuplicate):
- $ ls
- $ pip3 install -r jTestEnvFreeze.txt --> computes all the installations in this txt file.
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zv.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zw.png)

Now import pandas in the previously created notebook and it works.
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zx.png)

## 12.	Creating new environment in Jupyter with conda.
Check python3 installation:
- $ python3 -V
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zy.png)

Latest conda link:
https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh
- $ mkdir tmp --> creates a tmp folder
- $ cd /tmp
- $ curl -O https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh --> downloads anaconda
- $ ls
- $ bash Anaconda3-2019.10-Linux-x86_64.sh (Tip : type bash A+tab -- completes the file name)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zz.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zza.png)

After installation:
- $ conda
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zzb.png)

if it shows, conda command not found open a new terminal.
- $ conda
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zzc.png)
- $ conda create –name JCondaEnv3 python=3 --> creates new environment
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zzd.png)
- $ conda activate JCondaEnv3--> To activate the new environment
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zze.png)

With conda we can create environment in any version of python.

Displaying the environment created with conda in Jupyter home page:
- $ pip3 install ipykernel
- $ ipython kernel install - -user - -name=JasCondaEnv
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zzf.png)

Refresh Jupyter home page and new environment name appears. Open a new notebook in this environment and import pandas --> gives error as it is not installed. So install pandas in JCondaEnv3:
- $ conda install pandas
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zzg.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zzh.png)
![image.jpg](https://github.com/Jasmy118/AWS_Tutorials/blob/master/6.%20Jupyter%20Installation%20and%20Creating%20New%20Environment/Images/9zzi.png)

Now import pandas in the note book and it works.

Note: $ conda update  -n base -c defaults conda --> to update conda version

