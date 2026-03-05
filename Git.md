# Git

Git local setup

  Configure your Git identity locally to use it only for this project:

```
`git config --local user.name "fadi hajji"`

`git config --local user.email "fedihajji1@gmail.com"`
```

HTTPS

 Create a new repository

`git clone https://gitlab.com/fedihajji1/quizspring.git`

```
`cd quizspring`

`git switch --create main`

`git add README.md`

`git commit -m "add README"`

`git push --set-upstream origin main`
```

 Push an existing folder

   Go to your folder

```
`cd existing_folder`
```

   Configure the Git repository

`git init --initial-branch=main --object-format=sha1`

```
`git remote add origin https://gitlab.com/fedihajji1/quizspring.git`

`git add .`

`git commit -m "Initial commit"`

`git push --set-upstream origin main`
```

Push an existing Git repository

  Go to your repository

```
`cd existing_repo`
```

  Configure the Git repository

`git remote rename origin old-origin`

```
`git remote add origin https://gitlab.com/fedihajji1/quizspring.git`

`git push --set-upstream origin --all`

`git push --set-upstream origin --tags`
```

 