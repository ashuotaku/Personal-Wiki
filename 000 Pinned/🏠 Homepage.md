---
created_at: 2024-01-30T11:38:56+05:30
modified_at: 2024-02-17T13:32:26+05:30
tags:
  - homepage
  - followup
banner: https://i.imgur.com/9ZJBvN8.jpg
banner_y: 0.446
cssclasses:
---
- [[👤 Personal]] #mcl/list-column
- [[💼 Productivity]]
- [[📥 Inputs]]
- [[🧰 Utilities]]


## Goals

 ```dataviewjs
 let goals = dv.pages('"001 Goals"');
 dv.table(["Goal", "Deadline", "Progress"],
 goals.map(goal => [
 `<span style="font-size: 1.2em;">${goal.file.link}</span>`,
 goal.deadline,
 `<progress value="${goal.progress}" max="${goal.target}"></progress><br>${Math.round((goal.progress / goal.target) * 100)}% completed`
 ])
 );
```

## Daily Habit Tracker
```dataviewjs
const pages = dv.pages('#journal/dailynote')
.where((p) => "Meditation" in p || "Exercise" in p)
.sort((p) => p.file.day, "desc")
.map((p) =>
Object.create({
link: p.file.link,
day: p.file.day,
Meditation: p.Meditation,
Exercise: p.Exercise,
})
);
function getStreak(validate) {
let count = 0;
for (const note of pages) {
if (validate(note)) count++;
else break;
}
return count;
}
function getRecord(validate) {
let record = 0;
let count = 0;
for (const note of pages) {
if (validate(note)) {
count++;
record = Math.max(record, count);
} else {
count = 0;
}
}
return record;
}
const done = "✅";
const skip = "❌";
const fileRows = pages
.filter((p) => p.day >= moment().subtract(1, "w"))
.sort((p) => p.day)
.map((note) => [
note.link,
note.Meditation ? done : skip,
note.Exercise ? done : skip,
]);
const meditation = [
getStreak((note) => note.Meditation),
getRecord((note) => note.Meditation),
];
const workout = [
getStreak((note) => note.Exercise),
getRecord((note) => note.Exercise),
];
dv.table(
["Habits", "🧘", "💪🏼"],
[
...fileRows,
["‎"],
["**Streak**", meditation[0], workout[0]],
["**Record**", meditation[1], workout[1]],
]
);
```


