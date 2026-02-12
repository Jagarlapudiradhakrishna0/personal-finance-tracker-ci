# Personal Finance Tracker - CI Pipeline

A modular Personal Finance Tracker application with automated CI/CD pipeline using GitHub Actions.

## Project Structure

```
personal-finance-tracker/
├── dashboard/          # Dashboard module
├── expenses/           # Expenses module
├── income/             # Income module
├── .github/workflows/  # GitHub Actions workflows
└── build-all.js        # Root build script
```

## Features

- **Modular Architecture**: Separate modules for Dashboard, Expenses, and Income
- **Independent Testing**: Each module has its own test suite with Jest
- **Parallel CI Pipeline**: Tests run in parallel for all modules with Node.js versions 18 and 20
- **Conditional Build**: The build job only runs if all test jobs pass successfully
- **Artifact Storage**: Test results are stored as CI artifacts for later review

## Local Testing

### Run Dashboard Tests
```bash
cd dashboard
npm test
```

### Run Expenses Tests
```bash
cd expenses
npm test
```

### Run Income Tests
```bash
cd income
npm test
```

### Build All Modules
```bash
npm run build
```

## GitHub Actions Workflow

The CI pipeline (`.github/workflows/ci.yml`) is configured to:

1. **Test Dashboard** (Matrix: Node 18, 20)
   - Installs dependencies
   - Runs Jest tests
   - Uploads artifacts

2. **Test Expenses** (Matrix: Node 18, 20)
   - Installs dependencies
   - Runs Jest tests
   - Uploads artifacts

3. **Test Income** (Matrix: Node 18, 20)
   - Installs dependencies
   - Runs Jest tests
   - Uploads artifacts

4. **Build Application** (Conditional - runs only after all tests pass)
   - Builds all modules
   - Runs the build-all script
   - Uploads build artifacts

## How to Push to GitHub

1. **Create a new repository on GitHub**:
   - Go to [github.com/new](https://github.com/new)
   - Name: `personal-finance-tracker-ci`
   - Click "Create repository"

2. **Push your code**:
   ```bash
   cd personal-finance-tracker
   git remote add origin https://github.com/<YOUR_USERNAME>/personal-finance-tracker-ci.git
   git push -u origin main
   ```

   Replace `<YOUR_USERNAME>` with your actual GitHub username.

3. **Verify the CI Pipeline**:
   - Navigate to your repository on GitHub
   - Click the "Actions" tab
   - You should see your workflow running
   - All three test jobs will run in parallel
   - After all tests pass, the build job will execute

## Workflow Runs

Each push or pull request will trigger the workflow with:
- Dashboard tests (2 versions: Node 18, 20) = 2 jobs
- Expenses tests (2 versions: Node 18, 20) = 2 jobs
- Income tests (2 versions: Node 18, 20) = 2 jobs
- Build job (runs only after all 6 test jobs pass) = 1 job

Total: 7 parallel/sequential jobs per workflow run

## Test Results

All test results and artifacts are automatically uploaded to GitHub Actions and can be downloaded from the workflow run summary.

## Dependencies

- Node.js 18 and 20
- Jest (for unit testing)
