# Second Chapter: From Database to Dashboard

**AIS 2800 · Ohio University · Week 15**
**Due:** Wednesday, December 2, 11:59 PM

This assignment has two parts:

1. **[Part 1: Export your sales data from Neon](#part-1-export-your-sales-data-from-neon)**, about 5 minutes
2. **[Part 2: Build and publish a dashboard in Tableau Public](#part-2-build-and-publish-a-dashboard-in-tableau-public)**, about 30–45 minutes

Prefer screenshots on every step? Use the Scribe versions: [Part 1 Scribe](https://scribehow.com/o/tRYqoVDKQseRHf1hnUYbNQ/viewer/How_to_Export_Neon_Database_Data_to_CSV__HcOD1Q8DRQuefhAZbBSGyA) · [Part 2 Scribe](https://scribehow.com/o/tRYqoVDKQseRHf1hnUYbNQ/viewer/Create_and_Publish_a_Sales_Dashboard_in_Tableau_Public__F6tT3m1ISzmjA4Qi_00SFw)

---

## Part 1: Export your sales data from Neon

### It's been a year since you bought Second Chapter Thrift

When you took over, the store's sales lived in one messy file. Since then, you've normalized that data into a real database in Neon, with separate tables for items, sales, customers, consignors and more. That design keeps your data clean and consistent. But spreading data across tables also makes it harder to see the big picture at a glance.

Now it's time to plan for next year. Which categories bring in the most money? When are your busy months? Do donated items or consigned items earn the store more? To answer questions like these, you'll pull last year's sales back together into one **results table**, then take it into Tableau to look for trends.

This guide covers the first step: running the query in Neon and exporting the results as a **CSV** file. A CSV is a plain spreadsheet file that almost any tool can open, including Tableau and Excel. It's one of the most common ways businesses move data from where it's stored to where it's analyzed.

You'll use skills you already have: joins, LEFT joins and CASE. Copy the query, run it, and download your file. It takes just a few minutes.

**Before you start:** make sure your class version of Second Chapter is still loaded in Neon. You should see the class tables (item, sale, customer and the rest) in your project.

### Open the Project

**Step 2.** Navigate to [https://console.neon.tech](https://console.neon.tech)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/913370eb-1253-4e81-80b8-109b6b20efed/action-61c0910bcf9d413f8d18c21210c97fad_314e91056cf04826a0fae5014de444ad_text_export.jpeg)

**Step 3.** Click on your project

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/913370eb-1253-4e81-80b8-109b6b20efed/action-61c0910bcf9d413f8d18c21210c97fad_4fc4ba5fa21d4a0aa03334b9f9da135e_text_export.jpeg)

### Run the Query

**Step 4.** Click "SQL Editor"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/d5f561ba-915f-4fe2-b38a-5f8b14728c7c/action-d2b4091a4f97437d8a67c7ba3cc2029d_13c766216cab4b6ea34a6ceea9e4c0bb_text_export.jpeg)

**Step 5.** Click "Type SQL or Generate with AI..." and paste in this query:

```sql
SELECT
    s.receipt_id,
    s.sale_date,
    s.payment_method,
    COALESCE(cu.customer_tier, 'Walk-in')         AS customer_tier,
    i.item_id,
    i.item_description,
    c.category_name,
    b.brand_name,
    i.condition,
    t.tag_color,
    t.tag_discount,
    i.original_price,
    isl.sale_price,
    CASE WHEN i.consignor_id IS NULL THEN 'Donated'
         ELSE 'Consigned' END                      AS source_type,
    COALESCE(co.consignor_percent, 0)              AS consignor_percent
FROM item_sale AS isl
JOIN sale          AS s   ON isl.receipt_id  = s.receipt_id
JOIN item          AS i   ON isl.item_id     = i.item_id
LEFT JOIN category AS c   ON i.category_id   = c.category_id
LEFT JOIN brand    AS b   ON i.brand_id      = b.brand_id
LEFT JOIN tag      AS t   ON i.tag_id        = t.tag_id
LEFT JOIN customer AS cu  ON s.customer_id   = cu.customer_id
LEFT JOIN consignor AS co ON i.consignor_id  = co.consignor_id
ORDER BY s.sale_date, s.receipt_id;
```

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/61905b07-e2aa-4626-8918-581bcd9bd4ac/action-3ca0e4096a2048ed8edf1a06d729c0de_6bb0b49e9a5b4c58a2c5515a713393cc_text_export.jpeg)

**Step 6.** Click "Run"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/52305709-4dd6-4ba1-86ad-51d1483217e1/action-ae640da7de944ba5833b137ea8cee4c2_ce23de905dc9442fb3e3b3cd6e88e280_text_export.jpeg)

### Export the Results

