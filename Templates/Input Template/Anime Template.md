<%*
// Function for calculating regular expression durations
function calculate(str) {
  let multiplier = str.toLowerCase().includes("hour")||str.toLowerCase().includes("hr") ? 60 : 1;
  let res = str.match(/\d+/g).map(Number);
  return ((res[0] || 0) * multiplier + (res[1] || 0));
}
// Anime Choosing and Fetching
const anime_query = await tp.system.prompt('Enter the anime name: ')
const listresponse = await tp.obsidian.requestUrl("https://api.jikan.moe/v4/anime?q=" + anime_query + "&limit=20")
const listdata = listresponse.json.data
let titles = listdata.map(Q => ((Q.title_english != null ? p = Q.title_english : p = Q.title+' --> ( '+Q.aired.prop.from['year']+' )') != null ? p : Q.title+' --> ( '+Q.aired.prop.from['year']+' )'))
let mal_ids = listdata.map(Q => Q.mal_id)
const mal_id = await tp.system.suggester(titles, mal_ids)
let dataUrl = 'https://api.jikan.moe/v4/anime/'+mal_id+'/full'
let animeresponse = await tp.obsidian.requestUrl(dataUrl)
let d = animeresponse.json.data;
let title = (p = d.title_english) != null ? p : d.title;
let ortitle = title
title = title.replace("/", "");
title = title.replace(":", "");
title = title.replace("\\","");
console.log(d);
tp.hooks.on_all_templates_executed(async () => {
  const file = tp.file.find_tfile(tp.file.path(true));
  await app.fileManager.processFrontMatter(file, (frontmatter) => {
	year = (p = d.year) != null ? p : d.aired.prop.from.year;
    frontmatter["tags"] = ['anime/'+d.type];
    frontmatter["aliases"] = d['titles'].map(Q => Q.title);
    frontmatter["aliases"] += ', mal-'+mal_id;
    frontmatter["title"] = ortitle;
    frontmatter["japaneseTitle"] = (p = d.title_japanese) != null ? p : d.title;
    frontmatter["id"] = "anime-mal-"+mal_id;
    // Adding genres and demographics;
    genres = d['genres'].map(Q => Q.name);
    demographics = d['demographics'].map(Q => Q.name);
    explicits = d['explicit_genres'].map(Q => Q.name);
    themes = d['themes'].map(Q => Q.name);
    allgenres = genres.concat(demographics, explicits, themes);
    frontmatter["genres"] = allgenres.map(Q => "[["+Q+"]]");
    frontmatter["airing"] = d.airing;
	frontmatter["mal_id"] = mal_id;
	frontmatter["type"] = d.type;
	frontmatter["year"] = year;
	frontmatter["airedFrom"] = d.aired.prop.from.year+'-'+d.aired.prop.from.month+'-'+d.aired.prop.from.day;
	frontmatter["airedTo"] = d.aired.prop.to.year+'-'+d.aired.prop.to.month+'-'+d.aired.prop.to.day;
	frontmatter["season"] = d.season;
	frontmatter["source"] = d.source;
	frontmatter["onlineStatus"] = d.status;
	frontmatter["approved"] = d.approved;
	frontmatter["episodes"] = d.episodes;
	frontmatter["broadcast"] = d.broadcast;
	frontmatter["synonyms"] = d.title_synonyms;
	frontmatter["dataUrl"] = dataUrl;
	frontmatter["longupinfo"] = {
		"background":d.background,
		"genres":d['genres'].map(Q => Q.name),
		"external":d.external,
		"banner":d.images.jpg.large_image_url,
		"licensors":d.licensors,
		"producers":d.producers,
		"relations":d.relations,
		"streaming":d.streaming,
		"studios":d.studios,
		"synopsis":d.synopsis,
		"theme":d.theme,
		"trailer":d.trailer.url
	}
	frontmatter["onlineRating"] = d.rating;
	frontmatter["onlineScore"] = d.score;
	frontmatter["scoredBy"] = d.scored_by;
	frontmatter["favorites"] = d.favorites;
	frontmatter["members"] = d.members;
	frontmatter["popularity"] = d.popularity;
	frontmatter["rank"] = d.rank;
	frontmatter["url"] = d.url;
    frontmatter["cssclasses"] = "anime";
	frontmatter["durationWords"] = d.duration;
    frontmatter["rewatch"] = 0;
    frontmatter["priority"] = "Normal";
    frontmatter["banner"] = d.images.jpg.large_image_url;
    frontmatter["duration"] = calculate(d.duration);
    frontmatter["created_at"] = tp.file.creation_date('YYYY-MM-DD[T]HH:mm:ssZ');
    frontmatter["modified_at"] = tp.file.last_modified_date('YYYY-MM-DD[T]HH:mm:ssZ');
    frontmatter["status"] = "Planned";
    frontmatter["personalScore"] = 0;
    frontmatter["progress"] = 0;
    frontmatter["startDate"] = null;
    frontmatter["finishDate"] = null;
  });
});
-%> 
<%*
tp.hooks.on_all_templates_executed(async () => {
  const file = tp.file.find_tfile(tp.file.path(true));
  await app.fileManager.processFrontMatter(file, (frontmatter) => {
  let dv = DataviewAPI
  animes = dv.pages('"Inputs/Anime"').values
  for(let i in h=animes){
	if(h.length==0){
		tp.file.rename(title);
		console.log(title+' anime entry added')
	}
	else if (h[i].mal_id==mal_id){
		console.log('Anime Already Exists In Your Database');
		app.fileManager.trashFile(file);
		throw new Error("Code Stopped because anime already exists");
	}
	else {
		tp.file.rename(title);
		console.log(title+' anime entry added')
	}
}
  });
});
-%>
```dataviewjs
let dataUrl = 'https://api.jikan.moe/v4/anime/'+dv.current().mal_id+'/full';
let animeresponse = await requestUrl(dataUrl)
let d = animeresponse.json.data;
const file = app.vault.getAbstractFileByPath(dv.current().file.path);
console.log(file)
console.log(d)
await app.fileManager.processFrontMatter(file, (frontmatter) => {
	frontmatter["airing"] = d.airing;
	frontmatter["onlineStatus"] = d.status;
	frontmatter["broadcast"] = d.broadcast;
	frontmatter["onlineScore"] = d.score
	frontmatter["scoredBy"] = d.scored_by
	frontmatter["rank"] = d.rank
	frontmatter["favorites"] = d.favorites
	frontmatter["members"] = d.members
	frontmatter["popularity"] = d.popularity
});
```


