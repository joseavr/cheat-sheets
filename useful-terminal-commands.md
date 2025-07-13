Generate a 32 length secret key. For db passwords or env variables passwords.
```bash
openssl rand -base64 32
# or
npx auth secret
```


RS256 secret
```
ssh-keygen -t rsa
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

Get Wifi password

```bash
security find-generic-password -wa "The Wifi Name"
security find-generic-password -wa "The Wifi Name" | pb copy # copy to clipboard
```

Delete history of downlaods store in the macos sql (even clean history in Chrome)

```bash
sqlite3 ~/Library/Preferences/com.apple.LaunchServices.QuarantineEventsV* 'delete from LSQuarantineEvent'
```


Get your IP address

```bash
ifconfig ne0 | grep inet
```

Open a server that can be accessed from any device
- To access go to: this-device-ip:8000

```bash
python3 -m http.server 8000 --bind 0.0.0.0 
```