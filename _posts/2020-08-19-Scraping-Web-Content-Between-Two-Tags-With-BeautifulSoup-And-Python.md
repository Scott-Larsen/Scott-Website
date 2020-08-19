---
layout: post
title: Scraping Text between Two Tags with BeautifulSoup
---

Putting this here in case I need it in the future and because there wasn't much information online about how to grab the text between two tags with Beautiful Soup and Python. I think it's difficult to find a solution because most of the people who are searching for something similar can benefit from semantic/ nested HTML and just back up one layer and get `children` or `next_sibling`, etc. 

It seems straightforward enough, all I wanted to do was to pull the text contained within `<H2>` tags as a variable name and assign it any text that followed, up to the next set of `<H2>` tags. The problem I faced is that the website I'm scraping didn't do a good job of implementing semantic/ nested HTML so the tags between sets of `<H2>` tags could be any combination of other tags and unscrapable using built in BS4 commands.

Here's an example of what I was trying to scrape:
```
<H2>Job Property 1</H2>
    <ul>
        <li>Some text</li>
        <li>Some more text</li>
    </ul>
<H2>Job Property 2</H2>
    <p>Some more text</p>
<H2>Job Property 3</H2>
    Some more text</br>
``` 
What I ended up with is largely based on [Zrog's](https://stackoverflow.com/users/6454584/zroq) answer to a [question on StackOverflow](https://stackoverflow.com/questions/42820342/get-text-in-between-two-h2-headers-using-beautifulsoup) so they deserve most of the credit. I suspect there's a better way around this so please offer any feedback you have so we can get the best info out there.

    ```
    jobDetails = soup.find("div", class_="job-description")
    jobDescription = {}
    for header in jobDetails.find_all('h2'):
        jobDetail = header.get_text().strip()
        nextNode = header
        jobDetailText = []
        while True:
            nextNode = nextNode.nextSibling
            # This writes out the last of the H2 tags and its following contents
            if not nextNode:
                jobDescription[jobDetail] = "\n".join(jobDetailText)
                break
            # This adds non-H2 tags to the text to attach to the text of the H2
            elif isinstance(nextNode, NavigableString):
                if nextNode.strip():
                    jobDetailText.append(nextNode.strip())
                    pass
            # This detects the next H2 and writes the compiled text to the previous H2
            elif isinstance(nextNode, Tag):
                if nextNode.name == "h2":
                    jobDescription[jobDetail] = "\n".join(jobDetailText)
                    break
                jobDetailText.append(nextNode.get_text(strip=True))
                ```
