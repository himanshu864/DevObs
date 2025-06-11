#devops 

### Step 1: Set Up an AWS Account

1. **Sign up for AWS**: If you don’t already have an AWS account, sign up at [AWS Free Tier].

### Step 2: Launch an EC2 Instance

1. **Navigate to EC2 Dashboard**: Log in to the AWS Management Console and navigate to the EC2 Dashboard. And select nearest cloud server (Mumbai).
2. **Launch Instance**:
    - Click on "Launch Instance".
    - Select the Amazon Machine Image (AMI): Choose "Amazon Linux 2" or "Ubuntu 22.04 LTS". (free tier)
    - Choose an Instance Type: Select the `t2.micro` instance type (which is free tier eligible).
    - Create new key pair (SSH key connection). ***V.V.Imp: Keep it safe***
    - Review and Launch: Launch the instance and create a new key pair (or use an existing one).

### Step 3: Connect to Your EC2 Instance

1. **Connect to your instance**: Use an SSH client to connect to your instance.

```bash
ssh -i /path/to/your-key-pair.pem ec2-user@your-ec2-public-dns
``` 

### Step 4: Install Node.js and Git

1. **Update and install Node.js**:
```bash
# installs nvm (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# download and install Node.js (you may need to restart the terminal)
nvm install 20

# verifies the right Node.js version is in the environment
node -v # should print `v20.16.0`

# verifies the right npm version is in the environment
npm -v # should print `10.8.1`
```

2. **Install Git**:
Most probably preinstalled

### Step 5: Clone Your Repository and Install Dependencies

1. **Clone your repository**:

```bash
git clone https://github.com/yourusername/your-repo-name.git cd your-repo-name
```

2. **Install dependencies**:

```bash
npm install
```
### Step 6: Set Up Environment Variables

 **Create `.env` file**:

```bash
vim .env
```
Add your environment variables

### Step 7: Start Your Application

1. **Start your Node.js application**:

```bash
npm start
# node app.js
```

Alternatively, use a process manager like PM2 to keep your app running:

```bash
sudo npm install -g pm2
pm2 start app.js
pm2 startup
pm2 save
```

### Step 8: Configure Security Group to Allow Traffic

 **Update Security Group**:
 
- Go to the EC2 Dashboard, select your instance, and click on the associated Security Group.
- Edit the inbound rules to allow traffic on port 3000 (or whichever port your app is running on). Custom TSP.

### Step 9: Access Your Application

1. **Get your instance’s public IP or DNS** from the EC2 dashboard.

2. **Access your application**:
    - Open a web browser and navigate to `http://your-ec2-public-dns:3000`.

### Step 10: Enjoy your application on Cloud!

