# final-project-error-502
final-project-error-502 created by GitHub Classroom

# Catastrophic Backtracking

Analyzing news coverage differences between traditional server failures and AI-related outages.



Group members: Zehan Li, Simmons Yin, Brttany An

## Project Structure

```
├── data/           # Raw and processed datasets
├── scripts/        # Data collection and analysis code
└── visualizations/ # Figures and plots
```

## Team & Responsibilities

| Member   | Role                                    |
| -------- | --------------------------------------- |
| Brittany | Repository owner, Data collection,Visualizations |
| Zehan    | Data cleaning, Sentiment Analysis, Visualization |
| Simmons  | NLP preprocessing, Sentiment analysis   |

## Collaboration Workflow

We use a **Fork and Pull Request** workflow to ensure code quality through reviews.

### Setup (One-time)

1. **Brittany** maintains the upstream repository

2. **Zehan & Simmons** fork the repo to their own GitHub accounts

3. Clone your fork locally:

   ```bash
   git clone https://github.com/<YOUR_USERNAME>/catastrophic-backtracking.gitcd catastrophic-backtracking
   ```

4. Add upstream remote:

   ```bash
   git remote add upstream https://github.com/brittany/catastrophic-backtracking.git
   ```

### Development Cycle

1. **Before starting new work**, sync your fork with upstream:

   ```bash
   git fetch upstream
   git checkout main
   git merge upstream/main
   git push origin main
   ```

2. **Create a feature branch** for your work:

   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Commit and push** to your fork:

   ```bash
   git add .
   git commit -m "descriptive commit message"
   git push origin feature/your-feature-name
   ```

4. **Open a Pull Request** to upstream `main` branch

5. **Address review feedback**, then merge after approval

### Code Review Assignments

| PR Author | Reviewer(s)     |
| --------- | --------------- |
| Zehan     | Brittany        |
| Simmons   | Zehan, Brittany |
| Brittany  | Zehan, Simmons  |

## Getting Started

```bash
# Install dependencies
pip install -r requirements.txt

# Set up API credentials (see .env.example)
cp .env.example .env
```

