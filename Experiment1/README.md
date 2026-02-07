Step 1: Download Virtual Box from [here](https://www.virtualbox.org/wiki/Downloads)

**Step 2:Download Vagrant from [here](https://developer.hashicorp.com/vagrant/install)
![Download Vagrant](./Images/I1.jpeg)

Step 3:To verify the installation we will check the version via following command
``` bash
vagrant --version
```
![Version Check](./Images/I2.jpeg)


Step 4:Initialize Vagrant with Ubuntu box:
```bash
vagrant init hashicorp/bionic64
```
![Initialize](./Images/I3.png)

Step 5:Start the VM:
   ```bash
   vagrant up
   ```
![Vagrant up](./Images/I4.png)


Step 6:Access the VM:
```bash
vagrant ssh
```
![ssh](./Images/I5.png)


Step 7: Install Nginx inside VM
```bash
sudo apt update
sudo apt install -y nginx
sudo systemctl start nginx
```
![Install Nginx](./Images/I6.png)

Step 8: Verify Nginx
```bash
curl localhost
``` 
![Verify Nginx](./Images/I7.jpeg)

Step 9: Utilization Matrix In Running State
![Running State Matrix](./Images/I8.png)


Step 10:Stop VM
```bash
vagrant halt
```
![Halt Vagrant](./Images/I9.jpeg)

Step 11: Utilization Matrix In Stop State
![Stop State Matrix](./Images/I10.png)

Step 12:Remove VM
```bash
vagrant destroy
```
![Vagrant Deleted](./Images/I9.jpeg)



