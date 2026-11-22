# Final Project: Second Chapter, Year Two

**AIS 2800 · Ohio University · Fall 2026**
**Due:** December 9, 2026, 11:59 PM

You've owned Second Chapter Thrift for a year. You turned a messy file into a normalized database, protected your customers' data and turned a year of sales into a dashboard. Now it's time to show what you can do.

**Choose one option:**

| | Option 1: Year Two Changes | Option 2: Tell Your Story |
|---|---|---|
| **What you'll do** | Make your own business decisions and build them into your Neon database | Tell the story of one project from this semester using the STAR method |
| **You'll submit** | A document with 2 Change Requests, your updated ERD, your Tableau link and a short security section | Your completed STAR Project Entry guide and a Teams video, 2:00 or less |
| **Good fit if you…** | like building and want more SQL and Tableau practice | want interview practice and a story you can use after graduation |

Both options are worth the same. Pick the one that helps *you* most.

---

## Option 1: Year Two Changes

After a year of running the store, every owner finds things they'd do differently. In this option, you'll make **two changes** to how Second Chapter runs and build them into your database.

### Before you start

- Your **class version** of Second Chapter should be built and loaded in Neon.
- Have your **Tableau Public dashboard** from the Tableau assignment ready.
- Every change below comes with **SQL you can copy**. You're welcome to use the same change I demonstrate in the video (Option A). Your thinking goes into choosing the change, explaining why it helps the business and showing that it works.

### Step 1: Find your changes with the decision tree

Start with a question a real owner would ask, and follow it to a change.
<img width="1384" height="556" alt="image" src="https://github.com/user-attachments/assets/eb97aa79-60cd-45fe-9304-8b7e9a54e934" />

**Prefer a list?** Here's the same tree in words:

- **Items:** Is staff typing the same words over and over? **Yes → Option A** (flaws become a standard list). **No, we need a new detail → Option E** (rack location).
- **Customers:** Reach them → **Option F** (email). Reward them → **Option C** (points by category).
- **Prices and discounts → Option B** (Purple tag at 75% off).
- **Staff → Option D** (employee table).

### Step 2: Check your two choices

| Option | Change | Type | Gives you a Tableau chart? |
|---|---|---|---|
| **A** | Flaws become a standard list | Restructure | ✅ Flaws by category |
| **B** | Purple tag at 75% off | Add lookup values | ❌ |
| **C** | Points tied to category | Move a rule | ✅ Points by category |
| **D** | Employee table | Add a table + FK | ✅ Sales by employee |
| **E** | Rack location | Add a column | ✅ Sales by rack |
| **F** | Customer email | Add a column | ❌ |

**Rule of thumb:** pick at least one change marked ✅, so you have something new to chart in Tableau.

**Good to know:**
- You can make any two changes, in any order. They won't conflict.
- If you run the same change twice, Neon shows an error and nothing changes. That's the transaction (`BEGIN`/`COMMIT`) doing its job!
- Want to change something that's not on the list, like a different discount or a new table? Go for it! Check with me on Teams first so I can help with the SQL.

### Step 3: Make the change in Neon

1. In Neon, click **New query (⊕)**.
2. Paste the SQL for your change (see **The Change Menu** below) and click **Run**.
3. Run the **proof query** at the bottom of the SQL. Take a screenshot of the results.

### Step 4: Fill out a Change Request for each change

Real IT teams fill out a *change request* before they change a live database, so everyone knows what changed and why. Copy this table into your document once for each change.

| Section | What to write |
|---|---|
| **1. Business rule** | Old rule → new rule, in plain English |
| **2. How does that help the business?** | 1–2 sentences |
| **3. Type of change** | Add a column · Add lookup values · Move a rule · Add a table + FK · Restructure |
| **4. Tables affected** | Which tables are new, and which changed |
| **5. SQL** | Screenshot of your SQL running in Neon |
| **6. Proof** | Screenshot of your proof query results |

### Step 5: Update the ERD

Take the class ERD and mark what you changed: new tables, new columns and new relationship lines. Hand-drawn, Figma or any tool is fine, as long as it's clear what's new.

### Step 6: Add a chart to your Tableau dashboard

1. Run the **proof query** for one of your ✅ changes and **export the results as a CSV** (just like the Tableau assignment).
2. In Tableau Public, open your **Second Chapter Sales 2026** workbook and click **Edit**.
3. Add the new CSV as a data source, build one chart from it and add it to your dashboard.
4. Publish again, and copy your link.

### Step 7: Security check (2–3 sentences)

Your changes add new data to Second Chapter, and new data needs protecting. In 2–3 sentences:

- Name the MITRE ATT&CK technique for SQL injection (**T1190**).
- Pick one mitigation and explain how it would protect the data you just added.

