# oci-lab-ocne
Automation to set up OCNE in Oracle provided free lab environment (https://luna.oracle.com/lab/d18fe294-efb5-4498-9e7b-d5cc724d8619/steps)

At the time this code was created the lab timeslot is limited to 1 hour, which lead me to automate these tasks.

# Pre-Requisites on the execution machine:
- git client, ansible installed
    - verify with ```git version```and ```ansible --version```


# Instructions to setup

1. Launch Lab

    1.2. In Lab Environment click on "Luna Lab" ... wait until Resources are provisioned. Click "Resources" Tab to gather IP addresses for ocne-operator, ocne-control and ocne-worker

2. Checkout git repo from https://github.com/lschubert/oci-lab-ocne.git

    2.1 either within Lab Environment (Case: Lab Env), or

    2.1.1 Open Visual Studio Code. Select Topmost left Icon ("Explorer") and press "Clone Repository" button.
    Provide github URL: https://github.com/lschubert/oci-lab-ocne.git
    Select "Open Folder" and choose the local path of cloned repo

    2.2 on a local executor machine (Case: Local executor)

3.  In local git repo ...

    3.1. Modify ```hosts``` file to map IP adresses from step 1.2 to corresponding nodes.

4. In case of "Local executor": In Lab Environement ...

    4.1. Open Visual Studio Code, Select "Terminal > New Terminal"
    
        Hint: Minimize Browser window with Luna Lab

    4.2. In Terminal Window ```cat ~/.ssh/id_rsa``` and copy content - jump to step 4.1 

    4.3. In Terminal Window ```cat ~/.ssh/id_rsa.pub``` and copy content

5. In case of "Local executor": On execution machine

    5.1. create file ```~/.ssh/ocne_lab_id_rsa``` and copy contents from step 3.2 above.

    5.2. change file permission ```chmod 600 ~/.ssh/ocne_lab_id_rsa``` - jump to step 3.3

    5.3. create file ```~/.ssh/ocne_lab_id_rsa.pub```and copy contents from step 3.3 above.

    5.3. execute ```export ANSIBLE_HOST_KEY_CHECKING=False```

    5.4. Make sure "oci_executor" variable in setup.yml is set to false

    5.5. in oci-lab-ocne folder execute ```ansible-playbook -i ./hosts --private-key ~/.ssh/ocne_lab_id_rsa setup.yml```

6. In case of "Lab Env". 

    6.1. In Visual Studio Code in Lab Env select Terminal > New Terminal

    6.2. In Terminal execute ```export ANSIBLE_HOST_KEY_CHECKING=False```

    6.3. Make sure "oci_executor" variable in setup.yml is set to true

    6.4. In oci-lab-ocne folder execute ```ansible-playbook -i ./hosts setup.yml```


# Develop ToDo's
