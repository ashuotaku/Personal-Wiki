<% '---' %>
noteType: goal
area: 
tags: goal
progress: 
target: 100
startDate: 
deadline: 
completionDate: 
completed: false
created_at: <% tp.file.creation_date('YYYY-MM-DD[T]HH:mm:ssZ') %>
<% '---' %>

>[!multi-column]
>
>>[!blank-container]
>>Start Date: `=this.startDate`
>
>>[!blank-container]
>>Deadline: `=this.deadline`
>
>>[!blank-container]
>>Compleione Date: `=this.completionDate`

<br>

>[!multi-column]
>
>>[!blank-container]
>>**Completed:** `INPUT[toggle:completed]` 
>
>>[!blank-container]
>>**Area:** `=this.area`

```meta-bind
INPUT[progressBar(title('Progress'), minValue(0), maxValue(100)):progress]
```

> [!info] Why is this goal important to me?
> 1. 

> [!success]- What would I gain by achieving this goal?
> 1. 

> [!failure]- What are the possible risks and obstacles?
> 1. 

## Sub Goals:


## Related:


<% await tp.file.move("/001 Goals/" + tp.file.title) %>