**Step 7.** Click the export icon

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/241bc625-65ce-4ce2-977e-8a19a00b5593/action-3bce0959db9d446aa8a829b90963eace_675f6cabd2bd47e9ad16eb2aeede51a2_text_export.jpeg)

**Step 8.** Click "CSV"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/35b1ec73-0aec-4658-9d85-b1f6979f123f/action-2a1be2055a48440c901f1536b59cc9bb_e23d61f1f1ef462eb2ec20632675c7d1_text_export.jpeg)

### You did it!

You just took data spread across a normalized database, pulled it back together with a query, and exported it as a file you can use anywhere. This is how analysts work every day: the database stores the data, and a query brings back exactly what the business needs to see.

**Check your work:** your results should show **540 rows**, one for every item sold last year. If you see a different number, rerun the query and try the export again.

**Before you move on:**

- Find the CSV in your **Downloads** folder.
- Rename it to something you'll recognize, like `second_chapter_2026_sales.csv`.
- Save it somewhere easy to find.

**Up next:** you'll take this file into the **Tableau assignment**. There you'll turn 540 rows of sales into charts that show which categories bring in the most money, which months are busiest, and whether donated or consigned items earn the store more. That's where the data starts telling its story.

---

## Part 2: Build and publish a dashboard in Tableau Public

> **Prefer to watch?** [Watch the video walkthrough of Part 2](https://scribehow.com/embed/Create_and_Publish_a_Sales_Dashboard_in_Tableau_Public__F6tT3m1ISzmjA4Qi_00SFw?as=video). It opens in a new page, and you can pause it as you go.

### Turn last year's sales into a story

You have 540 rows of sales in a CSV file. That's a lot of numbers, and nobody wants to scroll through them to plan next year. A good chart can show in seconds what would take an hour to find in a spreadsheet.

That's what you'll build today: a **dashboard**, one screen with several charts that work together to answer real business questions about Second Chapter:

- Which categories bring in the most money?
- Which months are busiest, and which are slow?
- Do donated or consigned items earn the store more?

Dashboards like this are everywhere in business. Managers check them every morning, marketing teams use them to plan sales, and owners use them to decide what to stock and when to hire. Knowing how to build one, and how to explain what it shows, is a skill employers look for, whatever your major.

You'll use **Tableau Public**, a free version of one of the most widely used data visualization tools. It runs right in your browser, so there's nothing to install. You'll just need a free Tableau Public account.

This guide walks you through five parts, one click at a time:

- **Workbook Creation:** start a new project
- **Data Connection:** upload your CSV
- **Chart Creation:** build your charts
- **Dashboard Assembly:** put them together on one screen
- **Publishing:** share your dashboard with a link

**One thing to know:** anything you publish on Tableau Public can be seen by anyone. That's fine here, because Second Chapter's data is made up for class. In a real job, you'd use a private version of Tableau for company data.

**Want some inspiration first?** Scroll through **Viz of the Day** on the Tableau Public home page to see what's possible.

**Step 2.** Navigate to [https://public.tableau.com/app/discover](https://public.tableau.com/app/discover)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/50450377-5600-4e0b-9b58-62dc9467f63a/action-f16b8c1699c6442181a4d4c171d7f69e_eee6bd874fc849c2968a1f20099d55a5_text_export.jpeg)

### Workbook Creation

**Step 3.** Click **Create**, then click **Web Authoring**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/50450377-5600-4e0b-9b58-62dc9467f63a/action-f16b8c1699c6442181a4d4c171d7f69e_3898dad20ab94043ac6c7c70e9d2eb0f_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/9ee00e76-9959-4e95-8f9c-4aaf9bf50b8c/action-2f04eb689dbe494fa60edf04d5473af6_a3395b178afc42d49591c7e631856416_text_export.jpeg)

### Data Connection

**Step 4.** Click "Files"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/70ccd439-7321-4199-985f-1437aafefb44/action-29c91064824c42b1a9eb8551528f61cd_fd4ac4ce2c1a480cb0416cf2d3d60ccc_text_export.jpeg)

**Step 5.** Click "Upload from computer"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/6b078993-c5dc-464e-9ac8-1a5bcba2bf75/action-ce07735e028e4e0a88db9952719dd75c_e96f2e46f0564402940e2dd59e21c0b3_text_export.jpeg)

**Step 6.** Choose your `second_chapter_2026_sales.csv` file.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/70a1ab43-f0ac-422c-a062-61b4ca0b65fc/action-acc3872134a84be7bf63086ceaa6b414_6b7471d954e542ebb4422fc6ec39591a_text_export.jpeg)

### Chart Creation: Highest Earning Category

**Step 7.** Click "Category Name"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/fe21e13d-7047-4c95-aa4e-90dffa0cecb4/action-656c11f21e56431a982dc99c8b049316_32079e74b59e43d4b7d36bb583617ac1_text_export.jpeg)

