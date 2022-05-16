**101 getting started with Ansible ⚙️**

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.001.jpeg)

**What exactly is Ansible and why do we need it? 💭**

Automation is frequently used in the large-scale deployment of modern IT systems, both on-premises and in the cloud. Consider what would occur if we were unable to maintain settings! Furthermore, if we do it manually, the risk may increase.

Consistency of managed systems is configuration management’s main advantage. You can rest easy knowing that we have a system in place to take care of configuration management.

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.002.jpeg)

The term “Configuration management” is crucial here. If you’re here because you’ve heard about Ansible but don’t know what it is, it’s simply a configuration management tool like Puppet or Chef. To configure all of your servers and environments using code from a single central location without requiring direct access to these environments and servers, you would require a configuration management solution.

**How does it work in broad terms? 👨‍💻**

It used to be difficult to reliably and effectively manage servers. System administrators manually installed software, modified server configurations, and oversaw server functions. Scaling manually was time-consuming and difficult as managed servers increased in size and managed services became more complicated. 

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.003.jpeg)

Then Ansible appeared, which is useful for gathering a set of machines and defining how to configure them and what actions should be conducted. You may control all of these settings and operations from your local system, which serves as the central hub (named controller machine). There is no need for software to be installed on a remote computer before Ansible can connect to it and perform setup because it leverages SSH. It is easy to use, agentless, strong, and versatile. And it utilises YAML as the format.

**And most importantly, Ansible is free! 🆓**

Ansible is an open-source, totally free programme that can be used for business needs. The Red Hat Ansible Automation Platform is also offered in two variants that differ in support and functionality from Open Source Ansible. 

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.004.jpeg)

The cost is determined by the number of nodes. Up to 10 nodes can be handled for free using Ansible Tower.

**Some important Concepts 📑**

- **Ansible server:** Ansible’s installation machine, from which all tasks and playbooks will be executed
- **Module:** A module is essentially a command or group of related commands intended to be performed on the client-side.
- **Task:** A task is a part with only one procedure that needs to be finished.
- **Fact:** Information obtained by the gather-facts method from the global variables on the client system
- **Inventory:** Informational file for the Ansible client servers. further examples as the hosts file
- **Play:** implementing a playbook
- **Handler:** task that is only invoked in the presence of a notifier
- **Notifier:** A task’s section that calls a handler if the output is modified
- **Tag:** A task can be given a name that will subsequently be used to issue just that task or collection of tasks.
- **Role:** a method of arranging jobs and accompanying files to be called later in a playbook

**Deep dive into running your first Ansible playbook 🏃‍♀️**

**Setup ⚙️**

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.005.jpeg)

Below are the installation steps for MacOS

$ brew update
$ brew install ansible

Post installation, for confirmation :

*$ ansible -version*

Now Create an SSH connection to the target servers now.

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.006.jpeg)

Make sure you can successfully ssh to the server and connect using a certificate.

$ ssh -i /root/.ssh/your.key -t root@your\_server\_ip 'sudo mkdir -p /root/.ssh'

$ scp -i /root/.ssh/your.key /root/.ssh/id\_rsa.pub root@your\_server\_ip:/root/.ssh/id\_rsa.pub

$ ssh -i /root/.ssh/your.key -t root@your\_server\_ip 'cat /root/.ssh/id\_rsa.pub | sudo tee -a /root/.ssh/authorized\_keys ;echo "PermitRootLogin yes" | sudo tee -a /etc/ssh/sshd\_config'
ssh-keyscan yourserver | sudo tee -a /root/.ssh/known\_hosts

**Further configuration 🎰**

Customizing the Ansible configuration file is the next step. It controls how it acts. 

File location: /etc/ansible/ansible.cfg

This is the location of the default configuration file. You might need to modify a few key settings in the configuration file.

- inventory — where the inventory file is located (stores the IP addresses or hostnames of the managed nodes)
- remote\_user — the user name to use when logging in to managed hosts. The name of the current user is used if it is not supplied.
- ask\_pass — if an SSH password prompt should be displayed. Possibly false if SSH without a password is configured.
- become\_ask\_pass — whether to ask users of sudo permissions for a password. If passwordless sudo is set up in the managed node, the statement might be false.

**Creating the inventory file 📃**

Edit hosts file on */etc/ansible/hosts* and add your target server

random-servers

[dbservers]
one.example.com
two.example.com
three.example.com

