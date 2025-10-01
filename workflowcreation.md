# GitHub Actions Workflow Creation Prompt

## Objective
Create a comprehensive GitHub Actions workflow that automates the process of linting, building, and deploying a React application to GitHub Pages.

## Requirements

### Workflow Overview
Create a GitHub Actions workflow file (`.github/workflows/ci-cd.yml`) that performs the following tasks:
1. **Linting**: Check code quality and enforce coding standards
2. **Building**: Build the React application for production
3. **Deployment**: Deploy the built application to GitHub Pages

## Workflow Specifications

### 1. Trigger Configuration
The workflow should be triggered on:
- Push events to the `main` branch
- Pull request events targeting the `main` branch
- Manual workflow dispatch (for manual triggering from GitHub UI)

### 2. Environment Setup
- Use the latest Ubuntu runner
- Set up Node.js environment (version 18.x or later)
- Cache npm dependencies for faster builds
- Install project dependencies

### 3. Linting Stage
**Purpose**: Ensure code quality and consistency

**Tasks**:
- Run ESLint to check JavaScript/React code
- Check for code style violations
- Validate formatting (using Prettier if configured)
- Fail the workflow if linting errors are found
- Display linting results in the workflow logs

**Implementation**:
- Add a job named `lint`
- Run `npm run lint` or `npm run eslint`
- Configure to run on all triggers (push, PR, manual)
- Should complete before proceeding to build stage

### 4. Building Stage
**Purpose**: Compile and build the React application for production

**Tasks**:
- Build the React application using `npm run build`
- Optimize assets for production
- Generate production-ready static files
- Verify build completes successfully
- Upload build artifacts for deployment stage

**Implementation**:
- Add a job named `build`
- Depend on successful completion of `lint` job
- Run `npm run build`
- Upload the `build` or `dist` folder as an artifact
- Set appropriate artifact retention period

### 5. Deployment Stage
**Purpose**: Deploy the built application to GitHub Pages

**Tasks**:
- Download the build artifacts from the build stage
- Deploy to GitHub Pages
- Make the application accessible at `https://<username>.github.io/<repository-name>`
- Only deploy on successful builds from the `main` branch

**Implementation**:
- Add a job named `deploy`
- Depend on successful completion of `build` job
- Only run on push to `main` branch (not on PRs)
- Use the official GitHub Pages deployment action
- Configure proper permissions for GitHub Pages deployment

## Workflow Structure

### Complete Workflow Configuration

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
      - name: Setup Node.js
      - name: Cache dependencies
      - name: Install dependencies
      - name: Run linting

  build:
    needs: lint
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
      - name: Setup Node.js
      - name: Cache dependencies
      - name: Install dependencies
      - name: Build application
      - name: Upload build artifacts

  deploy:
    needs: build
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Download build artifacts
      - name: Setup GitHub Pages
      - name: Upload to GitHub Pages
      - name: Deploy to GitHub Pages
```

## Technical Requirements

### 1. Node.js Setup
- Use `actions/setup-node@v4`
- Specify Node.js version (18.x or 20.x)
- Enable dependency caching with `cache: 'npm'`

### 2. Dependency Management
- Use `npm ci` for clean, reproducible installs
- Cache `node_modules` to speed up subsequent runs
- Ensure `package-lock.json` is committed to the repository

### 3. Linting Configuration
- Ensure `lint` script exists in `package.json`
- Configure ESLint with React-specific rules
- Add `.eslintrc.json` or similar config file
- Include `.eslintignore` for files to skip

### 4. Build Configuration
- Ensure `build` script exists in `package.json`
- Configure build output directory (`build` or `dist`)
- Set correct base URL for GitHub Pages in build config
- Handle environment variables if needed

### 5. GitHub Pages Deployment
- Use `actions/upload-pages-artifact@v3`
- Use `actions/deploy-pages@v4`
- Configure repository settings for GitHub Pages:
  - Enable GitHub Pages in repository settings
  - Set source to "GitHub Actions"
  - Configure custom domain if applicable

### 6. Security and Permissions
- Use minimal required permissions
- Set `contents: read` for code checkout
- Set `pages: write` for GitHub Pages deployment
- Set `id-token: write` for authentication

## Additional Features

### Optional Enhancements
1. **Test Stage**: Add a testing stage before build
2. **Code Coverage**: Generate and upload coverage reports
3. **Build Matrix**: Test on multiple Node.js versions
4. **Notifications**: Send notifications on workflow failures
5. **Environment Variables**: Use GitHub Secrets for sensitive data
6. **Deployment Preview**: Deploy PRs to preview environments
7. **Rollback**: Implement versioning and rollback capabilities

### Error Handling
- Ensure each stage has clear failure messages
- Use `continue-on-error: false` for critical stages
- Add timeout limits to prevent hanging jobs
- Implement retry logic for flaky operations

## Expected Deliverables

1. **Workflow File**: `.github/workflows/ci-cd.yml` with all stages configured
2. **Documentation**: README section explaining the CI/CD pipeline
3. **Configuration Files**:
   - `.eslintrc.json` (ESLint configuration)
   - `.eslintignore` (files to ignore during linting)
   - Updated `package.json` with required scripts
4. **GitHub Pages Configuration**: Repository settings configured for deployment
5. **Working Pipeline**: Workflow successfully runs on push/PR and deploys to GitHub Pages

## Validation Checklist
- [ ] Workflow triggers correctly on push to main
- [ ] Workflow triggers correctly on pull requests
- [ ] Manual workflow dispatch works
- [ ] Linting stage runs and reports errors correctly
- [ ] Build stage produces production-ready artifacts
- [ ] Deployment stage only runs on main branch pushes
- [ ] Application is accessible on GitHub Pages after deployment
- [ ] Workflow fails appropriately on errors
- [ ] Dependencies are cached for faster runs
- [ ] All jobs complete within reasonable time limits

## Notes
- Ensure `homepage` field in `package.json` is set correctly for GitHub Pages
- Configure React Router with `basename` if using client-side routing
- Test the workflow thoroughly with both successful and failing scenarios
- Monitor GitHub Actions usage to stay within free tier limits
- Keep workflow files under version control and review changes carefully
