# Second Chapter Security: MITRE ATT&CK + Case Study

**AIS 2800 · Ohio University · Week 14**
**Due:** Wednesday, December 2, 11:59 PM

> Prefer the step-by-step version with screenshots? [Open the Scribe](https://scribehow.com/o/tRYqoVDKQseRHf1hnUYbNQ/viewer/How_to_Navigate_and_Search_the_MITRE_ATTCK_Framework__1hyxvVo7Rk6q20yNEaYlcw)

---

## Would you know if someone was stealing your customers' data right now?

In 2015, a UK phone and internet company called TalkTalk found out the hard way. An attacker typed a few sneaky characters into an old web page and walked away with the personal details of about 157,000 customers. The attack, called SQL injection, was over ten years old and had well-known defenses. TalkTalk was fined £400,000 anyway.

Here's why that matters to you. You own Second Chapter now, and that includes every rewards customer's name and phone number. Whether you end up in marketing, finance or management, you'll be part of decisions about protecting customer data. Security teams use a shared language called **MITRE ATT&CK** to name and sort attacks, and today you'll learn to speak it.

You don't need to write any code. You'll search a website, read a short real-world case and connect it to your store, one step at a time. It takes about 45 minutes.

By the end, you'll be able to name a real attack the way security professionals do. You'll also have a head start on the security section of your final project.

**As you go:** each part ends with a **Pause and Reflect** question. Jot your answers down; you'll submit them at the end.

---

## Why this matters for business majors

You might be thinking, "Isn't this the IT department's job?" The World Economic Forum, a global organization of business and government leaders, says it isn't that simple.

In its *Global Cybersecurity Outlook 2022*, the WEF found a gap between the people running businesses and the people protecting them. Nearly all business executives (92%) said cyber risk was built into how their company manages risk. Only about half of security leaders (55%) agreed. When leaders don't share the same picture, security priorities clash, and companies are left exposed.

The report found that a successful breach cost a company an average of $3.6 million. Small and medium-sized businesses like Second Chapter were seen as the weakest link by nearly 9 in 10 security leaders.

That gap closes when business people can speak the language of security. That's what MITRE ATT&CK gives you: a shared way to talk about attacks, so the store owner and the security team are looking at the same picture.

[Read the WEF press release](https://www.weforum.org/media/closing-the-cyber-gap-business-and-security-leaders-at-crossroads-as-cybercrime-spikes)

---

## Part 1: Get to Know MITRE ATT&CK

1. Navigate to [https://attack.mitre.org/](https://attack.mitre.org/)

### What is MITRE ATT&CK?

MITRE is a not-for-profit organization that does research for the U.S. government. One of its best-known projects is **ATT&CK**, which stands for **Adversarial Tactics, Techniques, and Common Knowledge**. That's a long name for a simple idea: a free, public library of how real attackers break into systems, built from attacks that have actually happened.

Think of it like a field guide for security teams. A bird watcher uses a field guide to name what they're seeing. A security team uses ATT&CK to name what an attacker is doing, how they're doing it and how to stop it.

ATT&CK is organized around two ideas:

- **Tactics** are the attacker's *goals*, the "why." For example, getting in the door for the first time, or stealing data on the way out.
- **Techniques** are the *methods*, the "how." Each technique has an ID, like a SKU on a price tag, so everyone can refer to the same thing.

On the website, tactics run across the top as columns, and the techniques for each goal are listed underneath them.

**Why do businesses use it?** It gives everyone, from the IT team to the store owner, a shared language. Instead of saying "we got hacked," a business can say exactly which technique was used, look up who else has been hit that way and see which defenses MITRE recommends. That makes it easier to decide where to spend money on security.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/c701ae30-1ba4-4231-8f20-e8c0ec2f1465/action-15905f18b1b742ac9d79f5bfcd536289_6610435fafc84443803900cfab37fe10_text_export.jpeg)

### Explore ATT&CK Domains

Not every business runs on the same technology, so ATT&CK is split into three **domains**. Each one is a separate matrix of tactics and techniques built for a different kind of technology. Click **Tactics** in the top menu to see all three:

- **Enterprise** covers the systems most businesses run on: company computers, networks, cloud services, websites and databases. Second Chapter lives here. So does its rewards lookup page and its database in Neon.
- **Mobile** covers phones and tablets. Think of a store app where customers check their points, or the tablet a cashier uses to ring up a sale.
- **ICS (Industrial Control Systems)** covers the equipment that runs physical operations: factories, power plants, water treatment and pipelines. An attack here can stop a production line or shut off the power.

In the Enterprise matrix, each column is a **tactic**, the attacker's goal. Read across the top and you'll see goals like Reconnaissance, Initial Access and Execution. Under each one, the number tells you how many **techniques**, or methods, MITRE has recorded for that goal. Initial Access, for example, lists 11 different ways attackers get in the door.

2. Click **Tactics**.

    > **Quick reminder:** a **tactic** is the attacker's goal, the "why" behind what they're doing. Getting into a system for the first time (Initial Access) is a tactic. The techniques listed under it are the different ways to reach that goal.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/c701ae30-1ba4-4231-8f20-e8c0ec2f1465/action-15905f18b1b742ac9d79f5bfcd536289_db91d4676d1d463699303353dedc91bd_text_export.jpeg)

3. Explore the different tactics for each domain (Enterprise, Mobile and ICS).

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/ad42a1e9-94da-4bb7-975a-1a1230fb847a/action-4d854006e529413e86e5c6b4cda52189_d2ecebf0701c4ec481e45e0868539f53_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/6372bce4-399a-46c6-9293-865a9730236d/action-808b4a9f3acd455d92a60498c391fe97_b06a047c9cce4de7893f7b212f699630_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/57668ab1-20d2-43b8-8ae5-7e82a13936f3/action-cb0b154b5d4546cc8e6b6d3dd4b2228c_914415ac31184c33af52d8e2bdbbccad_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/1d9ebe24-51dd-474b-b680-97e87da2ea66/action-504e7b08e0c549f4b09bed0a521cb206_5c321981a5cc400e871ce5dcb79fcb73_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/dc6a1c13-b733-4986-aba6-27844827ea8c/action-3013890d89924b15a678bffb4f3dddda_0364ad47afbc46f88744298b8c57495d_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/4b9c1d01-a918-454f-978f-f36ea5988600/action-154a1424a5f64dc684f148bd24ab5382_f6f8f20f7b6f4e1d96538090d2117c9a_text_export.jpeg)

