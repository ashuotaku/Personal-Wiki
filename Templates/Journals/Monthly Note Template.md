<% '---' %>
tags: journal/monthlynote
id: journal-<% tp.file.title %>
<% '---' %>
↑ `$=dv.pages().where(b => b.id == 'journal-<% tp.date.now('YYYY-[Q]Q', 0, tp.file.title, 'MMMM, YYYY') %>')[0].file.link`
←← [[<% tp.date.now('MMMM, YYYY', 'P-1M', tp.file.title, 'MMMM, YYYY') %>]] ← <% tp.file.title %> → [[<% tp.date.now('MMMM, YYYY', 'P+1M', tp.file.title, 'MMMM, YYYY') %>]] →→
<%* week = parseInt(moment(tp.file.title, "MMMM, YYYY").startOf("month").format("WW")) -%>
<%* year = tp.date.now('YYYY', 0, tp.file.title, 'MMMM, YYYY') %>
<%* tR+=`[[${year}-W${('0' + week).slice(-2)}|W${('0' + week).slice(-2)}]] • [[${year}-W${('0' + (week+1)).slice(-2)}|W${('0' + (week+1)).slice(-2)}]] • [[${year}-W${('0' + (week+2)).slice(-2)}|W${('0' + (week+2)).slice(-2)}]] • [[${year}-W${('0' + (week+3)).slice(-2)}|W${('0' + (week+3)).slice(-2)}]] • [[${year}-W${('0' + (week+4)).slice(-2)}|W${('0' + (week+4)).slice(-2)}]]` %>