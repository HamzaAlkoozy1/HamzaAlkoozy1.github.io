# The save that said "done" and wrote nothing

2026-11-26 · Hamza Alkoozy

💸 After an upgrade, a money field stopped saving and threw no error and wrote no log line.
The cause was one innocent `==` that thought 283.28 and 284 were the same number 👇

## 😱 What broke

We upgraded our framework, and everything looked green.

But on existing records, a money field stored as MongoDB `Decimal128` quietly stopped changing. Wallet balances and cached stats froze, with no exception and no warning 😶

The code called save, got no error back, and moved on.

## 🕵️ The clue

Before writing, the ORM checks which fields are "dirty", and it compared the old and new values with `==`.

The twist: in the MongoDB PHP extension (ext-mongodb), any two `Decimal128` objects are `==` to each other 🤯

```php
use MongoDB\BSON\Decimal128;

var_dump(new Decimal128('283.28') == new Decimal128('284'));
// bool(true)
```

So the ORM saw "nothing changed" and skipped the write.

## 🔧 The fix

My team added a `compare()` method to the cast, in a shared trait, so changes are detected by value instead of by `==`. Balances moved again ✅

## 💡 The lesson I took from it

The real question for me was why our tests didn't catch it.

After an update, the model in memory already holds the new value, even when nothing reached the database. So the test happily read back its own input 🙈

Now I enforce one rule: **a test that updates a saved record must assert on a fresh read.**

```php
$item->update(['amount' => '284.00']);

// ❌ passes even if nothing was written
$this->assertEquals('284.00', (string) $item->amount);

// ✅ checks what the database really holds
$this->assertEquals('284.00', (string) $item->fresh()->amount);
```

Ask the database what it stored. Don't trust what the object remembers 🧠

Trust the database, not the object. Happy coding! 🚀

Source: https://hamzaalkoozy1.github.io/posts/the-save-that-said-done-and-wrote-nothing.html
© 2026 Hamza Alkoozy · All rights reserved