### Browse Techniques

4. Click **Techniques**.

    > **Quick reminder:** a **technique** is *how* the attacker reaches their goal, the "how" behind the attack. Exploit Public-Facing Application is one technique for getting in the door (Initial Access). Each technique has its own unique ID, like T1190, so everyone can point to the exact same method.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/fc1d5dd4-84cc-4ef8-ba44-2546d25bcf14/action-767443a76aab47f98c54b21fe6bc7d97_af34a089f8694e759233e23e99cb3f17_text_export.jpeg)

5. Review the techniques associated with each domain.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/13fe77e3-0b78-4b6c-9ab3-662707b40b49/action-1551553c44844e3099b3440a38eaf578_9a40abae003845ddbe0bbceca4a92f79_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/b6f8cf3d-7497-4bb6-a5d8-ab336f8b0c8f/action-31b5eb22ca7e4d7988db1b6d7a49ddf1_63d8b11b544044b4a027d6436613e965_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/08abb295-8699-46b6-8d6d-b77688256852/action-40510291486a4bfc934a7731fd7f397d_f0635996d9ce41b4b420c6bd492cbff1_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/d26df04e-59c2-44c6-b09f-709f512f484b/action-602df8ea8ee946d8b9ed0e14fd5593c2_ff9ba502f8b1466892d63d1be4791795_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/6f86c12c-c775-4a61-bc55-3db2d6ee05c7/action-96569bc8017e42ef8b6134021b1ca274_64e386e203db46319234b461a5e1ba94_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/885a05af-fdd5-4255-8351-79d988629d40/action-06033ba349564b3ba5cde70cf4cba11b_06fb7aa181234867a2eef8f0404c9eb3_text_export.jpeg)

