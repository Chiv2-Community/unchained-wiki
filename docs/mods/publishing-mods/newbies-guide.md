# Publishing Your Mod to the launcher registry

This guide explains how to publish your mod to the mod registry that is used by the launcher, making it easily discoverable by Chivalry 2 players using the Unchained Launcher.

Publishing is done via github, so git and github.com will be used as part of this process. There is a lot that can be done with git, and it is an extremely useful tool for making changes to things without losing older versions. This guide will only use surface level git functionality, but there are many features it has that may help you maintain your mod.

## Table of Contents
- [Publishing Your Mod to the launcher registry](#publishing-your-mod-to-the-launcher-registry)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Step 1: Install Git](#step-1-install-git)
    - [Installing Git](#installing-git)
    - [Verify Installation](#verify-installation)
  - [Step 2: Set Up Your Mod Locally](#step-2-set-up-your-mod-locally)
    - [Initialize Git Repository](#initialize-git-repository)
    - [Configure Git](#configure-git)
    - [Add Your Mod Files](#add-your-mod-files)
  - [Step 3: Create a GitHub Repository](#step-3-create-a-github-repository)
  - [Step 4: Connect Local Repository to GitHub](#step-4-connect-local-repository-to-github)
  - [Step 5: Prepare Your Mod Configuration](#step-5-prepare-your-mod-configuration)
  - [Step 6: Create a GitHub Release](#step-6-create-a-github-release)
  - [Step 7: Submit Your Mod to C2ModRegistry](#step-7-submit-your-mod-to-c2modregistry)
  - [Step 8: Wait for Approval](#step-8-wait-for-approval)
- [Publishing Updates to Your Mod](#publishing-updates-to-your-mod)
- [Tips for a Successful Submission](#tips-for-a-successful-submission)
- [Troubleshooting](#troubleshooting)


## Prerequisites

Before you begin, make sure you have:

1. Completed your mod and have it ready for distribution
2. A [GitHub](https://github.com) account

## Step 1: Install Git

Before creating a GitHub repository, you need to install Git and set up your mod files locally. This approach allows you to version control your files and ensures a smoother upload process.

### Installing Git

1. Download Git from [https://git-scm.com/downloads](https://git-scm.com/downloads)
2. Choose your operating system (Windows, macOS, or Linux) and download the installer
3. Run the installer

### Verify Installation

Open a Command Prompt and type:
```bat
git --version
```
If Git is installed correctly, you'll see the version number.

## Step 2: Set Up Your Mod Locally

### Initialize Git Repository

1. Open a terminal/command prompt
2. Navigate to your mod's root directory using the `cd` command. For example:
   ```bat
   cd C:\Path\To\ArgonSDK\Content\Mods
   ```

3. Initialize Git in this directory:
   ```bat
   git init
   ```
   This creates an empty Git repository

### Configure Git

If this is your first time using Git, set up your identity:
```bat
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```
Use the same email you use for your GitHub account.

### Add Your Mod Files

1. Make sure all your mod files are in the directory
2. Create the `mod.json` file in the root directory (details below)
3. Add all files to Git tracking:
   ```bat
   git add .
   ```
   The dot (.) means "add all files in the current directory"

4. Create your first commit:
   ```bat
   git commit -m "Initial commit of my mod"
   ```

## Step 3: Create a GitHub Repository

First, you'll need to create a GitHub repository to host your mod:

1. Log in to your GitHub account
2. Click the "+" icon in the top-right corner and select "New repository"
3. Name your repository (ideally something that clearly identifies your mod)
4. Add a description for your mod if you wish. This is the description that would show on github.com (not the launcher)
5. Make sure the repository is set to public
6. Leave all other boxes unchecked. Do not add a README, .gitignore, or license. We will do that in a later step.
7. Click "Create repository"

## Step 4: Connect Local Repository to GitHub

After creating your GitHub repository (following instructions from Step 3), you'll be taken to a page with setup instructions. Since you've already initialized Git locally, follow these steps:

1. On the GitHub repository page, copy the repository URL (ends with .git)
2. In your terminal, connect your local repository to GitHub:
   ```bat
   git remote add origin https://github.com/$yourusername/$your-repo-name.git
   ```
3. Push your local commits to GitHub:
   ```bat
   git branch -M main
   git push -u origin main
   ```

## Step 5: Prepare Your Mod Configuration

Create or update the `mod.json` file at the root of your repository. You have two options:

### Option 1: Use the mod.json Generator (Recommended)

💡 **[Use our mod.json generator](../../mod-json-generator.md)** for an interactive way to create your mod.json file! Simply fill in the fields and it will generate a properly formatted file for you.

### Option 2: Create Manually

If you prefer to create the file manually, use the following structure:

```json
{
  "name": "Your Mod Name",
  "description": "A short description of your mod",
  "mod_type": "Client",  
  "authors": ["Your Name"],
  "dependencies": [
    {
      "repo_url": "https://github.com/Chiv2-Community/Unchained-Mods",
      "version": "0.1.0"  
    }
  ],
  "tags": ["Weapon"] 
}
```

**Available mod_type values:**
- `Client`: Client-side mods that only affect the player's game
- `Server`: Server-side mods that need to be installed on the server
- `Shared`: Mods that have both client and server components

*Note: The values are case-sensitive and use PascalCase.*

**Available tags:**
- `Mutator`: Gameplay-altering modifications
- `Map`: Map/level mods
- `Cosmetic`: Visual modifications and skins
- `Audio`: Sound effects and music modifications
- `Model`: 3D model replacements or additions
- `Weapon`: Weapon mods
- `Doodad`: Some kind of functionality that extends the game
- `Library`: Framework or library mods for other mods to use

*Note: The values are case-sensitive and use PascalCase.*

## Step 6: Create a GitHub Release

1. Once your mod files and `mod.json` are committed to your repository, navigate to your repository on GitHub
2. Click on "Releases" in the right sidebar
3. Click "Create a new release"
4. Enter a tag version (e.g., "v1.0.0") following semantic versioning
5. Add a title for your release
6. Provide release notes describing what your mod does and any important information
7. Upload your mod file as a `.pak` file (make sure it's a single file)
8. Click "Publish release"

## Step 7: Submit Your Mod to C2ModRegistry

Now that your mod is hosted on GitHub with a proper release, you need to submit it to the C2ModRegistry:

1. Go to the [C2ModRegistry repository](https://github.com/Chiv2-Community/C2ModRegistry)
2. Navigate to the "Issues" tab
3. Click "New issue"
4. Select the "Add Package" issue template 
5. Fill out the required information:

```json
{
  "action": "add_package",
  "repo_url": "https://github.com/yourusername/your-mod-repo",
}
```

6. Submit the issue

## Step 8: Wait for Approval

The C2ModRegistry maintainers will review your submission. If everything is correctly set up, your mod will be added to the registry and become available to all Chivalry 2 Unchained users through the mod launcher.

# Publishing Updates to Your Mod

When you want to publish an update to your mod:

1. Update your mod files in your local directory
2. Use Git to stage and commit your changes:
   ```bat
   git add .
   git commit -m "Description of changes"
   ```
3. Push the changes to GitHub:
   ```bat
   git push
   ```
4. Create a new release on GitHub with an increased version number (e.g., "v1.0.1")
5. Create a new issue on the C2ModRegistry repository:
   - Go to the [C2ModRegistry repository](https://github.com/Chiv2-Community/C2ModRegistry)
   - Navigate to the "Issues" tab
   - Click "New issue"
   - Select the "Add Release" issue template (if available)
   - Fill out the required information with your updated release tag:
   ```json
   {
     "action": "add_package_release",
     "repo_url": "https://github.com/yourusername/your-mod-repo",
     "release_tag": "v1.0.1"
   }
   ```
   - Submit the issue
6. Wait for approval

# Tips for a Successful Submission

- Ensure your `mod.json` file is correctly formatted and contains all required fields
- Make sure your mod is packaged correctly as a single `.pak` file
- Provide clear and detailed information about your mod in the release notes
- Choose appropriate tags to help users find your mod
- Test your mod thoroughly before submission to ensure it works properly

# Troubleshooting

If your submission is rejected or you encounter issues:

- Check that your `mod.json` file is correctly formatted
- Verify that your release contains the necessary files
- Ensure that all dependencies are correctly specified
- Review any feedback from the moderators in your issue
- Join the [Chivalry 2 Unchained Discord](https://discord.gg/chiv2unchained) for community support

---

By following these steps, you can successfully publish your mod to the C2ModRegistry and share it with the Chivalry 2 Unchained community.