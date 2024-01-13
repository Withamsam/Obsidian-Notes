---
creation date: January 13th 2024 (12:37 am)
last modified date: January 13th 2024 (12:37 am)
aliases: []
tags: 📖
---
 
Primary Categories: 
Secondary Categories:  
Links: [[stdout]]
# [[stderr]]  
**Standard error**(stderr) is an output stream that is usually used by programs to output error messages or diagnostics.

This is represented by `2>` if we want to redirect the stream to another file or stream shown below.

- A few programs use this as the default out though such as:
	- [[Netcat]]


## Output Redirection
### stderr -> file
```bash
grep da * 2> errors.txt
```

### stderr -> stdout
```bash
grep * 2>&1
```

### stderr -> null
```bash
grep da * 2>/dev/null
```

___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


