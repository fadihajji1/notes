# bun istallation

### Powershell:

- `powershell -c "irm bun.sh/install.ps1|iex"`     
- **Add to system path**:

```
[System.Environment]::SetEnvironmentVariable("Path",[System.Environment]::GetEnvironmentVariable("Path", "User") + ";$env:USERPROFILE\.bun\bin",[System.EnvironmentVariableTarget]::User)
```

OR---

```
[Environment]::SetEnvironmentVariable("Path",$env:Path + ";$HOME\.bun\bin","User")
```

- **restart pc**

 