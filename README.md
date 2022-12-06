# Cloud DevOps Engineer Capstone Project

This project represents the successful completion of the last final Capstone project and the Cloud DevOps Engineer Nanodegree at Udacity.
- Github: https://github.com/nvthinh1997/project5
- Docker: https://hub.docker.com/repository/docker/thinhnv1997/capstone-project
- CircleCI: [![CircleCI](https://circleci.com/gh/circleci/circleci-docs.svg?style=svg)](https://app.circleci.com/pipelines/github/nvthinh1997/project5)
## What did I learn?

In this project, I applied the skills and knowledge I developed throughout the Cloud DevOps Nanodegree program. These include:
- Using Circle CI to implement Continuous Integration and Continuous Deployment
- Building pipelines
- Working with Ansible and CloudFormation to deploy clusters
- Building Kubernetes clusters
- Building Docker containers in pipelines
- Working in AWS

## Application

The Application is based on a python3 script using <a target="_blank" href="https://flask.palletsprojects.com">flask</a> to render a simple webpage in the user's browser (and base on project 4).
A requirements.txt is used to ensure that all needed dependencies come along with the Application.

## Kubernetes Cluster

I used AWS CloudFormation to deploy the Kubernetes Cluster.
The CloudFormation Deployment can be broken down into four Parts:
- **Networking**, to ensure new nodes can communicate with the Cluster
- **Elastic Kubernetes Service (EKS)** is used to create a Kubernetes Cluster
- **NodeGroup**, each NodeGroup has a set of rules to define how instances are operated and created for the EKS-Cluster
- **Controller** is needed to configure and manage the Cluster and its deployments and services. I created two management hosts for extra redundancy if one of them fails.

#### List of deployed Stacks:
![CloudFormation](./ScreenShots/cloudFormation.png)

#### List of deployed Instances:
![Show Instances](./ScreenShots/instances.png)

## CircleCi - CI/CD Pipelines

I used CircleCi to create a CI/CD Pipeline to test and deploy changes manually before they get deployed automatically to the Cluster using Ansible.

#### From Zero to Hero demonstration:

![CircleCi Pipeline](./ScreenShots/circleci.png)

## Linting using Pylint and Hadolint

Linting is used to check if the Application and Dockerfile is syntactically correct.
This process makes sure that the code quality is always as good as possible.

#### This is the output when the step fails:

![Linting step fail](./ScreenShots/failedLint.png)


#### This is the output when the step passes:

![Linting step fail](./ScreenShots//passLint.png)

## Upload Docker Image After Successful Build

![Upload Docker](./ScreenShots/dockerImage.png)

## Access the Application

After the EKS-Cluster has been successfully configured using Ansible within the CI/CD Pipeline, I checked the deployment and service log on pipeline as follows:

```
    TASK [Get deployment] **********************************************************
    task path: /home/circleci/project/ansible/deploy-app.yml:20
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' 54.86.162.142 '/bin/sh -c '"'"'echo ~ubuntu && sleep 0'"'"''
    <54.86.162.142> (0, b'/home/ubuntu\n', b'')
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' 54.86.162.142 '/bin/sh -c '"'"'( umask 77 && mkdir -p "` echo /home/ubuntu/.ansible/tmp `"&& mkdir "` echo /home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710 `" && echo ansible-tmp-1670294505.8600507-1488-189876410604710="` echo /home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710 `" ) && sleep 0'"'"''
    <54.86.162.142> (0, b'ansible-tmp-1670294505.8600507-1488-189876410604710=/home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710\n', b'')
    Using module file /usr/lib/python3/dist-packages/ansible/modules/command.py
    <54.86.162.142> PUT /home/circleci/.ansible/tmp/ansible-local-1459zfjpsftq/tmpyp1d23mw TO /home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710/AnsiballZ_command.py
    <54.86.162.142> SSH: EXEC sftp -b - -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' '[54.86.162.142]'
    <54.86.162.142> (0, b'sftp> put /home/circleci/.ansible/tmp/ansible-local-1459zfjpsftq/tmpyp1d23mw /home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710/AnsiballZ_command.py\n', b'')
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' 54.86.162.142 '/bin/sh -c '"'"'chmod u+x /home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710/ /home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710/AnsiballZ_command.py && sleep 0'"'"''
    <54.86.162.142> (0, b'', b'')
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' -tt 54.86.162.142 '/bin/sh -c '"'"'sudo -H -S -n  -u root /bin/sh -c '"'"'"'"'"'"'"'"'echo BECOME-SUCCESS-qteetvhvhtsblaggwwuvzvtkaajwhtkx ; /usr/bin/python3 /home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710/AnsiballZ_command.py'"'"'"'"'"'"'"'"' && sleep 0'"'"''
    Escalation succeeded
    <54.86.162.142> (0, b'\r\n{"changed": true, "stdout": "NAME                          READY   UP-TO-DATE   AVAILABLE   AGE\\n****************-deployment   2/2     2            2           12h", "stderr": "", "rc": 0, "cmd": "./bin/kubectl get deployments", "start": "2022-12-06 02:41:46.076481", "end": "2022-12-06 02:41:46.997245", "delta": "0:00:00.920764", "msg": "", "invocation": {"module_args": {"chdir": "/root", "_raw_params": "./bin/kubectl get deployments", "_uses_shell": true, "warn": false, "stdin_add_newline": true, "strip_empty_ends": true, "argv": null, "executable": null, "creates": null, "removes": null, "stdin": null}}}\r\n', b'Shared connection to 54.86.162.142 closed.\r\n')
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' 54.86.162.142 '/bin/sh -c '"'"'rm -f -r /home/ubuntu/.ansible/tmp/ansible-tmp-1670294505.8600507-1488-189876410604710/ > /dev/null 2>&1 && sleep 0'"'"''
    <54.86.162.142> (0, b'', b'')
    changed: [54.86.162.142] => {
        "changed": true,
        "cmd": "./bin/kubectl get deployments",
        "delta": "0:00:00.920764",
        "end": "2022-12-06 02:41:46.997245",
        "invocation": {
            "module_args": {
                "_raw_params": "./bin/kubectl get deployments",
                "_uses_shell": true,
                "argv": null,
                "chdir": "/root",
                "creates": null,
                "executable": null,
                "removes": null,
                "stdin": null,
                "stdin_add_newline": true,
                "strip_empty_ends": true,
                "warn": false
            }
        },
        "msg": "",
        "rc": 0,
        "start": "2022-12-06 02:41:46.076481",
        "stderr": "",
        "stderr_lines": [],
        "stdout": "NAME                          READY   UP-TO-DATE   AVAILABLE   AGE\n****************-deployment   2/2     2            2           12h",
        "stdout_lines": [
            "NAME                          READY   UP-TO-DATE   AVAILABLE   AGE",
            "****************-deployment   2/2     2            2           12h"
        ]
    }


    TASK [Get service] *************************************************************
    task path: /home/circleci/project/ansible/deploy-app.yml:25
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' 54.86.162.142 '/bin/sh -c '"'"'echo ~ubuntu && sleep 0'"'"''
    <54.86.162.142> (0, b'/home/ubuntu\n', b'')
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' 54.86.162.142 '/bin/sh -c '"'"'( umask 77 && mkdir -p "` echo /home/ubuntu/.ansible/tmp `"&& mkdir "` echo /home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942 `" && echo ansible-tmp-1670294507.072761-1497-165618464556942="` echo /home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942 `" ) && sleep 0'"'"''
    <54.86.162.142> (0, b'ansible-tmp-1670294507.072761-1497-165618464556942=/home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942\n', b'')
    Using module file /usr/lib/python3/dist-packages/ansible/modules/command.py
    <54.86.162.142> PUT /home/circleci/.ansible/tmp/ansible-local-1459zfjpsftq/tmpfk415m4k TO /home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942/AnsiballZ_command.py
    <54.86.162.142> SSH: EXEC sftp -b - -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' '[54.86.162.142]'
    <54.86.162.142> (0, b'sftp> put /home/circleci/.ansible/tmp/ansible-local-1459zfjpsftq/tmpfk415m4k /home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942/AnsiballZ_command.py\n', b'')
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' 54.86.162.142 '/bin/sh -c '"'"'chmod u+x /home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942/ /home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942/AnsiballZ_command.py && sleep 0'"'"''
    <54.86.162.142> (0, b'', b'')
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' -tt 54.86.162.142 '/bin/sh -c '"'"'sudo -H -S -n  -u root /bin/sh -c '"'"'"'"'"'"'"'"'echo BECOME-SUCCESS-kyrnmiirraqrzkhfkerzibgxuctkmzvy ; /usr/bin/python3 /home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942/AnsiballZ_command.py'"'"'"'"'"'"'"'"' && sleep 0'"'"''
    Escalation succeeded
    <54.86.162.142> (0, b'\r\n{"changed": true, "stdout": "NAME                       TYPE           CLUSTER-IP       EXTERNAL-IP                                                              PORT(S)        AGE\\n****************-service   LoadBalancer   10.100.202.133   a149a1b88ba1b430298d8ad4e3e1a987-482593122.*********.elb.amazonaws.com   80:31702/TCP   12h\\nkubernetes                 ClusterIP      10.100.0.1       <none>                                                                   443/TCP        13h", "stderr": "", "rc": 0, "cmd": "./bin/kubectl get services", "start": "2022-12-06 02:41:47.289834", "end": "2022-12-06 02:41:48.196389", "delta": "0:00:00.906555", "msg": "", "invocation": {"module_args": {"chdir": "/root", "_raw_params": "./bin/kubectl get services", "_uses_shell": true, "warn": false, "stdin_add_newline": true, "strip_empty_ends": true, "argv": null, "executable": null, "creates": null, "removes": null, "stdin": null}}}\r\n', b'Shared connection to 54.86.162.142 closed.\r\n')
    <54.86.162.142> ESTABLISH SSH CONNECTION FOR USER: ubuntu
    <54.86.162.142> SSH: EXEC ssh -C -o ControlMaster=auto -o ControlPersist=60s -o StrictHostKeyChecking=no -o KbdInteractiveAuthentication=no -o PreferredAuthentications=gssapi-with-mic,gssapi-keyex,hostbased,publickey -o PasswordAuthentication=no -o 'User="ubuntu"' -o ConnectTimeout=10 -o 'ControlPath="/home/circleci/.ansible/cp/0b1884c00a"' 54.86.162.142 '/bin/sh -c '"'"'rm -f -r /home/ubuntu/.ansible/tmp/ansible-tmp-1670294507.072761-1497-165618464556942/ > /dev/null 2>&1 && sleep 0'"'"''
    <54.86.162.142> (0, b'', b'')
    changed: [54.86.162.142] => {
        "changed": true,
        "cmd": "./bin/kubectl get services",
        "delta": "0:00:00.906555",
        "end": "2022-12-06 02:41:48.196389",
        "invocation": {
            "module_args": {
                "_raw_params": "./bin/kubectl get services",
                "_uses_shell": true,
                "argv": null,
                "chdir": "/root",
                "creates": null,
                "executable": null,
                "removes": null,
                "stdin": null,
                "stdin_add_newline": true,
                "strip_empty_ends": true,
                "warn": false
            }
        },
        "msg": "",
        "rc": 0,
        "start": "2022-12-06 02:41:47.289834",
        "stderr": "",
        "stderr_lines": [],
        "stdout": "NAME                       TYPE           CLUSTER-IP       EXTERNAL-IP                                                              PORT(S)        AGE\n****************-service   LoadBalancer   10.100.202.133   a149a1b88ba1b430298d8ad4e3e1a987-482593122.*********.elb.amazonaws.com   80:31702/TCP   12h\nkubernetes                 ClusterIP      10.100.0.1       <none>                                                                   443/TCP        13h",
        "stdout_lines": [
            "NAME                       TYPE           CLUSTER-IP       EXTERNAL-IP                                                              PORT(S)        AGE",
            "****************-service   LoadBalancer   10.100.202.133   a149a1b88ba1b430298d8ad4e3e1a987-482593122.*********.elb.amazonaws.com   80:31702/TCP   12h",
            "kubernetes                 ClusterIP      10.100.0.1       <none>                                                                   443/TCP        13h"
        ]
    }  
```

Public LB DNS: http://a149a1b88ba1b430298d8ad4e3e1a987-482593122.us-east-1.elb.amazonaws.com/

![Access LB DNS](./ScreenShots/dns.png)