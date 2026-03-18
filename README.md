# GitHub Actions Tutorial 02 - Events

A React-based tutorial project demonstrating GitHub Actions workflows and event triggers. This project showcases how different GitHub events can trigger automated workflows for testing, building, and deploying applications.

## 📋 Project Overview

This tutorial focuses on GitHub Actions **events** - the triggers that start your workflows. The project includes:

- **React Application**: A simple educational app about Git, GitHub, and GitHub Actions
- **GitHub Workflow**: Demonstrates multiple event triggers including push, pull requests, and manual dispatch
- **Automated Pipeline**: Shows a complete CI/CD pipeline with testing, building, and deployment steps

## 🚀 Features

- Interactive React UI with help sections about Git and GitHub
- Comprehensive test suite with Vitest
- ESLint code quality checks
- Vite-powered development and build process
- GitHub Actions workflow with multiple event triggers

## 🛠️ Technology Stack

- **Frontend**: React 18, Vite
- **Testing**: Vitest, Testing Library
- **Code Quality**: ESLint
- **CI/CD**: GitHub Actions
- **Package Manager**: npm

## 📦 Installation

1. **Clone the repository**:

   ```bash
   git clone <repository-url>
   cd gha-tutorial-02-events
   ```

2. **Install dependencies**:

   ```bash
   npm install
   ```

3. **Start the development server**:

   ```bash
   npm run dev
   ```

4. **Open your browser** and navigate to `http://localhost:5173`

## 🔧 Available Scripts

| Command           | Description                              |
| ----------------- | ---------------------------------------- |
| `npm run dev`     | Start development server with hot reload |
| `npm run build`   | Build the application for production     |
| `npm run preview` | Preview the production build locally     |
| `npm run test`    | Run the test suite                       |
| `npm run lint`    | Run ESLint and fix issues automatically  |

## ⚡ GitHub Actions Workflow

The project includes a GitHub Actions workflow (`.github/workflows/demo1.yml`) that demonstrates various **event triggers**:

### Event Triggers

1. **Push Events**: Triggers on any push to the repository

   ```yaml
   on:
     push:
   ```

2. **Pull Request Events**: Triggers specifically when a PR is opened

   ```yaml
   on:
     pull_request:
       types:
         - opened
   ```

3. **Manual Dispatch**: Allows manual workflow execution
   ```yaml
   on:
     workflow_dispatch:
   ```

### Workflow Steps

The workflow performs the following actions:

1. **Event Data Output**: Displays the complete GitHub event data
2. **Code Checkout**: Retrieves the repository code
3. **Dependency Installation**: Installs npm packages
4. **Testing**: Runs the test suite
5. **Building**: Creates production build
6. **Deployment**: Simulates deployment process

## 🎯 How to Trigger Each Event

### 1. Push Events

**Triggers**: Any push to any branch in the repository

**How to trigger**:

```bash
# Make any change to your code
echo "# Test change" >> README.md

# Commit and push the change
git add .
git commit -m "Test push event trigger"
git push origin main
```

**What happens**: The workflow runs immediately after the push completes.

### 2. Pull Request Events (opened)

**Triggers**: Only when a new pull request is **opened** (not updated, closed, or merged)

**How to trigger**:

```bash
# Create and switch to a new branch
git checkout -b feature/test-pr-event

# Make some changes
echo "// PR test change" >> src/App.jsx

# Commit and push the new branch
git add .
git commit -m "Add test change for PR"
git push origin feature/test-pr-event

# Create a pull request (via GitHub CLI)
gh pr create --title "Test PR Event" --body "Testing PR opened event trigger"
```

**Alternative via GitHub Web Interface**:

1. Navigate to your repository on GitHub
2. Click "Pull requests" tab
3. Click "New pull request"
4. Select your feature branch
5. Click "Create pull request"

**What happens**: The workflow runs only when the PR is first created, not on subsequent updates.

### 3. Manual Dispatch (workflow_dispatch)

**Triggers**: Manual execution through GitHub interface or API

**How to trigger via GitHub Web Interface**:

1. Go to your repository on GitHub
2. Click the "Actions" tab
3. Select "Events Demo 1" workflow from the left sidebar
4. Click "Run workflow" button (top right)
5. Select the branch to run on
6. Click "Run workflow"

**How to trigger via GitHub CLI**:

```bash
# Trigger the workflow on the main branch
gh workflow run "Events Demo 1" --ref main

# Check the status
gh run list --workflow="Events Demo 1"
```

**What happens**: The workflow runs immediately on the selected branch.

## 📚 Learning Objectives

This tutorial teaches you about:

- **GitHub Events**: Understanding different types of events that can trigger workflows
- **Event Types**: Filtering specific pull request types (opened, closed, etc.)
- **Multiple Triggers**: Combining different events in a single workflow
- **Event Context**: Accessing event data within workflow steps
- **CI/CD Pipeline**: Building a complete automated pipeline

## 🧪 Testing

The project includes comprehensive tests:

- **Component Tests**: Testing React components with Testing Library
- **Integration Tests**: Verifying component interactions
- **Automated Testing**: Tests run automatically in GitHub Actions

Run tests locally:

```bash
npm run test
```

## 🏗️ Project Structure

```
├── .github/
│   └── workflows/
│       └── demo1.yml          # GitHub Actions workflow
├── src/
│   ├── components/
│   │   ├── HelpArea.jsx       # Help section component
│   │   ├── HelpBox.jsx        # Individual help item
│   │   ├── MainContent.jsx    # Main app content
│   │   └── *.test.jsx         # Component tests
│   ├── App.jsx                # Root component
│   └── main.jsx               # Application entry point
├── package.json               # Dependencies and scripts
└── vite.config.js            # Vite configuration
```

## 🎯 Key Concepts Demonstrated

### 1. Event-Driven Workflows

Learn how GitHub Actions responds to repository events automatically.

### 2. Event Filtering

Understand how to filter specific event types (e.g., only PR opens, not closes).

### 3. Multiple Triggers

See how one workflow can respond to different types of events.

### 4. Event Context

Access detailed information about the triggering event in your workflow.

## 🔍 Workflow Event Data

The workflow outputs complete event data using:

```yaml
- name: Output event data
  run: echo "${{ toJSON(github.event) }}"
```

This helps you understand what information is available for different event types.
