# 🤖 Daily Open Source Contributor

Automated daily contributions to open-source projects using GitHub Actions. This bot searches for good first issues and documentation improvements across popular ML/Data Engineering repositories and posts helpful comments.

## 🎯 Features

- **Automated Daily Runs**: Executes every day at 9 AM UTC via GitHub Actions
- **Smart Issue Discovery**: Searches across 13+ major ML/Data Engineering repositories
- **Targeted Labels**: Focuses on "good first issue", "documentation", "help wanted", "beginner", and "easy" labels
- **Intelligent Comments**: Posts context-aware comments based on issue type
- **Contribution Logging**: Maintains a JSON log of all contributions
- **Rate Limit Aware**: Respects GitHub API limits and avoids duplicate comments

## 📦 Repositories Monitored

- Apache Airflow
- Apache Spark
- dbt-core
- TensorFlow
- PyTorch
- Pandas
- Scikit-learn
- Hugging Face Transformers
- MLflow
- Ray
- Dagster
- Prefect
- Great Expectations

## 🚀 Setup Instructions

### 1. Fork this Repository

Click the "Fork" button at the top right of this page.

### 2. Create a GitHub Personal Access Token (PAT)

1. Go to GitHub Settings → Developer settings → [Personal access tokens](https://github.com/settings/tokens)
2. Click "Generate new token" → "Generate new token (classic)"
3. Give it a descriptive name: `Daily Contributor Bot`
4. Set expiration (recommend: 90 days or No expiration)
5. Select scopes:
   - ✅ `repo` (Full control of private repositories)
   - ✅ `workflow` (Update GitHub Action workflows)
6. Click "Generate token"
7. **Copy the token** (you won't see it again!)

### 3. Add Token as Repository Secret

1. In your forked repository, go to Settings → Secrets and variables → Actions
2. Click "New repository secret"
3. Name: `GH_PAT`
4. Value: Paste your personal access token
5. Click "Add secret"

### 4. Enable GitHub Actions

1. Go to the "Actions" tab in your repository
2. Click "I understand my workflows, go ahead and enable them"

### 5. Manual Trigger (Optional)

To test immediately:

1. Go to Actions tab
2. Click "Daily Open Source Contribution" workflow
3. Click "Run workflow" → "Run workflow"

## ⚙️ Configuration

Edit `contribute.py` to customize:

```python
# Add/remove repositories
TARGET_REPOS = [
    "your-org/your-repo",
    # ... more repos
]

# Modify search labels
LABELS_TO_SEARCH = [
    "good first issue",
    # ... more labels
]
```

## 📅 Schedule

The workflow runs:
- **Automatically**: Every day at 9 AM UTC (1 AM PST)
- **Manually**: Via Actions tab "Run workflow" button

To change the schedule, edit `.github/workflows/daily-contribution.yml`:

```yaml
on:
  schedule:
    - cron: '0 9 * * *'  # Change this cron expression
```

## 📊 Monitoring

- **Actions Tab**: View workflow runs and logs
- **contributions.json**: Local log of all interactions (committed to repo)
- **Email Notifications**: GitHub sends emails on workflow failures

## 🛡️ Best Practices

1. **Be Respectful**: The bot posts genuine, helpful comments
2. **Avoid Spam**: Built-in duplicate detection prevents re-commenting
3. **Follow Up**: Manually respond to maintainer feedback
4. **Rate Limits**: Script respects GitHub API limits
5. **Token Security**: Never commit your PAT to the repository

## 📝 How It Works

1. **GitHub Actions** triggers the workflow daily
2. **Python script** authenticates with GitHub API using your PAT
3. **Issue search** finds open issues with target labels
4. **Smart filtering** excludes already-commented issues
5. **Comment posting** adds helpful, context-aware comments
6. **Logging** saves contribution data to `contributions.json`

## 🔧 Troubleshooting

### Workflow fails with "Error: GitHub token not found"
- Verify `GH_PAT` secret is set correctly in Settings → Secrets

### No issues found
- Repositories may not have issues with target labels
- Try expanding `TARGET_REPOS` or `LABELS_TO_SEARCH`

### Rate limit errors
- Wait for rate limit reset (check workflow logs)
- Reduce frequency in cron schedule

## 📄 License

MIT License - feel free to fork and customize!

## 🙏 Contributing

Contributions welcome! Open an issue or PR to:
- Add more repositories
- Improve comment templates
- Enhance issue filtering logic
- Add new features

---

**Built with ❤️ for the open-source community**
