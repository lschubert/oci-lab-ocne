# oci-lab-ocne
Automation to set up OCNE in Oracle provided free lab environment (https://luna.oracle.com/lab/d18fe294-efb5-4498-9e7b-d5cc724d8619/steps)

At the time this code was created the lab timeslot is limited to 1 hour, which lead me to automate these tasks.

# Pre-Requisites on the local execution machine:
- git client, ansible installed
    - verify with ```git version```and ```ansible --version```


# Instructions to setup

1. Launch Lab

    1.2. In Lab Environment click on "Luna Lab" ... wait until Resources are provisioned. Click "Resources" Tab to gather IP addresses for ocne-operator, ocne-control and ocne-worker

2. Checkout this git repo 

    2.1 either within Lab Environment (Case: Lab Env) - this is RECOMMENDED

    2.1.1 Open Visual Studio Code. Select Topmost left Icon ("Explorer") and press "Clone Repository" button.
    Provide github URL: https://github.com/lschubert/oci-lab-ocne.git
    Select "Open Folder" and choose the local path of cloned repo

    2.2 or, on a local executor machine (Case: Local executor)

3.  In local git repo ...

    3.1. Modify ```vars/main.yml``` file to map IP adresses from step 1.2 to corresponding nodes.

4. In case of "Local executor": In Lab Environement ...

    4.1. Open Visual Studio Code, Select "Terminal > New Terminal"
    
        Hint: Minimize Browser window with Luna Lab

    4.2. In Terminal Window ```cat ~/.ssh/id_rsa``` and copy content - jump to step 4.1 

    4.3. In Terminal Window ```cat ~/.ssh/id_rsa.pub``` and copy content

5. In case of "Local executor": On execution machine

    5.1. create file ```~/.ssh/ocne_lab_id_rsa``` and copy contents from step 3.2 above.

    5.2. change file permission ```chmod 600 ~/.ssh/ocne_lab_id_rsa``` - jump to step 3.3

    5.3. create file ```~/.ssh/ocne_lab_id_rsa.pub```and copy contents from step 3.3 above.

    5.4. Make sure "oci_executor" variable in ```vars/main.yml``` is set to false

    5.5. in oci-lab-ocne folder execute ```./setup.sh``` 


6. In case of "Lab Env". 

    6.1. Open file ```vars/main.yml``` in Visual Studio Code and modify the values for ```ocne_control_ip```, ```ocne_operator_ip``` and ```ocne_worker_ip``` to match the corresponsing IPs from step 1

    6.2. Make sure "oci_executor" variable in ```vars/main.yml``` is set to true 

    6.3. In Visual Studio Code in Lab Env select Terminal > New Terminal

    6.4. in oci-lab-ocne folder execute ```./setup.sh```

# Usage Notes

The following three VMs are available in this Lab Environment

* ocne-operator: Linux VM with CLI Tools to access (OCNE) Kubernetes Cluster and the Platform API Server 
* ocne-control: (OCNE) Kubernetes Master Node running the Platform Agent
* ocne-worker: (OCNE) Kubernetes Worker Node running Platform Agent

From Visual Studio Code Terminal connect with
```ssh oracle@ocne-operator``` to execute typical command line operations like 

```olcnectl environment report --config-file myenvironment.yaml```

```olcnectl module instances --config-file myenvironment.yaml```

or 
```ssh oracle@ocne-control``` to execute typical command line operations like

```kubectl get nodes``` 