### Review Resources

MITRE doesn't just list attacks. It also teaches people how to use ATT&CK. Click **Resources** in the top menu and you'll see a long list: Get Started, FAQ, ATT&CK Data & Tools, even a yearly conference called ATT&CKcon. Security teams around the world use these to train staff, plan defenses and share what they've learned.

There's a lot here, and you don't need all of it. For this walkthrough, we'll open **Get Started**, which explains the basics in plain language. Think of today as your introduction. If something catches your interest, feel free to click around and explore beyond it. That curiosity is a win worth celebrating.

6. Click **Resources**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/ba290cdf-830f-4d1f-b6b9-650dcd3ccd16/action-8111b62b46c940778e1f1e3c8cc3a775_bff01c543e4343708f10bc067bb41dc5_text_export.jpeg)

7. Click **Get Started**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/2df2c3a1-32ce-4d07-8028-14b9d6f761c7/action-07e2e21e59374d0e9eb64da31454f86d_c700cb53269b4fd8bd73e6e2cd86bb1f_text_export.jpeg)

8. Read and watch the video "What is ATT&CK?"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/ae0324a5-d19d-4476-be9a-93f51d39b97c/action-838975e781694e039b4f5d075a49a920_63830cc5dbdc45e6b0e3fa69362596a7_text_export.jpeg)

9. Read the "Key Concepts."

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/ad6ee68b-ddff-44c0-b264-53c4b0e0e7a4/action-4e709c192d0d4648834c274187a830ea_febb74fe2c2445f7865044b54553097c_text_export.jpeg)

10. Read "How can I use ATT&CK?"

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/202cbe5c-a09f-4d1b-b3a6-b7ee6e266f65/action-c997ee675b9e4dd8925d9b35f80142f3_aa7df90c9df246a28b8938bcdd782a39_text_export.jpeg)

> **Pause and Reflect 1:** In your own words, what is MITRE ATT&CK, and why would a business use it?
>
> **Pause and Reflect 2:** What's the difference between a tactic and a technique? Use an example from Second Chapter (or a shoplifter!) to explain.

---

## Part 2: Search ATT&CK

ATT&CK has hundreds of techniques, so scrolling through them isn't the fastest way to find one. Most of the time you'll start the way security teams do: with a name you've heard. Maybe it showed up in a news story, an alert or a meeting.

Let's try it with one you already know. Click **Search** and type **SQL injection**. Before you open anything, scroll through the results and notice how many groups, tools and techniques mention it. That tells you something: SQL injection isn't a rare trick. Real attackers use it again and again, which is why protecting Second Chapter's customer lookup matters.

11. Click **Search**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/bfb863ed-1013-45f9-bb79-b6952140918f/action-a2323140174f4265be1caf2b50187937_0a8b9601069d40bb8f3e587424c5d672_text_export.jpeg)

12. Click the search field.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/d96e1d96-8e48-4455-b462-ded375c1a343/action-4e1d9eb87d0b4cc8b83eca25537b9343_76fa20320dd341168f926c2107cd3920_text_export.jpeg)

13. Type **sql injection**.

14. Review the results. Notice the number of results associated with this type of attack. Review as you like, then click **×** to close the window.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/cb45e852-fc72-4d16-a8f2-99dcde5e07f9/action-0fbc5e59d5724282991d1f6ee7ce240d_95e508a4084b4bfcacef5c88ed5e7e57_text_export.jpeg)

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/84c9b077-cfdb-4627-8045-59cd1de43e8b/action-797b533bfde049e29d1d0fc068e1fa5e_2bb354d248a148ea892ccb9f20a7322a_text_export.jpeg)

### Search Using an ATT&CK ID

Searching by name is a good way to explore. When you already know exactly what you're looking for, though, the **ID** is faster and more precise. Security teams use IDs the way a store uses SKUs: two people might describe the same item in different words, but the SKU always points to one thing.

