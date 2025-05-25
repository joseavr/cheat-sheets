Generate a 32 length secret key. For db passwords or env variables passwords.
```bash
openssl rand -base64 32

npx auth secret
```


Check node.js vulnerability
```bash
npx is-my-node-vulnerable
```


View latest version of a packcage
```bash
npm view [package-name@version] version 
```

View peerDepedencies of a npm package
```bash
npm info [package-name@version] peerDependencies
```


Check outdated npm packages
```bash
npm outdated
```