### What to submit (Option 1)

One document uploaded to Canvas with:

- [ ] Change Request #1
- [ ] Change Request #2
- [ ] Updated ERD
- [ ] Tableau Public link, with one sentence on what your new chart shows
- [ ] Security check

---

## Option 2: Tell Your Story (STAR Video)

> *"I would have written a shorter letter if I had more time."*
> Often attributed to Mark Twain

Two minutes sounds easy. It isn't. Cutting your story down to what matters is the real work, and it's exactly what you'll need to do in an interview. This option is a gift to your future self: a polished story you can use in your next interview.

### Step 1: Pick one project from this semester

Choose the one you have the most to say about: your Neon build, SQL injection, MITRE and the TalkTalk case, your Tableau dashboard, normalization or your midterm project.

### Step 2: Complete the STAR Project Entry guide

Fill out the [STAR Project Entry guide](https://github.com/TMPenwell/littlegreenbook/blob/main/LGB_Part5_STAR_Projects.pdf) from the ISAP career workbook. Your guide should include:

- one number and where it came from
- one thing that went wrong
- one decision you made, and the option you turned down
- where your proof lives (a link, a screenshot or a file)

### Step 3: Record your STAR video in Microsoft Teams (2:00 or less)

| Part | About how long | What to say |
|---|---|---|
| **Situation** | ~15 sec | The project, the class, who it was for |
| **Task** | ~15 sec | What *you* were responsible for. Say "I," not "we." |
| **Action** | ~60 sec | What you did and *why*. Include your decision, the option you turned down, and what went wrong and how you fixed it. |
| **Result** | ~20 sec | What changed, with **one number** and where it came from |
| **Close** | ~10 sec | What you learned, or what you'd do differently |

**Requirements:**
- **2:00 or less.** Videos over 2 minutes won't receive full credit.
- **Camera on.** It's interview practice!
- **Use your guide as notes, not a script.** It should sound like you talking, not reading.
- **Optional:** share your screen for a few seconds to show your proof.

**How to record in Teams:** start a meeting with just yourself (**Meet now**), click **Record**, tell your story, then stop recording. Share the recording link and make sure your instructor has permission to view it.

**Tip:** practice out loud once and time yourself before you record. Most first tries run long. That's normal!

Read more: [The STAR Method for Behavioral Interviews (MIT Career Advising & Professional Development)](https://capd.mit.edu/resources/the-star-method-for-behavioral-interviews/)

### What to submit (Option 2)

- [ ] Your completed **STAR Project Entry guide**
- [ ] Your **Teams video link**

---

## The Change Menu (Option 1)

Every change below has been tested on the class version of Second Chapter. Copy the whole block, including `BEGIN` and `COMMIT`.

### Option A: Flaws become a standard list (Restructure)

*Old rule:* staff type each flaw as free text. *New rule:* staff pick from a standard flaw list.

```sql
BEGIN;
-- 1. New lookup table: each flaw written once
CREATE TABLE flaw (
    flaw_id           SERIAL        PRIMARY KEY,
    flaw_description  VARCHAR(200)  NOT NULL UNIQUE
);
-- 2. Fill it from the flaws we already have
INSERT INTO flaw (flaw_description)
SELECT DISTINCT flaw_description FROM item_flaw ORDER BY flaw_description;
-- 3. New junction table: which item has which flaw
CREATE TABLE item_flaw_new (
    item_id  VARCHAR(10)  REFERENCES item (item_id),
    flaw_id  INT          REFERENCES flaw (flaw_id),
    PRIMARY KEY (item_id, flaw_id)
);
-- 4. Move the old rows over (a join turns text into IDs)
INSERT INTO item_flaw_new (item_id, flaw_id)
SELECT DISTINCT o.item_id, f.flaw_id
FROM item_flaw AS o
JOIN flaw AS f ON o.flaw_description = f.flaw_description;
-- 5. Check before you swap
SELECT (SELECT COUNT(*) FROM item_flaw) AS old_rows,
       (SELECT COUNT(*) FROM item_flaw_new) AS new_rows;
-- 6. Swap: drop the old table, rename the new one
DROP TABLE item_flaw;
ALTER TABLE item_flaw_new RENAME TO item_flaw;
COMMIT;
```

**Proof query** (expected: 10 rows, one per flaw):

```sql
SELECT * FROM flaw;
```

**Chart query** (export this one for Tableau):

```sql
SELECT c.category_name, f.flaw_description, COUNT(*) AS items_with_flaw
FROM item_flaw AS itf
JOIN flaw     AS f ON itf.flaw_id    = f.flaw_id
JOIN item     AS i ON itf.item_id    = i.item_id
JOIN category AS c ON i.category_id  = c.category_id
GROUP BY c.category_name, f.flaw_description
ORDER BY items_with_flaw DESC;
```

### Option B: Purple tag at 75% off (Add lookup values)

*Old rule:* four tag colors. *New rule:* a fifth tag for items that need to move fast.

```sql
BEGIN;
INSERT INTO tag (tag_id, tag_color, tag_discount)
VALUES ('T05', 'Purple', 75.00);
COMMIT;
-- Proof
SELECT * FROM tag ORDER BY tag_discount;
```

### Option C: Points tied to category (Move a rule)

*Old rule:* each item has its own point value. *New rule:* every item in a category earns the same points.

```sql
BEGIN;
ALTER TABLE category ADD COLUMN point_value INT DEFAULT 0;
UPDATE category SET point_value = CASE category_name
    WHEN 'Furniture'   THEN 50
    WHEN 'Electronics' THEN 25
    WHEN 'Jewelry'     THEN 20
    WHEN 'Clothing'    THEN 10
    WHEN 'Shoes'       THEN 10
    WHEN 'Housewares'  THEN 5
    WHEN 'Books'       THEN 5
    WHEN 'Toys'        THEN 5
END;
COMMIT;
-- Proof
SELECT c.category_name, c.point_value, COUNT(*) AS items_sold,
       c.point_value * COUNT(*) AS points_given
FROM item_sale AS isl
JOIN item     AS i ON isl.item_id    = i.item_id
JOIN category AS c ON i.category_id  = c.category_id
GROUP BY c.category_name, c.point_value
ORDER BY points_given DESC;
```

### Option D: Record who rang up each sale (Add a table + FK)

*Old rule:* no record of who rang up a sale. *New rule:* every receipt records the employee.

```sql
BEGIN;
CREATE TABLE employee (
    employee_id     VARCHAR(10)  PRIMARY KEY,
    employee_fname  VARCHAR(50)  NOT NULL,
    employee_lname  VARCHAR(50)  NOT NULL,
    employee_role   VARCHAR(20)                  -- Cashier, Manager
);
INSERT INTO employee (employee_id, employee_fname, employee_lname, employee_role) VALUES
    ('E01', 'Rosa',  'Kline',  'Manager'),
    ('E02', 'Dev',   'Archer', 'Cashier'),
    ('E03', 'Maddie','Shaw',   'Cashier');
ALTER TABLE sale ADD COLUMN employee_id VARCHAR(10) REFERENCES employee (employee_id);
-- Give last year's receipts to the three employees, taking turns
UPDATE sale SET employee_id = CASE CAST(receipt_id AS INT) % 3
    WHEN 0 THEN 'E01'
    WHEN 1 THEN 'E02'
    ELSE        'E03'
END;
COMMIT;
-- Proof
SELECT e.employee_fname, e.employee_role,
       COUNT(DISTINCT s.receipt_id) AS receipts,
       SUM(isl.sale_price)          AS total_sales
FROM sale AS s
JOIN employee  AS e   ON s.employee_id = e.employee_id
JOIN item_sale AS isl ON s.receipt_id  = isl.receipt_id
GROUP BY e.employee_fname, e.employee_role
ORDER BY total_sales DESC;
```

### Option E: Track where each item sits (Add a column)

*Old rule:* no record of where items are in the store. *New rule:* every item has a rack location.

```sql
BEGIN;
ALTER TABLE item ADD COLUMN rack_location VARCHAR(20);
UPDATE item SET rack_location = CASE category_id
    WHEN 'CAT01' THEN 'Back wall'
    WHEN 'CAT02' THEN 'Center racks'
    WHEN 'CAT03' THEN 'Front counter'
    WHEN 'CAT04' THEN 'Back room'
    WHEN 'CAT05' THEN 'Side shelves'
    WHEN 'CAT06' THEN 'Front counter'
    WHEN 'CAT07' THEN 'Center racks'
    WHEN 'CAT08' THEN 'Side shelves'
END;
COMMIT;
-- Proof
SELECT i.rack_location, COUNT(*) AS items_sold, SUM(isl.sale_price) AS total_sales
FROM item_sale AS isl
JOIN item AS i ON isl.item_id = i.item_id
GROUP BY i.rack_location
ORDER BY total_sales DESC;
```

### Option F: Collect customer emails (Add a column)

*Old rule:* customers are reached by phone only. *New rule:* rewards customers have an email on file.

```sql
BEGIN;
ALTER TABLE customer ADD COLUMN customer_email VARCHAR(100) UNIQUE;
UPDATE customer
SET customer_email = LOWER(customer_fname || '.' || customer_lname || customer_id || '@example.com');
COMMIT;
-- Proof
SELECT customer_fname, customer_lname, customer_email
FROM customer
LIMIT 5;
```

---

Questions? Reach out on Teams. I'm happy to help.
