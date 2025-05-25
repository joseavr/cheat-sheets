# Node Version Manager (NVM)

Check the current version

```bash
node -v
```

Check all releases or only the latest LTS
```bash
nvm ls-remote --lts

// only the latest LTS
nvm ls-remote --lts | tail -n 1
```

Check node version installed by nvm
```bash
nvm list
```

Use specific node version
```bash
nvm use [version]
```

Install version
```bash
nvm install [version]
```

Set default Node version
```bash
nvm alias default [version]
```


Install latest LTS version of Node using nvm
```bash
nvm install --lts
```