**Step 8.** Drag it to Rows

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/26aecd3b-5c31-433e-8391-31e9d6202a90/action-64fd1dc08bee42509d885b53af0c8805_80609d84898a497ba9f44cc27c5e8342_text_export.jpeg)

**Step 9.** Click "Sale Price"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/bac3371a-e05a-45db-9278-c0d7a14a6784/action-fad17ac196114177b51e812a56763326_0f5ea659903148a0968fd2b0267ddc7c_text_export.jpeg)

**Step 10.** Drag it to Columns

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/c44abe37-42a8-4597-8114-82c04f61ddc4/action-2fabe74724ed4b0185c42e23a70fdb2b_37ba561cf67e42a4b7577d5f39ae7e86_text_export.jpeg)

**Step 11.** Click the drop down arrow.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/9f8ab070-94e3-48c7-b25d-5b7e495724d9/action-b1c8b5e0a98f47e4a84cde3649aedb7f_5ce501e2ad6e4de1ad7a09f2b7d51d2f_text_export.jpeg)

**Step 12.** Click "SUM(Sale Price)"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/1655066f-f078-445e-9d36-478e50704ecd/action-e2765cb7249e4678bc8cec58c735cfdc_1f0b1876265a4a599f81d1ea2fbafc71_text_export.jpeg)

**Step 13.** The rows will be sorted in Descending (or Ascending) order.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/54ed0c23-f8e6-49df-9e65-21eca7df277d/action-2d824f5d82db4b96ae41626ddd5d8a11_41c562f6f65945d3898f99fd81593b71_text_export.jpeg)

**Step 14.** Rename the sheet. Begin by right-clicking the tab name.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/58497190-c45a-41e9-b8ce-f4cf387d7201/action-68ad762197e84c108ed55194a14f4d89_bb4cc47beb414d23a5d442f5960b1700_text_export.jpeg)

**Step 15.** Click "Rename"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/95df3d18-40d1-478d-90f4-feb0f1b2f0ec/action-9dd23ac506764be19e0b1be35f6b9c3c_b93e8d015fbc4d1da5f29c5483f6c397_text_export.jpeg)

**Step 16.** Type "Highest Earning Category"

**Step 17.** Click "OK"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/ab98e699-0e55-4cb5-9106-2d7632b3953b/action-9ad956242b26478d99997d4044d1ee56_7f2fa48a35074e0abbab8ec7f3d53828_text_export.jpeg)

**Step 18.** We see the tab name is also reflected in the sheet heading.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/b6130884-22b7-4f56-8011-8e833fc85695/action-db60786ebb6d4bf6bd1b60243fb2f70e_f3cb2b63b4e045c191b3cc89351550e4_text_export.jpeg)

**Step 19.** Create a new sheet by clicking the new sheet icon next to the tabs.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/a8c714b6-2506-44f8-a992-eb15a77726aa/action-9f96d11cd3e141f58edca0fdae56021a_ded973054fb64e27a9f7af2e55cfe949_text_export.jpeg)

### Chart Creation: Sales Month to Month

**Step 20.** **Drag Sale Date to Columns and Sale Price to Rows.**

**Wait, why is there only one dot?**

That's expected! Tableau's first guess is to group dates by **year**. All of Second Chapter's sales happened in 2026, so every sale lands in one group, and you get one dot: last year's total, about $14,500.

The chart isn't wrong, it's just not useful yet. It answers "how much did we sell in 2026?" but not "how did sales change month to month?" A chart that works isn't always a chart that answers your question.

**Let's fix it:**

- Click the arrow on the **YEAR(Sale Date)** pill in Columns.
- In the lower half of the menu, choose **Month** (the one that shows an example like *May 2015*).
- The pill turns **green**, and your single dot becomes a line across January through September.

**Why the lower Month?** The upper options group by month name only, so every January would be lumped together across years. The lower options keep each month in its own year, which is what you want for a trend over time.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/b18993b4-36ab-48af-ac10-52a86e29176b/action-f16a908df83845ce9a1a822572f80ac0_e4ed5d3424a342d0a4fe46772c734a01_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/77f98f82-4e58-4bbf-8af6-4ecd87fd197b/action-389609a411e746ca835260ecba828200_54330b2d41c44fa38ae9619d9c77d0a2_text_export.jpeg)

**Step 21.** Now you can easily see the highest and lowest months in the line chart.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/edba0579-ca66-4b50-964d-c4df3c531712/action-6fbf0118b0404a4a8d7912bc8b5637ba_e91919b9f87e486f9f97752d7455c2a9_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/4ee8cd85-305d-456a-9488-e860054e1a84/action-aecea6896bbb4c53a0731755b600c1dd_0b99a11c830c4ea39b9316f16a3684d1_text_export.jpeg)

