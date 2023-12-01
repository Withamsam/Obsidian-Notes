---
creation date: November 6th 2022
last modified date: November 6th 2022
aliases: []
tags: #📕
---

Primary Categories: [[01 - Pentest]] - [[01 - Red Team]]
Secondary Categories:  [[02 - Reconnaissance]]
Links: [[Websites]] - [[Content Discovery]] - [[Sitemap.xml]]
Search Tag: #📕  

# [[Robots.txt]]  
___

## Description:  
When added to the path of a site i.e. `https://www.youtube.com/robots.txt` you will see a document that lists pages that aren't allowed to show on search engine results.

```
# robots.txt file for YouTube
# Created in the distant future (the year 2000) after
# the robotic uprising of the mid 90's which wiped out all humans.

User-agent: Mediapartners-Google*
Disallow:

User-agent: *
Disallow: /comment
Disallow: /get_video
Disallow: /get_video_info
Disallow: /get_midroll_info
Disallow: /live_chat
Disallow: /login
Disallow: /results
Disallow: /signup
Disallow: /t/terms
Disallow: /timedtext_video
Disallow: /verify_age
Disallow: /watch_ajax
Disallow: /watch_fragments_ajax
Disallow: /watch_popup
Disallow: /watch_queue_ajax

Sitemap: https://www.youtube.com/sitemaps/sitemap.xml
Sitemap: https://www.youtube.com/product/sitemap.xml
```


![[Pasted image 20221106014912.png]]



___

## Resources:

| Hyperlink | Info |
| --------- | ---- |


Created Date: November 6th 2022 (01:13 am)  
Last Modified Date: <%+tp.file.last_modified_date("MMMM Do YYYY (hh:ss a)")%>
