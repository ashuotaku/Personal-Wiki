<% "---" %>
<%* let aliases = await tp.system.prompt('Enter the sentence of the day:') 
tR += "aliases: " + aliases %>
id: journal-<% tp.file.title %>
tags: journal/dailynote
Mood: 
Why: 
Meditation: false
Exercise: false
Study: 
Ultradian_Cycles: 
banner: https://i.imgur.com/hxMd3z1.jpg
banner_icon: 📅
banner_y: 0.68
created_at: <% tp.file.creation_date() %>
modified_at: <% tp.file.last_modified_date() %>
date: <% tp.file.title %>
<% "---" %>

↑ `$=dv.pages().where(b => b.id == 'journal-<% tp.date.now("gggg-[W]ww",0, tp.file.title, "YYYY-MM-DD") %>')[0].file.link`
<-<-  [[<% tp.date.now("YYYY-MM-DD",-1, tp.file.title, "YYYY-MM-DD") %>]]  <-  <% tp.file.title %>  ->  [[<% tp.date.now("YYYY-MM-DD",+1, tp.file.title, "YYYY-MM-DD") %>]]   ->->

<% tp.web.daily_quote() %>

---
# `=this.aliases`
## Info

> [!todo]- Study
> ```meta-bind
>INPUT[progressBar(title('Study Rating'), minValue(0), maxValue(10)):Study]
>```
> ```meta-bind
>INPUT[progressBar(title('Ultradian Cycles'), stepSize(0.2), minValue(0), maxValue(5)):Ultradian_Cycles]
>```

> [!info]- Mood
> ```meta-bind
> INPUT[progressBar(minValue(0), maxValue(10)):Mood]
> ```
> **Why:** `INPUT[text:Why]`

> [!danger]- Habit Tracker
> **Meditation:** `INPUT[toggle:Meditation]` | **Exercise:** `INPUT[toggle:Exercise]` 

---
## Things I am grateful for:
- 


## Glimpse of the day

**Dear Diary**,


*Ashutosh Thakur*

---

