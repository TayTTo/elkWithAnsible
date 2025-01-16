# Learn Ansible
**Learning resource:**
- Books:
    - Ansible for Devops(https://www.ansiblefordevops.com/)
    - Ansible Up and Running

- Document: Officical doc from red hat(https://docs.ansible.com/ansible/latest/index.html)
## Step 1:
Deploy virtual machine with vagrant and libvirt
Write a file named Vagrantfile and run `vagrant up`
> Result:
```
Bringing machine 'vagrant1' up with 'libvirt' provider...
==> vagrant1: Creating shared folders metadata...
==> vagrant1: Starting domain.
==> vagrant1: Domain launching with graphics connection settings...
==> vagrant1:  -- Graphics Port:      5900
==> vagrant1:  -- Graphics IP:        127.0.0.1
==> vagrant1:  -- Graphics Password:  Not defined
==> vagrant1:  -- Graphics Websocket: 5700
==> vagrant1: Waiting for domain to get an IP address...
==> vagrant1: Waiting for machine to boot. This may take a few minutes...
    vagrant1: SSH address: 192.168.121.183:22
    vagrant1: SSH username: vagrant
    vagrant1: SSH auth method: private key
==> vagrant1: Machine booted and ready!
==> vagrant1: Forwarding ports...
==> vagrant1: 80 (guest) => 8080 (host) (adapter eth0)
==> vagrant1: 443 (guest) => 8443 (host) (adapter eth0)
==> vagrant1: Machine already provisioned. Run `vagrant provision` or use the `--provision`
==> vagrant1: flag to force provisioning. Provisioners marked to run always will still run.
```

## Step 2:
Check whether ansible can connect to vm or not.
```
ansible all -i inventory -m ping
```
> Result:
```
[WARNING]: Found both group and host with same name: vagrant
vagrant | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}

```

## Step 3: Check whether install elasticsearch with ansible successful or not.

> Resutl:
![](./images/ansible.png)

## Step 4: Config elastic search.
> Result:
![](./images/pic2.png)

## Step 5: Do the same with kibana and check the result
- Run the command `ansible-playbook elk.yml`
> Result: 
```
 ___________________
< PLAY [Deploy elk] >
 -------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

 ________________________
< TASK [Gathering Facts] >
 ------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 _______________________________
< TASK [Import elastic PGP key] >
 -------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 _________________________
< TASK [Install from apt] >
 -------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 ________________________________________
< TASK [Save the repository definition.] >
 ----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [vagrant]
 _________________________________________
< TASK [Install elasticsearch and kibana] >
 -----------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 ______________________
< TASK [reload daemon] >
 ----------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [vagrant]
 _____________________________
< TASK [Enable elasticsearch] >
 -----------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 __________________________________________
< TASK [Set the elasticsearch config file] >
 ------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 ____________________________
< TASK [Start Elasticsearch] >
 ----------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 __________________________________
< TASK [Generate enrollment token] >
 ----------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [vagrant]
 ______________
< TASK [debug] >
 --------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant] => {
    "msg": "The token enrollment is eyJ2ZXIiOiI4LjE0LjAiLCJhZHIiOlsiMTkyLjE2OC4xMjEuODI6OTIwMCJdLCJmZ3IiOiI2N2M5MTFiMDFjZDA4ZGIyMGYzNmU2M2QxODYzZWMyYTdmNDQwMzk1N2U0MDA1ZTEwZGM2MDhiZjc4MTU0ZDQ3Iiwia2V5IjoiRjNONGI1UUJscU9YeEI0VFV2bVA6bjZpOTk0V2JRaGV1eF8wTUxDSDlzdyJ9"
}
 ______________________
< TASK [reload daemon] >
 ----------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [vagrant]
 ______________________
< TASK [Enable kibana] >
 ----------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 __________________________________________
< TASK [Set the elasticsearch config file] >
 ------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [vagrant]
 _____________________
< TASK [start kibana] >
 ---------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant]
 ___________________________________________
< TASK [Get user and password from elastic] >
 -------------------------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [vagrant]
 ______________
< TASK [debug] >
 --------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant] => {
    "msg": "The password for elastic is This tool will reset the password of the [elastic] user to an autogenerated value.\nThe password will be printed in the console.\n\n\nPassword for the [elastic] user successfully reset.\nNew value: 2ZhQiv_*g4n_SYaGs1Zm"
}
 _____________________________
< TASK [Get code from kibana] >
 -----------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

changed: [vagrant]
 ______________
< TASK [debug] >
 --------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

ok: [vagrant] => {
    "msg": "● kibana.service - Kibana\n     Loaded: loaded (/lib/systemd/system/kibana.service; enabled; vendor preset: enabled)\n     Active: active (running) since Thu 2025-01-16 13:17:45 UTC; 58min ago\n       Docs: https://www.elastic.co\n   Main PID: 575 (node)\n      Tasks: 11 (limit: 2256)\n     Memory: 127.2M\n     CGroup: /system.slice/kibana.service\n             └─575 /usr/share/kibana/bin/../node/glibc-217/bin/node /usr/share/kibana/bin/../src/cli/dist\n\nJan 16 13:17:46 ubuntu2004.localdomain kibana[575]: Native global console methods have been overridden in production environment.\nJan 16 13:17:48 ubuntu2004.localdomain kibana[575]: [2025-01-16T13:17:48.163+00:00][INFO ][root] Kibana is starting\nJan 16 13:17:48 ubuntu2004.localdomain kibana[575]: [2025-01-16T13:17:48.208+00:00][INFO ][node] Kibana process configured with roles: [background_tasks, ui]\nJan 16 13:17:55 ubuntu2004.localdomain kibana[575]: [2025-01-16T13:17:54.963+00:00][INFO ][plugins-service] The following plugins are disabled: \"cloudChat,cloudExperiments,cloudFullStory,dataUsage,investigateApp,investigate,profilingDataAccess,profiling,searchHomepage,searchIndices,securitySolutionServerless,serverless,serverlessObservability,serverlessSearch\".\nJan 16 13:17:55 ubuntu2004.localdomain kibana[575]: [2025-01-16T13:17:55.036+00:00][INFO ][http.server.Preboot] http server running at http://localhost:5601\nJan 16 13:17:55 ubuntu2004.localdomain kibana[575]: [2025-01-16T13:17:55.166+00:00][INFO ][plugins-system.preboot] Setting up [1] plugins: [interactiveSetup]\nJan 16 13:17:55 ubuntu2004.localdomain kibana[575]: [2025-01-16T13:17:55.181+00:00][INFO ][preboot] \"interactiveSetup\" plugin is holding setup: Validating Elasticsearch connection configuration…\nJan 16 13:17:55 ubuntu2004.localdomain kibana[575]: [2025-01-16T13:17:55.207+00:00][INFO ][root] Holding setup until preboot stage is completed.\nJan 16 13:18:02 ubuntu2004.localdomain kibana[575]: i Kibana has not been configured.\nJan 16 13:18:02 ubuntu2004.localdomain kibana[575]: Go to http://localhost:5601/?code=840497 to get started."
}
```

As result, central components consists of elasticsearch and kibana should be depoloy successfully
