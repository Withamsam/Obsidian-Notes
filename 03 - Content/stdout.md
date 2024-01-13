---
creation date: January 13th 2024 (12:07 am)
last modified date: January 13th 2024 (12:07 am)
aliases: []
tags: 📖
---
 
Primary Categories: 
Secondary Categories:  
Links: [[stderr]]
# [[stdout]]  
**Standard Output**(stdout) is as it sounds the standard output for programs. Not all programs use this though and sometimes we need to redirect streams.


## Output Redirection
### stdout -> file
```bash
ls -l > ls.txt
```

### stdout -> stderr
```bash
grep da * 1>&2
```

### stdout -> null
```
grep da * >/dev/null
```

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


