
<img width="924" alt="architecture-complete (5)" src="https://github.com/user-attachments/assets/fb589ba6-0d48-45fb-bd2e-d8de638e62e6" />

# Threat Detection with AWS GuardDuty

This project aims to provide a practical understanding of threat detection in the cloud using **Amazon GuardDuty.** Through a hands-on exercise, a vulnerable web application is deployed, attacks are simulated, and then **Amazon GuardDuty** is used to detect those threats. It is an excellent way to learn how to detect threats in a cloud environment.

## Key concepts

- **Amazon GuardDuty**
- **Amazon CloudFront**
- **Amazon S3**
- **AWS CloudFormation**
- **OWASP Juice Shop**


## Project Diagram
<img width="924" alt="architectura (5)" src="https://github.com/danf22/-Threat-Detection-with-AWS-GuardDuty/blob/main/Diagram.png" />

## Project objectives

The project aims to provide practical insight into cloud security and threat detection through the following steps:

1. **Learning by doing:** Act as both attacker and defender to understand how vulnerabilities are detected and exploited in a controlled environment.
2. **Using a vulnerable web application:** **OWASP Juice Shop**, a deliberately vulnerable web application, is used to simulate attacks.
3. **Simulating common attacks:**
   - **SQL injection**
   - **Command injection**
   - **Data exfiltration**

## Implementation instructions

### Requirements

1. Have an active AWS account.
2. Basic knowledge of AWS and its services (EC2, S3, CloudFormation, etc.).
3. Basic knowledge of **OWASP Juice Shop** and common vulnerabilities.

### Infrastructure deployment

The project is deployed using **AWS CloudFormation**, which automates the creation of all necessary resources:

1. **VPC** for the environment.
2. **Subnets and security groups** to control traffic.
3. An **EC2 instance** to host the Juice Shop application.
4. An **S3 bucket** to store data.
5. **GuardDuty** for continuous threat detection.

You can review the CloudFormation template to see the resources that are created in AWS.

### Simulated attacks

#### 1. **SQL injection**
- A malicious SQL query is entered in the password field to bypass authentication.
- Example of injection: `' OR 1=1;--`.

#### 2. **Command injection**
- Malicious commands are inserted into the username field, forcing the system to store temporary AWS credentials in a public JSON file.
- This reveals a vulnerability in the application's handling of inputs.

#### 3. **Data exfiltration**
- The stolen credentials are used to access and copy a file named **secret-information.txt** from an S3 bucket using the AWS CLI.

## Analysis with Amazon GuardDuty

**Amazon GuardDuty** continuously monitors the environment for suspicious activity. After simulating attacks, GuardDuty is used to detect events and generate detailed reports that include:

- What happened
- When it happened
- What resources were affected

GuardDuty detects unusual activity, such as unauthorized access to S3 buckets, and provides important details, such as which role was compromised and what API actions were performed.

### Malware detection

In addition to intrusion detection, malware detection can also be tested using an **EICAR** file, which is a synthetic malware test file. GuardDuty immediately detects it as a threat.

## Cleaning the environment

It is important to remove all resources after testing to avoid risks:

1. Delete the **CloudFormation** stack.
2. Delete the stolen credentials file.
3. Confirm that the environment is clean and that no resources remain exposed.

## Conclusion

This project highlights how **poor input validation** can lead to **data leaks**. An attacker does not need advanced skills to exploit vulnerabilities such as SQL or command injections. With poor input validation, an attacker can gain access to critical resources and exfiltrate sensitive data.

**Amazon GuardDuty** is a powerful defense tool that uses **machine learning** to identify threats in traffic patterns and logs. Although it cannot stop all threats, it is an excellent way to detect warning signs in real time.

## Key points to remember

- **Use secure systems for testing**, such as OWASP Juice Shop.
- **Deploy infrastructure with code** to have full control over resources.
- **Perform attacks and document the steps** that lead to a security breach.
- **Observe how GuardDuty responds** and verify that it detects the intrusion.
- **Remove all resources** after testing to avoid risks.
- 
This project will help you understand **security risk management** in a cloud environment. It is essential to conduct continuous testing, keep security strategies up to date, and explore new threat vectors. Starting with a structured project like this will give you a better understanding of how to defend a cloud environment.

## Additional resources

- [Documentación de AWS GuardDuty](https://aws.amazon.com/guardduty/)
- [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/)
- [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
