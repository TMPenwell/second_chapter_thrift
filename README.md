# Second Chapter Thrift 🛍️

**AIS 2800 · Business Intelligence · Ohio University**

Welcome! This is your home base for building the **Second Chapter** database in **Neon**. Everything you need is here: the SQL, the order to run it in, and help if something goes sideways.

**Take a few minutes to read this page before you start.** It will save you time later, and it answers the questions most students run into.

---

## What you're doing (and why)

You've worked with Second Chapter's sales data as one big spreadsheet. The same customer's name and phone number show up on row after row, and a single cell can hold a list of flaws. That works for a quick look, but it's hard to keep accurate.

In this project, you'll move that data into a **normalized database**: separate tables for customers, items, sales, and more, connected by keys. It's the same data, now organized the way a real business would store it.

You don't have to type the SQL yourself. You'll copy it from this repo, run it in Neon, and watch the database come together.

---

## Your files

| File | What it does | When |
|---|---|---|
| [`sql_for_neondb.md`](sql_for_neondb.md) | **Builds** the 9 empty tables | First |
| [`insert_values_into_tables.md`](insert_values_into_tables.md) | **Fills** the tables with the sales data | Second |

**To copy SQL:** hover over a gray code block and click the **copy icon** in its top-right corner.

---

## Before you start

- ✅ You're signed in to **Neon**
- ✅ Your project, `SecondChapterThrift - YourLastName`, is open
- ✅ You're in the **SQL Editor** (left menu → **Postgres database** → **SQL Editor**)

---

## Step by step

### 1. Build the tables

Open [`sql_for_neondb.md`](sql_for_neondb.md). For **each round**:

1. In Neon, click **New query (⊕)** to get a blank editor.
2. Copy the round from GitHub and paste it in.
3. Click **Run**.
4. Check that every result tab says **Statement executed successfully**.

Then move on to the next round.

### 2. Load the data

Open [`insert_values_into_tables.md`](insert_values_into_tables.md) and do the same thing, round by round.

### 3. Check your work

Each file ends with a **Check your work** query. Run it and compare your results with the expected results in the file. If they match, you did it! 🎉

---

## Why are there rounds?

Some tables **point to** other tables. For example, every item points to the consignor who brought it in. A table can only point to something that already exists, so the tables are built in order:

| Round | Tables | Why this order |
|---|---|---|
| 1 | consignor, brand, category, tag, customer | Don't point to anything |
| 2 | item, sale | Point to Round 1 |
| 3 | item_flaw, item_sale | Point to Round 2 |

Think of it like stocking a store: the shelves go up before anything goes on them.

---

## Tips that help

- **Click New query (⊕) before every round.** This is the #1 way to avoid errors. If your last round is still in the editor, Neon will try to run it again.
- **Your work is saved in History.** Nothing you run is lost. Click **History** on the left to find it.
- **"No result" is normal** after CREATE TABLE and INSERT. They don't return rows to look at.
- **Go one round at a time.** It's easier to spot a problem when you've only run a little bit.
- **The green text is comments.** They're notes for you, and the database skips them. Read them! They explain why each table is built the way it is.

---

## Got an error? That's okay.

Errors are part of working with databases, and every one of them tells you something. Read the message. It usually names the exact table or row that caused it.

| You see... | What it means | What to do |
|---|---|---|
| `already exists` | You ran a round twice. | Click **New query (⊕)** and run only the next round. |
| `does not exist` | The table isn't there yet, or it was already removed. | Make sure you built the tables first. |
| `violates foreign key constraint` | A row is pointing to something that isn't there yet. | Run the rounds in order: 1, then 2, then 3. |
| `duplicate key value` | That data is already loaded. | You probably ran a round twice. Skip it. |
| `cannot drop table ... other objects depend on it` | Another table still points to this one. | Remove tables in reverse order: Round 3 first. |

**Try to work it out yourself before clicking Fix with AI.** Reading an error and fixing it is a skill you'll use in every tool you learn.

---

## Need a fresh start?

No problem. At the end of [`sql_for_neondb.md`](sql_for_neondb.md), the **Start over** section removes all 9 tables in the right order. Delete the `--` at the start of each line, run it, and begin again from Step 1.

---

## A note about the data

The sales data has 541 rows from January to September 2026. Like most real business data, it has a few problems: a duplicate row, a consignor with two different splits, a phone number that changes partway through. [`insert_values_into_tables.md`](insert_values_into_tables.md) explains each decision made while loading it.

**As you read those decisions, ask yourself:** would you have made the same call if this were your store?

---

## Stuck?

You've got time and you've got support. If you've tried the tips above and you're still stuck, reach out. Bring a screenshot of your error and the round you were on, and we'll figure it out together.

*All names, phone numbers, and businesses are fictional.*
