<% "---" %>
tags: journal/weeklynote
id: journal-<% tp.file.title %>
week: <% tp.file.title %>
aliases: 
Mood:  
Why: 
banner: https://i.imgur.com/RvNY9BJ.png
banner_y: 0.8
banner_icon: 📅
created_at: <% tp.file.creation_date('YYYY-MM-DD[T]HH:mm:ssZ') %>
modified_at: <% tp.file.last_modified_date('YYYY-MM-DD[T]HH:mm:ssZ') %>
<% "---" %>

↑ `$=dv.pages().where(b => b.id == 'journal-<% tp.date.now("MMMM, YYYY",0, tp.file.title, "gggg-[W]ww") %>')[0].file.link`
<-<- [[<% tp.date.now("gggg-[W]ww","P-1W", tp.file.title, "gggg-[W]ww") %>]] <- <% tp.file.title %> -> [[<% tp.date.now("gggg-[W]ww","P+1W", tp.file.title, "gggg-[W]ww") %>]] ->->
M [[<% tp.date.weekday("YYYY-MM-DD", 0, tp.file.title, "gggg-[W]ww") %>|<% tp.date.weekday("DD", 0, tp.file.title, "gggg-[W]ww") %>]] • T [[<% tp.date.weekday("YYYY-MM-DD", 1, tp.file.title, "gggg-[W]ww") %>|<% tp.date.weekday("DD", 1, tp.file.title, "gggg-[W]ww") %>]] • W [[<% tp.date.weekday("YYYY-MM-DD", 2, tp.file.title, "gggg-[W]ww") %>|<% tp.date.weekday("DD", 2, tp.file.title, "gggg-[W]ww") %>]] • T [[<% tp.date.weekday("YYYY-MM-DD", 3, tp.file.title, "gggg-[W]ww") %>|<% tp.date.weekday("DD", 3, tp.file.title, "gggg-[W]ww") %>]] • F [[<% tp.date.weekday("YYYY-MM-DD", 4, tp.file.title, "gggg-[W]ww") %>|<% tp.date.weekday("DD", 4, tp.file.title, "gggg-[W]ww") %>]] • S [[<% tp.date.weekday("YYYY-MM-DD", 5, tp.file.title, "gggg-[W]ww") %>|<% tp.date.weekday("DD", 5, tp.file.title, "gggg-[W]ww") %>]] • S [[<% tp.date.weekday("YYYY-MM-DD", 6, tp.file.title, "gggg-[W]ww") %>|<% tp.date.weekday("DD", 6, tp.file.title, "gggg-[W]ww") %>]]

<% tp.web.daily_quote() %>

---

> [!info]+ Mood
> ```meta-bind
> INPUT[progressBar(minValue(0), maxValue(10)):Mood]
> ```
>  **Why:** `INPUT[text:why]`

>[!tip]+ Health
> ```meta-bind
> INPUT[progressBar(minValue(0), maxValue(10)):Health]
> ```

---

## What is worth remembering about this week?
- 

## What am I grateful for this week, and what am I thinking of?
- 

## What did I set to achieve this week?
- 

## What did I accomplish this week?
- 

## What could I have done better? What are my regrets?
- 

## What I want to achieve next week?
- 
