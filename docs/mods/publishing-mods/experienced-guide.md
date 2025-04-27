# Publishing Mods - GitHub Experienced Users Guide

This streamlined guide is for developers already familiar with Git and GitHub who want to publish their mods to the Chivalry 2 mod registry.

## Quick Start

1. Create a GitHub repository with your mod files. The root of your mod should be the root of the repo.
2. Add a properly formatted `mod.json` at the root
3. Create a GitHub release with your mod `.pak` file
4. Submit your repository URL to C2ModRegistry via an issue

## mod.json Structure

💡 **[Use the mod.json generator](../../mod-json-generator.md)** for an interactive way to create your mod.json file!

Place this at your repository root:

```json
{
  "repo_url": "https://github.com/yourusername/your-mod-repo",
  "name": "Your Mod Name",
  "description": "A short description of your mod",
  "home_page": "https://yourdocsite.com",  // Optional
  "image_url": "https://example.com/mod-image.png",  // Optional
  "mod_type": "Client",  // Client, Server, or Shared
  "authors": ["Your Name"],
  "dependencies": [
    {
      "repo_url": "https://github.com/Chiv2-Community/Unchained-Mods",
      "version": "0.1.0"  
    } // Add any other required mods as dependencies
  ],
  "tags": ["Weapon"],  // Mutator, Map, Cosmetic, Audio, Model, Weapon, Doodad, Library
  "maps": [],  // List of maps this mod provides (if any)
  "options": {
    "actor_mod": false  // Set to true if your mod affects actors
  }
}
```

**mod_type values** (PascalCase):
- `Client`: Client-side only
- `Server`: Server-side only
- `Shared`: Client and server components

**tag options** (PascalCase):
- `Mutator`: Gameplay modifications
- `Map`: Levels/maps
- `Cosmetic`: Visual mods
- `Audio`: Sound/music
- `Model`: 3D models
- `Weapon`: Weapon mods
- `Doodad`: Game extensions
- `Library`: Frameworks/libraries

## Publishing a new mod 

### 1. Repository Setup

```bash
# Initialize repo with mod files and mod.json
git init
git add .
git commit -m "Initial mod commit"
git remote add origin https://github.com/username/mod-name.git
git push -u origin main
```

### 2. Create Release

1. Tag your release following semver: `git tag v1.0.0`
2. Push tag: `git push origin v1.0.0`
3. Go to GitHub releases
4. Create release from tag
5. Attach your .pak file
6. Publish release

### 3. Submit to C2ModRegistry

1. Go to [C2ModRegistry Issues](https://github.com/Chiv2-Community/C2ModRegistry/issues)
2. Create new issue with "Add Package" template
3. Submit:
   ```json
   {
     "action": "add_package",
     "repo_url": "https://github.com/yourusername/your-mod-repo"
   }
   ```

## Publishing Updates

For updates:
1. Commit changes and create new tag
2. Create new GitHub release
3. Submit new issue to C2ModRegistry:
   ```json
   {
     "action": "add_package_release",
     "repo_url": "https://github.com/yourusername/your-mod-repo",
     "release_tag": "v1.0.1"
   }
   ```

## Best Practices

1. **Versioning**: Follow semantic versioning (MAJOR.MINOR.PATCH)
2. **Release Notes**: Include detailed changelogs
3. **Dependencies**: Keep dependency versions updated
4. **Testing**: Test mods before release

## Common Issues

1. **Invalid mod.json**: Ensure proper JSON formatting and required fields
2. **Missing release asset**: Attach .pak file to GitHub release
3. **Wrong mod_type**: Choose appropriate type based on mod functionality
4. **Dependency versions**: Specify exact dependency versions

## Registry API

The mod registry uses these actions:
- `add_package`: Add new mod to registry
- `add_package_release`: Add new version of existing mod

For advanced automation, you can create scripts to interact with the registry API via GitHub issues.

## Support
- Discord: Join the [Chivalry 2 Unchained server](https://discord.gg/chiv2unchained) for help
- Issues: Report problems on C2ModRegistry repository
- Updates: Watch C2ModRegistry for registry format changes