[ubuntu] 
172.31.13.18           # Node1 Private Ip. Which means "Ubuntu" 

[redhat] 
172.31.5.126           # Node2 Privete Ip. Which means "RedHat"

[krishna] 
172.31.5.126           # Node2 Privete Ip. Which means "RedHat"
172.31.13.18           # Node1 Private Ip. Which means "Ubuntu" 





--> Previsouly we are writeing two files in the Inventory.
--> Why we write two files, why not One?
--> Ansible Inventory broadly classified into two types.
      1. STATIC INVENTORY:- Where we mention the list of nodes to connect to in some file.
      2. DYNAMIC INVENTORY:- Where we mention some script/plugin which will dynamically find out the nodes to connect to.
--> As of now, Lets focus on Static Inventory.
    * Static Inventory means, Where we mention our Node details. 
--> https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#inventory-basics-formats-hosts-and-groups for official docs on Ansible inventory.
--> Static inventory can be mentioned in two formats
      1. Ini
      2. YAML.
--> Ini format:https://en.wikipedia.org/wiki/INI_file#:~:text=An%20INI%20file%20is%20a,sections%20that%20organize%20the%20properties.
    * We write the "[ ]" which represents the group. After whatever we write the values it belong to that Activity.
--> Go to Inventory and Create a groups called as "Ubuntu" and "RedHat". 
    [ubuntu]                                [redhat]
    172.31.13.18. One Entry.                172.31.5.126. One Entry.
--> We can change the host details in playbook. Now write the group Name.
            hosts: ubuntu           hosts: RedHat
--> One Machine might be present in Multiple Groups. 
               [krishna] 
               172.31.5.126           
               172.31.13.18
--> When we try to all, All the unique Ip Address (or) unique hostname. Whole Inventory file must be shown.
--> EXAMPLE,
            [NAME]  --> It represents the Group Name.
            0.0.0.0 --> Host Name (or) Private IP of the Node.
--> How to see the list of hosts? 
    <ansible-playbook -i <inventory path> <playbook path> --list-hosts>.

-- YAML FORMAT -- 
----------------- 
--> https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html for yaml format docs of Inventory.
--> I have children. In that children I have Group.







