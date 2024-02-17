<% '---' %>
tags: journal/quarterlynote
id: journal-<% tp.file.title %>
<% '---' %>
↑ `$=dv.pages().where(b => b.id == 'journal-<% tp.date.now('YYYY', 0, tp.file.title, 'YYYY-[Q]Q') %>')[0].file.link`
←← [[<% tp.date.now('YYYY-[Q]Q', 'P-1M', tp.file.title, 'YYYY-[Q]Q') %>]] ← <% tp.file.title %> → [[<% tp.date.now('YYYY-[Q]Q', 'P+4M', tp.file.title, 'YYYY-[Q]Q') %>]] →→
<%* YYYY = tp.date.now('YYYY', 0, tp.file.title, 'YYYY-[Q]Q') %>
<%* quarter = tp.date.now('Q', 0, tp.file.title, 'YYYY-[Q]Q') -%>
<%*
if(quarter==1){
tR += `[[Janurary, ${YYYY}|January]] • [[February, ${YYYY}|February]] • [[March, ${YYYY}|March]]`
}
else if(quarter==2){
tR += `[[April, ${YYYY}|April]] • [[May, ${YYYY}|May]] • [[June, ${YYYY}|June]]`
}
else if(quarter==3){
tR += `[[July, ${YYYY}|July]] • [[August, ${YYYY}|August]] • [[September, ${YYYY}|September]]`
}
else{
tR += `[[October, ${YYYY}|October]] • [[November, ${YYYY}|November]] • [[December, ${YYYY}|December]]`
}
%>