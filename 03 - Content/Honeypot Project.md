---
creation date: November 13th 2023
last modified date: November 13th 2023
aliases: []
tags: #📖
---

Primary Categories: 
Secondary Categories:  
Links: 
Search Tag: #📖  

# [[Honeypot Project]]  

# Blog Written

Welcome! In an effort to learn more about both Microsoft Azure & Sentinel I went looking for a project. I have found that for myself I can read documentation all day but without the implementation the information fades. 

# Used Code
## KQL
- Written in KQL (Kusto Query Language)
- The following is for RDP
```q
FAILED_RDP_WITH_GEO_CL
|extend username = extract(@"username:([^,]+)", 1, RawData),
         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
         latitude = extract(@"latitude:([^,]+)", 1, RawData),
         longitude = extract(@"longitude:([^,]+)", 1, RawData),
         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
         state = extract(@"state:([^,]+)", 1, RawData),
         label = extract(@"label:([^,]+)", 1, RawData),
         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
         country = extract(@"country:([^,]+)", 1, RawData),
         isp = extract(@"ISP:([^\s-]+(?:\s+[^\s-]+)*)", 1, RawData)
 |where destination != "samplehost"
 |where sourcehost != ""
 |where sourcehost != "YOUR IP HERE"
 |summarize event_count=count() by timestamp, label, country, state, sourcehost, username, destination, longitude, latitude, isp
```


- The following is for FTP
```q
FAILED_FTP_WITH_GEO_CL
|extend latitude = extract(@"latitude:([^,]+)", 1, RawData),
        longitude = extract(@"longitude:([^,]+)", 1, RawData),
        sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
        state = extract(@"state:([^,]+)", 1, RawData),
        country = extract(@"country:([^,]+)", 1, RawData),
        timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
        label = extract(@"label:([^,]+)", 1, RawData),
        isp = extract(@"ISP:([^\s-]+(?:\s+[^\s-]+)*)", 1, RawData)
|where sourcehost != "sample"
|where sourcehost != "YOUR IP HERE"
|summarize event_count=count() by latitude, longitude, sourcehost, state, country, timestamp, isp, label
```

- Changes made to ISP regex in order to correctly pull its input while ignoring the IP that comes along with it and getting rid of the space that would come between the final word and the "-"
	- This space was causing issues with mapping the data as it was counting the ones without the space at the end as a new entry even though they should be the same since we are only grouping by ISP not by IP for this section
```
csharpCopy code

`isp = extract(@"ISP:([^\s-]+(?:\s+[^\s-]+)*)", 1, RawData)`

Let's break down the changes:

1. `([^\s-]+)`: This part captures the first word of the ISP name, ensuring that it doesn't include spaces or hyphens.
    
2. `(?:\s+[^\s-]+)*`: This part handles the optional additional words in the ISP name, separated by spaces. `(?: ... )` is a non-capturing group, and `\s+` allows for one or more whitespace characters.
    

By incorporating `\s*` (zero or more whitespace characters) into the regex, you allow for the possibility of trailing spaces after the final word.

This modification should help handle cases where there's an extra space after the final word in the ISP information. However, keep in mind that the effectiveness of this solution depends on the variations in your raw data. If you encounter other patterns or unexpected variations, you may need to adjust the regular expression accordingly.
```



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 13th 2023 (05:08 pm)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
