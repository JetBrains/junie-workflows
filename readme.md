# 🤖 Junie — Your AI Coding Assistant

Hey there! 👋 Meet Junie, your friendly AI coding assistant that works right inside your GitHub repository!

## 🌟 About

Junie is a smart coding buddy that can help you with various programming tasks. Here's what makes Junie special:

### 🎯 Autonomous Task Handling
Just tell Junie what you need, and it'll figure out everything else! It automatically analyzes your project structure and uses the IDE to understand the context.

### 💡 Smart Code Generation
Junie leverages the IntelliJ Platform to ensure the code it generates is top-notch. It'll keep tweaking until the code meets the highest quality standards.

### 🤝 Your Coding Partner
Need help with complex stuff? Junie's got your back! It can write tests, run code, and fix bugs. The more you interact with Junie, the better it gets at understanding your needs.

Want to try Junie in your IDE? Check out our [IntelliJ Plugin](https://plugins.jetbrains.com/plugin/26104-jetbrains-junie)!

## 🚀 How to Use

Getting started is super easy! Junie works out the box in a private or internal GitHub repository under the JetBrains organization. For any other repository please leave a message in `#play-with-fire` channel
1. Make sure that the following GitHub Repository settings are enabled  
Settings → Actions → General → Workflow permissions → Read and write permissions ✅  
Settings → Actions → General → Allow GitHub Actions to create and approve pull requests ✅
2. Add file `.github/workflows/ej-issue.yml`
```yaml
name: Junie

on:
  issues:
    types: [opened]
  issue_comment:
    types: [created]
  pull_request_review_comment:
    types: [created]

jobs:
  junie:
    uses: JetBrains/junie-workflows/.github/workflows/ej-issue.yml@main
```

### 🎮 Three Ways to Use Junie:

1. **Via GitHub Issues**
   - Create an issue with `[junie]` in the title
   - Describe your task in the body (Markdown supported!)
   - No file attachments or images yet, but we're working on it!

2. **Fix Specific Code in PRs**
   - Add a review comment to any line of code
   - Start your comment with `junie: fix`
   - Junie will commit the fix directly to your PR branch

3. **Fix All PR Comments**
   - Comment on the PR (not in the review mode!) with exactly `junie: fix all`
   - Junie will address all review comments at once
   - Changes will be pushed to your PR branch

You can find examples of how to use Junie in the [demo repository](https://github.com/JetBrains/junie-demo).

## ❓ FAQ
### 💬 Where can I leave feedback?
Join us in the `#play-with-fire` Slack channel!

### Do I need to request any access or tokens?
Junie GH workflows work out of the box in any JetBrains repository. For access to repositories outside JetBrains leave a message in the `#play-with-fire` channel.

### Can I use it in Space repositories?
Unfortunately, no. Junie GH workflows work only on GitHub for now.
But you can mirror your Space repository to GitHub and use it there.

### 🔒 Security: Can Junie break my repository?
Nope! Junie only has the permissions it absolutely needs through GitHub Actions. Here's what it can do:
```yaml
permissions:
  contents: write # For pushing commits
  pull-requests: write # For creating PRs
  packages: read # For downloading Junie's docker image
```
Check out GitHub's [permissions documentation](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/controlling-permissions-for-github_token) for more details.

### 🛠️ Technical Questions

**Which tech stacks are supported?**
Since Junie runs on IntelliJ IDEA Ultimate, it works best with Java/Kotlin applications. On other tech stacks it might not has all usefull code inspections, but still can use all powers of LLM and IntelliJ IDEA.

**Python support?**
While our [IntelliJ plugin](https://plugins.jetbrains.com/plugin/26104-jetbrains-junie) works great with Python, the GitHub Actions implementation is still being optimized. Soon we will add more specializations images for different tech stacks.

**Can I customize the workflow?**
Absolutely! You can create your own GitHub workflow — just copy the `Run junie plugin` step and use our Docker image: `ghcr.io/jetbrains/junie_workflows/amd64-idea-ej:latest`. Check out the existing workflow for implementation details.