Here's when that matters. Imagine this memo lands in your inbox on a Monday morning:

> **MEMO: Second Chapter Thrift: All Staff**
> **From:** Store Management
> **Re:** Attempted attack on our rewards lookup page
>
> Over the weekend, our website flagged unusual activity on the rewards points lookup page. Someone typed code into the phone number box, trying to pull every customer's information at once. Our security review classified the attempt as **MITRE ATT&CK T1190, Exploit Public-Facing Application**.
>
> No customer data was taken. As a precaution, we have updated the page and are reviewing who has access to the customer table.
>
> **What we need from you:** If a customer reports anything unusual about their rewards account, write down the date, time and what they saw, and let a manager know right away. Please don't discuss the incident with customers.
>
> Questions? Stop by the office.

Most staff would read "T1190" and move on. You won't. Type **T1190** into the search box. The first result is the technique itself, tagged **Technique** and **Enterprise**. Below it are real campaigns where attackers used this same technique. In a few seconds, one ID tells you what the attacker tried, which goal it served and how other companies were hit the same way.

15. Let's do another search. Click **Search**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/811a1930-5af8-4731-95dc-55cabff4ad49/action-b763a01165944c9c9a948e5cabe24762_97ca77071a13486e9c6c420ae9affba3_text_export.jpeg)

16. Type **t1190**.

17. Click **Exploit Public-Facing Application, Technique T1190 - Enterprise**.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/4e87dabc-e10e-498e-99dd-0fb8923b1754/action-55f39bdf3bb7415aabb798547845654c_1b5da3c8ca064c64a94a97025d56846f_text_export.jpeg)

---

## Part 3: Review Technique Details

You've found T1190. Now let's read it like a professional. Every technique page in ATT&CK follows the same layout, so once you can read one, you can read them all.

Start with the box on the right. It's like a product label: it tells you the essentials at a glance.

- **ID:** T1190, the same ID from the memo.
- **Tactic:** Initial Access. This is the attacker's goal: getting in the door for the first time.
- **Platforms:** the kinds of systems this technique has been used against.
- **Contributors:** the people and companies who helped document it. Notice that one of them is Stifel Financial, a financial services firm. Businesses share what they learn so other businesses can defend themselves.
- **Last Modified:** ATT&CK is updated as attackers change their methods. This page was revised in May 2026.

Then read the description on the left. Notice the line about databases (like SQL). That's the connection to Second Chapter: a page anyone on the internet can reach, sitting in front of your customer database.

Keep scrolling and you'll find real-world examples, detection tips and mitigations: what happened to other companies, and what they could have done about it.

18. Review the information in the box on the right.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/8b8fca71-fb2e-417e-a9c7-0758d34456a7/user_cropped_screenshot_9b2f718f30454c68b49f48fc1e265059_text_export.jpeg)

### Reading Procedure Examples

19. Scroll down to **Procedure Examples**. This is where the technique stops being a definition and becomes real: it's a list of who has actually used T1190, and how.

The table has three columns:

- **ID:** the first letter tells you what kind of entry it is.
    - **G** = **Group**, a known team of attackers (for example, G0007 is APT28).
    - **S** = **Software**, a tool attackers use (for example, S0225 is sqlmap, a tool that automates SQL injection).
    - **C** = **Campaign**, a specific series of attacks (for example, C0002 is Night Dragon).
- **Name:** who or what it is. Click it to see everything else ATT&CK knows about them.
- **Description:** one or two sentences on what they did with this technique. This is the part to read.

**How to read a row:** ask yourself three questions.

1. **Who** did it? (the Name)
2. **What** did they go after? (look for words like *websites*, *servers* or *databases*)
3. **How** did they get in? (look for *SQL injection* or another method)

**Tip:** the list is long. Press **Ctrl+F** (**Cmd+F** on a Mac) and search for **SQL injection** to jump to the rows that match.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/5cd73aac-bcfa-444f-a5cd-e25581ecdd89/user_cropped_screenshot_b3527e90a2764c4792364485e891bfdc_text_export.jpeg)

