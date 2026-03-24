# Homework – Mini Power Platform Chain (Click-only)

## Goal
Build a very small **end-to-end Power Platform solution** using only the UI (no Plan Designer).

You will create:

- 1 Dataverse table  
- 1 Canvas App screen  
- 1 Power Automate flow  
- 1 Copilot Studio agent  
- 1 simple Power BI report (from Excel)

**Estimated time:** 30–40 minutes  
**Deliverable:** Screenshots or a short screen recording showing each step working.

## ⚠️ Important – Use English UI

Make sure your browser and Power Platform UI language is set to **English**.

🧠 **Why this matters**

- Most documentation and tutorials are in English
- Field names, actions and formulas appear in English
- Easier to follow guides and search for solutions
- Avoids confusion when working in teams

---

# 0. Solution creation

> ### 💡 Tip – Work in a Solution
>
> Before creating any components, it is recommended to create and work inside a **Solution**.
>
> A Solution is a container that groups together:
> - tables  
> - apps  
> - flows  
> - agents
> - connections
> - etc. 
>
> 🧠 **Why this matters**
>
> In real projects, Solutions are used to:
> - organize related components  
> - move your work between environments (Dev → Test → Prod)  
> - manage versions and deployments  
>
🧭 For this exercise:

1. Navigate to **Solutions**
2. Click **New solution**
3. Set a name, e.g.:

 ```
HomeworkSolution
 ```

4. Open the solution and create all components **inside it**


> ℹ️ Note – Already created something outside a Solution?
>
> No problem 👍  
>
> You can add existing components to a Solution:
>
> - Open the Solution  
> - Click **Add existing**
> - Select the component type (table, app, flow, etc.)
>
> 👉 In real projects, this is very common when organizing or cleaning up work.


# 1. Dataverse – Create 1 Table and 1 Column

Go to:
https://make.powerapps.com

Select your **training environment**.

## Create a Table

> ⚠️ Make sure you are working inside your **HomeworkSolution**

1. Navigate to **Tables** (Dataverse)
2. Click **New (table)**

>
> ### 💡 Tip – Multiple ways to create a table
>
> After clicking **New table**, you may see different options depending on the UI version (the interface changes frequently).
>
> The most common entry points are:
>
> - **Start from blank** → create a single table manually
> - **Create multiple tables / Data modeler** → opens a modeling view for designing multiple related tables  
> - **Virtual table** → connects to external data *(data not stored in Dataverse)*  
> - **Copilot / AI-assisted creation** → describe your table in natural language  
> - **Import from Excel or SharePoint** → generate a table from existing data
>

🧭 For this exercise, choose:

**Start from blank**

3. Set the name:

```
HomeworkRequest
```

> ### 💡 Tip – Table naming (Display vs Plural Name)
>
> When creating a table, you will also see additional properties:
>
> - **Display Name** → human-readable name shown in the UI  
> - **Plural Name** → used by the system in certain contexts (e.g. lists, APIs, logic)
>
> 🧠 **Why this matters**
>
> In development, you often reference the table by name in:
> - formulas  
> - flows  
> - integrations  
>
> However, the platform may sometimes expect the **plural name**, and this is not always clearly indicated.
>
> 👀 **Recommendation**
>
> To avoid confusion, it's common practice to remove the plural form (e.g. avoid adding "s") and set **Display Name** and **Plural Name** to the same value 
>
> This way:
> - You reduce ambiguity  
> - You avoid subtle bugs when referencing the table name  
>
> Example:
>
> ```
> Display Name: HomeworkRequest
> Plural Name: HomeworkRequest
> ```

---

## Add One Column

> When creating a new table, you must define at least one custom column before saving.
> The table cannot be saved without it.

1. Click (edit) **New column** / **Primary column**

2. Fill the basic fields:

```
Display name: ShortTitle
Data type: Text
Required: Business required
```

> ### 💡 Tip – Column basics
>
> When creating columns, you typically define:
>
> - **Display name** → what users see in the UI
> - **Description** → optional field to document the purpose of the column (useful for other developers and future maintenance)
> - **Data type** → defines how the data is stored  
> - **Format** → optional, depends on the data type  
> - **Required level** → ensures that users must provide a value before saving a record.

---

