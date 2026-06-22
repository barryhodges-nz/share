

![][image1]

**Genie Code Workshop Labs**

Author: Barry Hodges, Databricks Senior Solution Architect, New Zealand

Version: 3

Date: 22-Jun-2026

**Contents**

[Introduction	3](#introduction)

[The Databricks Workspace UI (after clicking '+ New', 'Notebook')	6](#the-databricks-workspace-ui-\(after-clicking-'+-new',-'notebook'\))

[Setup	7](#setup)

[Lab 1: Getting Started \- Setup, Modes and Navigation	7](#lab-1:-getting-started---setup,-modes-and-navigation)

[Lab 2: Exploratory Data Analysis with Agent Mode	9](#lab-2:-exploratory-data-analysis-with-agent-mode)

[Lab 3: SQL Query Optimisation and Debugging	10](#lab-3:-sql-query-optimisation-and-debugging)

[Lab 4: Data Workflow with Lakeflow Designer	12](#lab-4:-data-workflow-with-lakeflow-designer)

[Lab 5a: Data Workflow with Lakeflow Spark Declarative Pipelines	15](#lab-5a:-data-workflow-with-lakeflow-spark-declarative-pipelines)

[Lab 5b: Data Workflow with Lakeflow Spark Declarative Pipelines (Self-Directed)	16](#lab-5b:-data-workflow-with-lakeflow-spark-declarative-pipelines-\(self-directed\))

[Lab 6a: Data Analysis and Visualisation	18](#lab-6a:-data-analysis-and-visualisation)

[Lab 6b: Data Analysis and Visualisation (Self-Directed)	19](#lab-6b:-data-analysis-and-visualisation-\(self-directed\))

[Lab 7a: Price Prediction with Machine Learning	20](#lab-7a:-price-prediction-with-machine-learning)

[Lab 7b: Price Prediction with Machine Learning (Self-Directed)	22](#lab-7b:-price-prediction-with-machine-learning-\(self-directed\))

[Lab 8: Analysing Text with AI SQL Functions	23](#lab-8:-analysing-text-with-ai-sql-functions)

[Lab 9: Genie Spaces \- Talk to your Data	25](#lab-9:-genie-spaces---talk-to-your-data)

[Lab 10: Customise Genie Code	28](#lab-10:-customise-genie-code)

[What Next?	32](#what-next?)

## 

## **Introduction** {#introduction}

[Genie Code](https://docs.databricks.com/aws/en/genie-code/) is an autonomous AI partner purpose-built for data work in Databricks. Unlike other AI assistants, Genie Code is deeply integrated with Unity Catalog, allowing it to understand your complete data landscape, including tables, columns, and lineage. This contextual awareness enables Genie Code to accelerate complex data workflows while autonomously adapting to your specific data and governance model. Genie Code is designed for data teams to use every day, from experimentation and model development to production pipelines and BI dashboards. It is available throughout the Databricks Lakehouse, and chat threads persist as you navigate between pages. 

These hands-on labs will guide you through Genie Code's core capabilities using a [Databricks Free Edition](https://docs.databricks.com/aws/en/getting-started/free-edition) workspace.

### **What you will cover**

* **Lab 1: Getting Started \- Modes and Navigation** \- Get familiar with Genie Code basics.

* **Lab 2: Exploratory Data Analysis with Agent Mode** \- Let Agent Mode autonomously plan and execute a full exploratory data analysis (EDA).

* **Lab 3: SQL Query Optimisation and Debugging** \- Format, document, optimise, and repair broken SQL.   

* **Lab 4: Lakeflow Designer** \- Build a simple no-code ETL pipeline using the Lakeflow Designer canvas and prompts.

* **Lab 5a & 5b: Build a Data Transformation Workflow** \- Construct a full medallion ETL pipeline, extending it iteratively via follow-up prompts.

* **Lab 6a & 6b: Data Analysis and Visualisation** \- Create an AI/BI Dashboard from the Lab 5a or 5b tables \- all driven by natural language.

* **Lab 7a & 7b: Price Prediction with Machine Learning** \- Build, train, and evaluate an end-to-end ML model that predicts property price.

* **Lab 8: AI Functions** \- Use various AI functions in Databricks such as ai\_classify, ai\_summarize and ai\_query.

* **Lab 9: Genie Spaces** \- Build a Genie Space to support natural language analysis.

* **Lab 10: Customise Genie Code** \- Direct Genie Code to work the way you work.

**\*\* IMPORTANT \*\***

* You can complete the labs in this guide without prior Databricks experience, but a basic understanding of Databricks concepts such as Notebooks, Lakeflow Spark Declarative Pipelines, Machine Learning, etc. will help you better appreciate Genie Code's value.

* Apart from the Setup lab, labs 1–5, 8–10 are standalone with no pre-requisite dependencies on any other lab. Labs 6 and 7 depend on the tables created in Lab 5\.

* It is recommended you complete Labs 1–3 before trying any of the other Labs as this will get you familiar using Genie Code. 

* Self-Directed Labs (5b, 6b, 7b)

  * These three labs cover the same ground as Labs 5a, 6a and 7a \- but instead of giving you the prompts, they give you a starting point and a goal and let you drive the conversation with Genie Code. 

  * They are intended for participants who are comfortable enough with Databricks and Genie Code to design the workflow themselves.

  * State outcomes, not steps. Tell Genie Code what you want, not how to build it. Iterate via follow-ups when the first attempt isn't quite right.

* Instructions in earlier labs are in some cases more verbose than later labs \- the assumption is you don't need every specific detail as you move through labs. For example, at the start of most of the labs there is a check list of steps you must complete before proceeding (**similar** to the following). **Missing any means you will almost certainly run into problems**. Completing the Setup will help you understand how to complete these steps.

  '**\+ New**' → '**Notebook**' ✅, Default language '**SQL**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

* You don't need to complete every lab in a single sitting. Focus on the ones most relevant to your role. Keep in mind that these labs run on the Free Edition \- true to its name, it remains free \- so you can progress at your own pace.

### **Working with Free Edition and Genie Code** {#working-with-free-edition-and-genie-code}

* **Free Edition shares back-end resources** and has daily serverless compute [quotas and other limitations](https://docs.databricks.com/aws/en/getting-started/free-edition-limitations#compute-limitations), so expect it to be slower than production Databricks and potentially throttled (quotas reset the next day). But hey, it's free 🙂.

* **Genie Code is non-deterministic** \- your results may vary. So:

  * Always **review generated code** before executing \- Genie Code is powerful but can make mistakes.  
  * **Be specific** \- more context \= better output. Include column names, expected formats, and desired visualisation types.  
  * **Try both modes** \- switch between Agent Mode (for doing) and Chat Mode (for understanding) to see how they differ.  
  * **Work in one chat per lab** \- context compounds, and Genie Code gets better at predicting what you want as the conversation grows.  
  * **If Genie Code goes off-track** \- stop it (red square button) and re-prompt rather than letting it build on a bad foundation.  
  * **Most importantly, play** \- write your own prompts to explore. If you get errors, work with Genie Code to resolve.

* **Use** @\<table-name\> **to point Genie Code at a specific table**. When you paste a fully-qualified name from this doc (e.g. @samples.tpch.orders), click the pasted text and select the table from the picker. Shortcut: type just @orders and pick the right one from the list.

* **Approvals and controls** \- Genie Code asks for approval before running code or updating pipelines. Click '**Allow**', '**Decline**', '**Continue**', or '**Reject**' as appropriate. You can also select '**Allow in this thread**' or '**Always allow**' to reduce prompts or even [turn on](https://docs.databricks.com/aws/en/genie-code/use-genie-code#set-a-default-approval-mode) Auto-approve. Auto-approve is an AI classifier reviews each proposed action against your stated intent and approves or blocks each one, minimizing manual approvals while blocking risky actions. In these labs, we recommend you click '**Allow**' (one step at a time) so you can observe what is happening. To stop Genie Code mid-task, click the red stop button ![][image2].

* Genie Code is a **rapidly evolving** technology. The experience and features may change (for the better) when you next try these labs.

### **Resources:**

* [Databricks Free Edition Documentation](https://docs.databricks.com/aws/en/getting-started/free-edition)

* Genie Code Documentation ([AWS](https://docs.databricks.com/en/genie-code/index.html), [Azure](https://learn.microsoft.com/en-nz/azure/databricks/genie-code/), [GCP](https://docs.databricks.com/gcp/en/genie-code))

* [Introducing Genie Code](https://www.databricks.com/blog/introducing-genie-code) \- launch announcement and feature overview

* [Get to Know Genie Code](https://www.databricks.com/resources/demos/videos/get-know-genie-code) \- demo covering pipelines, dashboards, and Agent Mode

* [Databricks YouTube Channel](https://www.youtube.com/@Databricks/search?query=%22genie%20code%22) (filtered by 'Genie Code') \- tutorials and demos

* [Databricks Genie Code: Full Practice Guide and Examples](https://medium.com/dbsql-sme-engineering/databricks-genie-code-full-practice-guide-f3bcb13596f2)

* [From Genie to Genie Code: Agentic Data Work on Databricks](https://medium.com/data-science-collective/from-genie-to-genie-code-agentic-data-work-on-databricks-039593b01689)

* [Agentic Data Engineering with Genie Code and Lakeflow](https://www.databricks.com/blog/agentic-data-engineering-genie-code-and-lakeflow?utm_source=bambu&utm_medium=social&utm_campaign=advocacy)

## **The [Databricks Workspace UI](https://docs.databricks.com/aws/en/workspace/navigate-workspace)** (after clicking '+ New', 'Notebook') {#the-databricks-workspace-ui-(after-clicking-'+-new',-'notebook')}

![][image3]  

| Click to create a new Notebook / ETL Pipeline / etc. Bring up the Genie Code panel Toggle Genie Code between Chat and Agent modes Start a new chat Toggle Notebook default language between Python and SQL | Select compute type (Serverless or Serverless Starter Warehouse) Run Cell  Click '\+ Code' to add an empty cell below the current cell Unity Catalog \- explore data related objects  |
| :---- | :---- |

## ---

## **Setup** {#setup}

**Objective:** Setup your Databricks Free Edition workspace; Create a schema where objects such as tables will be created.

---

1. If you haven't already, sign up for **Databricks Free Edition** at [databricks.com/try-databricks](http://databricks.com/try-databricks) (work or personal email).

2. Once connected to your Databricks Free Edition workspace, click on '**\+ New**' in the main menu on the left, then select '**Notebook**'.

3. At the top left you may see '**Python**'. Click on this and change it to '**SQL**' (this sets the notebook's default language).

4. Open the Genie Code pane by clicking the **Genie Code** icon in the upper-right corner ![][image4].

5. Ensure '**Agent**' (versus '**Chat**') is selected at the bottom right.

6. In the chat pane, type the following prompt:

   Create a new schema workspace.genie\_demo.

7. When prompted, click '**Allow**' so Genie Code can run the generated code and create the schema which is used by several of the labs.

---

## **Lab 1: Getting Started \- Setup, Modes and Navigation** {#lab-1:-getting-started---setup,-modes-and-navigation}

**Objective:** Setup your Databricks Free Edition workspace; Learn to interact with Genie Code; Explore the UI; Use @ table references.

---

1. '**\+ New**' → '**Notebook**' ✅, Default language '**SQL**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

2. In the chat pane, type the following prompt:

   What tables are available in the samples.tpch schema? Describe each table and how they relate to each other.

3. Genie may ask to run code, potentially multiple times. During these labs we recommend you accept the default '**Ask every time**' and click '**Allow**'.

4. Review the final response. Genie Code uses Unity Catalog metadata to describe the tables and their relationships.

5. Use the @ reference to ask a specific question about a specific table (remember the tips above in [Working with Free Edition and Genie Code](#working-with-free-edition-and-genie-code)):

   How many columns does @samples.tpch.orders have? What does each column represent?

6. Next, ask Genie Code to generate a simple query:

   Write a SQL query that shows the top 10 customers by total order value from @samples.tpch.orders and @samples.tpch.customer.

7. Genie Code should generate the SQL in a new cell in the notebook. When prompted to run the cell, click '**Allow**'. 

   You may also see '**Run suggested**', '**Reject**', and '**Accept**' buttons in the cell \- ignore them and drive execution via Genie Code's '**Allow**'.

8. Try the /explain command. Either: 

* click the kebab at the top right of the cell and click on the Genie icon and type /explain  
* in your cell, press '**Cmd+I**' (Mac) or '**Ctrl+I**' (Windows) and type /explain  
* in the Genie Code pane type explain this query line by line  
9. Note there are several other [/ commands](https://docs.databricks.com/aws/en/notebooks/code-assistant#cell-actions) you can use with Genie Code including (but not limited to): 

   * /findTables \- searches for relevant tables based on Unity Catalog metadata

   * /getTableLineages \- view upstream and downstream dependencies.

   * /getTableInsights \- access metadata-driven insights, such as user activity and query patterns.

10. Switch Genie Code to '**Chat**' mode (bottom right of the Genie Code panel where it should currently show '**Agent**'). Enter the following question:

    What is a window function in Spark? How does it differ from a regular GROUP BY? When would I use one over the other?

11. Follow up with:

    What is the difference between RANK(), DENSE\_RANK(), and ROW\_NUMBER()? Show me an example using samples.tpch.orders where the difference matters \- where the three functions produce different results.

12. If example code appears in the Genie Code pane, use the '**\<\<**' button at the top of the snippet to insert it into a new cell.

    To create a new cell, move the mouse below the last cell until '- \- \-  **\+Code   \+Text**   ![][image4] **Genie Code**  \- \- \-' pops up \- click on '**\+Code**'.

    Once the code has been entered into the new cell, run the sql statement (click the '►' run cell button top left). Verify you can see where the three functions diverge.

---

## **Lab 2: Exploratory Data Analysis with Agent Mode** {#lab-2:-exploratory-data-analysis-with-agent-mode}

**Objective:** Use Genie Code to perform a full exploratory data analysis on a dataset, demonstrating Genie Code's ability to plan, execute, and iterate autonomously.

---

1. '**\+ New**' → '**Notebook**' ✅, Default language '**Python**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

2. Enter the following prompt:

   Perform an exploratory data analysis on @samples.nyctaxi.trips. Include: row count, schema overview, summary statistics for numeric columns, distribution of trip distances, fare amount trends by hour of day, and identify any data quality issues. Use Python with matplotlib for visualisations.

3. Watch as Genie Code plans the analysis steps / creates multiple notebook cells.

4. Once the cells have been created, either run each cell within the Notebook (as opposed to Genie Code) or drive the cells using Genie Code to observe what happens (i.e. click **run suggested** in the top left of each cell). For any cell you want to understand better, select the code, press '**Cmd+I**' (Mac) or '**Ctrl+I**' (Windows), and type:

   /explain

5. If you encounter any errors, follow the prompts to use Genie to diagnose the error and rerun revised code (this may be easier to do by clicking '**Accept**' in Genie Code and have it run the cells again for you \- it should handle any errors via retry, repeating if necessary until it works).

6. If you haven't already, in the Genie Code pane click **Allow** to run all cells. It will re-execute the same cells which is ok before moving on to summarise its findings.

7. Now ask a follow-up question in the Genie Code pane:

   Based on the EDA, what are the most interesting patterns? Are there any outliers worth investigating?

8. Let Agent Mode dig deeper into the patterns it identified (which is likely to include additional code cells \- run these via the Genie Code pane when prompted).

9. Review the deeper analysis.

---

## **Lab 3: SQL Query Optimisation and Debugging** {#lab-3:-sql-query-optimisation-and-debugging}

**Objective:** Use Genie Code's slash commands to tidy up, optimize and diagnose errors in SQL queries.

**New in this lab:** Genie Code includes three commands aimed at SQL hygiene and performance: /prettify (formatting), /doc (inline comments) and /optimize (rewrite for performance). When a cell errors, Genie Code's Diagnose Error feature reads the failure, proposes a fix, and offers to re-run. Some commands run from the Genie Code pane and some from the inline assistant (Cmd+I / Ctrl+I) \- the lab points out which is which.

---

1. '**\+ New**' → '**Notebook**' ✅, Default language '**SQL**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

2. Paste the following SQL statement into the empty cell at the top of the Notebook \-  this is intentionally suboptimal and messy:

   `SELECT c.c_name, sum(l.l_extendedprice * (1 - l.l_discount)) as revenue` 

   `FROM samples.tpch.customer c, samples.tpch.orders o, samples.tpch.lineitem l` 

   `WHERE c.c_custkey = o.o_custkey and o.o_orderkey = l.l_orderkey` 

   `AND o.o_orderdate >= '1994-01-01' and o.o_orderdate < '1995-01-01'` 

   `GROUP BY c.c_name ORDER BY revenue DESC`

3. Using the Genie Code pane, type:

   /prettify

4. You should see the original version highlighted in red and recommended changes highlighted in green. Click '**Accept'** to accept the formatted version. The query should now be more readable.

5. This next step does not happen in the Genie Code pane\! Instead, highlight the SQL code in the cell, and either click the kebab at the top right of the cell and click on the Genie icon or press '**Cmd+I**' (Mac) or '**Ctrl+I**' (Windows), and type:

   /doc

6. '**Accept**' the documentation \- Genie Code will add clear inline comments explaining the query logic.

7. Run the cell (hit the '►' run cell button top left).

8. Back in the Genie Code pane, type:

   Is the query suboptimal? If so, why?

9. Ask Genie Code to optimise it.

   /optimize

10. Review the suggested changes \- Genie Code may suggest replacing implicit joins with explicit JOIN syntax, adding appropriate filters, or restructuring the query. 

11. Accept and run the adjusted code via the Genie Code pane \- once done you should get an explanation why this new version is an improvement of the previous version.

12. An '**Optimize**' button also appears at the bottom right of the SQL cell. Optionally click it for a post-execution analysis, and apply any further recommendations.

13. If you ran the query before and after /optimize, try '**compare execution times**' (offered as a button, or type it into Genie Code if you don't see this button).

14. Now, create a new SQL cell with the following broken SQL query (move the mouse below the last cell until '- \- \-  **\+Code   \+Text**   ![][image4] **Genie Code**  \- \- \-' pops up \- click on '**\+Code**'):

    `SELECT c_name, total_spent`

    `FROM samples.tpch.customer`

    `JOIN (`

      `SELECT o_custkey, SUM(o_totalprice) AS total_spent`

      `FROM samples.tpch.orders`

      `WHERE o_orderdate > '1998-01-01'`

      `GROUPBY o_custkey`

    `) AS order_totals`

    `ON c_custkey = order_totals.o_custkey`

15. Run the cell \- it will fail. 

16. Genie Code may go straight to '**Attempting to fix**'. If not, click the '**Diagnose Error**' button that appears in the cell output.

17. Genie Code will identify the issues (e.g., `GROUPBY` should be `GROUP BY`, possible date range issues) and suggest a quick fix. Click '**Allow'** to apply and re-execute.

---

## **Lab 4: Data Workflow with Lakeflow Designer** {#lab-4:-data-workflow-with-lakeflow-designer}

**Objective:** Build a no-code ETL pipeline in Lakeflow Designer that uploads a CSV, applies quality transforms (case normalisation \+ a row filter), joins to a second source from Unity Catalog, aggregates, and writes a result table \- all driven by Genie Code from the Designer canvas.

**New in this lab:** Lakeflow Designer is a visual, no-code pipeline builder for ETL on Databricks. It uses a drag-and-drop canvas plus Genie Code, so a business analyst can build a production-grade pipeline without writing code. Behind the scenes, every Designer pipeline compiles down to a Lakeflow Spark Declarative Pipeline (see Labs 5a and 5b) \- so it gets the same governance (Unity Catalog), observability, scheduling and reliability as a hand-coded pipeline. See [Announcing Lakeflow Designer](https://www.databricks.com/blog/announcing-lakeflow-designer-no-code-etl) /  [Lakeflow Pipelines Editor](https://docs.databricks.com/aws/en/ldp/multi-file-editor).

---

1. '**\+ New**' → '**Notebook**' ✅, Default language '**SQL**' ✅,

2. Paste the following SQL statement into the empty cell at the top of the Notebook:

   `SELECT *`

     `FROM samples.tpch.orders`

    `WHERE o_orderdate >= DATE '1998-07-01'`

   `LIMIT 1000;`

3. In the result table, click the download icon ( **∨** ) at the bottom-left of the result grid and choose '**Download CSV**'**.** Save the file as '**orders\_recent.csv**' somewhere easy to find on your laptop. 

4. Click '**\+ New**' → '**Visual data prep**'. The Lakeflow Designer canvas opens.

5. Click '**Upload a file**', click on '**browse**', '**select files**' and select '**orders\_recent.csv**' from your laptop. 

6. When prompted for a destination Volume, click '**\+ Create volume**'. 

   * Volume name \= '**uploads**', 

   * Volume type \= '**Managed volume**'

   * Catalog \= '**workspace**' 

   * Schema \= '**genie\_demo**'

7. Click '**Create**' and then '**Upload**'. If processing does not move past “Preview” after a minute, refresh the browser tab. 

8. Once the upload finishes a new Source node appears on the canvas, connected to the uploaded '**orders\_recent.csv**' file (which is now stored in the volume you created).

9. In the Preview section below, scan the columns and notice:

   * 'o\_orderpriority' holds values like 1-URGENT, 2-HIGH, etc. \- already upper-case in this dataset, but we'll demonstrate a case-normalisation transform on it anyway.  
   * 'o\_totalprice' ranges across small and large orders. We'll filter out orders below 50,000.  
10. In the following steps you will use Genie Code to do the work. Note however you have the option of doing everything yourself by dragging operators from the left menu onto the Designer canvas and / or by right clicking on the canvas and selecting the required operator from there.

11. Also, unlike previous labs where you have used the Genie Code pane from the top-right of the page, this time you have the option of using the Genie Code pane at the bottom of the canvas. What follows assumes you are using the Genie Code pane on the Designer canvas.

12. In the Genie Code pane on the Designer canvas, enter the following prompt:

    Remove rows where o\_totalprice is less than 50000 and lower-case the o\_orderpriority column. 

13. Genie Code should create two new operators connected downstream from the source. Click '**Accept All**'.

14. Inspect the filter node:

    * Click the filter node, then the Edit operator icon. This will open the editing pane on the right where you can see an expression being applied to the source data similar to `o_totalprice is greater than or equal to "50000"`.

    * Sort the output preview at the bottom right by `o_totalprice` ascending and confirm the smallest value is now ≥ 50,000. The row count (at the very bottom) should also drop from the 1000 rows showing under the Input preview.

15. Inspect the case-lowering node:

    * Click the case-lowering, then the Edit operator icon \- you should see something like `LOWER(o_orderpriority)`.

    * Compare `o_orderpriority` in the Input / Output previews to confirm the column is now lower-case in the output.

16. Add the customer dimension as a second source. Using Genie Code, prompt:

    Add samples.tpch.customer as a source.

17. Click '**Accept All**'.

18. Click on the Customers source operator, then change '**Rows scanned: Limit**' to '**Rows scanned: Max**' under the output pane (see very bottom of the output pane). This ensures all the rows from the customer table are brought through in the preview.

19. Ask Genie Code to join the two datasets:

    Join the orders source with the customer source. Every order should show the customer details.

20. Click '**Accept All**'. 

21. Tidy the canvas: right-click on the canvas and click on the **Auto layout** button or select it from the top of the canvas.

22. Click the Join node, then the Edit operator icon. Note:

    * The join keys (`o_custkey` \= `c_custkey`).

    * The join type (`Left join`)

    * The rows produced in the output include both fact and dimension columns (e.g. o\_totalprice and c\_name).

23. Ask Genie Code to aggregate:

    Give me the average o\_totalprice, and the count of orders, grouped by customer market segment (c\_mktsegment).

24. Click '**Accept All**'. 

25. Inspect the new aggregation node \- Logic and Input/Output preview should show one row per market segment with the average price and order count. 

26. Ask Genie Code to write the results to a table:

    Write the data to a table orders\_avg\_by\_segment in the schema workspace.genie\_demo.

27. Click '**Accept All**'. 

28. Click on the final output node,then the Edit operator icon \- you should see '**Run**' in the operator editor.

29. Click '**Run**'.

30. Once the run has successfully finished, click on '**View in Catalog'** in the operator editor (table symbol on the top right). This will open Unity Catalog in a new tab.

31. Click '**Sample Data**' (you may need to start the compute). You should see five rows \- one per TPC-H market segment (AUTOMOBILE, BUILDING, FURNITURE, HOUSEHOLD, MACHINERY) with average price and order count.

32. Click '**Lineage**', '**See lineage graph**' to see the associated python notebook (which always opens in Lakeflow Designer) and sources (orders\_recent.csv file in the volume and the customers table in the samples.tpch schema).

---

## **Lab 5a: Data Workflow with Lakeflow Spark Declarative Pipelines** {#lab-5a:-data-workflow-with-lakeflow-spark-declarative-pipelines}

**Objective:** Use Genie Code to build a simple data transformation workflow using Lakeflow Spark Declarative Pipelines, demonstrating Genie Code's data engineering capabilities. **This lab contains all the prompts you need to achieve the objective. If you prefer more DIY, skip to Lab 5b.**

**New in this lab:** Lakeflow Spark Declarative Pipeline is a declarative, framework-managed way to build batch or streaming ETL pipelines in SQL or Python. You describe the target tables you want; Databricks figures out the dependencies, ordering, retries, and incremental processing for you. Pipelines are governed by Unity Catalog and run on Databricks Runtime. See [Lakeflow Spark Declarative Pipelines](https://docs.databricks.com/aws/en/ldp/) / [Concepts](https://docs.databricks.com/aws/en/ldp/concepts) / [Medallion architecture](https://docs.databricks.com/aws/en/lakehouse/medallion).

---

1. '**\+ New**' → '**ETL pipeline**' ✅, Default language '**SQL**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

2. In the ETL Pipeline UI, change the pipeline catalog and schema from '**workspace.default**' to '**workspace.genie\_demo**' (top left) to avoid catalog permission issues.

3. Enter the following prompt to create the bronze tables:

   Create a pipeline with bronze streaming tables that ingest samples.wanderbricks tables properties, reviews, hosts, amenities, property\_amenities, destinations. No transformations, just add table comments. Target schema workspace.genie\_demo.

4. Genie Code may go ahead and create the python files required to complete this step. Genie Code may instead provide you with a plan (e.g. you may see something like 'Does this structure work for you, or would you like to modify the naming or organization?', followed by some suggested follow up prompts. Click the prompt that creates the python files (e.g. 'Yes, proceed with this structure').

5. Feel free to click on any of the generated files to see the python code generated for each table. 

6. When prompted '**Dry-running pipeline**', click '**Allow**'. You may also get warned "**blocked execution for safety reasons**" \- click '**run**' to continue. 

7. Dry-running the pipeline checks the code to make sure it works as a unit. If the Dry run fails, it should diagnose what went wrong and retry. 

8. Once the Dry run completes without error you will be prompted to '**Running pipeline**'. Click '**Skip**'.

9. Now ask Genie Code to create the silver tables:

   Add silver tables in same schema that clean the bronze layer: cast prices to double and dates to date type, put in expectations that drop rows where base\_price is null or zero, join amenities to property\_amenities to get amenity names per property, aggregate reviews per property (avg scores, review count, most recent review date), standardise categoricals to lowercase. Calculate host\_tenure\_days from host start date.

10. Once the Dry run completes without error you will be prompted to '**Running pipeline**'. As before, click '**Skip**'.

11. Finally ask Genie Code to create the gold table:

    Add a gold table gold\_price\_prediction\_features in the same schema that joins all silver tables into one denormalised row-per-property table. Include base\_price, property features, host features including host\_tenure\_days, destination/location features, aggregated review metrics, and pivot the top 15 most common amenities into binary flag columns. Add calculated features, price\_per\_person and price\_per\_bedroom. Add column comments.

12. Once the Dry run completes without error, when prompted with '**Running pipeline**', this time click '**Allow**' (alternatively click '**Run Pipeline'** in the top right). Make sure to select workspace.genie\_demo for the pipeline table creation.

13. Once the pipeline starts running, switch from the Genie Code view to the Pipeline Graph (top right on far right \-![][image5]) and monitor the pipeline run (expand the pane to see the Pipeline Graph more clearly).

14. After the pipeline completes, you can toggle back to Genie Code to see final checks and messages Genie Code applied. 

15. Click on '**Runs**' under '**Data Engineering**' in the left hand menu navigator.

16. Click on '**Pipelines**' \- you should see your pipeline execution. Click on the pipeline Start time or Name to open the pipeline run and explore.

17. In the Pipeline graph, hover over gold\_price\_prediction\_features, click the kebab (3 dots) → '**View in catalog**'. In the Unity Catalog tab that opens, click '**Sample Data**' to see the rows (you may need to click '**Select Compute**' first).

---

## **Lab 5b: Data Workflow with Lakeflow Spark Declarative Pipelines (Self-Directed)** {#lab-5b:-data-workflow-with-lakeflow-spark-declarative-pipelines-(self-directed)}

**Objective:** Use Genie Code to build a simple data transformation workflow using Lakeflow Spark Declarative Pipelines, demonstrating Genie Code's data engineering capabilities \- design and prompt the pipeline yourself **(refer Lab 5a if you need help)**.

**New in this lab:** Lakeflow Spark Declarative Pipeline is a declarative, framework-managed way to build batch or streaming ETL pipelines in SQL or Python. You describe the target tables you want; Databricks figures out the dependencies, ordering, retries, and incremental processing for you. Pipelines are governed by Unity Catalog and run on Databricks Runtime. See [Lakeflow Spark Declarative Pipelines](https://docs.databricks.com/aws/en/ldp/) / [Concepts](https://docs.databricks.com/aws/en/ldp/concepts) / [Medallion architecture](https://docs.databricks.com/aws/en/lakehouse/medallion).

---

1. '**\+ New**' → '**ETL pipeline**' ✅, Default language '**SQL**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

2. At the top of the pipeline UI ensure the catalog/schema is set to `workspace.genie_demo` (top left)

3. **Starting point:** The `samples.wanderbricks` schema contains source tables for short-term-rental property data: `properties`, `reviews`, `hosts`, `amenities`, `property_amenities`, `destinations`.

4. **Goal:** A Lakeflow Spark Declarative Pipeline producing a single gold table `gold_price_prediction_features`, ready to feed an ML model that predicts `base_price`. The table must be denormalised (one row per property), pull features from all six source tables (property attributes, host attributes, destination/location, review aggregates, amenity flags), and contain at least two calculated features.

5. **Constraints:**

* Use the medallion pattern: bronze \-\> silver \-\> gold

* Bronze must be **streaming** with no transformations \- just ingestion plus table comments

* Silver must enforce data quality (e.g. drop rows where `base_price` is null or zero, cast prices to double and dates to date type)

* Silver must aggregate reviews per property (avg scores, review count, most recent review date)

* Gold must pivot the most common amenities into binary flag columns

* All tables land in `workspace.genie_demo`

6. **How to approach:** 

* Using Genie Code, describe the medallion pipeline you want in your own words. 

* Resist the urge to dictate every column \- let Genie Code make sensible choices and iterate via follow-up prompts when the result isn't quite right. 

* Use `@samples.wanderbricks.<table>` references when you want to be specific. 

* When prompted to dry-run, click "**Allow**"; when prompted to run the full pipeline, "**Skip**" until you have all three layers in place, then "**Allow**" the final run.

7. **Done when:**

* Pipeline runs end-to-end without error and the Pipeline Graph shows bronze \-\> silver \-\> gold flow

* `gold_price_prediction_features` is queryable and joins data from at least four source tables

* You can explain (and Genie Code can explain) every transformation in the pipeline

---

## **Lab 6a: Data Analysis and Visualisation** {#lab-6a:-data-analysis-and-visualisation}

**Objective**: Use Genie Code within AI/BI Dashboards to build an interactive business dashboard from the pipeline tables created in Lab 5a or 5b, demonstrating how Genie Code can generate datasets and widgets directly on a dashboard canvas. **This lab contains all the prompts you need to achieve the objective. If you prefer more DIY, skip to Lab 6b.**

**New in this lab:** Databricks AI/BI Dashboards are governed, low-code dashboards built natively on Unity Catalog. Each dashboard is composed of datasets (SQL queries against your tables) and widgets (the visualisations that read from those datasets). Genie Code can author both \- you describe the chart you want and it produces the dataset SQL plus the widget on the canvas. When you publish, the dashboard becomes available to viewers and Databricks automatically creates a companion Genie Space, letting end users ask follow-up questions of the same data in natural language. See [Databricks AI/BI](https://docs.databricks.com/aws/en/ai-bi/), [What is a Genie Space](https://docs.databricks.com/aws/en/genie/).

---

1. **\*\*\* IMPORTANT \*\*\*** this lab requires the pipeline from Lab 5a or 5b to have completed successfully.

2. '**\+ New**' → '**Dashboard**' (a blank AI/BI Dashboard will open) ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

3. Enter the following prompt to create the first dataset and widget (click '**Allow**' if prompted, this time and each time throughout this lab):

   Using workspace.genie\_demo.gold\_price\_prediction\_features, add a dataset and widget showing total properties, average base\_price, average price\_per\_person, and average price\_per\_bedroom as a counter row across the top of the dashboard.

4. Now ask Genie Code to add a price distribution chart:

   Add a dataset and widget showing the distribution of base\_price as a histogram. Title it "Price Distribution".

5. Next, ask for a property features analysis:

   Add a dataset and widget showing average base\_price by number of bedrooms as a bar chart. Title it "Average Price by Bedrooms".

6. Add a review metrics widget:

   Using workspace.genie\_demo.silver\_reviews\_aggregated, add a dataset and widget showing a scatter plot of average review score vs total review count per property. Title it "Review Score vs Review Volume".

7. Add a host analysis, a destination breakdown and an amenity impact analysis:

   Using workspace.genie\_demo.gold\_price\_prediction\_features, add a dataset and widget showing the relationship between host\_tenure\_days and average base\_price. Bucket host tenure into 6-month intervals and show average price per bucket as a bar chart. Title it "Price by Host Experience". After that add a dataset and widget showing average base\_price and property count by destination as a table, sorted by average price descending. Title it "Destination Summary". Finally using the amenity flag columns in workspace.genie\_demo.gold\_price\_prediction\_features, add a dataset and widget that calculates the average base\_price for properties with vs without each of the top 15 amenities. Show the price difference as a horizontal bar chart sorted by impact. Title it "Amenity Price Impact".

8. Finally, review the dashboard layout. Ask Genie Code to tidy it up:

   Give the dashboard tab a name and rearrange the layout so the counters are at the top, the price distribution and bedrooms charts are side by side below, then the scatter plot and host experience charts side by side, and the destination table and amenity impact chart at the bottom.  Use colours more effectively. 

9. Click on the '**Data**' tab (top left of the Dashboard) to see all the datasets Genie Code generated to support these visualization widgets (in each case created from a SQL dataset). 

10. Click '**Publish**' (top right corner), accept defaults for subsequent prompts.

11. Click '**View Published**' (top middle) to see the Dashboard as end users will see it (close Genie Code). 

---

## **Lab 6b: Data Analysis and Visualisation (Self-Directed)** {#lab-6b:-data-analysis-and-visualisation-(self-directed)}

**Objective**: Use Genie Code within AI/BI Dashboards to build an interactive business dashboard from the pipeline tables created in Lab 5a or 5b, demonstrating how Genie Code can generate datasets and widgets directly on a dashboard canvas \- design and prompt the Dashboard yourself **(refer Lab 6a if you need help)**.

**New in this lab:** Databricks AI/BI Dashboards are governed, low-code dashboards built natively on Unity Catalog. Each dashboard is composed of datasets (SQL queries against your tables) and widgets (the visualisations that read from those datasets). Genie Code can author both \- you describe the chart you want and it produces the dataset SQL plus the widget on the canvas. When you publish, the dashboard becomes available to viewers and Databricks automatically creates a companion Genie Space, letting end users ask follow-up questions of the same data in natural language. See  [Databricks AI/BI](https://docs.databricks.com/aws/en/ai-bi/), [What is a Genie Space](https://docs.databricks.com/aws/en/genie/).

---

1. **\*\*\* IMPORTANT \*\*\*** this lab requires the pipeline from Lab 5a or 5b to have completed successfully.

2. '**\+ New**' → '**Dashboard**' (a blank AI/BI Dashboard will open) ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

3. **Starting point:** A blank dashboard canvas plus the silver and gold tables in `workspace.genie_demo`.

4. **Goal:** A published dashboard that answers this business question *"What drives base\_price across our property portfolio, and where are the most attractive markets to invest in?"*  The dashboard should include:

* Headline KPIs across the top

* A widget showing price distribution

* A widget showing how host attributes relate to price

* A widget  showing how location/destination relates to price

* A widget showing how amenities impact price

* A deliberate, clean layout

5. **Constraints:**

* All datasets sourced from `workspace.genie_demo`

* Try and use both gold and silver tables

* Mix widget types \- don't make every chart a bar chart

* Apply an intentional colour palette (don't just take the default)

6. **How to approach:** 

* Build iteratively. Start by asking Genie Code what's interesting in the data, then add widgets one at a time. 

* When the content is right, ask Genie Code to redesign the layout in a single follow-up prompt. 

* Publish at the end and view the published version (close the Genie Code pane to see it as end users will).

7. **Done when:**

* The dashboard answers the business question above.

* The dashboard is published.

---

## **Lab 7a: Price Prediction with Machine Learning** {#lab-7a:-price-prediction-with-machine-learning}

**Objective:** Use Genie Code to build, train, and evaluate a machine learning model that predicts property base\_price from the feature table created in Lab 5a or 5b. **This lab contains all the prompts you need to achieve the objective. If you prefer more DIY, skip to Lab 7b.**

**New in this lab:** Mosaic AI is Databricks' integrated ML platform: feature engineering, model training, experiment tracking, and serving in one place. The two pieces this lab touches directly: 

* **MLflow** \- automatically tracks every model run (parameters, metrics, artefacts) so you can compare attempts and reproduce results. Genie Code logs to MLflow without you having to wire anything up \- you'll see runs appear under the Experiments sidebar.   
* **Hyperparameter tuning** \- Genie Code may run multiple training jobs with different parameter combinations to find a better-performing model. This is the slow step in the lab.

See [MLflow on Databricks](https://docs.databricks.com/aws/en/mlflow/) / [Mosaic AI overview](https://docs.databricks.com/aws/en/machine-learning/).

---

1. **\*\*\* IMPORTANT \*\*\*** this lab requires the pipeline from Lab 5a or 5b to have completed successfully.

2. '**\+ New**' → '**Notebook**' ✅, Default language '**Python**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

3. Make sure the compute you are attached to is **Serverless**, not **Serverless Starter Warehouse.**

4. Enter the following prompt:

   Using @workspace.genie\_demo.gold\_price\_prediction\_features, I want to be able to forecast base\_price using property features (bedrooms, bathrooms, accommodates etc), price\_per\_person, price\_per\_bedroom, host\_tenure\_days, review metrics (average scores, review count), and the amenity flag columns.

5. Genie Code will generate a multi-cell ML pipeline (EDA, feature engineering, preprocessing, training \- your exact cells may differ). Click "**Allow**" to run the cells via Genie Code. Genie Code may choose to run groups of cells such as the EDA steps. If an error is encountered, Genie Code should self diagnose the issue and retry. Note the Hyperparameter tuning and Model training cells may take a while to run. 

   To understand any cell, highlight the code, click on the kebab menu and select the Genie Code icon or press **Cmd+I** (Mac) / **Ctrl+I** (Windows), and type:

   /doc   or  /explain

6. Once the last cell has run, you should see output similar to the following:

   ![][image6]

7. Feel free to click on '**1 run**' or '**experiment**' to explore what has been created.

8. Finally test the model. Enter the following into Genie Code:

   test the model with a sample property for a 2-bedroom property in San Francisco with 2 bathrooms to predict the base\_price

---

## **Lab 7b: Price Prediction with Machine Learning (Self-Directed)** {#lab-7b:-price-prediction-with-machine-learning-(self-directed)}

**Objective:** Use Genie Code to build, train, and evaluate a machine learning model that predicts property base\_price from the feature table created in Lab 5a or 5b \- construct the prompt to create the machine learning model yourself **(refer Lab 7a if you need help).**

**New in this lab:** Mosaic AI is Databricks' integrated ML platform: feature engineering, model training, experiment tracking, and serving in one place. The two pieces this lab touches directly: 

1. **MLflow** \- automatically tracks every model run (parameters, metrics, artefacts) so you can compare attempts and reproduce results. Genie Code logs to MLflow without you having to wire anything up \- you'll see runs appear under the Experiments sidebar.   
2. **Hyperparameter tuning** \- Genie Code may run multiple training jobs with different parameter combinations to find a better-performing model. This is the slow step in the lab.

See  [MLflow on Databricks](https://docs.databricks.com/aws/en/mlflow/) / [Mosaic AI overview](https://docs.databricks.com/aws/en/machine-learning/).

---

3. **\*\*\* IMPORTANT \*\*\*** this lab requires the pipeline from Lab 5a or 5b to have completed successfully.

4. '**\+ New**' → '**Notebook**' ✅, Default language '**Python**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅

5. **Starting point:** An empty Python notebook, with `@workspace.genie_demo.gold_price_prediction_features` as your feature table.

6. **Goal:** An end-to-end ML pipeline producing a trained model for predicting property `base_price`, with documented evaluation metrics and the ability to score a new property described in natural language. 

7. **Constraints:**

* EDA before modelling \- don't throw features at an algorithm blindly

* Sensible train/test split with no data leakage

* Log the run to MLflow (it is automatic \- just verify the experiment exists)

* Compare at least two model approaches before settling on one

* Report evaluation metrics in plain English (RMSE alone is not an answer)

* End by predicting the price of a sample property you describe in your own words

8. **How to approach:** 

* Describe what you want in business terms in a single Genie Code prompt, then iterate. 

* If Genie Code skips a step you care about (e.g. feature scaling, hyperparameter tuning, residual analysis), ask for it explicitly as a follow-up. 

* Use /explain on cells you want to understand more deeply. 

* Hyperparameter tuning and model training cells may take a while on Free Edition serverless \- be patient.

9. **Done when:**

* Model is trained, metrics are recorded, and the MLflow run is visible

* You can articulate which features matter most and why

* You have a price prediction for a property you described in natural language

---

## **Lab 8: Analysing Text with AI SQL Functions** {#lab-8:-analysing-text-with-ai-sql-functions}

**Objective:** Use Databricks built-in AI SQL functions to classify, summarise, and generate content from unstructured text \- all directly in SQL, with no model serving or MLflow setup required.

**New in this lab:** AI Functions are built-in SQL functions that call large language models \- no model serving setup, no MLflow, just SQL. They run on Databricks-managed Foundation Model API endpoints (the same model gateway used elsewhere on the platform) and respect Unity Catalog governance. They count against your daily token  quota \- keep LIMIT clauses modest while you are exploring. That said, the dataset we are using in this lab only has 204 rows, so you should be OK. Note, we are only using 3 of the ai functions available \- see the [documentation](https://docs.databricks.com/aws/en/large-language-models/ai-functions) as well as [Enrich data using AI Functions](https://docs.databricks.com/aws/en/large-language-models/ai-functions), ['ai\_classify'](https://docs.databricks.com/aws/en/sql/language-manual/functions/ai_classify), ['ai\_summarize'](https://docs.databricks.com/aws/en/sql/language-manual/functions/ai_summarize), ['ai\_query'](https://docs.databricks.com/aws/en/sql/language-manual/functions/ai_query)

---

1. '**\+ New**' → '**Notebook**' ✅, Default language '**SQL**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅.

2. Start with a quick reconnaissance of the dataset:

   What does @samples.bakehouse.media\_customer\_reviews contain? Show me the schema and 5 sample rows with the full review text.

3. Genie Code may do the sampling in Genie Code or it may do it in the Notebook, in which case accept and run the generated query. Confirm the result set has the free-text '**review**' column \- everything that follows uses it.

4. First we will use **ai\_classify**. Create a new SQL cell with the query below:

   `SELECT` 

     `ai_classify(`

       `'The sourdough was incredible, crispy crust and perfect crumb. Coffee was average.',` 

       `ARRAY('positive', 'negative', 'mixed', 'neutral')`

     `) AS sentiment;`

5. Run the cell (hit the '►' run cell button top left). It should come back with '**mixed**'.

6. Apply the function at scale. Ask Genie Code:

   Classify every row in @samples.bakehouse.media\_customer\_reviews as positive, negative, mixed, or neutral using ai\_classify, and return the count per label ordered by the most common.

7. Accept and run the generated SQL. You now have sentiment distribution across the whole review set \- no model deployment, just SQL.                                 

8. Now we will use **ai\_summarize**. Produce one short summary per sentiment label in a single query. Create a new SQL cell with the query below:

   `SELECT`

     `ai_classify(review, ARRAY('positive', 'negative', 'mixed', 'neutral')) AS sentiment,` 

     `ai_summarize(array_join(collect_list(review), ' | '), 40) AS summary`

    `FROM samples.bakehouse.media_customer_reviews`

   `GROUP BY 1;`

9. You should get one row per sentiment label, each with a summary distilled from all the reviews in that group. The second argument to ai\_summarize **(40)** is the maximum length of the summary in words \- change it to **15** and re-run to see the effect on terseness.

10. Next we will use **ai\_query**. This general-purpose function calls a foundation model with your own prompt (in this case **databricks-meta-llama-3-3-70b-instruct**). Use it to turn review highlights into a marketing tagline. Create a new SQL cell with the query below:

    `SELECT ai_query('databricks-meta-llama-3-3-70b-instruct','Based on these bakery customer reviews, write a 2-sentence marketing tagline in British English. Return only the tagline, no preamble. Reviews: ' ||array_join(collect_list(review),' ||| ')) AS tagline`

    `FROM (`

        `SELECT review`

        `FROM samples.bakehouse.media_customer_reviews`

        `WHERE ai_classify(review,ARRAY('positive', 'negative', 'mixed', 'neutral')) = 'positive'`

        `LIMIT 10);`

11. Run it and inspect the tagline. Re-run the cell a couple of times \- the output varies because the model is non-deterministic. Try editing the prompt (e.g. "**write a formal tagline**" vs "**write a playful one**") to see how prompt wording or swapping the foundational model to '**databricks-gpt-oss-120b**' shapes the result.

12. Combine everything in a view. Ask Genie Code:

    Using @samples.bakehouse.media\_customer\_reviews, create a view in the workspace.genie\_demo schema called review\_insights with these columns: the original review, a sentiment label from ai\_classify, and a one-sentence summary from ai\_summarize. Then show me the first 10 rows.

13. Review the DDL before running. AI functions in a view re-run on every query \- fine for exploration, but in production you'd cache results in a table.

14. Finally, visualise the output. Ask Genie Code:

    Generate a bar chart of sentiment label counts from my review\_insights view.

15. Accept the chart and run it. Genie Code should make the chart available as a second tab in the cell result set beside '**Table**' \- i.e. something like '**Sentiment Distribution**'.

    You now have an end-to-end path from raw text to sentiment-labelled BI, all in SQL.

---

## **Lab 9: Genie Spaces \- Talk to your Data** {#lab-9:-genie-spaces---talk-to-your-data}

**Objective:** Create a Genie Space over a Unity Catalog table, curate it with a few business definitions, and have a natural-language conversation with your data \- the same experience you would hand to a non-technical stakeholder.

**New in this lab**: Genie Space (cf. Genie Code \- don't confuse them) are a different, business-user-facing surface: a curated chat interface published over a set of Unity Catalog tables, designed to be used by non-technical stakeholders. You shape Genie Space behaviour by adding Instructions (business definitions, rules, vocabulary) and Certified Queries (vetted SQL that Genie will reuse for high-stakes questions instead of generating SQL on the fly). This lab only scratches the surface on what is possible in terms of setting up a Genie Space. See [What is a Genie Space](https://docs.databricks.com/aws/en/genie/), [Curate an effective Genie Space](https://docs.databricks.com/aws/en/genie/curate).

---

1. In the left menu, click '**Compute**', then '**SQL warehouses**', then '**Serverless Starter Warehouse**'. If Status is not '**Running**', click '**Start**' top right.

2. In the left menu, click '**Genie Spaces**', then '**\+ New**' to create a new Genie Space. 

3. In '**Connect your data**' type '**samples.nyctaxi.trips**' \- select the table from the pick list, then click '**Create**'.

4. In the chat box (where it says '**ask your question …**'), toggle from '**Agent**' to '**Chat**'.

5. Now type:

   How many trips are in this dataset and what date range do they cover?

6. Review the generated answer. Click 'Show code' (you may need to expand the result table and then click 'Show code') to see the SQL Genie produced \- this is how you verify Genie is doing the right thing.

7. Ask something analytical:

     What is the average fare amount per hour of day? Show the result as a bar chart.

8. Follow up in the same chat to show conversational context:

   Now show me the same thing but only for trips on weekends.

9. Notice the shape \- each question gets one SQL query, one answer, one chart. This is Chat mode: fast, focused, good for known questions.

10. In the chat box toggle from '**Chat**' to '**Agent**':

    Weekend fares seemed different to weekday fares. Investigate why. Look at average fare, trip distance, trips per hour, and pickup location distribution. Tell me which factors most explain the weekend/weekday difference and where it shows up most strongly.

11. Watch the thinking trace stream (click on '**Thinking** …') as Agent mode plans its approach, runs several queries in parallel, learns from each result, and iterates.

12. Review the final report. You should see a structured summary with multiple supporting charts and tables, and citations back to the SQL Genie actually ran. 

13. Expand the citations to inspect any query you want to double-check.

14. In summary:

    * **Chat** \- one-shot SQL, immediate result, best for "what is X?" type questions 

    * **Agent** \- plan \+ multiple queries \+ synthesis, slower, best for "why is X happening?" or "find patterns in Y" type questions

15. In the space settings, find '**Instructions**', '**General Instructions**' and paste:

    \- A "long trip" is any trip with trip\_distance greater than 10 miles. 

    \- Always exclude trips where fare\_amount is 0 or negative \- these are cancellations.

    \- When grouping by location, use pickup\_zip.

16. Click '**Save**'. Start a New chat in '**Chat**' mode and ask:

    What proportion of all trips are long trips, and which pickup zip has the most long trips?

17. Confirm Genie applies your definitions without being told.

18. Now ask a question Genie can't answer \- same as before, but 'really long' instead of 'long'.

    What proportion of all trips are really long trips?

19. Genie should respond with something like 'The question cannot be answered because "really long trip" is not defined. Please clarify what trip distance should be considered a "really long trip.'

20. Provide the definition in the chat window as follows:

    a really long trip is more than 15 miles

21. Genie will now run the query. But that definition only lives in this chat \- add it to Instructions to make it available to everyone.

22. Finally, add a Certified Question so a high-stakes answer is always consistent. In the space settings under '**SQL Queries**', click '**Add**'. 

23. In '**What question does this query answer?**' type:

    What is the busiest hour of day by trip count?

24. In the SQL text box type:

    `SELECT hour(tpep_pickup_datetime) AS hour_of_day, count(*) AS trips`

      `FROM samples.nyctaxi.trips`

      `WHERE fare_amount > 0`

      `GROUP BY 1`

      `ORDER BY trips DESC`

      `LIMIT 24`

25. Click '**Preview**' to make sure it runs and then '**Save**'

26. Start a New chat in '**Chat**' mode and ask:

    What is the busiest hour of day by trip count?

27. Genie runs your certified SQL rather than generating fresh SQL (see this by clicking on 'Show code').

---

## **Lab 10: Customise Genie Code** {#lab-10:-customise-genie-code}

**Objective:** See first-hand how Genie Code's output changes when skills are loaded. Build the same pipeline twice \- once with no guidance, once with two skills installed \- and compare.

**New in this lab**: Genie Code skills are short markdown files following the open [Agent Skills](https://agentskills.io/) standard \- each one is a task-specific set of rules Genie Code applies when relevant. They live in your Databricks workspace at `/Users/<your-email>/.assistant/skills/`, are picked up automatically the next time you start a chat, and can also be invoked explicitly with `@skill-name`. Instructions are a separate, single markdown file at `/Users/<your-email>/.assistant_instructions.md` that Genie Code reads at the start of every chat. Use it to tell Genie Code *which* skills to apply by default and *when*. Together, skills \+ instructions let you bake your enterprise standards (table naming, audit columns, PII handling, AI-function patterns, etc.) into Genie Code itself \- so any prompt produces standards-compliant output without you having to re-state the rules each time. See [Genie Code overview](https://docs.databricks.com/aws/en/genie-code/) and [genie-code-skills-demo on GitHub](https://github.com/databricks-solutions/genie-code-skills-demo).

---

1. '**\+ New**' → '**ETL pipeline**' ✅, Default language '**SQL**' ✅, Genie Code pane open ✅, '**New Chat**' ✅, **Agent** Mode ✅.

2. The first step is to baseline a Lakeflow Spark Declarative Pipeline without custom skills.

3. In the ETL Pipeline UI, change the pipeline catalog and schema from '**workspace.default**' to '**workspace.genie\_demo**' (top left) to avoid catalog permission issues.

4. We'll start by asking Genie Code to build a sentiment pipeline with no extra guidance, so we can see how unconstrained it is. Submit the following prompt in Genie Code:

   Build a Lakeflow Spark Declarative Pipeline that reads samples.bakehouse.media\_customer\_reviews and produces a sentiment dataset. Each output row should include the original review text, an overall sentiment label, a topic classification, and any named entities extracted from the review.

5. Genie Code should eventually ask you to dry-run the pipeline. Click '**Allow**'.

6. Once it has completed the dry-run click '**Skip**'.

7. In the canvas click '**Accept**' to accept the code

8. Inspect the generated SQL file(s) taking note of what's there (and what's missing). Typical baseline observations:

* Table names may or may not follow a consistent `bronze_/silver_/gold_` convention  
* No audit columns (`audit_timestamp`, `source_system`)  
* No `TBLPROPERTIES` quality tags  
* AI functions may be called directly in a single bronze table (cheaper to call them once at silver)  
* No standardised output schema  
  This code is okay \- it just doesn't follow any standards. That's exactly what skills will fix.  
9. The next step is to create a Lakeflow Spark Declarative Pipeline with custom skills. The skills we will use live in the [genie-code-skills-demo](https://github.com/databricks-solutions/genie-code-skills-demo) GitHub repo. We'll install three of them at user level \- no admin rights needed.

10. Click on **Workspace** in the left menu, then Navigate to **Workspace** → **Users** → **'\<your-email\>'**.

11. Right-click your user folder → **Create** → **Folder**. Name it **'.assistant'** (note the leading dot).

12. Inside **.assistant**, create another folder named **'skills'**. You should now have: **/Workspace/Users/\<your-email\>/.assistant/skills/**

13. In your **skills** folder, create three folders named **table-governance**, **sdp-basics** and **sentiment-analysis**. 

14. In the folder **/Workspace/Users/\<your-email\>/.assistant/skills/table-governance,** right-click → **Create** → **File**. Name it **'[SKILL.md](http://SKILL.md)'**

15. In a new browser tab open [https://github.com/databricks-solutions/genie-code-skills-demo/blob/main/skills/data\_eng/table-governance.md](https://github.com/databricks-solutions/genie-code-skills-demo/blob/main/skills/data_eng/table-governance.md) 

16. Have a scan through the file to see how skills are defined.

17. Click **Raw** (top right) so you have the plain markdown content visible. Copy and paste the raw content into **SKILL.md**. 

18. Repeat for  [https://github.com/databricks-solutions/genie-code-skills-demo/blob/main/skills/data\_eng/sdp-basics.md](https://github.com/databricks-solutions/genie-code-skills-demo/blob/main/skills/data_eng/sdp-basics.md) into **/Workspace/Users/\<your-email\>/.assistant/skills/sdp-basics/[SKILL.md](http://SKILL.md).**

19. Repeat for  [https://github.com/databricks-solutions/genie-code-skills-demo/blob/main/skills/dsml/sentiment-analysis.md](https://github.com/databricks-solutions/genie-code-skills-demo/blob/main/skills/dsml/sentiment-analysis.md) into **/Workspace/Users/\<your-email\>/.assistant/skills/sentiment-analysis/[SKILL.md](http://SKILL.md).**

20. You should now have three folders each with a **SKILL.md** file visible at **/Workspace/Users/\<your-email\>/.assistant/skills/**.

21. **'+ New' → 'ETL Pipeline' ✅, Default language 'SQL' ✅, Genie Code pane open ✅, 'New Chat' ✅, Agent Mode ✅**.

22. In the ETL Pipeline UI, change the pipeline catalog and schema from '**workspace.default**' to '**workspace.genie\_demo**'

23. Invoke the skills explicitly with **@** (\!\!\! make sure you type @skill-name to locate each skill): 

    **use @table-governance, @sdp-basics, and @sentiment-analysis as standards.** Build a Lakeflow Spark Declarative Pipeline that reads samples.bakehouse.media\_customer\_reviews and produces a sentiment dataset. Each output row should include the original review text, an overall sentiment label, a topic classification, and any named entities extracted from the review. 

24. Genie Code should eventually ask you to dry-run the pipeline. Click '**Allow**'

25. Once it has completed the dry-run click '**Skip**'

26. In the canvas click ''**Accept**' to accept the code 

    * Open the generated SQL file(s) and compare against the previous output. You should now see:

    * **Layered table names** \- `bronze_reviews`, `silver_reviews_sentiment`, possibly `gold_reviews_summary`

    * **Comments** on every table describing its purpose

    * **'TBLPROPERTIES'** with at least `"quality" = "bronze"|"silver"|"gold"`

    * **'current\_timestamp() AS audit\_timestamp'** and **''\<source\>' AS source\_system'** as the LAST columns of each SELECT

    * **AI functions called only at silver** (`ai_analyze_sentiment`, `ai_classify`, `ai_extract`) \- bronze just passes the text through unchanged

    * **A standard sentiment output schema** (`<entity>_id`, `source_text`, `sentiment_label`, `topic_label`, `extracted_entities`, `data_quality_flag`, audit columns)

27. If you don't want to type `@skill-name` on every prompt, you can install a user instructions file that tells Genie Code which skills to apply automatically.

28. Navigate to **Workspace** → **Users** → **'\<your-email\>'**.

29. Right-click → **Create** → **File**. Name it **'.assistant\_instructions.md'** (note the leading dot)

30. Open the following URL in new browser tab:

    [https://github.com/databricks-solutions/genie-code-skills-demo/blob/main/instructions/.assistant\_instructions.md](https://github.com/databricks-solutions/genie-code-skills-demo/blob/main/instructions/.assistant_instructions.md) 

    Click **Raw** so you have the plain markdown content visible. Copy and paste the raw content into `.assistant_instructions.md` and save.

31. **'+ New' → 'ETL Pipeline' ✅, Default language 'SQL' ✅, Genie Code pane open ✅, 'New Chat' ✅, Agent Mode ✅**.

32. In the ETL Pipeline UI, change the pipeline catalog and schema from '**workspace.default**' to '**workspace.genie\_demo**'

33. Submit the same prompt as before, but this time you do not invoke the skills explicitly: 

    Build a Lakeflow Spark Declarative Pipeline that reads samples.bakehouse.media\_customer\_reviews and produces a sentiment dataset. Each output row should include the original review text, an overall sentiment label, a topic classification, and any named entities extracted from the review.

34. As before, click '**Allow**' when prompted. The output should now look like the previous pipeline even though you never mentioned the skills \- the user-instructions file applied them for you

35. If you get stuck:

    * Genie Code seems to ignore the skills. Make sure you clicked '**New Chat**' after installing them \- Genie Code reads the skills folder when a chat starts, not on every message. Also confirm the folder name is exactly `.assistant` (with the leading dot) and the files end in `.md`.

    * Folders starting with a dot don't appear in the workspace browser. Some workspace browsers hide dot-prefixed folders. They are still there \- you can navigate by typing the path manually in the URL bar (`/Workspace/Users/<your-email>/.assistant/skills/`) or by using the '**Show hidden'** option in the workspace settings.

    * If you still can't work out what's going on, ask Genie Code why it is not using your skills \- you may need to provide the path to a sample skill file so it can compare what you have to what it is doing.

36. Once skills feel comfortable, the natural next steps are to make the skills available to all users in the workspace:

    * Workspace-level skills \- install at `/Workspace/.assistant/skills/` so every user picks them up (needs workspace admin)

    * Workspace-level instructions \- `/Workspace/.assistant_workspace_instructions.md` (highest precedence, applies to all users)

    * MCP (Model Context Protocol) connection \- fetch skills directly from a GitHub repo at chat-start time, instead of copying files into the workspace. This requires DAB \+ secrets and is out of scope for Free Edition, but the pattern is documented in the demo repo's `mcp/` folder.

## 

## **What Next?** {#what-next?}

You have driven Genie Code through notebooks, ML, AI SQL functions, and a Genie Space. To keep building on what you have learned, here are some resources we recommend \- all free.

### **Keep Practising in Your Own Workspace**

[**Databricks Academy**](https://customer-academy.databricks.com/learn) \- if the company you work for is an existing Databricks customer, then you should have access to [free self-paced courses](https://docs.databricks.com/aws/en/getting-started/free-training) via your work email address. Good starting points after this lab: *Generative AI Fundamentals*, *Get Started with Databricks for Data Analysis*, *Get Started with Databricks for Data Engineering*, and *Get Started with Databricks for Machine Learning*.

### **Go Deeper on the Topics in This Lab**

* [Genie Code Overview](https://docs.databricks.com/aws/en/notebooks/databricks-assistant-faq)

* [Genie Code overview, Use Genie Code, Genie Code for data science, Extend Genie Code with agent skills](https://docs.databricks.com/aws/en/genie-code/)

* [What is a Genie space, Curate an effective Genie space, Build a knowledge store, From Data to Dialogue (blog)](https://docs.databricks.com/aws/en/genie/)

* [AI functions on Databricks, ai\_query reference](https://docs.databricks.com/aws/en/large-language-models/ai-functions)

### **Watch and Learn**

* The Start Learning courses in Free Edition (linked in the home page) \- Databricks Fundamentals, Intro to Data Engineering and Intro to AI/BI

* [**Databricks on YouTube**](https://www.youtube.com/@Databricks) \- product demos, conference talks, and how-to videos. Worth subscribing to for new feature drops.

### **Community and Events**

* [**Databricks Community**](https://community.databricks.com/) \- ask questions, share notebooks, browse the Genie and AI/BI forums.

* [**Data \+ AI Summit**](https://www.databricks.com/dataaisummit) \- annual conference. Past sessions are free to stream and are a fast way to see what others are building with Genie, AI/BI, and Lakeflow.

[image1]: <data:image/png;base64,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>

[image2]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA8AAAANCAYAAAB2HjRBAAAAHklEQVR4XmP4TwFggDF22PgTjUc1j2omiKmrmRwAAMtDOCnCQwa7AAAAAElFTkSuQmCC>

[image3]: <data:image/png;base64,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>

[image4]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABIAAAAOCAYAAAAi2ky3AAACHUlEQVR4XoWSXWsTQRiF8wMtQSuItbGRiNGLam0LTSmBtjQGrIqoiNULxSuRildFamOlClLBDwy17Ux2N9kk+5FsNpud/QHHdzYxm1i1Fw9zNQ/nnJlYUK5BIsp1CM0gTMKCH2ITDXTUZg8HntoiXKJNePCUDtqKj9hxknSeYyrL/ytpKwIxoZFIq9MlgzC7EtWmizJJAzMLDNlpRpdIorh0SeL16MAlkVuSovLfk/gaVdEcLE1x3E6zKAkJPDVK0lYCuGogE/2WSEEkycxx5CY57l9keDrO8GqUoTByGKb4U+JI0WCdr7vG0LAfntXw/CzD61MMn68r/TpSZG6pMAsM1vY+mqqQIgsv3uhI3+CYlnvMsGhY2mMjzvBupBhtUvLxY2wN+4lVlJJZVFLX0NBCkY0rOY7Zhe7L3LrM8Hgi2uR9/Ds+ntzp1fFRHHuIg8TNsE5TC0gSwC6H1RqYy3CsXJVJWoSL9dMM1c1GOOzgJlaBg51fgXYhMySxKiTqPnMT91LRE2+dOMBOfBefRjehrn2D+VbB3rm7JFkiyWy4iaxjlQVMwqgIKXL6SQY/W+nRHr6ceUl7PMHP8TvgE4uwt4uUREqiJKYewNDDREclgz/WpSdu0elQiq5EHJHUqySKfmx76Hnljz1M5KEm56GnJmFeSsKWdXqVZJ26LlCrClSJ2L8kLqWoLj6AsbwKO7cMJz8/tElfUhPQiV8MRXGcwk44eQAAAABJRU5ErkJggg==>

[image5]: <data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAwAAAAMCAYAAABWdVznAAAATUlEQVR4XqWRSQ4AIAgD+THP43kaDphSNG6TeFA65aC0S4QfdiwFVS3HSYKZlUAwFTDE7UngAbcjQ0D4jrxtCDDIBTErAgdw5vz9wwkdk670aCRQgEkAAAAASUVORK5CYII=>

[image6]: <data:image/png;base64,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>