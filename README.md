# .github

GitHub Actions Workflow Templates Repository

## Overview

This repository provides reusable GitHub Actions workflow templates for .NET projects. These templates are based on best practices and include comprehensive CI/CD, testing, validation, and maintenance workflows.

## Available Templates

### 1. 🏗️ .NET CI/CD Pipeline (`dotnet-ci-cd.yml`)

A comprehensive CI/CD pipeline that includes:
- **Build & Test**: Automated building and testing with detailed test reporting
- **Code Quality Analysis**: Static code analysis and formatting checks
- **Security Scan**: Vulnerability and deprecated package detection
- **Build Status**: Comprehensive pipeline summary with all job statuses

**Triggers**: Push to main/develop, Pull requests, Manual dispatch

### 2. ✅ .NET PR Validation (`dotnet-pr-validation.yml`)

Automated pull request validation with:
- Complete build and test execution
- PR title validation (semantic commit format)
- Automatic labeling based on file changes
- PR size analysis and labeling

**Triggers**: Pull request events (opened, synchronize, reopened)

### 3. 🚀 .NET Release (`dotnet-release.yml`)

Automated release workflow featuring:
- Build and test validation
- Application publishing
- Artifact creation and compression
- Automatic changelog generation
- GitHub release creation with artifacts

**Triggers**: Version tags (v*.*.*), Manual dispatch

### 4. 🔧 Repository Maintenance (`maintenance.yml`)

Scheduled maintenance tasks:
- Outdated package detection and reporting
- Old cache cleanup (>7 days)
- Stale issue and PR management

**Triggers**: Weekly schedule (Sunday 2 AM), Manual dispatch

### 5. 🐛 .NET Test Debugging (`dotnet-test-debug.yml`)

Manual test debugging workflow with:
- Configurable test filters
- Adjustable verbosity levels (quiet to diagnostic)
- Code coverage collection
- Detailed test reporting

**Triggers**: Manual dispatch only

## Usage

### Using Templates in Your Repository

1. **Navigate to Actions**: Go to your repository's "Actions" tab
2. **New Workflow**: Click "New workflow"
3. **Choose Template**: Browse and select one of the available templates
4. **Configure**: Update the environment variables to match your project:

```yaml
env:
  DOTNET_VERSION: '8.0.x'           # Your .NET version
  SOLUTION_PATH: 'YourSolution.sln' # Path to your solution file
  TEST_PROJECT: 'YourProject.Test/YourProject.Test.csproj' # Path to test project
```

### Configuration Requirements

#### For PR Validation Template
If using the auto-labeling feature, create a `.github/labeler.yml` file:

```yaml
'area/docs':
  - '**/*.md'
  
'area/tests':
  - 'test/**/*'
  - '**/*.Test/**/*'
  
'area/ci':
  - '.github/**/*'
```

#### For Release Template
For automatic changelog generation, create `.github/changelog-config.json`:

```json
{
  "categories": [
    {
      "title": "## 🚀 Features",
      "labels": ["feat", "feature"]
    },
    {
      "title": "## 🐛 Bug Fixes",
      "labels": ["fix", "bug"]
    },
    {
      "title": "## 📚 Documentation",
      "labels": ["docs"]
    }
  ]
}
```

## Template Customization

### Common Customizations

1. **Change .NET Version**: Update `DOTNET_VERSION` environment variable
2. **Adjust Triggers**: Modify the `on:` section to match your branching strategy
3. **Add/Remove Jobs**: Customize the pipeline by adding or removing job sections
4. **Modify Test Settings**: Adjust test verbosity, filters, and reporting options

### Example: Custom Branch Names

```yaml
on:
  push:
    branches: [ master, staging, production ]
  pull_request:
    branches: [ master, staging ]
```

## Features

### 📊 Rich Test Reporting
- Detailed test summaries with pass/fail counts
- Failed test details with error messages
- Test result artifacts for historical analysis

### 🔒 Security First
- Automated vulnerability scanning
- Deprecated package detection
- Security-focused code analysis

### 🎨 Beautiful GitHub Summaries
- Emoji-rich status reports
- Markdown-formatted summaries
- Clear visual indicators for success/failure

### ⚡ Performance Optimized
- Dependency caching
- Parallel job execution where possible
- Incremental build support

## Best Practices

1. **Start with CI/CD**: Implement the CI/CD pipeline first to establish baseline quality
2. **Add PR Validation**: Protect your branches with PR validation requirements
3. **Semantic Commits**: Use conventional commit messages for better changelog generation
4. **Regular Maintenance**: Enable the maintenance workflow to keep dependencies updated
5. **Label Your PRs**: Use consistent labeling for better organization and changelog generation

## Support

For issues or questions about these templates:
1. Check the workflow run logs for detailed error information
2. Ensure all required configuration files are present
3. Verify environment variables match your project structure

## Contributing

To update these templates:
1. Make changes to the workflow files in `workflow-templates/`
2. Update corresponding `.properties.json` files if metadata changes
3. Update this README with any new features or requirements
4. Test templates in a sample repository before committing

## License

These templates are provided as-is for use in paz-dev-com projects.