> **Pause and Reflect 3:** Find one group, tool or campaign in Procedure Examples that used SQL injection. Who was it, and what did they go after?

### Reading Mitigations

20. Keep scrolling to **Mitigations**. If Procedure Examples show what went wrong for other companies, Mitigations show what they could have done about it. This is the part a business owner cares about most.

The table has three columns:

- **ID:** every mitigation starts with **M**, like M1050. Just like technique IDs, the same M number means the same defense everywhere in ATT&CK.
- **Mitigation:** the name of the defense. Click it to see every other technique it helps stop.
- **Description:** how that defense applies to *this* technique.

**How to read a row:** ask yourself three questions.

1. **What does it stop?** Does it keep the attacker out, or limit the damage once they're in? For example, **M1050 Exploit Protection** uses a web application firewall to block bad traffic *before* it reaches the website. **M1037 Filter Network Traffic** won't stop the first break-in, but it limits what the attacker can do *after*.
2. **What would it look like at Second Chapter?** Picture it in your store. Look back at the memo: "reviewing who has access to the customer table" is a mitigation in action.
3. **Is it worth it?** Every defense costs time or money. Which one gives the store the most protection for the effort?

**Tip:** you don't need every mitigation. Real businesses pick the few that fit their size and their biggest risks. Find the one you think fits Second Chapter best. You'll use it in your Pause and Reflect.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/2e6560f0-f387-475b-b3c5-0afe49081304/user_cropped_screenshot_91700a248e0147fd8e1ee30e91ec51ac_text_export.jpeg)

> **Stuck? Start here.** Try **M1026 Privileged Account Management**. The idea is simple: give each account only the access it needs to do its job. Security pros call this **least privilege**.
>
> At Second Chapter, the rewards lookup page only needs to show *one* customer's points. It doesn't need to see every customer's name and phone number, and it definitely doesn't need to change or delete anything. If the page's account can only read the points balance, an attacker who breaks in through that page gets very little.
>
> You've already done this! Think back to GRANT and REVOKE: you gave an account only the permissions it needed and took away the rest. That's M1026 in action.

### Reading the Detection Strategy

21. Keep scrolling to **Detection Strategy**. Mitigations try to stop an attack. A **Detection Strategy** helps you *notice* one while it's happening.

Fair warning: this part is written for security professionals, so you'll see technical terms like *HTTP*, *4xx/5xx* and *webshell*. You don't need to understand every word. Focus on the **pattern**.

The table has a few columns:

- **ID:** detection strategies start with **DET**. This one is DET0080.
- **Analytic ID:** each row starts with **AN** and covers a different kind of system, such as different kinds of web servers.
- **Analytic Description:** a numbered **chain** of warning signs, connected by arrows (→).

**How to read the chain:** think of it like spotting a shoplifter. One odd moment means nothing, but a string of them in a row tells a story. For T1190, the story goes:

1. **Strange requests:** someone keeps sending odd input to the website, like typing code into the phone number box.
2. **Errors pile up:** the website starts throwing more errors than usual.
3. **The server acts out of character:** it starts running programs it normally never would.
4. **Calling home:** the server reaches out to a computer the attacker controls.

Each step alone might be nothing. Together, they're a clear sign of an attack.

**How does that help the business?** Look back at the memo: "our website flagged unusual activity." That's step 1 being caught early, before any customer data left the building.