> ### ⚠️ Important – What cannot be changed later
>
> Some column properties are flexible, others are not:
>
> - ✅ **Display name** → can be changed later, but not recommended
> - ❌ **Schema name** → cannot be changed after creation  
> - ❌ **Data type** → cannot be changed after saving  
>
> 🧠 **Why this matters**
>
> 👉 In technical scenarios, you will mostly work with the **schema name** (or **logical name**), not the display name.
> - The **schema name** and an auto-generated **logical name** are used in:
>   - Power Automate flows  
>   - integrations  
>

---

> ### 🧪 Try this (optional)
>
> Before saving, explore the available **data types**:
>
> - Text  
> - Number  
> - Choice  
> - Date  
> - Yes/No  
>
>  Think about:
> - Which type would you use for a **Status** field?  
> - Which one would you use for a **SubmitDate**?

---

> ℹ️ Note
>
> If you use the **data modeler view** (multiple tables option), you can:
>
> - design tables and relationships  
> - and **enter data immediately** after creating the structure


3. Save the column

4. Save the table

---

## Test the Table

1. In the left menu, navigate to **Tables**
2. Use the **filter (e.g. Custom)** to find your created tables
3. Open the **HomeworkRequest** table
4. In the table (grid) view, enter a value for **ShortTitle**

Example:

```
Laptop keyboard issue
```

✅ **Checkpoint**

Your Dataverse table can store records and the `ShortTitle` field is required.

---

> 💡 **Tip** – Primary Name & Keys
>
> Every Dataverse table has a **Primary Name column** (like a title).
> This is what users will see in lookups and the UI.
>
> 👀 **Recommendation**
>
> - If you need a **unique identifier**, it is recommended to use something like:
>   - `ID`
> - Otherwise, you can use a more descriptive field (e.g. name or title)
>
> 🧠 **Why this matters**
>
> - The Primary Name is mainly for **display purposes**
> - It is not guaranteed to be unique
>
> 👉 For real-world scenarios, you often need a proper **unique key** e.g. code.

---

> **Key (Alternate Key) – What and why**
>
> A **Key** ensures that a record can be uniquely identified based on one or more columns.
>
> It is useful for:
> - preventing duplicate records  
> - integrations (e.g. matching records from external systems)  
> - enforcing business rules  
>
> 👉 In practice:
> - The system automatically creates a unique identifier (**GUID**) for each record. This is stored in a system column, which is typically named after the table (e.g. `homeworkrequestid`)  
> - But **Keys allow business-level uniqueness** (e.g. RequestID)

---

> ⚙️ **How to create a Key**
>
> 1. Open your table (**HomeworkRequest**)  
> 2. In the top menu, locate the sections:
>    - Table properties  
>    - **Schema**
>    - Data experiences 
>    - Customizations
>
> 3. Go to **Schema → Keys**
> 4. Click **New key**
>
> 5. Set:
>
> - **Display Name** → recommended format:
>
> ```
> ShortTitle_PK
> ```
>
> - Select the column:
>   - `ShortTitle`
>
> 6. Save the key
>
> 👉 This ensures that the selected column acts as a **unique identifier**
---


# 2. Power Apps – Create a Simple App

> ⚠️ Make sure you are working inside your **HomeworkSolution**

## Create a Canvas App

1. Go to **Apps**
2. Click **New app**
3. Select **Canvas app**
4. Choose **Tablet layout**

---

## Connect to Dataverse

1. Click **Data** on the left menubar
2. Add a data source
3. Select:

```
Dataverse → HomeworkRequest
```

---

## Add a Form

1. Insert → **Edit Form**
2. Set the properties:

```
DataSource = HomeworkRequest
DefaultMode = New
```

3. Add the field:

```
ShortTitle
```

> 💡 Tip – Field not visible?
>
> If the field is not added automatically to the form:
>
> 1. Select the form  
> 2. In the right-side **Properties** panel, go to the **Display** section  
> 3. Find **Fields**  
> 4. Add `ShortTitle`

---

## Add a Save Button

Insert → **Button**

Button text:

```
Save
```

Set the **OnSelect** property:

```
SubmitForm(Form1);
ResetForm(Form1);
```

---

## Test the App

1. Click **Play**
2. Enter a value in **ShortTitle**
3. Press **Save**

✅ **Checkpoint**

A new record appears in the Dataverse table.


