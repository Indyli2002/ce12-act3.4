# flask-app
Coaching 2: Building a Python Flask Application



Run your Flask app on the instance
The following instructions assumes you have already created an EC2 instance and configured it correctly. You may refer to the activities we covered in lessons 1.5 and 1.6 for detailed instructions.

Connect to your instance
First, we want to ssh into our EC2 instance.
ssh -i "your-key.pem" ec2-user@your-public-dns 
Install dependencies
We want to run an update on dnf.
sudo dnf update -y

We want to install git, python and pip.
sudo dnf install git python3-pip -y
Clone your repo on the instance
Clone your git repository.
git clone https://github.com/<your-username>/<your-flask-repo>.git

Alternatively, if you don’t want to use git you may use scp. However, it is recommended that you use git instead.
scp -i "your-key.pem" -r /path/to/your/flask-app ec2-user@your-public-dns:~
Run your web server
Create and activate the Python virtual environment.
cd your-flask-app
python3 -m venv .venv
source .venv/bin/activate

Install dependencies.
pip install flask

Run the web server.
python app.py


Create a new file in the /etc directory. You may use vim or nano.
sudo vim /etc/httpd/conf.d/flask_proxy.conf

Add the following lines to the file:
<VirtualHost *:80>
    ProxyPreserveHost On
    ProxyPass / http://127.0.0.1:8080/
    ProxyPassReverse / http://127.0.0.1:8080/
</VirtualHost>

Once you start or restart httpd, you should be able to visit your site on port 80