**Step 22.** Right-click the sheet tab, click **Rename**, type **Sales Month to Month** and click **OK**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/9d03f578-09dc-4c3e-8941-4e5c04076f77/action-b58c7d875ae24e6fa70cea61cbe85634_1e1f067264a54d378711f3f6555ad68e_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/bf17a19e-5bff-498f-bc43-4baaac15b0f9/action-c939d82a5fa0483ab0f001ba5294d3f8_b46470f6d09349038ad7aaac504499ca_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/a729db48-47ff-48e2-9231-0d19d8bfb038/action-99d210d314bf4c7ca4a75f680f9fc4b4_5ce5920c44e24693aa9619ae9458ac78_text_export.jpeg)

### Chart Creation: Consigned vs Donated Earnings

**Step 23.** **Creating a Calculated Field**

Here's a question every thrift store owner should ask: *when an item sells, how much of that money does the store actually keep?*

It depends on where the item came from:

- **Donated items:** someone gave the item away, so the store keeps **100%** of the sale.
- **Consigned items:** someone is selling through the store, so they get a cut. If a consignor's split is 60%, they get 60% of the sale and the store keeps 40%.

Look at your data pane. You have **Sale Price** and **Consignor Percent**, but no column that says what the store keeps. That's where a **calculated field** comes in.

A calculated field is a new column you create with a formula, much like typing a formula in Excel. Tableau runs it on every row, then lets you use the result like any other field.

Here's the formula you'll use:

```
[Sale Price] * (1 - [Consignor Percent] / 100)
```

Read it like a sentence: *take the sale price, and keep whatever percent is left after the consignor's share.*

- A **$20 consigned item** with a **60%** split: $20 × (1 − 0.60) = **$8** for the store
- A **$20 donated item** (consignor percent is 0): $20 × (1 − 0) = **$20** for the store

**Notice:** donated items show a consignor percent of **0**, not blank. That's thanks to the `COALESCE` in your Neon query. Without it, the formula would return blank for every donated item. Your SQL did this chart a favor before you ever opened Tableau.

**Check yourself:** when you're done, Donated should show about **$8,413** and Consigned about **$3,013**.

**Step 24.** Click the tab to create a new sheet.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/b770ccd0-58d4-47ec-8e90-09b6e4620581/action-cd2fdf5c90224699aba48f7c34d2fbd2_b3604ded319740b9a26ae7db9054dad6_text_export.jpeg)

**Step 25.** Click "Analysis"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/3e3766ed-fe29-4617-88d2-87f20bbe33c1/action-6aa19cf9f7f34f2585d7891d7067d14c_e1c0785b4d164c8996fdee14b206cfd0_text_export.jpeg)

**Step 26.** Click "Create Calculated Field..."

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/870a9370-dbae-4140-987f-096e1e62e5cd/action-0cc8e2b39ed34cafb3a1af6d748de735_a431d0cc07874528b3ee3432dedca9f4_text_export.jpeg)

**Step 27.** Create the calculated field using the specified name and formula

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/094067d9-75f2-4eb9-b2be-bf15829ad28d/action-6934c0c7a7a64d2a8f7e29132719c556_b7fdfb98469544b6bb782420024ace9f_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/194f0c40-c6b6-411e-aba0-cb8882f8add5/action-661bed5b4f6c4c4cacb06a958bbe9666_6041d6db660e42baa5b20b72ad229762_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/82217551-a7d0-455e-a7cc-95589e8c4660/action-d70a348bf8e745e49f61e29fd988e8c9_724595b4fcce4cbf946ca1ed2141c001_text_export.jpeg)

**Step 28.** Drag the Source Type and Store Keeps to Columns and Rows as shown.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/6928d457-2cec-450d-8320-f473893098d7/action-432ba7fea1a94bba9345249bf78a3bc4_cd0ce68afd9f4e19b3b4f3f1f372acac_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/90ab75c6-7f7f-4e45-827a-30855621e393/action-83b31848fa1743e0b0b198dc86f3630f_e6b6d9fa1f65402c8d1ce67ea810fc4d_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/c1d2a198-d07a-4ae9-9650-b8249313a697/action-c713ec3ed0474711be5eea1db8d815c0_fb965a4da67249f6adfcf95542b15397_text_export.jpeg)

**Step 29.** Rename the sheet to "Consigned vs Donated Earnings"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/01d7bfc5-fbba-4224-8d86-9a8820ece683/action-40e46c9ab9834ba1ab58d24151287a4c_6e1bcf37530b4f3ea4b70469d0c2338a_text_export.jpeg)

### Dashboard Assembly

**Step 30.** You now have three charts, each on its own sheet:

