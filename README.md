# rpi-manifests
Contains the dependencies for the yocto build

## Installing and Using Repo Tool

### Prerequisites
- Python 3.6 or later
- Git

### Installing Repo on Ubuntu

```bash
sudo apt update
sudo apt install repo
```

### Using Repo with this manifest

1. **Create a new directory for your project:**
   ```bash
   mkdir rpi-yocto-build
   cd rpi-yocto-build
   ```

2. **Initialize repo with this manifest:**
   ```bash
   repo init -u https://github.com/ivrabie/rpi-manifests.git -b main -m rpi-manifest.xml
   ```

3. **Sync all repositories:**
   ```bash
   repo sync
   ```

4. **To update all repositories to latest versions:**
   ```bash
   repo sync
   ```

### Common Repo Commands

- `repo status` - Show status of all projects
- `repo diff` - Show differences in all projects
- `repo forall -c 'command'` - Run a command in all project directories
- `repo start <branch-name>` - Start a new branch in all projects
- `repo upload` - Upload changes for review (if using Gerrit)

### Troubleshooting

If you encounter permission issues during installation, make sure:
- The repo binary is executable: `chmod +x ~/bin/repo`
- Your PATH includes the bin directory: `echo $PATH`
- You have proper Git configuration: `git config --global user.name "Your Name"` and `git config --global user.email "your.email@example.com"`
