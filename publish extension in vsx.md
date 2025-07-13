# VSX

Vsx Registry is an open source VS Code marketplace that host extensions.

Cursos uses VSX instead of the Microsoft Marketplace to install extension.

**Skip Step 3 and 4** if already created an account in Eclipse Foundation and logged in on your terminal to vsx.

## 1. Install Open VSX publishing tool

```bash
npm install -g ovsx 
```

## 2. Build `.vsix` package 

(Optional) Install `vsce` to create `.vsix`
```bash
npm install -g vsce
```

Run

```bash
node esbuild.js --production
# or
vsce package
```

This will create `your-extension.vsix`


## 3. Create Account at open-vsx.org
- Go to open-vsx.org and create account
- Create an account at [Eclipse Foundation](https://auth.eclipse.org/realms/community/protocol/openid-connect/auth?client_id=drupal_accounts&response_type=code&scope=openid%20email%20profile&redirect_uri=https%3A//accounts.eclipse.org/openid-connect/auth_eclipse_org) . Needed for signing terms for publishing and link with Github Account 
- Go back to open-vsx.org, go to publish -> profile, then sign Eclipse Foundation Open VSX Publisher Agreement 
- Create a Namespace, which is your publisher name. Go to publish -> namespaces. Follow the links to create your namespace. Here direct link to claim your namespace and be verified [link](github.com/EclipseFdn/open-vsx.org) 
- Wait to be approved 

## 4.  Authenticate via CLI to VSX 
- Go to open-vsx.org -> publish -> access token
- Create a new token
- Save token

Authenticate via CLI:

```bash
ovsx login <vsx-login-name> 
```

Then it wil ask your token, paste your token.

Should get a message like this:
- 🚀  PAT valid to publish at joseavr



## 5. Publish your extension

Run command

```bash
ovsx publish
```


## ✅ Notes for Success

Make sure publisher in your package.json matches the Open VSX publisher name.

Your extension's GitHub repo must be public.

Recommended: Include a README.md and CHANGELOG.md.

# VSCE

Vscode Marketplace from Microsoft


Check out if you are logged in first

```bash
vsce ls-publishers
```

If not then go to step 1
## 1. Renew token

- Go to https://dev.azure.com/publisher-name/_usersSettings/tokens
- Click to create a new token
- Give full permission

Then login 
```bash
vsce login <publisher-name>
```

Then override to create a new token
```bash
Do you want to overwrite its PAT? [y/N]
> y
```

## 2. Publish Extension

Edit the package.json by upgrading the version

Then publish

```bash
vsce publish
```


Check your published extension in the marketplace: https://marketplace.visualstudio.com/manage/publishers/<publisher-name>


