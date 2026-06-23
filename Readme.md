# 🚗 Vehicle Insurance MLOps Project

An end-to-end **Machine Learning Operations (MLOps)** project for predicting vehicle insurance outcomes using a complete production-grade pipeline.

The project covers:

* 📊 Data Ingestion from MongoDB Atlas
* ✅ Data Validation
* 🔄 Data Transformation
* 🤖 Model Training
* 📈 Model Evaluation
* ☁️ AWS S3 Model Registry
* 🐳 Docker Containerization
* 🔄 CI/CD with GitHub Actions
* 🚀 Deployment on AWS EC2
* 🌐 Prediction Web Application

---

# 📂 Project Architecture

```bash
vehicle-insurance/
│
├── artifact/
├── notebook/
├── src/
│   ├── components/
│   ├── configuration/
│   ├── constants/
│   ├── data_access/
│   ├── entity/
│   ├── exception/
│   ├── logger/
│   ├── pipeline/
│   ├── aws_storage/
│   └── utils/
│
├── static/
├── templates/
├── .github/workflows/
├── app.py
├── demo.py
├── requirements.txt
├── setup.py
├── pyproject.toml
└── README.md
```

---

# 🔄 Complete Workflow

```text
MongoDB Atlas
      │
      ▼
Data Ingestion
      │
      ▼
Data Validation
      │
      ▼
Data Transformation
      │
      ▼
Model Training
      │
      ▼
Model Evaluation
      │
      ▼
AWS S3 Model Registry
      │
      ▼
Prediction Pipeline
      │
      ▼
Flask Application
      │
      ▼
Docker + CI/CD
      │
      ▼
AWS EC2 Deployment
```

---

# ⚙️ Project Setup

## 1️⃣ Create Project Template

Run:

```bash
python template.py
```

This will generate the complete project folder structure.

---

## 2️⃣ Configure Local Package Installation

Update:

```text
setup.py
pyproject.toml
```

to enable importing local packages throughout the project.

---

## 3️⃣ Create Virtual Environment

### Using Conda

```bash
conda create -n vehicle python=3.10 -y
conda activate vehicle
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Verify installation:

```bash
pip list
```

---

# 🍃 MongoDB Atlas Setup

## Create Database

1. Create MongoDB Atlas Account
2. Create New Project
3. Create M0 Free Cluster
4. Create Database User
5. Configure Network Access

Allow:

```text
0.0.0.0/0
```

6. Copy Python Connection String

Example:

```text
mongodb+srv://username:password@cluster.mongodb.net/
```

---

## Upload Dataset to MongoDB

Create notebook:

```bash
notebook/mongoDB_demo.ipynb
```

Load dataset and push records into MongoDB.

Verify data:

```text
MongoDB Atlas
   ↓
Database
   ↓
