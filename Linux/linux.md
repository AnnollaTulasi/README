**Authentication**
1. What you know -- Username + Password
2. What you have -- Username + token/OTP
3. What you are -- Fingerpints,retina

```
ssh-keygen -f <file_name>  generates public and private key
```
~ -> Home directory

public keys contains ssh-rsa or ssh-ed at the beginning

* The public key created can in added in keypair in AWS (Import Key pair)
* To connect to server we should have IP,Username,passwort,protocol,port
* we should be in the folder where the key is present (relative path) or can can give the absolute path(entire path)
* [$] --> normal user
* [#] --> root
* uname --> Kernel name
* [-] --> for a character
* [--] --> for word
eg: -h or --help

/ is the root directory in linux
* to enter root directory in linux ,cd / is the cmd to be used