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
* [Project Features](#project-features)
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
This project builds a reproducible end-to-end pipeline to train a binary image classifier that detects whether an image contains Saint George (positive) or not (negative). Using two provided image archives (one per class), the pipeline covers data preparation, augmentation, model training, evaluation, experiment tracking, and artifact storage so others can reproduce results quickly.

The main goal is to maximize model quality (accuracy, precision, recall, F1) through practical techniques including transfer learning (e.g., EfficientNet/ResNet), data augmentation and class balancing, hyperparameter tuning, mixed precision training, learning-rate scheduling, early stopping, and optional ensembling. Evaluation will include confusion matrices, example misclassifications, and a clear final metrics report.

---
## Project Features
---
**Data ingestion and organization**: 
Loaders to extract/validate images from the two archives, directory sanitization, and automated train/validation/test split with stratification.

**Data preprocessing & augmentation**:
Resizing, normalization, label encoding, and configurable augmentations (random flip/rotation, color jitter, cutout/mixup/cutmix, lighting transforms) with easy on/off settings.

**Model architectures**:
configurable use of pretrained backbones (EfficientNet, ResNet, Vision Transformers) with customizable classifier heads.

**Training pipeline**:
Training loop with gradient accumulation, validation, and early stopping.

**Loss & metrics**:
Binary cross-entropy, and real-time logging of accuracy, precision, recall, F1 on epoch-levels.

**Experiment tracking & logging**:
Integrated logging via logging module with automatic saving of best parameters for each model.

**Hyperparameter tuning**:
For each model, hyperparameters are fine-tuned based on learning rates and weight decay rates using grids. The best hyparameters are selected based on the validation results.

**Evaluation & analysis tools**:
Confusion matrix and some misclassification with explainations.

**Inference & Deployment**:
The model inferences are executed within the Colab notebook solely for evaluation and experimentation, without deploying the model. However, this feature will be added in the soon future.

**Reproducibility**
Colab environment has been set up for reproducibility

---
## Instructions
---
Here are the instructions for using your Colab setup effectively:

---

### Overview:
This Colab notebook leverages the power of Google's extensive GPU infrastructure, making it ideal for users with limited local GPU resources. It is fully cross-platform, allowing anyone to run the code regardless of their operating system. The notebook provides real-time logs and print outputs, making monitoring and debugging straightforward without the need for tedious save operations involving I/O,thus streamlining your workflow.

**How to Use:**  
1. **Start by running cells one by one:**  
   Click on each cell and execute sequentially to initialize your environment, load data, and run your analysis. This step-by-step approach ensures smooth execution and easy debugging. Please note that the design follows established software design patterns and architecture principles, ensuring that dependencies are installed and loaded in the correct order within the environment. This structured approach helps maintain modularity, reproducibility, and clarity throughout the development process.

2. **Clear Cache When Necessary:**  
   If you encounter memory issues or need to reset the environment, manually clear the cache by using the "Runtime" menu → "Factory reset runtime" or by restarting runtime via **Runtime > Restart runtime**. This will free up memory and allow for fresh execution.

3. **Monitor Outputs in Real-Time:**  
   All logs, print statements, and outputs are shown immediately below each executed cell. Use this to monitor your progress, debug, and verify intermediate results on the fly.

4. **Save Outputs Manually:**  
   The outputs, such as trained models, results, or important logs, can be copied directly from the output cells and saved on your local device at your convenience. This manual save process is encouraged as it allows you to select and store critical data selectively, providing flexibility over automated saving.

**Feel free to follow these steps for a smooth and efficient experience while leveraging Colab’s powerful environment.**

### Architecture:
<img src="deliverables/D3/Images/SignIn.png" alt="Alt Text" width="600"/>

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