![Screenshot](https://colony-recorder.s3.us-west-1.amazonaws.com/files/2026-11-21/1aba1e87-2c39-4d0a-b3ad-03f6498d6d67/user_cropped_screenshot_5e64893dd2f841208661f6fe31fc2cf9_text_export.jpeg)

---

## Part 4: Case Study: TalkTalk (2015)

Now let's see what happens when a real company misses these steps.

TalkTalk is a phone and internet company in the United Kingdom. In October 2015, an attacker used SQL injection to steal the personal data of about 157,000 customers.

**How it happened**

- **They bought another company and inherited its systems.** TalkTalk had acquired another internet provider, Tiscali. Along with Tiscali came three old web pages that were still online and still connected to a customer database.
- **They didn't know what they owned.** TalkTalk never scanned those inherited pages, so it didn't know they existed or that they were open to SQL injection.
- **The software was out of date.** The database software had a known bug. A fix had been available for over three and a half years, but it was never applied.
- **They missed the warning signs.** Attackers had already used SQL injection on the same pages twice earlier that year, in July and September. No one was watching the pages, so no one noticed.

**What it cost**

- Customers' names, addresses, dates of birth, phone numbers and email addresses were taken. About 15,600 bank account numbers were stolen too.
- The UK's data protection regulator (the ICO) fined TalkTalk £400,000 (about $510,000), its largest fine ever at the time.
- The regulator pointed out that SQL injection had been well understood for more than ten years, and the defenses were well known.

Want the full story? Read the regulator's own timeline: [TalkTalk cyber attack: how the ICO investigation unfolded](https://ico.org.uk/about-the-ico/media-centre/talktalk-cyber-attack-how-the-ico-investigation-unfolded).

> **Pause and Reflect 4:** TalkTalk's attack matches the T1190 page you just read. Name two details from the case that fit "Exploit Public-Facing Application."

### Connect it to Second Chapter

Your story and TalkTalk's start the same way: a business bought from someone else, along with everything the previous owners left behind.

| TalkTalk | Second Chapter |
| --- | --- |
| Bought Tiscali and inherited its web pages | Bought the store and inherited the previous owners' data |
| Customer database reachable from a public web page | A website page where rewards customers type a phone number to see their points |
| Names, phone numbers and emails exposed | Your customers' names, phone numbers and points balances |
| Two earlier attacks went unnoticed | Would you know if someone tried? |

> **Pause and Reflect 5:** TalkTalk didn't know what it had inherited. What did *you* inherit when you bought Second Chapter, and what is one thing you would check first?
>
> **Pause and Reflect 6:** Pick one mitigation from the T1190 page and explain how it could protect Second Chapter's customers. How does that help the business?

---

## Wrapping Up

You just learned to read an attack the way a security team does, and you did it without writing a single line of code.

Starting with a name you'd heard, SQL injection, you:

- found its technique ID (T1190) and its tactic (Initial Access)
- saw the real groups and tools that have used it
- picked out the defenses that stop it
- learned the warning signs that it's happening
- saw what happened to a real company that missed them

That's the whole point of MITRE ATT&CK. It gives everyone, from the IT team to the store owner, one shared language. When a memo says "T1190," you now know what happened, why it matters and what questions to ask next.

You don't need to be a security expert to protect a business. You need to know enough to ask good questions, make smart decisions about where to spend money, and notice when something looks off. That's what the people who run Second Chapter need from you, whether you end up in marketing, finance or management.

---

## What to Submit

In Canvas, submit your answers to the six Pause and Reflect questions. A few sentences each is plenty.

- [ ] Pause and Reflect 1: What MITRE ATT&CK is and why a business uses it
- [ ] Pause and Reflect 2: Tactic vs. technique
- [ ] Pause and Reflect 3: One group, tool or campaign that used SQL injection
- [ ] Pause and Reflect 4: Two ways the TalkTalk case fits T1190
- [ ] Pause and Reflect 5: What you inherited and what you'd check first
- [ ] Pause and Reflect 6: One mitigation and how it helps Second Chapter

Hang on to your answers. The final project has a security section, and this is a head start on it.

---

### Sources

- [MITRE ATT&CK: T1190 Exploit Public-Facing Application](https://attack.mitre.org/techniques/T1190/)
- [MITRE ATT&CK: Get Started](https://attack.mitre.org/resources/)
- [World Economic Forum: Closing the Cyber Gap (Global Cybersecurity Outlook 2022)](https://www.weforum.org/media/closing-the-cyber-gap-business-and-security-leaders-at-crossroads-as-cybercrime-spikes)
- [ICO: TalkTalk cyber attack, how the ICO investigation unfolded](https://ico.org.uk/about-the-ico/media-centre/talktalk-cyber-attack-how-the-ico-investigation-unfolded)
