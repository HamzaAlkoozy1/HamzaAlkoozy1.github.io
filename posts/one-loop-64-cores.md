# One tiny loop. 64 CPU cores at 100%.

2026-11-26 · Hamza Alkoozy

🔥 One tiny loop kept all 64 CPU cores of a production server at 100%.
The fix took a few lines: 21 seconds → 0.01. Then I went hunting for its cousins 👇

## 😱 What broke

A "most popular items" list was eating the whole server.

The code looked so clean:

```php
foreach ($itemIds as $itemId) {
    $count = $rows->where('id', $itemId)->value('count');
}
```

But `where()` walks the whole list on every call 🐢 And it did that twice per item, once for each of its two data sources.

About 1,200 items had activity that day. That is up to ~2.9 million checks, and 21 seconds of CPU for every single visit 😬

## 🔧 The fix

Build a lookup by id once, then read each item straight from it:

```php
$countById = [];
foreach ($rows as $row) {
    $countById[$row['id']] = $row['count'];
}

foreach ($itemIds as $itemId) {
    $count = $countById[$itemId] ?? 0;
}
```

- ⏱️ 21 s → 0.01 s per request
- ✅ same output, checked on real production data
- 🧹 then the hunt: the same day I sent 6 more performance commits through 28 files of the API's hot paths

## 💡 The lesson

Code that is fine with 10 rows can melt with 1,200. Before you write the loop, ask two questions: how many rows, and how often? 🤔

I work with AI coding agents every day, so I turned this into a standing rule for them. Every loop over a list of unknown size must say its cost, and every change that touches queries or loops gets a performance check before I even see it 🤖

Small loop, big lesson. Happy coding! 🚀

Source: https://hamzaalkoozy1.github.io/posts/one-loop-64-cores.html
© 2026 Hamza Alkoozy · All rights reserved
