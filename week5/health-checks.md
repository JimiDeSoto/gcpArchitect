Go to Health checks page in the GCP Console.
Click Create health check.
Set name to autohealer-check.
Set Protocol to HTTP.
Set Request path to /health
Set health criteria:
a) Set check interval to 10.
b) Set timeout to 5.
c) Set Healthy treshold to 2.
d) Set Unhealthy treshold to 3.
Click Create.
Go to the Create Firewall rule page in GCP console (Networking-> VPC -> Firewall Rule)
Enter name, select default for network, for target select all instances in network.
For source filter select IP ragnes and enter 0.0.0.0/0
In protocol and porst select tcp and enter 80.
Goto to the instace templates page in GCP console.
Click create instance template.
Set the name to webserver-template.
For machnie type select f1-micro.
Under firewall select allow http traffic.
Click management, security disks, networking, sole tenancy to reveal advanced settings.
Under the Management tab, find automation and enter script:

sudo apt-get install -y git
sudo apt-get install -y gunicorn3
sudo apt-get install -y python3-pip
git clone https://github.com/GoogleCloudPlatform/python-docs-samples.git 
cd python-docs-samples/compute/managed-instances/demo
sudo pip3 install -r requirements.txt
sudo gunicorn3 --bind 0.0.0.0:80 app:app --daemon

Click create.
Go to the Instance groups page in the GCP Console.
Click Create instace group.
Set name to webserver-group.
Select region: europe-west1
For instance template select webserver-template.
For autoscaling select Off.
Set number of instances to 3.
Select created healthcheck.
Set initial delay to 90.
Click create.
Go to VM instances and check external IP column and open it in new tab on your browser.
Create unhealthy state and check the results.