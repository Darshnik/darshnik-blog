---
title: "What LinkedIn's 100,000 Tables Taught Me About Data"
description: "Lessons from working with data at scale — not about the technology, but about the people and decisions behind it."
pubDate: 2026-03-05
tags: ["tech"]
featured: true
draft: false
---

When people hear "100,000 tables," they usually ask about the technology. What database? What schema? How do you even query that?

Those are the wrong questions.

The right question is: how do 100,000 tables *happen*? Because nobody sits down and designs a system with that many tables. It grows. Organically. Over years and years of decisions — some brilliant, some pragmatic, some deeply questionable — made by thousands of engineers who mostly never talked to each other.

Understanding that process taught me more about data than any textbook ever could.

## How tables are born

A table starts its life with purpose. Someone on the Messaging team needs to store read receipts. Someone on the Feed team needs to track impressions. Someone on the Ads team needs to record bid prices. Each table is clean, well-documented, and perfectly suited to its use case.

For about six months.

Then something happens. Another team discovers the table. They need *almost* the same data, but not quite. So they either:

1. Add columns to the existing table (fast, messy)
2. Create a new table that's 80% similar (clean, duplicative)
3. Build a view that joins this table with three others (clever, fragile)

All three choices are reasonable. All three create problems at scale.

## The naming problem

Here's something that sounds trivial but isn't: naming things.

At scale, table names become archaeological layers. You can read the organizational history of a company in its table names:

```
user_profiles              -- 2003, the early days
member_profiles            -- 2008, rebranding from "users" to "members"
member_profiles_v2         -- 2012, the great migration
member_data_unified        -- 2015, the data platform team's attempt at order
mbr_prof_unified_v3_final  -- 2018, someone gave up
```

This isn't a LinkedIn-specific problem. It's a *scale* problem. Every organization that lives long enough develops its own linguistic fossils.

## The ownership problem

The hardest problem in data at scale isn't technical. It's organizational.

Who owns a table? Not "who created it" — that person left three years ago. Not "who uses it" — that's literally everyone. Who is *responsible* for it? Who decides if a column can be deprecated? Who gets paged when the ETL job fails at 3 AM?

At small companies, this is obvious. At large ones, it's the single most important question you can ask about any piece of data infrastructure.

I've seen tables that were:
- Used by 50 teams
- Owned by zero teams
- Costing $200,000/year in storage
- Nobody could explain what three of the columns meant

This is not a failure of engineering. It's a failure of institutions. And it happens everywhere.

## What I learned

After working with data at this scale, here are the things I believe:

**1. Schema is destiny.** The way you structure your data in year one determines what's easy and what's impossible in year five. Think about it like city planning — you're laying roads that future generations will have to drive on.

**2. Documentation rots faster than code.** A wiki page about a table has a half-life of about 18 months. After that, it's actively misleading. The only documentation that stays current is the kind that's generated from the data itself.

**3. The real data model is social, not technical.** Understanding data at scale requires understanding the organization that created it. Why does this table exist? Which team's OKRs drove its creation? What political compromise does this schema represent?

**4. Simplicity is the hardest thing to maintain.** Anyone can add complexity. Removing it — deprecating a table, consolidating schemas, deleting a column — requires courage, coordination, and an almost religious commitment to simplicity.

**5. Every data problem is really a people problem.** The technology is the easy part. The hard part is getting humans to agree on definitions, own their data, and resist the urge to create "just one more table."

## The broader lesson

I think about data infrastructure as a metaphor for institutional knowledge in general. Every large organization — a company, a government, a university — accumulates layers of decisions, structures, and processes that made sense when they were created but eventually become inscrutable.

The challenge isn't building the thing. It's maintaining it. It's knowing when to refactor and when to leave it alone. It's understanding that every system you build will outlive your understanding of it.

That's humbling. And it's also kind of beautiful.

---

*If you've ever stared at a database schema and wondered "why?", I'd love to hear your story. Find me on [X](https://x.com/darshnik).*
