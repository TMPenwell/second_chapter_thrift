# Second Chapter: Build the Class Version in Neon

**AIS 2800 · Ohio University**

9 tables · 8 foreign keys · matches the class schema drawing

## How to use this script

Run each round in the **Neon SQL Editor**, one round at a time. Before you run the next round, comment out or delete the code from the round before it. Otherwise you'll see an `already exists` error.

**Build order rule:** a table with a foreign key can only be built **after** the table it points to.

| Round | Tables | Why this order |
|---|---|---|
| 1 | consignor, brand, category, tag, customer | No foreign keys |
| 2 | item, sale | Point to Round 1 tables |
| 3 | item_flaw, item_sale | Point to Round 2 tables |

**How to read each CREATE TABLE:**

- `PRIMARY KEY`: the column that makes each row unique (the PK in your drawing)
- `REFERENCES`: a foreign key that points to another table's primary key (the FK in your drawing, and one line on your schema)
- `NOT NULL`: this column can't be left blank
- `UNIQUE`: no two rows can have the same value
- `DEFAULT`: the starting value if none is given

IDs are stored as text (`VARCHAR`) so they can hold values like `C06` or `OR`.

---

## Round 1: Tables with no foreign keys

Build these first.

```sql
-- =====================================================================
-- ROUND 1: Tables with no foreign keys. Build these first.
-- =====================================================================

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

**Expected result:** 5 tabs, `1: CREATE` through `5: CREATE`, each saying *Statement executed successfully*.

---

## Round 2: Tables that point to Round 1

Comment out or delete Round 1 before you run this.

```sql
-- =====================================================================
-- ROUND 2: Tables that point to Round 1 tables.
-- =====================================================================

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

**Expected result:** 2 tabs, `1: CREATE` and `2: CREATE`.

---

## Round 3: Tables that point to Round 2

Build these last. Comment out or delete Round 2 before you run this.

```sql
-- =====================================================================
-- ROUND 3: Tables that point to Round 2 tables. Build these last.
-- =====================================================================

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

**Expected result:** 2 tabs, `1: CREATE` and `2: CREATE`.

---

## Check your work

List every table you built. You should see **9 tables**.

```sql
-- =====================================================================
-- CHECK YOUR WORK: list every table you just built.
-- You should see 9 tables.
-- =====================================================================
SELECT table_name
FROM information_schema.tables
WHERE table_schema = 'public'
ORDER BY table_name;
```

**Expected result:** 9 rows: `brand`, `category`, `consignor`, `customer`, `item`, `item_flaw`, `item_sale`, `sale`, `tag`.

---

## Start over: drop the tables

Only run this if you need to clear your database, for example before you build your own version.

**Drop in reverse build order.** A table can't be dropped while another table still points to it. Remove the `--` at the start of each line to run these.

```sql
-- =====================================================================
-- START OVER (only if you need to): drop tables in REVERSE build order.
-- A table can't be dropped while another table still points to it.
-- Remove the -- at the start of each line to run these.
-- =====================================================================

-- Round 3 tables first
-- DROP TABLE item_sale;
-- DROP TABLE item_flaw;

-- Then Round 2
-- DROP TABLE sale;
-- DROP TABLE item;

-- Then Round 1
-- DROP TABLE customer;
-- DROP TABLE tag;
-- DROP TABLE category;
-- DROP TABLE brand;
-- DROP TABLE consignor;
```

### Troubleshooting

| Error | What it means | Fix |
|---|---|---|
| `relation "..." already exists` | You ran a CREATE TABLE a second time. | Comment out or delete the rounds you've already run. |
| `cannot drop table ... because other objects depend on it` | Another table still points to this one. | Drop the table that points to it first (reverse build order). |
| `table "..." does not exist` | That table was already dropped. | Comment out or delete that line. Or use `DROP TABLE IF EXISTS`. |

**About CASCADE:** `DROP TABLE item CASCADE;` drops `item` **and** removes the foreign key links that point to it. The other tables stay, but they're no longer connected to `item`. It works, but it's easy to lose track of what changed, so use reverse build order when you can.
