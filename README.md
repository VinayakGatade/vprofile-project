# VProfile Project

## Overview
VProfile is a full-stack Java web application designed to demonstrate modern DevOps practices, microservices-inspired architecture, and enterprise-grade user management. It integrates a variety of technologies and tools to simulate a real-world production environment, making it ideal for learning, demonstration, and as a template for similar solutions.

## Features
- User registration, login, and profile management
- Role-based access control (Spring Security)
- File upload (profile images)
- User list and details for admins
- Integration with Memcached, RabbitMQ, and ElasticSearch
- Automated provisioning with Vagrant and Ansible
- CI/CD pipeline with Jenkins

## Tech Stack
- **Backend:** Java, Spring MVC, Spring Security, Spring Data JPA, Hibernate
- **Frontend:** JSP, Bootstrap, CSS, JavaScript
- **Database:** MySQL
- **Caching:** Memcached
- **Messaging:** RabbitMQ
- **Search:** ElasticSearch
- **Build:** Maven
- **Web Server:** Tomcat
- **CI/CD:** Jenkins
- **Provisioning:** Ansible, Vagrant

## Architecture
```
+-------------------+      +-------------------+      +-------------------+
|   Nginx (web01)   | ---> |  Tomcat (app01)   | ---> |   MySQL (db01)    |
+-------------------+      +-------------------+      +-------------------+
        |                        |                        |
        v                        v                        v
+-------------------+      +-------------------+      +-------------------+
| Memcached (mc01)  |      | RabbitMQ (rmq01)  |      | ElasticSearch     |
+-------------------+      +-------------------+      +-------------------+
```
Each service runs on its own VM (provisioned by Vagrant) to mimic a production-like environment.

## Setup Instructions

### Prerequisites
- JDK 17 or 21
- Maven 3.9
- MySQL 8
- Vagrant & VirtualBox (for VM setup)
- Ansible (for automated provisioning)

### 1. Local Setup (Manual)
1. Clone the repository:
   ```sh
   git clone https://github.com/YOUR_USERNAME/vprofile-project.git
   cd vprofile-project
   ```
2. Import the MySQL dump:
   ```sh
   mysql -u <user_name> -p accounts < src/main/resources/db_backup.sql
   ```
3. Configure `src/main/resources/application.properties` as needed.
4. Build the project:
   ```sh
   mvn clean install
   ```
5. Deploy the WAR file to Tomcat.

### 2. Vagrant Multi-VM Setup
1. Navigate to the Vagrant directory:
   ```sh
   cd vagrant/Automated_provisioning_WinMacIntel
   ```
2. Start all VMs:
   ```sh
   vagrant up
   ```
   This will provision:
   - `db01` (MySQL)
   - `mc01` (Memcached)
   - `rmq01` (RabbitMQ)
   - `app01` (Tomcat + app)
   - `web01` (Nginx)

### 3. Ansible Automation
- Use the playbooks in the `ansible/` directory to automate Tomcat and app setup:
  ```sh
  ansible-playbook -i inventory site.yml
  ```

### 4. Jenkins CI/CD
- The `Jenkinsfile` defines a pipeline for build, test, code analysis, and deployment.
- Configure Jenkins with JDK 17, Maven 3.9, and required credentials.

## Usage
- Access the application via the Nginx or Tomcat VM IP address in your browser.
- Register a new user or log in with existing credentials.
- Admin users can view and manage all users.

## Contribution Guidelines
1. Fork the repository
2. Create a new branch (`git checkout -b feature/your-feature`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature/your-feature`)
5. Open a Pull Request

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
