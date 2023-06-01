
---------------------------------------------------------------------------------------------------------

## Ansible ##
-------------
# --> Create Two Virtual Machines(vm's) in any Cloud(AWS,Azure).Just for Understanding Purpose, We are giving Some names.
    - ansible control node.
    - Node
# --> What is that we need now?
    -  on both the Machines, we need one user to be created that user should have admin permissions and initially to create that users. we need password based authentication enabled for some time. We can continue or disabled it's our wish.
# --> Try to login the both the machine's in terminal(or)powershell with the help of public ip.
    - ssh -i <path to pem> user@ip
    - we did not give "-i" in two cases.
        1. When it is a password based authentication.
        2. if we refering to id_rsa file(it means when we create "ssh-keygen" and import that key in cloud. that id_rsa file present in our home directory).
# --> <sudo apt update>. It means, It updateing the package definetions not updateing the packages.
# --> For Enableing password based authentication, we need to go with
    - sudo vi /etc/ssh/sshd_config
    - When get into the vi editor. ("/" this help for search some words(or) text in <vi editor>).
    - vi editor is popular and strong editor in linux.
    - nano editor is simple editor. like nodepad.
    - openvim is to learn about vi editor. 
    - We need to change the <PasswordAuthentication no> to <PasswordAuthentication yes>.
# --> After Password based Authentication is enabled. We have to go with, <sudo systemctl restart sshd>.
# --> Now we are going with "<sudo adduser "anyname">". (We can give anything in anyname=devops,krishna,aws,etc.). Here, it asks to create the password we need to create it. We added the user.
# --> "<sudo visudo>" We have to give sudo permissions for the user, which we create. The user go to do some installs.
    - nano can opened. nano and vi are two different editors. In nano editor we can get some characters it means that are the controls.
    - In nano editor, we go to <All memembers of group sudo to execute any command>.
        %sudo   ALL=(ALL:ALL) ALL
        anyname ALL=(ALL:ALL) NOPASSWD:ALL. And save the file. then logout or exit.
    - Now we can login like <ssh anyname@ip(publicip)>. It is a password based auhtentication it can ask password. Beacuse, We created the user with password based authentication. It login as user which we create.
    - In built in linux machines <python> already present.
# --> Now, Installing the Ansible With some basic commands.
        sudo apt update
        sudo apt install software-properties-common -y
        sudo add-apt-repository --yes --update ppa:ansible/ansible
        sudo apt install ansible -y
# --> Shortcut for linus keys for copy and paste.(I did not try this)
        ctrl+insert is for copy.
        shift+insert is for paste.
# --> To check the ansible version.
        ansible --version

# --> In the Second machine, which is nothing but node. In that, we have to do.

# --> For Enableing password based authentication, we need to go with
    - sudo vi /etc/ssh/sshd_config
    - When get into the vi editor. ("/" this help for search some words(or) text in <vi editor>).
    - vi editor is popular and strong editor in linux.
    - nano editor is simple editor. like nodepad.
    - openvim is to learn about vi editor. 
    - We need to change the <PasswordAuthentication no> to <PasswordAuthentication yes>.
# --> After Password based Authentication is enabled. We have to go with, <sudo service sshd restart>. just interchangeing they can work.
# --> Now we are going with "<sudo adduser "anyname">". (We can give anything in anyname=devops,krishna,aws,etc.). Here, it asks to create the password we need to create it. We added the user.
# --> <sudo visudo> We have to give sudo permissions for the user, which we create. The user go to do some installs.
    - nano can opened. nano and vi are two different editors. In nano editor we can get some characters it means that are the controls.
    - In nano editor, we go to <All memembers of group sudo to execute any command>.
        %sudo   ALL=(ALL:ALL) ALL
        anyname ALL=(ALL:ALL) NOPASSWD:ALL. And save the file. then logout or exit.
    - Now we can login like <ssh anyname@ip>. It is a password based auhtentication it can ask password. Beacuse, We created the user with password based authentication. It login as user which we create.
    - In built in linux machines <python> already present.
