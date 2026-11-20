# Second Chapter: How a Query Gets Hijacked

**AIS 2800 · Ohio University · Week 14**

Second Chapter wants a page on its website where rewards customers type their phone number and see their points. You'll build two versions of that lookup in Neon: one that trusts whatever is typed into the box, and one that doesn't. Then you'll see what happens when someone types something sneaky.

## Before you start

- Your **class version** of Second Chapter should be built and loaded in Neon (the `customer` table needs its 38 rows).
- Click **New query (⊕)** before each step so you start with a blank editor.
- Have your **guided notes** open. Each step has a blank to fill in.

---

## Step 1: Build the three functions

A **function** is a saved query you can run by name, like the trigger function from Week 13. You don't need to write these. Copy and run them, then read the comments.

```sql
-- =====================================================================
-- STEP 1: Build three functions. Run this whole block once.
-- =====================================================================

-- SHOW_QUERY: shows the query the website WOULD build.
-- It glues the customer's typing into the middle of a query, like this:
--   ... WHERE customer_phone = '  +  what they typed  +  ';
-- It doesn't run anything. It just shows you the finished query text.
CREATE FUNCTION show_query(typed_phone TEXT)
RETURNS TEXT AS $$
  SELECT 'SELECT customer_fname, customer_lname, customer_rewards_balance FROM customer WHERE customer_phone = '''
         || typed_phone || ''';';
$$ LANGUAGE sql;

-- POINTS_LOOKUP_UNSAFE: the website version that TRUSTS the typing.
-- It builds the query by gluing text together (same as show_query),
-- then runs whatever query comes out.
CREATE FUNCTION points_lookup_unsafe(typed_phone TEXT)
RETURNS TABLE (first_name VARCHAR, last_name VARCHAR, points INT) AS $$
BEGIN
  RETURN QUERY EXECUTE
    'SELECT customer_fname, customer_lname, customer_rewards_balance FROM customer WHERE customer_phone = '''
    || typed_phone || '''';
END;
$$ LANGUAGE plpgsql;

-- POINTS_LOOKUP_SAFE: the website version that does NOT trust the typing.
-- The query is written once, with a placeholder (typed_phone).
-- Whatever is typed is treated as a VALUE to compare, never as part of the query.
-- This is called a PARAMETERIZED query.
CREATE FUNCTION points_lookup_safe(typed_phone TEXT)
RETURNS TABLE (first_name VARCHAR, last_name VARCHAR, points INT) AS $$
  SELECT customer_fname, customer_lname, customer_rewards_balance
  FROM customer
  WHERE customer_phone = typed_phone;
$$ LANGUAGE sql;
```

**Expected result:** 3 tabs, each saying *Statement executed successfully*.

---

## Step 2: A normal customer looks up their points

Willa Mercer types her phone number into the box.

```sql
-- =====================================================================
-- STEP 2: A normal lookup.
-- =====================================================================

-- What query did the website build?
SELECT show_query('740-555-6045');

-- Run it.
SELECT * FROM points_lookup_unsafe('740-555-6045');
```

**Expected result:** The first tab shows the finished query. The second shows **1 row**: Willa Mercer, 293 points. Everything works the way the business wanted.

---

## Step 3: Someone types something sneaky

This time, someone types this into the phone number box:

```
x' OR '1'='1
```

**About the `$$` marks:** they're just how we hand Neon the exact characters someone typed, quote marks and all. On the real website, there'd be no `$$`. The person would only type what's between them.

```sql
-- =====================================================================
-- STEP 3: The same box, with sneaky typing.
-- =====================================================================

-- What query did the website build this time?
SELECT show_query($$x' OR '1'='1$$);

-- Run it.
SELECT * FROM points_lookup_unsafe($$x' OR '1'='1$$);
```

**Expected result:** The second tab shows **38 rows**: every customer's name and points balance.

**Look closely at the first tab.** Find the `WHERE` clause and fill in your guided notes:

- What did the first `'` in the typing do?
- What condition got added?
- Why is that condition true for every row?

This is **SQL injection**: typing that changes the query instead of filling it in.

---

## Step 4: The safe version

Run the same two lookups against the safe version.

```sql
-- =====================================================================
-- STEP 4: The safe (parameterized) version.
-- =====================================================================

-- Normal lookup: still works.
SELECT * FROM points_lookup_safe('740-555-6045');

-- Sneaky typing: no longer works.
SELECT * FROM points_lookup_safe($$x' OR '1'='1$$);
```

**Expected result:** The first tab shows **1 row** (Willa). The second shows **0 rows**.

The safe version looked for a customer whose phone number is literally `x' OR '1'='1`. Nobody has that phone number, so it found no one. The typing stayed a **value**. It never became part of the **query**.

---

## Clean up (when you're done)

```sql
-- =====================================================================
-- CLEAN UP: remove the three functions. Your tables stay as they are.
-- =====================================================================
DROP FUNCTION show_query(TEXT);
DROP FUNCTION points_lookup_unsafe(TEXT);
DROP FUNCTION points_lookup_safe(TEXT);
```

### Troubleshooting

| Error | What it means | Fix |
|---|---|---|
| `function ... already exists` | You ran Step 1 a second time. | Skip Step 1, or run the clean-up block first. |
| `relation "customer" does not exist` | The class tables aren't in this database. | Build and load the class version first (see the README). |
| `0 rows` in Step 2 | The phone number doesn't match. | Copy it exactly: `740-555-6045`. |
| `unterminated dollar-quoted string` | A `$$` is missing. | Make sure the typing has `$$` on **both** sides. |
