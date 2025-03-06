# GIT

0. Install git
```bash
yum install git
git version
```
1. Initialize a git repo
```bash
git init
```

2. Configure Files to Track
```bash
git status

git add LICENSE README.md main.py .......
```

3. Git Tracks Changes
```bash
git status          #
```

4. Stage Changes
```bash
git add main.py
```

5. Commit Changes
```bash
git commit -m "Initial Commit"
```

6. Add remote repo
```bash
git remote add <name> <url>

git remote add github https://github.com/ribesh/my-app.git
```

7. Push code to remote repo
```bash
git push <name> <branch>

git push -u github master
```

Clone
```bash
git clone https://github.com/ribesh/my-app.git
```

More commands
```bash
git remote -v
git pull
```