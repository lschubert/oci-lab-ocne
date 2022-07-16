# oci-lab-ocne
Automation to set up OCNE in Oracle provided free lab environment (https://luna.oracle.com/lab/d18fe294-efb5-4498-9e7b-d5cc724d8619/steps)

At the time this code was created the lab timeslot is limited to 1 hour, which lead me to automate these tasks.

# Pre-Requisites on the execution machine:
- git client, ansible installed
    - verify with ```git version```and ```ansible --version```


# Instructions to setup

1. Launch Lab

    1.2. In Lab Environment click on "Luna Lab" ... wait until Resources are provisioned. Click "Resources" Tab to gather IP addresses for ocne-operator, ocne-control and ocne-worker

2.  In git repo ...

    2.1. Modify ```hosts``` file to map IP adresses from step 1.2 to corresponding nodes.

3. In Lab Environement ...

    3.1. Open Visual Studio Code, Select "Terminal > New Terminal"
    
        Hint: Minimize Browser window with Luna Lab

    3.2. In Terminal Window ```cat ~/.ssh/id_rsa``` and copy content - jump to step 4.1 

    3.3. In Terminal Window ```cat ~/.ssh/id_rsa.pub``` and copy content

4. On execution machine

    4.1. create file ```~/.ssh/ocne_lab_id_rsa``` and copy contents from step 3.2 above.

    4.2. change file permission ```chmod 600 ~/.ssh/ocne_lab_id_rsa``` - jump to step 3.3

    4.3. create file ```~/.ssh/ocne_lab_id_rsa.pub```and copy contents from step 3.3 above.

    4.3. execute ```export ANSIBLE_HOST_KEY_CHECKING=False```

    2.2. in oci-lab-ocne folder execute ```ansible-playbook -i ./hosts --private-key ~/.ssh/ocne_lab_id_rsa setup.yml```