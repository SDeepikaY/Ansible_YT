# Ansible_YT


Connect to my EC2 instance :  chmod 600 ~/Desktop/devops_courseYT/testkp.pem     \
ssh -i ~/Desktop/devops_courseYT/testkp.pem ubuntu@44.203.1.105 

we are using linux now 
sudo apt update - to update ; 
sudo apt install ansible - to install ansible ; 
 note - we are using ansible to configurion target_ansible server using current(test) server    \ 

 step 1 -: we should make it password less authentication 
 ssh-keygen - wil generate public and private key , these are stored in home/ubuntu/ .ssh/id_ed25519
 ls/home/ubuntu/.ssh - to check the private  and public key \
 cat /home/ubuntu/.ssh/id_1559.pub - to access public key \ 
 copy public key and paste in the ~/.ssh/authentication_keys file of target_server \\ 
 which mean we are pasting public key of ansible server  to  target_server authention_keys file to make it passwordless authentication. \\
therefore : ssh (paste private key of target ansible server ) - we can connect to target server from root server withut authentication  \\ 

 step 2 :  
 adding IP adress of target server to ansible server invenory file
 mkdir ansible \
 nano ~/ansible/inventory \  - a file will be created and opened paste IPV4 adres of target_server. 
 cat ~/ansible/inventory   \  - to view content in inventory file.  \\
 
 step 3 : 
scenario 1: creating files in target server writing ansible adhoc commands or play book  \

 -i inventory all -m "shell" -a "touch devopsclass"  \ - this will create file named devopsclass  in the target server. \\ 

  in case if we want to run comand on only few servers and other command on other servers then we groups IP adreess in inventory file and change the adhoc command to group name instal of all  \  \\

 step 3 :
 scenario 2: install and restart nginx in servers  \
 
 vim firstplaybook.yml \  -nsible playbooks are written in yml format
 the above command will open firstplaybook.yml file in that 
 
  3 dashes (---)
  -name : imstall and start nginx
    host : all
    become : root
    tasks :
      -name: install nginx
      apt:
        name:nginx
        state: present
      -name:starte nginx
      service:
        name:nginx
        state:started
    esc-:wq! <img width="657" height="653" alt="image" src="https://github.com/user-attachments/assets/6f78a472-3252-4d6e-80f3-9eb157472d1d" />
    
ansible-playbook -i inventory first_playbook.yml  - to execute playbook

 - to check - in target server  \
sudo systemctl status nginx  \\

 step 4 : 
ansible_playbook --v -i inventory first_playbook.yml - for debug 




 
 
 
 
 
 https://www.youtube.com/watch?v=Z6T2r3Xhk5k&list=PLdpzxOOAlwvIKMhk8WhzN1pYoJ1YU8Csa&index=22 
 

Yml file for installing and restart nginx on target servers using ansible from from other server we do this by configuring inventory file by adding IP address of target file in inventory. before that we instal ansible and make the ansible to connect to target servers without authentication (i.e without password).   

