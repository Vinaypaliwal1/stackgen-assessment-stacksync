# Task 2 – Overview & Setup for Non-Technical Audience


##  Overview 

The **StackSync AI Connector** ensures that the information used by your AI tools remains up to date. Whenever configuration changes occur in **appStack**, the connector sends updates to **Cloud2Code**, allowing your AI features to utilize the latest data. 

You can start the sync yourself through **StackBuilder**, and you can also check the progress there. The button you use for this is now called **Run AI Sync**.


### How it fits into your workflow

- **appStack** — where your settings come from
- **Cloud2Code** — where your AI tools use those settings
- **StackBuilder** — where you start a sync and check its status


## Set Up and Usage

**Before you start**

Make sure you have access to your project in **StackBuilder**.


### Set up

1. Confirm your **appStack** project is connected to **StackBuilder** for updates.
2. Make sure your **Cloud2Code** workspace is ready to receive the synced information.
3. Open your stack in **StackBuilder** and turn on the **StackSync AI Connector** for it.


### Run a sync

- **Manual**: Go to your stack in **StackBuilder** and select **Run AI Sync**.
- **Automatic**: The system runs a sync whenever it detects a change in your **appStack** project.


### Check sync status

1. Open the stack in **StackBuilder**.
2. You’ll see a section that shows the latest sync activity and whether it finished successfully.
3. If the sync doesn’t show up, reach out to your **DevOps** or **admin** team to check the system logs.





---



# Task 3 – Metadata Fix + Explanation


## Fixed metadata

After reviewing the validator errors, use the following corrected metadata block:

  ```yaml
  description: Explain how to set up and monitor StackSync AI Connector in StackBuilder.
  title: StackSync AI Connector
  read_time: '4 min read'
  customFields:
    ai_index: true
    clusters:
      - appStack
      - cloud2code
  audience:
    - developer
    - DevOps
  product_version: '1.0'
  ```


## Explanation

- **ai_index:** Flags the content as relevant to AI indexing features so the docs site surfaces and groups AI-related pages and enables AI-specific tooling (search/index pipelines).  

- **clusters:** Lists the environment or cluster targets the doc applies to (for example **appStack**, **cloud2code**); StackGen uses this to filter documentation and validate metadata for stack-specific operations.  

- **read_time:** A human-friendly estimated reading time displayed on the docs site and validated by the metadata validator; it must match the pattern `\d+ min read`.


---


# Task 4 – Prioritization Slack Message

```
I’ll prioritize in the following order:

1) Fix October metadata errors (1 hr) — release blocker.  
2) Update MCP internal links (2 hr) — prevents broken navigation.  
3) Draft AI-Validator guide (3 hr) — important but not blocking release.

Please let me know if any task needs a different priority.
```



---


# Task 5 – Reviewer Feedback Slack Reply

```
Thanks for the feedback — I appreciate the guidance. 
I worked late on the fixes, so before I start the rewrite, could you share 2–3 examples from the Style Guide you want me to follow? That will help me align the tone correctly and avoid rework. Once I have that clarity, I can complete the update efficiently.
```