- **Highest Earning Category:** where the money comes from
- **Sales Month to Month:** when the money comes in
- **Consigned vs Donated Earnings:** how much of it the store keeps

Each one answers a question. But a manager planning next year doesn't want to click between three tabs. They want to see the whole picture at once.

That's what a **dashboard** does. It puts several charts on one screen so they can be read together. Together, they tell a bigger story than any single chart. For example, you might notice that Furniture earns almost as much as Clothing, and then wonder whether those big-ticket items were donated or consigned.

Building a dashboard is mostly drag and drop. You'll create a new dashboard, then drag each sheet onto it and arrange them so they're easy to read.

**Before you start, check your third chart:** your bars should show Donated at about **$8,413** and Consigned at about **$3,013**. At the bottom of the screen, the total should read **SUM(Store Keeps): 11,426**. That's how much of last year's $14,482 in sales the store actually kept.

**Tip:** think like the person who'll read this. Put the chart that answers the most important question at the top or on the left, where eyes land first.

**Step 31.** Click "New Dashboard"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/fd7c7e86-ef36-42a5-b0d3-a5af61a64ca3/action-6f461c856041457c87afceb5ea33b9b1_cacaf13d31244b73b1cc89954b8bfd89_text_export.jpeg)

**Step 32.** Click each sheet and drag into the main area

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/56c6e319-1f8f-4f85-b107-4dd29ca37db5/user_cropped_screenshot_e344d8c6b2084d2baabe8f16f29df3b8_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/4fd0bbf9-dc6d-4eed-9c5a-175907664901/action-cc2506f9bcd244ab96a521f8ad552c8e_d3b402e3dfd54432a845c4b15459657f_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/2a7cfe60-5bbe-43db-bd86-f7b298c48aaf/action-186e63daf31546e0b5f575a20aff7898_4035e0911cd54ad19d22a057f301970f_text_export.jpeg)

### Dashboard Views

**Step 33.** A dashboard is only useful if people can read it, and not everyone reads it on the same screen. The owner might check sales on a laptop at the register, while a manager glances at it on their phone between customers.

In this section, you'll learn to set your dashboard's **size** and use **Device Preview** to see how it looks on a desktop and on a phone. Think of it like a store window: the same display has to work for someone standing close and someone walking by.

**As you work, ask yourself:** if someone looked at this for ten seconds, would they know what it's telling them?

**Step 34.** Tableau lets you plan for this. On the left side of the dashboard, you'll find two tools:

- **Size:** sets how big the dashboard is. **Desktop Browser** fits a typical laptop or computer screen, which is what you'll use here.
- **Device Preview:** shows what your dashboard looks like on other screens, such as a **Phone**. You can even build a separate phone layout so it reads well on a small screen.

**Why this matters:** a dashboard only helps the business if people can actually read it. Before you publish, look at your work through your reader's eyes. Can you see every chart? Are the titles clear? Would someone glancing at it for ten seconds know what it's telling them?

**Check yourself:** all three charts should be visible on your dashboard, with **Sales Month to Month**, **Consigned vs Donated Earnings** and **Highest Earning Category** each showing its title.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/00dc8744-8c41-4e0f-9346-32005dea189f/action-e9e224474dc04a7ca73c6aa7b500c2a0_bc9427197f9f4000a4195ecc6bd3b3fd_text_export.jpeg)

**Step 35.** **Fixed size or Automatic?**

Right now, your dashboard is set to **Fixed size**: exactly 1000 pixels wide by 800 tall. That means it stays that size no matter who opens it. On a big monitor, it might sit in a corner with empty space around it. On a small laptop, viewers might have to scroll to see everything.

Click the **Fixed size** dropdown and choose **Automatic**. Tableau will then stretch or shrink the dashboard to fit whatever screen it's opened on.

**Which is better?** It depends on your reader.

- **Fixed size** gives you full control. Everything stays exactly where you put it. It's good when you know everyone uses the same kind of screen.
- **Automatic** adapts to the viewer. It's good when you don't know who'll open it, or on what device.

For Second Chapter, you don't know if the owner will check it on a laptop, a desktop or the computer at the register, so **Automatic** is a safe choice.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/80bac4ac-b973-4610-8c47-0ab3d46e8968/action-64904346028245c99cf2f54a749b3711_f6506236a049451bad3c6bcec3b96356_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/d9196043-d846-44ec-b956-6c3efbe5717f/action-9e0695ba65b44a24ba78612582b32121_64b0554a7b844f7b946d428fdf9fb9c5_text_export.jpeg)

### Device Preview

**Step 36.** **Preview it on other devices**

Your dashboard is now set to **Automatic**, so it resizes to fit any screen it's displayed on. But "fits" doesn't always mean "easy to read." Three charts side by side might look great on a laptop and be squeezed on a phone.