[webservers]
foo.example.com
bar.example.com

Once this is finished, let’s use the command below to ping all of the specified remote hosts.

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.007.jpeg)

$ ansible all -m ping

Ansible sends a ping command to a remote host and displays the output as follows:

servername | SUCCESS => {
"changed": false,
"ping": "pong"
}

By substituting all with a group name, we can even construct groups in the inventory file and run ansible operations. The server in the example below is our group name as it appears in the inventory file.

$ ansible server -m ping

**Writing your first ansible playbook 🧾**

Now to specify a list of tasks, you develop a playbook. Playbooks can be used again. They can be controlled in the version control system because they are in YAML format. 

A play is a collection of sequential tasks that compares inventory. Ad-hoc commands are a playbook substitute.

Note : Please use caution during indentation when building a playbook. ⚠️

A sample playbook :

\# first-playbook-.yml- name: creating a test file
`  `hosts: all
`  `become: yes
`  `tasks:
`    `- name: Create a test file in dir : '/home/user/random/file.txt' 
`      `copy:
`        `content: This is my first playbook
`        `dest: /home/username/random/file.txt

How has the aforementioned playbook been set up?

\# first-playbook-.yml- name: <Name of Play>
`  `hosts: <Management Host>
`  `become: <privilege escalation>
`  `tasks:
`    `- name: <Name of task> 
`      `<module>:
`         `<arg-1>
`         `<arg-2>

or like:

\---
\- hosts: [hosts]
`  `tasks:
`    `- [first task]
`    `- [second task]

The syntax can be checked before executing.

$ ansible-playbook --syntax-check first-playbook-.yml

**Now running the Ansible playbook** 

To run this playbook

$ ansible-playbook first-playbook-.yml

We obtain the following outcome when we run the aforementioned playbook using the command “ansible-playbook playbook.yml.” Getting information is the initial outcome of this. This occurs because ansible runs a unique module called “setup” prior to carrying out any action. 

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.008.jpeg)

This module establishes a connection to a remote host and collects a variety of data, including IP address, disc space, CPU, and other details. After doing this, the test directory is created by running our create directory job.

PLAY [all] \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*TASK [Gathering Facts] \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
ok: [webservers]TASK [Creates directory] \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
changed: [webservers]PLAY RECAP \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*
webservers             : ok=2    changed=2    unreachable=0    failed=0

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.009.jpeg)

Numerous modules and instructions are accessible for execution on distant hosts. We can set up a server, install software, and perform many more activities with ansible.

**Ad-Hoc Commands?**

The ansible command-line tool is used by the ansible ad-hoc command to automate a task on managed nodes. 

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.010.jpeg)

Instead of using playbooks, these activities employ modules to quickly perform any operation on nodes.

For pinging all nodes : 

$ ansible all -m ping# format of command
$ ansible **[**host**-**pattern**]**  -m **[**module**]** -a "[module options]"  -i     "[inventory]"

To make certain that if a ‘httpd’ service is initiated on each webserver:

$ ansible all -m ansible.builtin.service -a "name=httpd state=started"

Congratulations! You completed running your first Ansible playbook with success. Learning Ansible opens up countless future possibilities. This is only a straightforward script, but you may expand it to create a larger infrastructure by including additional modules. 

In conclusion, I hope you can now begin to recognise Ansible’s strength. Additionally, we can configure a large number of servers if we so choose. Every configuration imaginable is possible using Ansible.

![](Aspose.Words.51f35a84-d0a5-4a81-8919-d6836be446ce.002.jpeg)

**Github URL for this article 💻**

<https://github.com/devangtomar/learning-devops-masterclass/tree/main/ansible>

**Let’s connect and chat! Open to anything under the sun 🏖️🍹**

🐦 Twitter : [devangtomar7](https://twitter.com/devangtomar7)
🔗 LinkedIn : [devangtomar](https://www.linkedin.com/in/devangtomar)
📚 Stackoverflow : [devangtomar](https://stackoverflow.com/users/8198097/devangtomar)
🖼️ Instagram : [be_ayushmann](https://instagram.com/be_ayushmann)
Ⓜ️ Medium : [Devang Tomar](https://medium.com/u/8f5e1c86129d?source=post_page-----e42119a306ca--------------------------------)
☊ Hashnode : [devangtomar](https://devangtomar.hashnode.dev/)


