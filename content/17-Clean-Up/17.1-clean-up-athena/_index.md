---
title : "Clean Up Athena"
date : "2025-08-10T20:24:00Z"
weight : 1
chapter : false
pre : " <b> 17.1 </b> "
---

Drop the analytics database created for this workshop.

#### Drop Database in Athena

1. Go to **Amazon Athena** → **Query editor**
2. In the query pane, enter the following SQL:

```sql
DROP DATABASE leftover_analytics;
```

3. Click **Run** to execute

![Athena Drop Database](/images/17/17-1.png?featherlight=false&width=90pc)

{{% notice note %}}
If tables were created under the database with external locations, you may need to drop the tables first or use `DROP DATABASE leftover_analytics CASCADE;` where supported.
{{% /notice %}}

#### Result

The `leftover_analytics` database is removed from Athena.