Browse Collections
```

---

# 📝 Logging & Exception Handling

## Logger

Create:

```bash
src/logger/
```

Test:

```bash
python demo.py
```

---

## Custom Exception

Create:

```bash
src/exception/
```

Test:

```bash
python demo.py
```

---

# 📥 Data Ingestion

### Components

```text
constants
configuration
data_access
entity
components
pipeline
```

Responsibilities:

* Connect MongoDB Atlas
* Fetch records
* Convert records into DataFrame
* Split train/test data
* Save artifacts

---

## MongoDB Environment Variable

### Bash

```bash
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net/"
```

Check:

```bash
echo $MONGODB_URL
```

---

### PowerShell

```powershell
$env:MONGODB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net/"
```

Check:

```powershell
echo $env:MONGODB_URL
```

---

# ✅ Data Validation

Purpose:

* Schema Validation
* Missing Columns Check
* Data Drift Detection
* Data Quality Verification

Files:

```text
config/schema.yaml
utils/main_utils.py
```

---

# 🔄 Data Transformation

Tasks:

* Missing Value Handling
* Feature Engineering
* Encoding
* Scaling
* Feature Selection

Artifacts Generated:

```text
preprocessor.pkl
train.npy
test.npy
```

---

# 🤖 Model Training

Models are trained using transformed data.

Outputs:

```text
trained_model.pkl
metric_artifact
```

Responsibilities:

* Model Selection
* Hyperparameter Tuning
* Best Model Selection

---

# 📊 Model Evaluation

The newly trained model is compared against the production model stored in AWS S3.

Threshold:

```python
MODEL_EVALUATION_CHANGED_THRESHOLD_SCORE = 0.02
```

If performance improves:

```text
Accept New Model
```

Else:

```text
Reject New Model
```

---

# ☁️ AWS Configuration

## Create IAM User

```text
IAM → Create User
```

Name:

```text
firstproj
```

Permission:

```text
AdministratorAccess
```

Generate:

```text
Access Key
Secret Key
```

---

## Set Environment Variables

### Bash

```bash
export AWS_ACCESS_KEY_ID="YOUR_KEY"
export AWS_SECRET_ACCESS_KEY="YOUR_SECRET"
```

### PowerShell

```powershell
$env:AWS_ACCESS_KEY_ID="YOUR_KEY"
$env:AWS_SECRET_ACCESS_KEY="YOUR_SECRET"
```

---

# 🪣 AWS S3 Model Registry

Create bucket:

```text
my-model-mlopsproj
```

Constants:

```python
MODEL_BUCKET_NAME = "my-model-mlopsproj"
MODEL_PUSHER_S3_KEY = "model-registry"
```

Purpose:

* Store Production Models
* Version Control Models
* Model Retrieval

---

# 🔮 Prediction Pipeline

Responsible for:

* Loading latest production model
* Accepting user input
* Returning prediction

Structure:

```text
Prediction Pipeline
      │
      ▼
Preprocessor
      │
      ▼
Model
      │
      ▼
Prediction
```

---

# 🌐 Web Application

Launch:

```bash
python app.py
```

Access:

```text
http://localhost:5000
```

Routes:

```text
/
```

Home Page

```text
/vehicledata
```

Prediction Form

```text
/training
```

Model Training Trigger

---

# 🐳 Docker Setup

Build Image:

```bash
docker build -t vehicle-project .
```

Run Container:

```bash
docker run -p 5080:5000 vehicle-project
```

---

# 🔄 GitHub Actions CI/CD

Create:

```text
.github/workflows/aws.yaml
```

Pipeline:

```text
Code Push
     │
     ▼
GitHub Action
     │
     ▼
Docker Build
     │
     ▼
Push to ECR
     │
     ▼
Deploy on EC2
```

---

# 📦 AWS ECR Setup

Repository:

```text
vehicleproj
```

Stores Docker Images.

---

# 🚀 EC2 Deployment

Launch:

```text
Ubuntu 24.04
t2.medium
30 GB Storage
```

Install Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

Verify:

```bash
docker --version
```

---

# 🔗 Self Hosted GitHub Runner

GitHub:

```text
Settings
 → Actions
 → Runners
 → New Self Hosted Runner
```

Run all provided commands on EC2.

Start Runner:

```bash
./run.sh
```

Runner Status:

```text
Idle
```

---

# 🔐 GitHub Secrets

Add the following secrets:

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO
```

---

# 🌍 Production Deployment

Open EC2 Security Group.

Add inbound rule:

```text
Type: Custom TCP
Port: 5080
Source: 0.0.0.0/0
```

Access Application:

```text
http://<EC2_PUBLIC_IP>:5080
```

---

# 🛠️ Tech Stack

### Machine Learning

* Scikit-Learn
* Pandas
* NumPy

### Database

* MongoDB Atlas

### Cloud

* AWS S3
* AWS ECR
* AWS EC2

### MLOps

* GitHub Actions
* Docker
* CI/CD

### Backend

* Flask

### Development

* Python 3.10
* Conda

---

# 🎯 Project Workflow

```text
constants
    ↓
config_entity
    ↓
artifact_entity
    ↓
components
    ↓
pipeline
    ↓
app.py / demo.py
```

---

# 👨‍💻 Author

**Prashant Kumar**

B.Tech Artificial Intelligence | Machine Learning Engineer | MLOps Enthusiast

---

⭐ If you found this project useful, don't forget to star the repository.
