
<img width="924" alt="architecture-complete (5)" src="https://github.com/user-attachments/assets/fb589ba6-0d48-45fb-bd2e-d8de638e62e6" />

# -Threat-Detection-with-AWS-GuardDuty
That’s the idea behind the Threat Detection with GuardDuty project. It’s a hands-on exercise where I deploy a vulnerable web application, attack it, and then use Amazon GuardDuty to detect those attacks. The goal is to give me a practical understanding of threat detection.
If I want to learn how to detect threats in a cloud environment, the best way is to simulate them myself. That’s the idea behind the Threat Detection with GuardDuty project. It’s a hands-on exercise where I deploy a vulnerable web application, attack it, and then use Amazon GuardDuty to detect those attacks. The goal is to give me a practical understanding of threat detection.

Working with a vulnerable web application is one way to learn about security threats. There’s a project involving an app called OWASP Juice Shop, which contains multiple flaws. The idea is to deploy it in AWS and then see how Amazon GuardDuty detects suspicious actions when it gets attacked.

KEY CONCEPTS

Amazon GuardDuty
Amazon CloudFront
Amazon S3
AWS CloudFormation
OWASP Juice Shop
I started by using an AWS CloudFormation template. The template builds the underlying pieces:

• A Virtual Private Cloud for the environment
• Subnets and security groups for traffic control
• An EC2 instance hosting the Juice Shop
• An S3 bucket for data
• GuardDuty for continuous threat detection

CloudFormation helps skip manual work. You can review the template to see every resource AWS will create.

The project revolves around a few key ideas:

Learning by Doing
The best way to understand cybersecurity is to practice it. In this project, I play both the attacker and the defender. I exploit vulnerabilities in a controlled environment and then analyze how those exploits are detected. This dual perspective is invaluable.
Using a Vulnerable Web Application
The project uses OWASP Juice Shop, a deliberately vulnerable web application. It’s designed to have security flaws so I can practice exploiting them without causing real harm. I deploy it using AWS CloudFormation, which automates the setup of the infrastructure.
Simulating Common Attacks
I simulate three types of attacks:
SQL Injection: Bypassing login authentication by injecting malicious SQL code.
Command Injection: Executing malicious commands on the web server.
Data Exfiltration: Stealing sensitive data from an S3 bucket.
Analyzing Results with GuardDuty
Amazon GuardDuty is a machine learning-powered service that monitors my AWS environment for suspicious activity. After simulating the attacks, I use GuardDuty to detect them. The service provides detailed findings, including what happened, when it happened, and which resources were affected.

When the Juice Shop is up, there’s a login page with a standard email and password prompt. SQL injection is the first trick. You enter something like ' or 1=1;-- in the password field to bypass authentication. The approach is to break the query's logic so the server treats every login attempt as valid. It's a classic attack from older web apps, though it still appears in production environments.

Then there’s a command injection. You place malicious instructions in the username field and rely on the server to run them. In this project, those instructions force the system to store temporary AWS credentials in a public JSON file. It reveals a gap in the app’s input handling. When code from user input runs on the server, it opens a door to every resource the instance can reach.

Next, I switched to AWS CloudShell, which is a managed environment for running AWS CLI commands. I took the stolen credentials and turned them into a new CLI profile. Then I used the profile to copy an S3 object called secret-information.txt. The file had a short message signaling the attack was successful.

At this point, it’s useful to see how GuardDuty reacts. GuardDuty monitors the environment, so when it notices a suspicious event, it reports a finding. In this case, it flagged abnormal S3 activity within 15 minutes. The summary explained which role had been compromised and which API actions had been used. It’s the detail you need if you plan to track the source of an incident.

Enabling malware protection in GuardDuty is an extra step. You can upload an EICAR test file to see if GuardDuty responds. EICAR is a synthetic piece of malware, so it doesn’t break anything. GuardDuty detects it and logs a new finding.

It’s important to clean up after a test. I removed the CloudFormation stack, deleted the credentials file, and confirmed the environment was gone. It’s easy to leave a system exposed if you don’t tidy up.

Projects like this highlight the link between poor input validation and data breaches. The moment an app processes unfiltered data, it invites attackers to poke around. An attacker does not need advanced skills to run an injection. A few lines of text can bypass a login or exfiltrate secrets.

GuardDuty is an example of how machine learning can assist with defense. It parses logs and traffic patterns, looking for anything suspicious. It won’t stop every threat, but it can catch major red flags. The best approach is to combine tight coding, robust IAM policies, and a service like GuardDuty to watch for anomalies.

I recommend starting with a test environment. You can learn AWS tools, see how a live attack unfolds, and figure out how a defender responds. This cycle of build-break-fix is the core of cybersecurity. It’s not about theoretical examples. It’s about real workloads, real logs, and real alerts.

Bullet Points to Remember:

• Look for systems which are safe to hack, like Juice Shop
• Deploy them with infrastructure-as-code, so you control every piece
• Attack them and note every step which leads to a compromise
• Watch for how GuardDuty responds and see if it catches the intrusion
• Avoid leaving any traces after you’re done

This kind of practice builds an intuitive sense of risk. You see the difference between a random scan and a targeted approach. You see how data can vanish if an attacker grabs credentials. You see how a single open door can lead to a bigger breach.

There’s a lot to keep learning in AWS security. It’s not enough to enable a single service and walk away. You need constant testing, constant updates, and constant exploration of new threat vectors. But a structured project with a tool like Juice Shop is a good place to begin. Once you’ve seen what an attacker does, it’s much easier to defend.

Further Reading::
🤖ChatGPT for Vulnerability Detection by Tahir Balarabe

What are AI Agents?

Stable Diffusion Deepfakes: Creation and Detection

The Difference Between AI Assistants and AI Agents (And Why It Matters)

☁️ Building Scalable Three-Tier Web Apps with AWS

🐳Deploying a Backend Application with Kubernetes on AWS EKS

Encrypt Data with AWS Key Management Service KMS

Automating S3 Buckets with Terraform🏗️

Mastering Database on AWS: From QuickSight to DynamoDB

Creating and Deploying a Containerized Application with Docker and AWS Elastic Beanstalk

How to Secure Your Cloud with AWS IAM Policies

MY JOURNEY ON AWS(AMAZON WEB SERVICES)