# --> Next thing is I want to create the key pair I don't use the password based authentication. There is no problem, we can use password based authentication in ansible also. But, generally passwords are excepted to be entered. But, We are using Ansible for automation, While this automation executes who will enter passwords. We want the automation executed without human intervention. when it excepts passwords we have to enter the passsword. That's why we go with key based authentication.

# --> Lets, create the key pair in first machine <ssh-keygen>.
    - After creating the key pair, we have to do <ssh-copy-id username@ip> . since both the machines are in same network we can use private ip of other machine.
    - Now I added the key. from that moment i want to login in this machine I just need to give <ssh private ip>.


# --> Lets, Create the "RedHat" Machine as "NODE2".

# --> For Enableing password based authentication, we need to go with
    - sudo vi /etc/ssh/sshd_config
    - When get into the vi editor. ("/" this help for search some words(or) text in <vi editor>).
    - vi editor is popular and strong editor in linux.
    - nano editor is simple editor. like nodepad.
    - openvim is to learn about vi editor. 
      # To disable tunneled clear text passwords, change to no here!
      #PasswordAuthentication yes
      #PermitEmptyPasswords no
    - We need to change the #PasswordAuthentication yes to PasswordAuthentication yes.

# --> After Password based Authentication is enabled. We have to go with, <sudo service sshd restart>. just interchangeing they can work.

# --> Now we are going with "<sudo adduser "anyname">". (We can give anything in anyname=devops,krishna,aws,etc.). Here, it asks to create the password we need to create it. We added the user.

--> In RedHat Commands are slightly different. It could not ask the password creation.For this we need do the Password creation. With the help of <sudo passwd "username">.

# --> <sudo visudo> We have to give sudo permissions for the user, which we create. The user go to do some installs.

    - vi can opened. nano and vi are two different editors. In nano editor we can get some characters it means that are the controls.
    - In vi editor, we go to <All memembers of group wheel to execute any command>.
           ## Allows people in group wheel to run all commands
            %wheel  ALL=(ALL)       ALL
            ansible ALL=(ALL)       NOPASSWD:ALL
    - In RedHat, it shows "WHEEL GROUP" it means Admin Group in RedHat family. There is slight difference in "ubuntu" and "RedHat" Machines.
    - Exit and Relogin with the user what we create.
    - In the Nodes Pyhton to be Installed. Whatever the operating System. Whatever the python version.<python --version>.
    - Do ssh-copy-id in Ansible Control Node. Give the Private Ip of Node2.
    <ssh-copy-id username@private Ip>
    - In Inventory, we have to create redhat file and put the Private Ip.
       <ansible -i 'private ip' -m ping all>. There is no need to give Inventory file.
    - Go for "YUM" package manager module in Ansible."YUM" is a package manager for RedHat.
    
## Let's create Something in Ansible
------------------------------------

# --> Lets create Inventory file
    - mkdir inventory
    - vi inventory/hosts. in the file we have to add node machine private ip.
    - ansible -m ping -i inventory/hosts all. To check for the every machine that is present in Inventory. To see whether working or not.
# --> Why local host failing?
    - Just give localhost in <vi inventory/hosts>. Ansible is excepting that a public key is present on the machine we are trying to connect. So, it doesn't differentiate whether it is same machine or other machine, we have to <ssh-copy-id username@localhost>. It will ask for password.
    - Now do, ansible -m ping -i inventory/hosts all. To check for the every machine that is present in Inventory.
    - It is working for both the machines. So even if it is for the same machine we have to do copy id.<Ansible is trying to compare our machine private key versus other machine public key>. Even if it is for same machine we have to excute ssh-copy-id.(22.06 min)
    - For some reasons we are working on the machine not on the localhost.

---------------------------------------------------------------------------------------------------------