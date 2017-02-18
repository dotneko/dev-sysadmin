# Linux

```
sha1sum <filename>
sha256 <filename>
sha512sum <filename>
md5 <filename>
```

# Windows
-
```
certutil -hashfile <filename>               # By default checks with sha1
certutil -hashfile <filename> <algorithm>   # Can specify algorithm
certutil -hashfile <filename> md5           # Checks with md5 algorithm
```
- More info: [MS TechNet CertUtil](https://technet.microsoft.com/en-us/library/cc732443(v=ws.11).aspx)
