# Git

#### **Git local setup**

  Configure your Git identity locally to use it only for this project:

```
`git config --local user.name "fadi hajji"`

`git config --local user.email "fedihajji1@gmail.com"`
```

---

#### **clone project**

`git clone https://github.com/fadihajji1/Recouvra.git`

---

#### **…or create a new repository on the command line**

```
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/fadihajji1/test.git
git push -u origin main
```

#### **…or push an existing repository from the command line**

```
git remote add origin https://github.com/fadihajji1/test.git
git branch -M main
git push -u origin main
```

---

---

---

### **pull changes:**

1. **If you don’t have the repo yet (first time)**

```
#clone project
    git clone https://github.com/fadihajji1/Recouvra.git
#Then go into the folder:
    cd Recouvra
#Then switch to master (if needed):
    git checkout -b master
```

```
#pull the latest changes from the master branch
    git pull origin master
#resolve conflicts in files
    git add .
    git commit -m "resolve merge conflict"
    git push origin master
```

2. **If the repo already exists locally**

```
     cd Recouvra
#Then pull from master:
     git pull origin master
```

---

### Fix the conflict manually after pull request

1. **when you encounter this:**

```
<<<<<<< HEAD
your local code
=======
incoming code from origin/master
>>>>>>> origin/master
```

2. **accept or decline changes in each file**

# or

1. **in bash command:**

- `--ours` → keeps **your local changes**
- `--theirs` → keeps **remote repository changes**

#### ****Keep local version for a specific file**

```
#keep local version for specific file     
     git checkout --ours app.js
     git add app.js
#keep all local version     
     git checkout --ours .
     git add .
     git commit -m "Keep local changes"
```

#### ****Keep remote version instead (for comparison)**

```
#keep Remote version for specific file
     git checkout --theirs app.js
     git add app.js
#or keep all Remote version
     git checkout --theirs .
     git add .
     git commit -m "Keep remote changes"
```

```
#push NEW changes
     git push origin master
```

```
git push -f origin master
```

---

 