> 💡 Tip – App OnStart (Initialization logic)
>
> Every Power App has an **OnStart** property, which runs when the app is loaded.
>
> 🧠 **Why this matters**
>
> OnStart is used to:
>
> - initialize variables  
> - load data (e.g. from Dataverse)  
> - set up default values  
> - prepare the app state before the user interacts with it  
>
> 👉 In real applications, this is where most of the **setup logic** happens
>
> Examples:
>
> - `Set(CurrentUser, User())`  
> - `ClearCollect(Requests, HomeworkRequest)`  
>
> ⚠️ Important:
>
> - OnStart does **not run automatically every time you edit the app**
> - You may need to manually trigger it using **Run OnStart**

---

# 3. Power Automate – Create 1 Flow

> ⚠️ Make sure you are working inside your **HomeworkSolution**

Go to:

https://make.powerautomate.com

---

## Create Flow

1. Click **Create/New**
2. Select **Automated Cloud Flow**

Name:

```
HomeworkRequest Notification
```

---

## Trigger

Select:

```
Microsoft Dataverse
When a row is added, modified or deleted
```

Configuration:

```
Change type: Added
Table: HomeworkRequest
(Scope: User)
```

---

## Add Email Action

Add step:

```
Send an email (V2)
```

Fill fields:

```
To: your own email
Subject: New Homework Request created
Body: A new request was created: ShortTitle
```

Use **Dynamic Content → ShortTitle**.

---

## Test

Create a new request from the Power App.

✅ **Checkpoint**

You receive an email notification.

---

# 4. Copilot Studio – Create a Simple Agent

> ⚠️ Make sure you are working inside your **HomeworkSolution**

Open:

https://copilotstudio.microsoft.com

---

## Create Agent

Click **New Agent**

Name:

```
Homework Helper
```

Description:

```
Helps users create a homework request.
```

---

## Create Topic

Topic name:

```
Create Request
```

Trigger phrases:

```
create request
new request
report problem
```

---

## Ask a Question

Add node:

```
Ask a question
```

Question:

```
What short title should I use for the request?
```

Store the response in variable:

```
varTitle
```

---

## Create Dataverse Record

Add action:

```
Create row in Dataverse
```

Mapping:

```
Table: HomeworkRequest
ShortTitle = varTitle
```

---

## Test

Open **Test Chat**

Type:

```
create request
```

Provide a title.

✅ **Checkpoint**

A new record appears in Dataverse.

---

# 5. Power BI – Import Excel and Create a Report

This step practices basic reporting.

---

## Step 1 – Create Sample Excel File

Create an Excel file called:

```
HomeworkRequests.xlsx
```

Add this table:

| RequestID | Category | Status | CreatedDate |
|-----------|----------|--------|-------------|
| 1 | IT | Open | 2026-03-01 |
| 2 | HR | Closed | 2026-03-02 |
| 3 | IT | Open | 2026-03-03 |
| 4 | Facilities | Open | 2026-03-03 |
| 5 | IT | Closed | 2026-03-04 |

Save the file.

---

## Step 2 – Open Power BI

Go to:

https://app.fabric.microsoft.com

Open your **workspace**.

---

## Step 3 – Upload Excel

1. Click **New**
2. Select **Upload a file**
3. Upload:

```
HomeworkRequests.xlsx
```

4. Choose **Create dataset and report**

---

## Step 4 – Create Visuals

Create three visuals.

### Visual 1 – Requests by Category

Chart type:

```
Column Chart
```

Fields:

```
X-axis: Category
Values: Count of RequestID
```

---

### Visual 2 – Requests by Status

Chart type:

```
Donut Chart
```

Fields:

```
Legend: Status
Values: Count of RequestID
```

---

### Visual 3 – Requests Over Time

Chart type:

```
Line Chart
```

Fields:

```
X-axis: CreatedDate
Values: Count of RequestID
```

---

## Step 5 – Save Report

Report name:

```
Homework Requests Report
```

✅ **Checkpoint**

You created a simple Power BI dashboard.

---

# 6. What to Submit

Please share screenshots of:

1. Dataverse table with at least one record  
2. Power Apps screen (form + Save button)  
3. Successful Power Automate run  
4. Copilot Studio chat creating a record  
5. Power BI report page

---

# Optional Challenge

Extend the exercise:

- Add a **Status column** in Dataverse  
- Include **Status** in the Power Automate email  
- Add a **Power BI KPI card** showing total requests
