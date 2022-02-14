# Proxy Setting for Command Line Programs (CLI)
## Instruction
Some Command Line Programs doesn't use system proxy setting by default. You need to setup manually.  
Here suppose `172.16.0.33:1080` is your proxy server:

## SSH ([Doc](https://gist.github.com/coin8086/7228b177221f6db913933021ac33bb92#ssh-protocol))
Usage: Git command via SSH will need this.  
**Window**:  
`C:\Users\${YOUR_USER}\.ssh\config` (Create if not exist)  
```
Host github.com
  ProxyCommand "C:\Program Files\Git\mingw64\bin\connect.exe" -H 172.16.0.33:1080 %h %p
``` 

**macOS / Linux**:  
`~/.ssh/config` (Create if not exist)
```
Host github.com
  ProxyCommand nc -x 172.16.0.33:1080 %h %p
```

## Git ([Doc](https://gist.github.com/coin8086/7228b177221f6db913933021ac33bb92#httphttps-protocol))
Usage: Git command via http/https will need this.  
Set for specific host
```
-- Set
git config --global http.https://github.com.proxy http://172.16.0.33:1080

-- Unset
git config --global --unset http.https://github.com.proxy
```

Or edit `C:\Users\${YOUR_USER}\.gitconfig` on Windows, `~/.gitconfig` on macOS or Linux manually
```
[http "https://github.com"]
        proxy = http://172.16.0.33:1080
```

## NPM ([Doc](https://docs.npmjs.com/cli/v7/using-npm/config#https-proxy))
Usage: For `npm install` to download packages from NPM registry.
Note that some packages will have dependencies that are from GitHub via either https or SSH, that will need Git and SSH proxy above.
```
-- Set
npm config set https-proxy http://172.16.0.33:1080
npm config set proxy http://172.16.0.33:1080
-- Bypass internal registry, can't use proxy
npm config set noproxy npm.neulion.net.cn

-- Unset
npm config rm https-proxy
npm config rm proxy
```

Or edit `C:\Users\${YOUR_USER}\.npmrc` on Windows, `~/.npmrc` on macOS or Linux manually
```
https-proxy=http://172.16.0.33:1080/
proxy=http://172.16.0.33:1080/
noproxy=npm.neulion.net.cn
```

## Mac Terminal
```
export https_proxy="http://172.16.0.33:1080"
```
Only affect current window
