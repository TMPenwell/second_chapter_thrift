# Build Second Chapter in Neon

**AIS 2800 · Week 13 · Ohio University**

Everything you need is on this one page: set up your Neon project, take a quick look around, then copy each round of SQL into the SQL Editor. Keep this page open beside Neon and work top to bottom.

**9 tables · 8 foreign keys · matches the class schema drawing.** Like stocking shelves, you build from the bottom up:

| Round | Tables | Why this order |
|---|---|---|
| 1 | consignor, brand, category, tag, customer | No foreign keys |
| 2 | item, sale | Point to Round 1 tables |
| 3 | item_flaw, item_sale | Point to Round 2 tables |

**Jump to:** [1 · Set up](#part-1-create-your-neon-project) · [2 · Look around](#part-2-take-a-quick-look-around) · [3 · Build tables](#part-3-build-the-tables) · [4 · Check](#part-4-check-your-work) · [Start over & help](#start-over--troubleshooting)

---

## Part 1: Create your Neon project

In Neon, a **project** is the container for your database. Think of it as renting a building for your store. Everything you build this week will live inside this one project, and Neon sets up a PostgreSQL database for you automatically. There's nothing to install.

### 1. Go to [console.neon.tech](https://console.neon.tech) and sign in

This is your home base. The usage box shows how much of your free plan you've used. You don't need to manage these numbers; class work stays well within the free limits. A database uses three kinds of resources, a lot like running a store:

- **Compute** is the brainpower. It's used whenever the database is working, like running a query. When you're not using it, Neon puts it to sleep.
- **Storage** is the shelf space where your tables and data live.
- **Network transfer** is the delivery truck: data moving between Neon and you.
- **History** is a backup of recent changes, so Neon can restore your data if something goes wrong.

*Note: you won't have the yellow banner saying a project was deleted.*

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/47493e3e-6029-45ba-bce4-45185f1ab94f/user_cropped_screenshot_e9fdab9996a243c2a0fc3b83bf0b72aa_text_export.jpeg" width="560" alt="Neon console home showing free plan usage and no projects">

### 2. Click **Create project**

You'll see "You currently have no projects." That's what we're fixing.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/2d62e113-93ef-4e1d-a178-3ffea08645f4/action-483e6a3af8234df8884bbce589414d68_2512f15ff58045c1bd10f2bdab1a553e_text_export.jpeg" width="560" alt="Create project button in the Neon console">

### 3. Name your project and check the settings

- **Project name:** `SecondChapterThrift - YourLastName` (for example, *SecondChapterThrift - Sloan*). Your last name makes it easy to spot when you share your screen or ask for help.
- **Region:** **AWS US East 2 (Ohio)**. This is where Neon's computers physically store your database. Neon runs on Amazon Web Services (AWS).
- **Services:** leave **Postgres database** on and everything else off.
- **Free plan:** includes 1 GB of storage and a database that **scales to zero** (goes to sleep) when you're not using it.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/27899cc4-9c24-4a52-bcdf-4ebe3a3eab12/action-b44c5b63d9274206b9fc5f235dfb6f94_cd99206398b843058cdcea1a54e3a7dc_text_export.jpeg" width="560" alt="Project name, region, and services settings">

### 4. Click **Create project**, then **Go to project**

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/3ca86712-e6d2-4575-b7f0-dc80ad35c77c/action-f488392e38394971b2613990e61824ee_079aa3615d764a649b25400a45a68936_text_export.jpeg" width="560" alt="Create project button at the bottom of the settings form">

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/3ef1c30b-cd32-4317-bc21-349b6fabcbf0/action-88f19fd70c7841c69a4971e362ea3974_54939c4d69b74ec4be112132fd27a376_text_export.jpeg" width="560" alt="Go to project button">

### 5. Check your Branch overview

- **Branch: production.** A branch is a copy of your database that businesses use to test changes safely. We'll do all our work on production.
- **Postgres database:** *1 database, 1 compute*, one place to store data and one engine to run queries.
- **Right panel:** confirm your project name, **AWS US East 2 (Ohio)**, and **Free plan**.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-17/8ab6e477-4ead-451a-a99b-4f23116ac7a3/user_cropped_screenshot_c516adac84e14e84a6a2ca2b551b22c8_text_export.jpeg" width="560" alt="Branch overview for the new project">

---

## Part 2: Take a quick look around

You've been querying tables all semester. Now you get to see where those tables actually live. There's nothing to type here; just click each item in the left menu and notice how the pieces fit together. Open each section below as you go.

<details open>
<summary><strong>Postgres database → Tables</strong></summary>

In the left menu, click **Postgres database**. This opens the database itself, where your tables, data, and tools are kept.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-17/007ad0bb-6ce0-43d0-b802-ec9b221cada9/user_cropped_screenshot_7a8108d0a5d2426194c29da5826c15f7_text_export.jpeg" width="560" alt="Postgres database in the left menu">

Then click **Tables**. This screen shows how a database is organized, from biggest to smallest:

- **Database (`neondb`):** the whole storage space for your project.
- **Schema (`public`):** a folder inside the database that groups related tables.
- **Tables:** where data lives, in rows and columns. Right now: **0 tables in public schema**.

Skip the **Create table** button. We'll build tables with SQL so you can see how each one is put together.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/1eb8d2bb-7a12-487b-b2b4-fd74a98c4b2c/action-ecd8dddfe2d841e88e67f2996aeac7ff_a10c9b9c6eaa47d4babfcd5f83ddb282_text_export.jpeg" width="560" alt="Tables screen showing neondb, public schema, and 0 tables">

</details>

<details>
<summary><strong>Backup &amp; Restore</strong></summary>

- **Restore from history:** roll your database back to any point in the past **6 hours**, like an "undo" button for your data.
- **Create snapshot:** a saved copy of your database at one moment, like a photo before big changes.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/4650cb35-0f54-458d-b140-531942f6db2c/action-7cc79fcac6544959a1fd5d59f1660498_2a89f61a5db549e09d9f2cbc138d7efd_text_export.jpeg" width="560" alt="Backup and Restore page">

</details>

<details>
<summary><strong>Computes</strong></summary>

- **Primary – ACTIVE:** your main compute, awake right now. It sleeps when you stop working.
- **Size 0.25 ↔ 2 CU:** CU means **compute unit**. Neon **autoscales**: a little power for light work, more when a query needs it. Businesses pay for what they use.
- **Read Replicas:** read-only copies so reports and dashboards (like the Tableau work coming up) don't slow down the database handling sales.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/1861fbd9-d6ff-40da-b9b1-e9057a2a0659/action-e889d0c3bb524c99926895f2ebd5b220_b9a69f953c0d4c13b42d5cb9e0c0d4d1_text_export.jpeg" width="560" alt="Computes page showing the primary compute and autoscaling size">

</details>

<details>
<summary><strong>Realtime</strong></summary>

Realtime makes data **update live** in an app the moment it changes. For Second Chapter, a shopper could see an item marked "Sold" the second it's rung up. Leave this off.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/732cde7b-fae5-4d5b-bb4e-fdbb055f5a9f/action-f4dad10e064c4448ae1152f7510bd9dc_552d5af4df824704aaf6e225a904826f_text_export.jpeg" width="560" alt="Realtime page with a live stock update example">

</details>

<details>
<summary><strong>Data API</strong></summary>

An **API** lets other apps talk to your database over the internet. Think of a waiter: the app places an order, and the API brings back data from the kitchen. **Row-Level Security** lets businesses limit each user to only their own rows, like a customer seeing only their own orders.

Leave this off. Opening a database to the web is a big security decision.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/8fbd981f-888f-4b96-a0aa-421f3be77977/action-14ab0488588841018fb4e6d62b91f61b_7fe97e91fb8f48ff85103e0bd65e12f8_text_export.jpeg" width="560" alt="Data API page">

</details>

<details>
<summary><strong>Roles</strong></summary>

A **role** is a user account inside the database, with **permissions** that control what it can do. **neondb_owner** owns `neondb` and can do everything; it's who you are in the SQL Editor. At Second Chapter, a cashier role might only record sales, while a manager role can also update prices.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/8856526d-54a4-4cc0-91c2-13add26eb334/action-e30f50ead23d4aa4bff0dac2fd907b56_282d5ec1e4cd4a088d16fdf4629642a0_text_export.jpeg" width="560" alt="Roles page showing neondb_owner">

</details>

<details>
<summary><strong>Databases</strong></summary>

Your project has one database, **neondb**, owned by **neondb_owner**. That's how roles and databases connect. A business might keep sales in one database and employee records in another; we only need `neondb`.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/eb61e3c1-be67-43d3-8377-db6d808ff857/action-4f58ae9180204cb6ac3d576a408d4003_8f95aca4d0b942f29b9fb3d76e5046b2_text_export.jpeg" width="560" alt="Databases page listing neondb">

</details>

<details>
<summary><strong>Data masking</strong></summary>

Businesses often share data with analysts without exposing **PII** (personally identifiable information) like names, phone numbers, and addresses. Masking swaps real values for `*****` so the data keeps its shape but can't be traced to a customer. The Second Chapter customer rewards table would be a good candidate before sharing with a marketing team. Just looking today.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/dc0c821f-55d1-475c-ab41-6f4774cf6cd0/action-a42988f3c5b24260b4b0db7b6ea4b0bc_40696246ffa64e5badc682f463c54915_text_export.jpeg" width="560" alt="Data masking page showing masked ZIP codes">

</details>

---

## Part 3: Build the tables

In the left menu, click **SQL Editor**. This is where you'll write and run SQL, much like DataLab but connected to your own database. **Primary – Active** at the top means your compute is awake, and **neondb** shows which database your SQL runs against.

<img src="https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-16/41dc1d5b-ef08-4c21-96a2-08f465d0e94a/action-93c95ab6795e4200a3c66acccca08767_63efe5c22cd84930a01990337bfe020c_text_export.jpeg" width="560" alt="Neon SQL Editor with sample code">

> **Before you start:** Neon puts sample code in the editor. Select all of it and delete it. If you already clicked Run on the sample, that's okay; it made a practice table you'll clear in the [Start over](#start-over--troubleshooting) section.

### The rhythm for each round

1. Click the **copy** icon in the top-right corner of the round's code block.
2. Clear the editor, paste, and click **Run**.
3. Check the expected result, then move to the next round.

Clearing the editor between rounds keeps you from running a table twice (that gives an `already exists` error).

**Build order rule:** a table with a foreign key can only be built *after* the table it points to.

### How to read each CREATE TABLE

| Keyword | What it means |
|---|---|
| `PRIMARY KEY` | The column that makes each row unique (the PK in your drawing) |
| `REFERENCES` | A foreign key pointing to another table's primary key (the FK in your drawing, and one line on your schema) |
| `NOT NULL` | This column can't be left blank |
| `UNIQUE` | No two rows can have the same value |
| `DEFAULT` | The starting value if none is given |

IDs are stored as text (`VARCHAR`) so they can hold values like `C06` or `OR`.

### Round 1: Tables with no foreign keys

consignor, brand, category, tag, customer. Nothing points anywhere yet, so these go first.

```sql
-- CONSIGNOR: people who bring in items to sell.
-- Core table: every consignment store needs it.
CREATE TABLE consignor (
    consignor_id       VARCHAR(10)  PRIMARY KEY,
    consignor_fname    VARCHAR(50)  NOT NULL,
    consignor_lname    VARCHAR(50)  NOT NULL,
    consignor_phone    VARCHAR(20),
    consignor_percent  NUMERIC(5,2),          -- the consignor's split, like 40.00
    consignor_address  VARCHAR(150)
);

-- BRAND: lookup table so brand names are spelled the same way every time.
-- Decision table: it exists because of a business decision.
CREATE TABLE brand (
    brand_id    VARCHAR(10)  PRIMARY KEY,
    brand_name  VARCHAR(50)  NOT NULL UNIQUE  -- UNIQUE: no two rows can say "Levi's"
);

-- CATEGORY: lookup table so category names are spelled the same way every time.
-- Decision table. Business decision: each item belongs to ONE category.
CREATE TABLE category (
    category_id    VARCHAR(10)  PRIMARY KEY,
    category_name  VARCHAR(50)  NOT NULL UNIQUE
);

-- TAG: each tag color and the discount it sets at checkout.
-- Decision table. If tag colors didn't set a discount, this table would go
-- away and tag_color would just be a column in ITEM.
CREATE TABLE tag (
    tag_id        VARCHAR(10)   PRIMARY KEY,
    tag_color     VARCHAR(20)   NOT NULL UNIQUE,
    tag_discount  NUMERIC(5,2)  DEFAULT 0     -- percent off, like 50.00; starts at 0
);

-- CUSTOMER: shoppers in the rewards program.
-- Core table. Walk-in customers don't get a row here.
CREATE TABLE customer (
    customer_id               VARCHAR(10)   PRIMARY KEY,
    customer_fname            VARCHAR(50)   NOT NULL,
    customer_lname            VARCHAR(50)   NOT NULL,
    customer_phone            VARCHAR(20),
    customer_address          VARCHAR(150),
    customer_tier             VARCHAR(20),  -- a label like Silver or Gold (business decision: not a foreign key)
    customer_rewards_balance  INT           DEFAULT 0
);
```

✅ **Expected result:** 5 tabs, `1: CREATE` through `5: CREATE`, each saying *Statement executed successfully*.

### Round 2: Tables that point to Round 1

item, sale. Clear the editor first.

```sql
-- ITEM: every piece of inventory. The center of the schema.
-- Core table. Four foreign keys = four lines on the drawing:
--   CONSIGNOR |--< ITEM   (one consignor brings in many items)
--   BRAND     |--< ITEM   (one brand is on many items)
--   CATEGORY  |--< ITEM   (one category holds many items)
--   TAG       |--< ITEM   (one tag color is on many items)
-- No receipt_id here: in this version, items connect to sales through ITEM_SALE.
CREATE TABLE item (
    item_id           VARCHAR(10)   PRIMARY KEY,
    consignor_id      VARCHAR(10)   REFERENCES consignor (consignor_id),  -- left blank for donated items
    brand_id          VARCHAR(10)   REFERENCES brand (brand_id),
    category_id       VARCHAR(10)   REFERENCES category (category_id),
    tag_id            VARCHAR(10)   REFERENCES tag (tag_id),
    item_description  VARCHAR(200)  NOT NULL,
    size              VARCHAR(20),
    condition         VARCHAR(20),
    intake_date       DATE,
    original_price    NUMERIC(8,2),
    item_status       VARCHAR(20)   DEFAULT 'Available',  -- where the item is NOW: Available, Sold, On hold
    point_value       INT                                 -- business decision: points are tied to the item
);

-- SALE: one row per receipt (one checkout).
-- Core table. One foreign key = one line:
--   CUSTOMER |--< SALE   (one customer makes many sales)
-- No item_id here: one receipt can hold many items, and a primary key
-- can't repeat, so the items are listed in ITEM_SALE instead.
CREATE TABLE sale (
    receipt_id      VARCHAR(10)  PRIMARY KEY,
    customer_id     VARCHAR(10)  REFERENCES customer (customer_id),  -- left blank for walk-ins
    sale_date       DATE         NOT NULL,
    payment_method  VARCHAR(20)                                      -- cash, card, etc. (describes the whole receipt)
);
```

✅ **Expected result:** 2 tabs, `1: CREATE` and `2: CREATE`.

### Round 3: Tables that point to Round 2

item_flaw, item_sale. Clear the editor first. These go last.

```sql
-- ITEM_FLAW: each flaw on an item, typed as free text.
-- Decision table. One foreign key = one line:
--   ITEM |--< ITEM_FLAW   (one item can have many flaws)
-- One row per flaw, so a shirt with a stain AND a missing button gets
-- two rows. No lists in one cell (1NF).
CREATE TABLE item_flaw (
    flaw_id           VARCHAR(10)   PRIMARY KEY,
    item_id           VARCHAR(10)   NOT NULL REFERENCES item (item_id),  -- every flaw belongs to an item
    flaw_description  VARCHAR(200)  NOT NULL                             -- free text, like "stain on left cuff"
);

-- ITEM_SALE: the JUNCTION TABLE between ITEM and SALE.
-- Business decision: returned items go back on the rack with the SAME
-- item_id, so one item can be on many receipts AND one receipt can hold
-- many items. That's many-to-many, so it needs a junction table.
-- Two foreign keys = two lines:
--   SALE |--< ITEM_SALE   (one receipt lists many items)
--   ITEM |--< ITEM_SALE   (one item can be on many receipts, if resold)
-- The primary key is the PAIR (receipt_id, item_id): a composite key.
-- Each key is also a foreign key, which is why the drawing says (PK, FK).
-- 2NF check: sale_price depends on BOTH keys (this item on this receipt),
-- so it belongs here. sale_date and payment_method depend only on
-- receipt_id, so they stay in SALE.
CREATE TABLE item_sale (
    receipt_id  VARCHAR(10)   REFERENCES sale (receipt_id),
    item_id     VARCHAR(10)   REFERENCES item (item_id),
    sale_price  NUMERIC(8,2)  NOT NULL,          -- price paid for this item on this receipt
    PRIMARY KEY (receipt_id, item_id)            -- composite primary key
);
```

✅ **Expected result:** 2 tabs, `1: CREATE` and `2: CREATE`.

---

## Part 4: Check your work

Clear the editor and run this to list every table you built.

```sql
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public'
ORDER BY table_name;
```

✅ **Expected result:** 9 rows: `brand`, `category`, `consignor`, `customer`, `item`, `item_flaw`, `item_sale`, `sale`, `tag`.

You can also click **Tables** under Postgres database again. The screen that said *0 tables* now shows your 9. You built a working cloud database for a real kind of business, and that's a win worth celebrating.

**Pause and Reflect:** Pick one decision table (brand, category, tag, or item_flaw). How does having it help the business?

---

## Start over & troubleshooting

### Clear the Neon sample table

Only if you ran Neon's sample code earlier and see an extra table in your check (often named `playing_with_neon`). Use the name you actually see.

```sql
DROP TABLE IF EXISTS playing_with_neon;
```

### Drop all 9 tables

Only run this if you need to clear your database, for example before you build your own version. **Drop in reverse build order**: a table can't be dropped while another table still points to it.

```sql
-- Round 3 tables first
DROP TABLE item_sale;
DROP TABLE item_flaw;

-- Then Round 2
DROP TABLE sale;
DROP TABLE item;

-- Then Round 1
DROP TABLE customer;
DROP TABLE tag;
DROP TABLE category;
DROP TABLE brand;
DROP TABLE consignor;
```

**About CASCADE:** `DROP TABLE item CASCADE;` drops `item` **and** removes the foreign key links that point to it. The other tables stay, but they're no longer connected to `item`. It works, but it's easy to lose track of what changed, so use reverse build order when you can.

### Common errors

| Error | What it means | Fix |
|---|---|---|
| `relation "..." already exists` | You ran a CREATE TABLE a second time. | Clear the editor and paste only the round you haven't run yet. |
| `relation "..." does not exist` (while creating) | You ran a round before the round it depends on. | Run the earlier round first (build order rule). |
| `cannot drop table ... because other objects depend on it` | Another table still points to this one. | Drop the table that points to it first (reverse build order). |
| `table "..." does not exist` (while dropping) | That table was already dropped. | Delete that line, or use `DROP TABLE IF EXISTS`. |

Stuck? Share your screen with your project name showing, or reach out on Teams. Extra help is always available when you ask.

---

*Next up: adding data to your tables.*
