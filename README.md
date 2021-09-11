# ansible-akatsuki

Problem Statement:
•	Configure Ansible server on VM 1 to deploy a webserver to VM2 and VM3 on port 8080 that displays the message: “Hello World from SJSU”
•	Un-deploy all webserver resources
Team AKATSUKI:
 
•	Archana Miyar Kamath
•	Simran Tanvir Memon
•	Mounica Kamireddy
•	Limeka Dabre
 
Implementation: 
•	An AWS EC2 instance was created and Ansible was installed on this server (VM1)
•	Using Ansible server(VM1) playbook, deployed webservers(nginx) on VM2 and VM3

Step1:
•	Create an EC2 instance and download the secret key (new_ansible.pem). 
•	Open the terminal and connect to this instance using ssh -i "new_ansible.pem" ubuntu@ec2-54-186-95-252.us-west-2.compute.amazonaws.com

![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step1.PNG?raw=true)

•	Install ansible on this server using the command: sudo apt install ansible and you can check the ansible version using ansible –version

![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step1a.PNG?raw=true)

Step 2:
•	Like VM1, create two other EC2 instances – VM2 and VM3
•	Set the inventory by updating hosts file under /etc/ansible/hosts using command: sudo nano /etc/ansible/hosts in the following format:
[ansible_clients]
client_1 ansible_host=35.164.161.246
client_2 ansible_host=34.217.4.182
•	Check the updated inventory using command: ansible-inventory --list -y

![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step2.PNG?raw=true)

Step 3:
•	Make sure that the webservers VM2 and VM3 are reachable by pinging from server VM1 using command: ansible all -m ping --private-key new_ansible.pem

![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step3.PNG?raw=true)
 
Step 4:
•	Install nginx on VM2 and VM3 through playbook(final_webservice.yml) with change of port to 8080 and required message as follows:
 
 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step4.PNG?raw=true)
 
Step 5: Below is the code to change the port to 8080

 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step5.PNG?raw=true)

Step 6:
•	Source (src) index.html file in playbook is as follows:
 
 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step6a.PNG?raw=true)

Step 7:
•	Run the playbook on VM1 server using: ansible-playbook final_webservice.yml --private-key new_ansible.pem -b
 
 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step7a.PNG?raw=true)

•	Check the status of the webserver deployed using command: sudo service nginx status
 
 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step7b.PNG?raw=true)


•	Simultaneously, check if the desired message from the updated index.html exists on VM2 at http port 8080
 
 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step7c.PNG?raw=true)


Step 8:
•	Similarly, check the nginx status for VM3 and corresponding webpage. 
 
  ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step8.PNG?raw=true)
 
  ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step8a.PNG?raw=true)

Step 9:
The following playbook (stop_nginx.yml) helps in un-deploying the webserver:

 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step9.PNG?raw=true)

 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step9a.PNG?raw=true)
  
•	Make sure that the webserver got un-deployed successfully using command: sudo service nginx status

 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step9b.PNG?raw=true)

•	Simultaneously check the http port 8080 on webpage.

 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step9c.PNG?raw=true)
 

Step 10:
•	Similarly, check the nginx status for VM3 and corresponding webpage. 

 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step10.PNG?raw=true)

 ![alt text](https://github.com/archana-kamath/ansible-akatsuki/blob/main/screenprints/Step10a.PNG?raw=true)