>[!info]- Information
> **Synonyms**:  `=this.aliases`
> **Duration**:  `=this.durationWords`
>
>>[!multi-column]
>>
>>>[!blank-container]
>>>**Online Status**:  `=this.onlineStatus`
>>
>>>[!blank-container]
>>>**Episodes**:  `=this.episodes`
>
>
>>[!abstract]- URLs
>> **Data JSON**:  `=this.dataUrl`
>> **MAL URL**:  `=this.url`

>[!abstract]+ Subjective Details
>```meta-bind
>INPUT[progressBar(title('Progress'), minValue(0), stepSize(1), maxValue(<% d.episodes %>)):progress]
>```
>
>>[!tip]+ Personal Rating
>>```meta-bind
>>INPUT[progressBar(stepSize(0.1), minValue(0), maxValue(10)):personalScore]
>>```
>
>>[!multi-column]
>>
>>>[!blank-container]
>>>**Status:** `INPUT[inlineSelect(option(Watching), option(Completed), option(Holded), option(Dropped), option(Planned)):status]`
>>
>>>[!blank-container]
>>>**Priority:** `INPUT[inlineSelect(option('Very High'), option(High), option(Normal), option(Low), option('Very Low')):priority]`
>
><br>
>
>>[!multi-column]
>>
>>>[!blank-container]
>>>**Time Spent:**  `=(this.duration)*(this.progress)/60` Hours
>>
>>>[!blank-container]
>>>**Rewatch Times:** `INPUT[slider(addLabels(true), minValue(0), maxValue(5), stepSize(1)):rewatch]` 
>>
>
><br>
>
>>[!multi-column]
>>
>>>[!blank-container]
>>>**Start Date:** `INPUT[datePicker:startDate]`
>>
>>>[!blank-container]
>>>**Finish Date:** `INPUT[datePicker:finishDate]`
>>
>

---
# My Notes:

> **My tags**:: 


# Plot:
<%* tR += d.synopsis %>

# Background:
<%* tR += d.background %>

# Resources:

## Trailer:

<%* tR+='![Trailer]('+d.trailer.url+')' %>

## Relations:
<%* for(let i in g=d.relations){
	tR += '#### '+g[i].relation+':\n'
	for(let j in h=g[i].entry){
		tR+='- ['+h[j].name+']('+h[j].url+')\n'
	}
} %>
## Theme Songs:
### Openings:
<%* for(let i in g=d.theme.openings){
	tR += g[i]+'\n'
} %>
### Endings:
<%* for(let i in g=d.theme.endings){
	tR += g[i]+'\n'
} %>
## Producers:
<%* for(let i in g=d.producers){
	tR+='- ['+g[i].name+']('+g[i].url+')\n'
} %>
## Licensors:
<%* for(let i in g=d.licensors){
	tR+='- ['+g[i].name+']('+g[i].url+')\n'
} %>
## Studios:
<%* for(let i in g=d.studios){
	tR+='- ['+g[i].name+']('+g[i].url+')\n'
} %>
## Streaming:
<%* for(let i in g=d.streaming){
	tR+='- ['+g[i].name+']('+g[i].url+')\n'
} %>
## Externals:
<%* for(let i in g=d.external){
	tR+='- ['+g[i].name+']('+g[i].url+')\n'
} %>