Click **Device Preview** to see for yourself. Tableau will show what your dashboard looks like on different devices, such as a desktop, a tablet or a phone.

**As you preview, ask yourself:**

- Can you still read every chart title?
- Are the labels and numbers big enough to see?
- Would the store owner understand it in a quick glance on their phone?

If the phone view feels crowded, that's normal. Professional dashboard designers often build a separate phone layout that stacks charts top to bottom instead of side by side. You won't need to do that for this assignment, but now you know the option is there.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/f944b07e-5abb-49f1-b60d-9f1df2805a86/action-a980d4c4e586471a9baae10d3e1fb08a_8d240839dc1d4424b6270ce8b4ca774f_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/e47c7d10-d5e3-469b-9e06-5f73a3b4f2c0/action-c5bc1fa55f974efe825b395648b28c07_065b5e2639b0434d94c8a7bea8075a81_text_export.jpeg)

**Step 37.** Follow the next few steps to explore different view options or practice on your own.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/fff16449-6d7e-4b31-ba5f-283281dcd036/action-080db0f0c3f14fe9a52012cabfa39757_9b2299e4d69a40eb99c07e484997c3f6_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/067c4e09-8169-42f6-a564-f6fa797c826c/action-3a2ebca0a4674dc0ac8ac9828d2436c2_0f05f587d22643cb9b1c08e5d01eebd0_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/040dc60b-4e86-4d1d-9783-17d827dac1c6/action-54a82972714f4d2b8957dcb145f91378_b8a220a5e4304b9085f97274074092cf_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/25c6ecbc-2d32-4f79-ac42-90408543d10d/action-67b0e3189b7f47bc97295e01706856cf_9f007abc88ed455fad929971e49c80cf_text_export.jpeg)

**Step 38.** **Tiled or Floating?**

You're now looking at the **phone layout**. Tableau stacked your charts top to bottom so they fit a narrow screen, which is much easier to read on a phone than three charts squeezed side by side.

On the left, under **Selected Item**, you'll see a checkbox called **Floating**. It controls how a chart sits on the dashboard:

- **Tiled (unchecked):** charts snap into place next to or under each other, like tiles on a floor. Tableau handles the spacing for you. This is the default, and it keeps things neat.
- **Floating (checked):** the chart sits *on top* of the dashboard, and you control exactly where it goes and how big it is, using the **X**, **Y**, **Width** and **Height** boxes.

Click **Floating** to see how it works. Notice that the position and size boxes become active, so you can move and resize this chart freely.

**When would a business use Floating?** For small extras, like a store logo in the corner or a note that says "Data through September 2026." For main charts, tiled is usually easier, because the layout stays clean when the screen size changes.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/16e7dee2-e5ad-49e5-b551-86fade283b0e/action-dd53ced4313841209e1cff250c87c45a_417d47b0c49a4232946d46a4f7b6c07c_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/b605d4a4-73da-4b55-9709-dffcff4121ac/action-4d508609f31d43a8a4e0e1a804a3a8e6_7bcfb04a528b42789d703f88e4aa6167_text_export.jpeg)

**Step 39.** **Uh oh, what happened to the charts?**

Look closely at the phone preview. The **Consigned vs Donated Earnings** chart is now sitting *on top of* **Highest Earning Category**, and the two charts overlap so neither one is easy to read.

That's the catch with **Floating**. A floating chart doesn't move out of the way for anything else. It stays exactly where you put it, even if that means covering another chart. On a big screen you might not notice, but on a narrow phone screen there's no room to hide it.

This is exactly why you preview before you publish. Better to catch it now than have the store owner open a jumbled dashboard on their phone.

**Let's fix it:**

- Click the **Device Type** dropdown and choose **Default**. This takes you back to the main dashboard layout.
- Click the chart that's floating, then **uncheck Floating**.
- The chart snaps back into place as a **tiled** chart, sitting neatly beside the others instead of on top of them.

**Takeaway:** for main charts, tiled is usually the safer choice. Save floating for small extras that won't get in the way.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/a3c49acf-9975-4f0d-8681-f6c7ffb44825/action-a64eb23f73e2430baaf39bcbe56c8cbd_5e76607fa2c14f44aeca75b26dc9e477_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/a0d92142-3749-482a-8783-5092c3b2ed46/action-c9728eb80efc4a7e8d7e31b3c82fdc32_a074d88b9e5b4280923241ef84499aa6_text_export.jpeg)

**Step 40.** Keep experimenting with different layouts until you're happy with how your dashboard looks on a desktop and on a phone.

