# windhawk mod submitting

### Submission Checklist

1. Verify Your Mod Metadata

Your mod file already has:  

✓ @id (mic-switcher2)  
✓ @name (Mic Switcher)  
✓ @description  
✓ @version (1.0.1)  
✓ @github ([https://github.com/fadihajji1](https://github.com/BlackPaw21))  

2. Key Requirements for Submission:

- Your @github URL must match your GitHub profile **(you have this set)**
- The file must be named exactly: mods/mic-switcher2.wh.cpp ✓ **(already correct)**
- The Pull Request should **only** modify this single file

3. Create & Push Your Submission:

```
# Navigate to your repo
cd "c:\Users\CALLMEFAD\Desktop\windhawk mods\windhawk-mods"
# Create a new branch for your mod
git checkout -b add-mic-switcher2
# Stage your mod file
git add mods/mic-switcher2.wh.cpp
# Commit with a clear message
git commit -m "Add Mic Switcher to toggle between two preferred audio inputs."
# Push to your forked repo
git push origin add-mic-switcher2
```

4. Submit the Pull Request:

- Go to [https://github.com/ramensoftware/windhawk-mods](https://github.com/ramensoftware/windhawk-mods) (the original repo)  
- Click "New Pull Request" 
- IMPORTANT: click on **"compare across forks"** link
- Select your fork as the source branch (add-mic-switcher2)  
- Fill in the PR title: "Add Mic Switcher mod"  
- Verify it shows only mods/mic-switcher2.wh.cpp as the changed file  
- Submit!

5. What Happens Next:

The maintainers will review your mod  
They'll verify the @github field matches your account  
Once approved, your mod goes live on windhawk.net and is available in Windhawk.exe