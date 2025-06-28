# Flask Python App on AWS Elastic Beanstalk

This project is a simple Flask application deployed on AWS Elastic Beanstalk, with support for multiple environments (dev & prod), Git-based deployments.

---

## 🚀 Project Structure

```

flask_python_advantage/
├── app.py # Flask app (must contain `application = Flask(...)`)
├── requirements.txt # Python dependencies
├── templates/
│ └── index.html # HTML page rendered by Flask
├── .ebextensions/
│ └── deploy.config # Deployment strategy configuration (optional)
└── .gitignore # Optional Git ignore list

```

---

## 📦 Setup & Deploy

### 1. Initialize Git

```bash
git init
git add .
git commit -m "Initial commit"
```

### 2. Initialize Elastic Beanstalk

```bash
eb init
```

- Region: `eu-west-3` (Paris)
- Platform: `Python 3.12`
- CodeCommit: `n`

---

## 🌱 Create Environments

### Dev Environment

```bash
eb create dev-env --instance_type t3.micro --envvars STAGE=dev
```

### Prod Environment

```bash
eb create prod-env --instance_type t3.micro --envvars STAGE=prod
```

---

## 🔀 Switch Between Environments

```bash
eb use dev-env   # to deploy to dev
eb use prod-env  # to deploy to production
```

---

## 🚀 Deploy

```bash
git add .
git commit -m "Your commit message"
eb deploy
```

To control batch size, use `.ebextensions/deploy.config`.

Example `.ebextensions/deploy.config`:

```yaml
option_settings:
  aws:elasticbeanstalk:command:
    DeploymentPolicy: Rolling
    BatchSizeType: Percentage
    BatchSize: 50
```

---

## 🛠️ Logs & Troubleshooting

```bash
eb logs --all
eb ssh
cat /var/log/eb-engine.log
```

## 🔗 Open App in Browser

```bash
eb open
```

Bien sûr ! Voici uniquement la section demandée en **Markdown**, propre et prête à copier dans ton `README.md` :

## 💥 Terminate an Environment (destroy)

```bash
eb terminate dev-env
eb terminate prod-env
```

⚠️ This will **delete the environment completely** (use with caution).

## 🛠️ Add OS-level packages

Create a file `.ebextensions/packages.config`:

```yaml
packages:
  yum:
    git: []
    curl: []
```

This installs OS-level packages on the EC2 instances that Elastic Beanstalk uses.