> **Before you publish, remember: Tableau Public is *public*.** Anyone with the link can see your dashboard, and it shows up on your Tableau Public profile. That's fine here, because Second Chapter's data is made up for class. In a real job, never publish company or customer data to Tableau Public.
>
> **Here's the upside: this is portfolio material.** Your Tableau Public profile works like an online portfolio, a place to show employers what you can do. Once you publish, you'll have a shareable link you can:
>
> - add to your **LinkedIn** profile
> - include on your **resume** under projects or skills
> - send to a recruiter or bring up in an **interview**
>
> A link to a dashboard you built, with a clear story about what it shows, says a lot more than "familiar with Tableau" in a skills list. Take an extra minute to polish your titles and layout. This one's worth showing off.

### Publishing

**Step 41.** Click "Publish As..."

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/926ef4c1-db8b-4671-9d05-cfd45f4dfae7/action-afe51052c2ee42f3a8d1ae1af4b1f53a_26d3b6e8f17a430c8579898aaa3cf91a_text_export.jpeg)

**Step 42.** Name the workbook **Second Chapter Sales 2026**. Check the box to show sheets as tabs, then click **Publish**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/92b6eeaf-4552-4a3b-b75e-7ffc9e351e81/action-be19b20317ad4261a888319831b5b7ea_04f3c006f38f4010a6345169a36e3dce_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/b8c47b80-c47f-4cf7-90f4-c8b6551afe8f/action-b67c8e35f49645cf992d1eb2d04b2c1a_c91dc019ce2b4ed6b024ac6dad28e017_text_export.jpeg)

**Step 43.** Close the modal

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/d4e57a06-4147-4811-a598-26bf08c4cd60/action-fd7bfbf7a9164225b20ad955e3cf93f2_bdd76d405ee04733b39d8dd93d9e0491_text_export.jpeg)

### Finding the Viz and Sharing the Link

**Step 44.** Your dashboard is live! Now let's find it and get the link you'll submit.

Everything you publish is saved to your **Tableau Public profile**. Think of it as your online gallery: one place that holds every viz you've built. Knowing how to get there matters, because your profile link is what you'll share on LinkedIn or a resume, and it shows off *all* your work, not just one dashboard.

**Step 45.** Click your **profile icon** in the top right corner, then choose **My Profile**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/81ab04d5-736d-4407-a152-d1caa6417069/action-90e4fe147e0e4ba9b18c7e769aa866e9_bc456efb29d6482b84165010c3dfa7c9_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/6cca9595-8b93-4107-9a0b-72502d3413a4/action-feb68dc0f9c6457895bbcefaddcd5250_f312d36f25b9444695cef69c9d265aee_text_export.jpeg)

**Step 46.** **What's a viz?**

**Viz** (rhymes with "fizz") is short for *visualization*. On Tableau Public, it's the word for anything you publish: a single chart, a set of charts or a full dashboard like yours. Your **Second Chapter Sales 2026** is one viz.

Your profile shows each viz as a **card** with a preview image, the title and your name. Click the title **Second Chapter Sales 2026** to open it.

**If this is your first time using Tableau Public**, you'll probably see just *one* card: your Second Chapter dashboard. The other cards in the screenshot are from my past work.

**Step 47.** Click "Second Chapter Sales 2026"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/6226a3ba-ba4e-40dd-8fab-c0a8694fc2a8/action-13684e9ed2ad4ca7bd469903b2e80f16_2f9d6030a4b2410d97ea37bb8231e6bf_text_export.jpeg)

**Step 48.** Confirm everything looks as you intended. Click through each tab: **Highest Earning Category**, **Sales Month to Month**, **Consigned vs Donated Earnings** and **Dashboard 1**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/8afb60e4-5deb-4a36-97bf-52a8a1fe7858/action-1394a4abdfdb403bb38d86655bd36aad_f17e6515cc9043d995e1302205e07609_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/fb0eb944-fbb7-4dea-ae6e-20249fbfb609/action-ab25d3449eab4aba9350e70bfdec37e4_51b53c8ba2d7477c8384f84865401b58_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/7f9948fd-4d87-43e5-808f-55664ab271b2/action-30a530662cf0428392e759c049fb75fa_295962f312ab44d7ad40c594a803bd8e_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/74472d6c-b9b7-415d-9fc0-62a1dc38500d/action-ffd6af20f7af45d3b386d29fdf18ddfd_85ad771aee8d42a397f882fde6568bd5_text_export.jpeg)

> **Need to make a change?** Click the **Edit** button (the pencil-and-chart icon in the toolbar) to go back to the workbook and fix it. You'll land back in the same editing screen where you built your charts.
>
> When you're done, **publish again to save your changes**. Publishing to the same viz updates it, so the link you already shared should stay the same. Anyone who opens it will see your newest version.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/af3a6c58-7592-4800-a58d-7373d3d03b0c/screenshot_ffb75da068a1470aa2ba55a9d1386473_text_export.jpeg)

