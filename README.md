# SaintGeorgeClassify

### Partner

* Partners: BiFu Company

* A leading AI-based inspection company located in Shanghai with global clients

### Quick Links

> **Access Our Dashboard Site:** http://3.23.199.226:3000/
> Default Login: demo@gmail.com
> Default Password: 123456
> Access code to sign up new account: 123456

> **Access Our Technical README:** https://github.com/csc301-2025-s/project-3-VantEdge-Labs-1/blob/main/TechDetails.md

> **Watch Our Dashboard Demo:** https://www.youtube.com/watch?v=UNWtBmgGcYw&ab_channel=ZeZhengGu

## Table of Contents

* [Introduction](#introduction)
* [Features](#vantedge-dashboard-features)
* [Instructions](#instructions)
* [Technical Details](#technical-details)
* [Deployment](#deployment)
* [Github Workflow](#github-workflow)
* [Contribution](#contribution)
* [License](#licenses)
* [Contact](#partner)
---
## Introduction
---
VantEdge Labs is a cutting-edge platform that simplifies containerization, deployment, and management of AI applications in the cloud. Built by experts in cloud infrastructure and distributed systems, VantEdge Labs automates the process of packaging AI code, launching it on major cloud providers (like AWS/GCP), and monitoring performance—all through a user-friendly dashboard. By removing the need for extensive DevOps expertise, VantEdge Labs empowers organizations of all sizes to deploy AI at scale efficiently and reliably. Watch the VantEdge Labs platform demo [here](https://www.youtube.com/watch?v=mgYdTT_61a4&ab_channel=VantEdgeLabs).

Our project works on delivering the real-time analytics dashboard for our partner's clients' use, acting as a one-stop shop for clients to monitor their application's health. Grafana is an open-source analytics and visualization platform for monitoring and exploring time-series data from various sources. Prometheus is an open-source monitoring and alerting toolkit designed for collecting and querying time-series metrics, especially from cloud-native applications. Along with several other tools discussed in the technical details section, we created a custom dashboard suitable to all of VantEdge's clients' needs. Watch our VantEdge Dashboard demo [here](https://www.youtube.com/watch?v=UNWtBmgGcYw&ab_channel=ZeZhengGu).

By utilizing the power of Grafana, the customizable configurations and dynamic monitoring of our dashboard become a key feature of this project. Connecting Grafana with Prometheus, this dashboard will allow users to monitor container statistics, track resource utilization and system costs, monitor application performance, and identify issues with their applications. Among other metrics, the dashboard will display real-time data and visualizations for the following using various tools:

<div style="border:3px solid #ccc; padding:10px; border-radius:5px;">
<ul>
  <li>Container Health & Resource Utilization</li>
  <li>Container Lifecycle & State</li>
  <li>Application-Level Metrics</li>
  <li>Orchestration Metrics</li>
  <li>Infrastructure-Specific Metrics</li>
  <li>Cloud Costs</li>
</ul>
</div>

---
## VantEdge Dashboard Features
---
### Site Features
**User Authentication**
To access the full functionality of the VantEdge platform, users must first register and log into the VantEdge dashboard site. User authentication is required to view metrics and visualizations, receive metric alerts, and explore additional features that will be introduced by VantEdge over time. In addition, the platform employs multi-factor authentication (MFA) for access to Grafana dashboards. This means users cannot access their Grafana dashboards until they have been authenticated by both VantEdge and the Nginx which serves as a reverse proxy.

The purpose behind this design is to enhance security. Since the Grafana server is hosted on a public-facing server accessible by anyone with the URL (currently its IP), Nginx is used as a reverse proxy to restrict unauthorized access and ensure that only authenticated users can view the dashboard.

Account creation (Sign Up) requires an Access Code (set to 123456) known only to organization members who will have the opportunity to create an account.

![Watch the video](deliverables/assets/images/csc301-userAuth-demo.gif)

**The dashboard site has several features that can be accessed through the sidebar**.

**Dashboard**: The main page, where the full grafana dashboard can be viewed to monitor metrics. (Explained below in Grafana Dashboard section).
**Metrics Handbook**: This page provides brief descriptions of the metrics displayed on the dashboard. It’s meant to be used as a reference to understand what each metric represents and how it’s measured.

![MetricsHandbook](deliverables/D3/Images/MetricsHandbook.gif)

**Alerts**: A library of alert rules to notify users about critical events and performance issues in real-time. Users can toggle specific alerts on or off, allowing them to prioritize notifications they find relevant. Alerts are automatically sent to the email address registered during sign-up and login.

![AlertsPage](deliverables/D3/Images/AlertsPage.gif)

**Logout**: To exit user account.

### Grafana Dashboard Features
1. Monitor running applications through a visual dashboard that displays real-time statistics and performance metrics like error rate and throughput on the application level.
2. Monitor container-level metrics of the container running the client's application.
3. Monitor host-level metrics of the host machine that is running the containers that run the client's application as well as other monitoring tools.
4. Customize the monitoring dashboard to show the metrics as wished by toggling the header of each section.
5. Monitor the cost of deploying the application in real time​.

The dashboard allows users to easily navigate and monitor their instances and services with VantEdge. With the power of customization, you can easily configure what you want to see. Our customized data panels allow you to monitor whatever process or containers you want with ease, and many more features await in VantEdge Dashboard.

**Here is a GIF demonstration showcasing the key features.**

[![Watch the video](deliverables/assets/images/csc301-demo.gif)](https://www.youtube.com/watch?v=a8e8sAcJMGU)

Below is an example of a utilization metrics dashboard for an application/service. This dashboard visualizes resource usage, including CPU, memory, disk, and network metrics, while also assessing usage efficiency at both the container and host levels. It presents data in both time series and timestamp formats.

![Memory Usage](deliverables/D3/Images/memory.png)
![NetworkUsage](deliverables/D3/Images/network.png)
![Resources Utilization Efficiency](deliverables/D3/Images/efficiency.png)

---
## Instructions
---
### Accessing the Dashboard

#### Accessing the Project Site

From a browser, access [3.23.199.226:3000](http://3.23.199.226:3000/)

Users will be greeted by the Login Page. Create an account if needed by clicking on Sign Up.

<img src="deliverables/D3/Images/SignIn.png" alt="Alt Text" width="600"/>

<img src="deliverables/D3/Images/SignUp.png" alt="Alt Text" width="600"/>

Use access code 123456 to create an account. The access code ensures not just anyone can have access to the dashboard.

Once signed in, the main page will be the metrics dashboard. The Grafana dashboard is explained below in the Understanding the Dashboard Section.

By clicking on the options in the sidebar one can make use of the features available. These features are described above in the Features section.

<img src="deliverables/D3/Images/Sidebar.png" alt="Alt Text" width="200"/>

In the Metrics Handbook Page, one can find metric descriptions for reference to understand how metrics are measured and how to interpret them.

<img src="deliverables/D3/Images/MetricsHandbook.png" alt="Alt Text" width="800"/>

In the Alerts page, users will be able to toggle specific alerts on or off, allowing them to prioritize notifications they find relevant.

### Understanding the Dashboard

The main dashboard consists of multiple panels displaying key metrics in real-time.

#### Key Metrics Monitored

* **Container Health** – Status of running AI containers.
* **CPU & Memory Usage** – Resource consumption trends.
* **Network & Disk I/O** – Data transfer rates and storage performance.
* **Error Rates & Alerts** – Logged issues and failures.
* **Cost Tracking** – Cloud resource expenses over time.

### Interacting with the Dashboard

* Use the time range selector (top-right) to view specific periods (e.g., last 24 hours, last 7 days).
* Apply filters (dropdown menus) to focus on a specific container, node, or service.
* Click and drag over a graph to zoom into specific time intervals.
* Hover over data points for exact values and timestamps.

### Customizing the Dashboard

* Hide groups of panels by collapsing the rows they belong to.
* To collapse a row, click on the small **"chevron"** icon (▲ or ▼) at the top of the row, where the header of the section is located.

#### Rearranging Panels and Rows

* **Moving Panels:**  
  1. Enter **Edit Mode** by clicking on "Edit" in the top right corner of the page.
  2. Click and **drag** a panel to a new position.  
  3. Resize by dragging the edges of the panel.  

* **Reordering Rows:**  
  1. Click on the row title to expand options.  
  2. Use the **drag handle** (⋮⋮ icon) to move the row up or down.

#### Saving Changes

* After making modifications, click **"Save Dashboard"** so that changes persist.

#### Specify Time Range of Metrics

* Use the time range selector (top-right) to view specific periods (e.g., last 24 hours, last 7 days).

---
## Technical Details
---
Visit [this page](TechDetails.md) for more technical details.

### Development requirements


* Node JS: Latest
* Next JS: Latest
* Docker: Latest
* Docker Compose: Latest

### OS requirement

All operating systems that support our dependencies including Windows, Mac, Linux.

### Installation Instructions

Visit this [file](README.Docker.md) for detailed instructions on how to deploy our Dockerized product.

This starts the containers pre configured in `compose.yaml`. You should be able to access [Vantedge Dashboard](“localhost:3000”) now at localhost:3000. At this point, you should be able to manage Grafana’s ecosystem and dashboard as well.

---

## Deployment

---

### DevOps & Automated testing 

#### Automated Deployment
 We use GitHub Actions to automate deployment. Whenever a new pull request is merged into the main branch, the GitHub Action is triggered. 
 By storing necessary credentials in GitHub Secrets, the GitHub-hosted runner can SSH into the AWS VMs, pull the latest changes, and rerun the deployment using Docker Compose.

 Note that we have deployed two VMs for our project. One to host the containers including Grafana and the sample applications to monitor, and the other to host the Next.js web app. Therefore, automated deployment occurs concurrently in both VMs with different deployment scripts.

#### Deployment General Guidelines

The following steps are the general big pictures of the steps to be taken. The detail steps can be followed here

Set up Grafana dashboard

1. **In AWS EC2, create a launch template by uploading "user_data.sh" and then launch instance based on the launch template.**
   <img width="500" alt="Screenshot 2025-04-05 at 5 31 59 PM" src="https://github.com/user-attachments/assets/83ffab61-b648-45e8-9304-75e87e54a731" />
2. **Clone This Repo on the Cloud (if applicable).**
3. **Run `docker compose --profile backend up -d` to deploy all containers on the machine.**
4. **Go to port 3001 of your instance(make sure you have access to the ports) to set up Grafana.**


#### Automated Testing

We use **GitHub Actions** to automate testing. Since most of our work is on the backend (as the UI is provided by Grafana), we use **Postman** for API testing. Our tests can be categorized into two main groups:

-   Vantedge dashboard verification
-   Authentication (e.g., duplicate email, incorrect password etc.)
-   Alert functionality
 - Monitoring Service Verification
 	- Prometheus, Loki, Promtail, and Grafana containers are healthy
	-  The container responsible for collecting cloud usage and calculating cloud cost is healthy
	- The container running the sample test application is healthy

---
## Github Workflow
---

1. **Default Branches**

   * `main` : Active development branch where completed features are merged and tested.
   * `production`: Stable production-ready code only. This branch should always be clean and deployable.

2. **Branching Strategy**

   * Each developer should create branches for their work based on the task at hand and delete the branch after they have merged to the main branch.
   * Suggested naming conventions:
     * **Feature branches**: `{feature-name}` (for new features)
     * **Bug fix branches**: `bugfix/{description}`
     * **Hotfix branches**: `hotfix/{description}` (for urgent fixes directly from `main`)
     * **Release branches**: `Deliverable/{version}` (for final integration before merging to `main`)

3. **Commit Message Guidelines**

   * Use clear and descriptive commit messages:

   ```markdown
   [type]: Short description

   [type] examples: feat, fix, docs, refactor, chore
   ```

   For example:

   ```markdown
   feat: Add login feature with OAuth integration
   ```

4. **Pull Request (PR) Workflow**
   1. Open PRs early:
   Encourage developers to open PRs early to get feedback.
   2. Review requirements:
       * At least one reviewer must approve before merging.
       * PR titles should reflect changes and updates.
       * PR descriptions should include documentation updates and testing details.
   3. PR Template: Set up a PR template with sections for the feature description, testing steps, and any linked issues.

5. **Code Review Best Practices**
   * Assign a reviewer.
   * Focus on readability, maintainability, and functionality.
   * Use GitHub comments to discuss code issues.
   * Tag issues in PRs (e.g., closes #123).

6. **Continuous Integration (CI)**
   * CI/CD Setup: Use GitHub Actions for
     * Standardize the Pull Request Format
     * Automated test
     * Deployment pipelines

7. **Issue Tracking and Task Assignment**
   * Maintain several WhatsApp groups for different discussions.
   * Have a central group for setting reminders and pinning important information.
   * Assign developers to specific issues for clear task ownership.

8. **Weekly Sync**
   * Conduct bi-weekly sync-ups on Tuesdays and Fridays to review updates, PR status, blockers, and upcoming goals.
   * Schedule a weekly meeting with partners on Thursdays to discuss progress and prioritized items.

## Coding Standards and Guidelines

We follow the UofT CS department coding standard and guidelines as a reference:

* Start with function definitions with correct parameter/return types if applied
* Always start with the docstring which uses the parameter names to explain what the function does and returns.
* Name the parameters/functions with meaning, avoid meaningless/complicated naming.

For example:

```python
def fibonacci(n: int) -> int: 
  """
  Return the nth number of fibonacci sequence
  """
  # Implementation Omitted
```

## Contribution

1. Kenji Tan (tankenji): Project Manager & Fullstack Developer
2. ZeZheng Gu (JG-e): Fullstack Developer & DevOps
3. Wendy Wan (wennapengooin): Product Manager & Fullstack Developer
4. Xuerong (Snow) Zhou (kaixinrongzi): Fullstack Developer
5. Zixiu Meng (zixiumeng): Backend Developer
6. Alyssa Lu (lualyssa): Backend Developer
7. Jayson Camargo (Nzy4J): Frontend Developer

## Licenses

We will not be licensing our codebase as the agreement does not allow disclosure upon coding.
