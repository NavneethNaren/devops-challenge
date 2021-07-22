# Challenge Solution

## Create a windows VM via aws console (region - us-east-1)

1. Launch an ec2 windows instance Microsoft Windows Server 2019 Base - ami-03295ec1641924349
2. In security group configuration, allow RDP port 3389, winrm ports 5985 and 5986 inbound access.
3. RDP into the windows instance.
4. Open powershell
5. Run
   ```
   Invoke-WebRequest -Uri https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1 -OutFile ConfigureRemotingForAnsible.ps1

   .\ConfigureRemotingForAnsible.ps1
   ```

## Create linux instance in aws and install jenkins

1. Launch an amazon linux ec2 instance Amazon Linux 2 AMI (HVM), SSD Volume Type - ami-0dc2d3e4c0f9ebd18
2. In security group configuration, allow SSH port 22, and jenkins port 8080 inbound access.
3. SSH into the instance.
4. Install jenkins

  ```bash
  $ sudo yum update –y
  $ sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
  $ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
  $ sudo yum upgrade -y
  $ sudo yum install jenkins java-1.8.0-openjdk-devel -y
  $ sudo systemctl daemon-reload
  $ sudo systemctl start jenkins
  $ sudo systemctl status jenkins
  ```

5. Install ansible

  ```bash
  $ sudo amazon-linux-extras install ansible2
  ```

6. Install winrm package

  ```bash
  $ curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py
  $ python get-pip.py
  $ pip install winrm
  ```

## Create Jenkins Job

1. Get admin password from /var/lib/jenkins/secrets/initialAdminPassword.
2. Access jenkins via browser.
3. Login with admin password
4. Set up new user.
5. Create a new jenkins pipeline job and select pipeline from scm and provide github url as https://github.com/NavneethNaren/devops-challenge.git
6. Run and test the job by passing windows VM IP, username and password and build parameters.