**Step 49.** **Sharing your viz**

Click the **Share** icon in the toolbar. A box will open with two options:

- **Embed Code:** a chunk of code that places your live dashboard inside a website or blog. A business might use this to put a dashboard on its company site. You don't need it for this assignment.
- **Link:** a regular web address that opens your viz. **This is the one you want.**

Click **Copy Link**, then paste it into your Canvas submission.

**Test it before you submit:** paste the link into a private or incognito browser window. That shows you exactly what your instructor, or a future employer, will see when they open it. If your dashboard loads, you're all set!

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/49d74e1f-129c-46cb-bea8-c17fa927144d/action-a791da1346604122a88de0510d5340b5_2a7a2b838a4b4ca7965892d06778c9db_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/14413552-3923-4842-b50d-6f1ff5c1ddd1/action-d397975238aa4030a78c9e6162d46d77_2ee1e747a9cd46dfb1f0aad4a3654e6f_text_export.jpeg)

> **Optional: Turn this into an interview story**
>
> You just built something you can show an employer. But a link alone won't get you the job. In an interview, someone is going to say, *"Tell me about a project you worked on,"* and you'll need the story behind it.
>
> **Why interviewers ask about past projects:** Employers use *behavioral questions* because past behavior is their best clue to future performance. According to MIT's career office, interviewers aim to objectively assess a candidate's past behavior as a predictor of future performance. Candidates are asked for specific examples of when they used particular skills or behaviors. You'll hear questions like *"What is a project you're most proud of?"* or *"Tell me about a time you failed."*
>
> **The STAR method** gives your answer a shape a listener can follow:
>
> - **S: Situation.** Where and when? Set the scene in a sentence or two.
> - **T: Task.** What were *you* responsible for?
> - **A: Action.** What did you do, and why? This is the heart of the story. MIT suggests it should be the largest part of your answer, about 60% of your time.
> - **R: Result.** What happened because of your work? Use a number if you can.
>
> **You already have STAR stories, and not just this one.** Look back at the last few weeks. You bought a messy thrift store file, made business decisions, normalized the data, built tables in Neon, protected customer data from SQL injection and turned a year of sales into a dashboard. Each of those is a story. So are projects from your other classes, a case competition or a part-time job.
>
> **This dashboard already has what a strong STAR story needs:**
>
> - **A number and where it came from:** pick one finding from your dashboard.
> - **Something that went wrong:** a chart that didn't look right at first, and how you fixed it.
> - **A decision you made, and the option you turned down:** for example, tiled vs. floating, or Automatic vs. Fixed size.
> - **Your proof:** your Tableau Public link.
>
> **Try it:** use the [**STAR Project Entry guide**](https://github.com/TMPenwell/littlegreenbook/blob/main/LGB_Part5_STAR_Projects.pdf), part of the career-prep workbook I created for ISAP students, to capture this project while it's fresh. It's easiest to talk about the week you finish it, and hardest the week someone asks. Then practice saying it out loud in about 90 seconds. MIT recommends preparing 3–5 stories in outline form rather than memorizing scripts, so you can adapt them during the interview.
>
> Read more: [The STAR Method for Behavioral Interviews (MIT Career Advising & Professional Development)](https://capd.mit.edu/resources/the-star-method-for-behavioral-interviews/)
>
> *This is optional and not graded. But future you, sitting in an interview, will be glad you did it.*

### Wrapping Up

Look at what you just did. You started with 540 rows in a CSV file and turned them into a dashboard that answers real business questions:

- **Which categories bring in the most money?** Clothing leads, but Furniture is close behind with far fewer items sold.
- **When are the busy months?** Sales peaked in July and dipped in September.
- **Do donated or consigned items earn the store more?** Donated items, by a wide margin, once you account for the consignor's share.

Along the way, you connected data, built charts, wrote a calculated field, designed for different screens and published your work for anyone to see. Remember the single dot that turned into a monthly trend? A chart that works isn't always a chart that answers your question. Knowing the difference is what makes you an analyst, not just someone who clicks buttons.

**Before you go:**

- Submit your **Tableau Public link** in Canvas by **Wednesday, December 2, 11:59 PM**.
- Open the link in a private or incognito window to make sure it loads.
- Save your link somewhere you'll remember. It's portfolio material!

**Up next: the final project.** You'll come back to Second Chapter one more time: making your own business changes to the database, building on this dashboard and protecting your customers' data. Everything you practiced today will come with you.

---

## What to Submit

In Canvas, submit your **Tableau Public link** by **Wednesday, December 2, 11:59 PM**.

---

### Sources

- [The STAR Method for Behavioral Interviews (MIT Career Advising & Professional Development)](https://capd.mit.edu/resources/the-star-method-for-behavioral-interviews/)
