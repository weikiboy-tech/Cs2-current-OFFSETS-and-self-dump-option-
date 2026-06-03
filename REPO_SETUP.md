# CS2 Current OFFSETS and Self-Dump Option — GitHub Setup

## 1) GitHub repository create (CLI)

```powershell
# Install gh cli once
winget install --id GitHub.cli

gh auth login
gh repo create cs2-current-offsets-and-self-dump-option --description "CS2 current OFFSETS and self dump option" --public
```

## 2) Link local repo (run in your project root)

```powershell
git remote remove origin
git remote add origin https://github.com/<your-github-username>/cs2-current-offsets-and-self-dump-option.git
git branch -M main
```

## 3) Initial commit + push

```powershell
git add .
git commit -m "feat: initial professional cs2 current offsets + self-dump option setup"
git push -u origin main
```

## 4) Optional release tags

```powershell
git tag -a v1.0.0 -m "Initial release"
git push --tags
```

## 5) Verify workflow

Actions -> Release/CI should run and publish artifacts on the first tag push.
