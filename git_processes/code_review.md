This post describes best practices of code review for the Enterprise Data Science & Analytics teams. The process has been developed by assessing the team's code review practices, as well as researching the best practices of [Palantir](https://medium.com/palantir/code-review-best-practices-19e02780015f), [Trivago](https://tech.trivago.com/2017/01/20/code-review-best-practices-and-common-pitfalls/), [IBM](https://www.ibm.com/developerworks/rational/library/11-proven-practices-for-peer-review/index.html), and [Apteo](https://medium.com/apteo/code-reviewing-data-science-work-774747248e33).

# Code Review Benefits

> _*"None of us is AS smart AS all of us." --Ken Blanchard*_

Code review is traditionally considered a part of software development. However, when data science and business intelligence teams are developing products that are to be operationalized, work products should be placed through the same quality assurance rigor.  Below are some highly-accepted benefits to developing and maintaining a strong team code review culture:

- **Knowledge sharing.** Code review allows data sources, logic, programming/coding techniques and optimization processes to be cross-pollinated between authors and reviewers, increasing everyone's awareness and abilities.
- **Legibility and consistency.** Code review encourages code authors to develop in a manner that is easy for reviewers to read and understand. Authors tend to develop with a greater sense of pride when they know that a peer will be reviewing their efforts; authors use better syntax, styling, and commenting than they would if the code was developed and pushed in isolation.
- **Bug checking.** Even the best of us make mistakes. Typos, overlooked unit tests, and incorrect references are bound to happen if you program enough. Code reviews greatly reduce the chance that a program will be plagued with simple (and honest) mistakes.


# Code Review Roles and Responsibilities

Code reviews consist of two parties: _*code authors*_ and _*code reviewers*_. The code author develops clear, efficient, and well-documented code that is passed on to the code reviewer(s) prior to being released into production. "Production" for the team consists of anything submitted for customer consumption.


### Define the code reviewer up front.
Before any code is developed for a new project, the code author is required to identify the appropriate code reviewer(s) for the project. The code reviewer should be someone who has experience in the programming languages being used and the domain area being addressed. The code author should only come to management for support in obtaining a code reviewer _*after*_ a failed attempt at successfully identifying one on their own.    

All data scientists and data analysts are expected to commit up to 20% of their time to code review for their peers.

### Code Author Responsibilities

1. **Identify and engage the appropriate code reviewer prior to development work.** (See section directly above.)

2. **Author code using team style guides for R, Python, and SQL.**

3. **Self-test the code in the appropriate environment prior to submitting for review.**
    - If the review is for code executed in Cloudera Data Science Workbench, self-test the code in a new project whose sessions won't retain all of the historic package installs that the code author's scratch space project might have.
    - If the review is for code executed in Hue, self-test in the SQL query engine that will be used for the final product. e.g., the code may have been developed iteratively in Impala, but if it is an ETL job that needs to be scheduled, then the review code should be written to run in Hive.

4. **Submit fewer than 400 lines of code for a single review.** Studies have shown that light-weight code reviews are better at identifying bugs than reviews that involve a greater number of lines.

5. **Formally assign the code review through a Pull Request in GitHub.** This includes the following steps:
    - Create a Pull Request using a branch other than the master branch.
    - Assign the code reviewer.
    - Include a desired delivery date in the Pull Request comment.
    - In 80 words or less (and with correct capitlizations) in the Pull Request comment, annotate the code, meaning that the code author should provide an English description of the code's process and data sources used. This is in addition to solid comments in the code.
    - Include a [markdown checklist](https://blog.github.com/2014-04-28-task-lists-in-all-markdown-documents/) of the code's intended functionality. Even if the code reviewer is aware of the program's intent (which they always should be), a checklist ensures that reviewers will be on the lookout for the Pull Request's intended enhancements or bug fixes.
    - Bad Example of an Enhancement Pull Request:

      _*"updated the source of claim dollars"*_
    - Better Example of an Enhancement Pull Request:

      _*"Update to the source of claims dollars.*_

      _*This enhancement corresponds with Issue #12. Per discussions with the business, claims dollars for this project should be sourced from the `amountpaid` field in the plandata.claimdetail table instead of the `totalpaid` field in the plandata.claim table. The plandata.claim table is still needed because `claimid` is used to identify the appropriate recods in plandata.claimdetail.*_

      _*@elew: Please review this code by 12/10/2018 for the following enhancements:*_

        - [ ] _*Correctly sum the `amountpaid` from plandata.claimdetail to represent the dollar amount.*_
        - [ ] _*Duplicates are NOT introduced through the new join.*_
        - [ ] _*Rows are NOT lost through the new join."*_

6. **Supply complimentary unit test code, when appropriate.**

      Example:

      _*Below are the unit testing scripts that can be copied, pasted, and executed in Impala to compare the values to the Tableau workbook in dev for the dollars paid, total claims, and total membership.*_

      _Impala Script for Total without RCAC Region Filter_:
      ```
      SELECT lob
           , CAST(SUM(totalpaid) AS int) AS total_paid
           , COUNT(claimid) AS paid_claims_count
           , COUNT(DISTINCT carriermemid) AS distinct_members_served
        FROM fakedb.claims_universe
       WHERE startdate >= '2017-01-01'
             AND billtype2 = 'IP-Hosp'
             AND ltach <> 'yes'
       GROUP BY lob
       ORDER BY SUM(totalpaid) DESC;
      ```

      _Impala Script for Total with RCAC Region Filter_:
      ```
      SELECT cu.lob
           , CAST(sum(cu.totalpaid) AS INT) AS total_paid
           , COUNT(cu.claimid) AS paid_claims_count
           , COUNT(DISTINCT cu.carriermemid) AS distinct_members_served  
        FROM (SELECT *
                FROM fakedb.claims_universe
               WHERE startdate >= '2017-01-01'
                     AND billtype2 = 'IP-Hosp'
                     AND ltach <> 'yes') cu
             INNER JOIN
             (SELECT *
                FROM swat.provider_latlon
               WHERE rcac_region_desc = 'Antelope Valley') pr
             ON cu.npi = pr.npi    
       GROUP BY cu.lob
       ORDER BY sum(cu.totalpaid) desc;
      ```

      *You can test the different RCAC regions by changing the value in quotes on the `WHERE rcac_region_desc = 'Antelope Valley'` line of the script above.*

7. **After the code review has been received and changes made, post the changes to the same branch but AS a new commit.**

### Code Reviewer Responsibilities

1. **Confirm receipt of the Pull Request and either agree to or comment with a new review delivery date.** If the code reviewer finds the requested delivery date not feasible, contact the code author directly to propose a new date before responding on the Pull Request.

2. **Review no more than 400 lines of code in one sitting, reviewing at a rate of 400 lines per hour.** Studies have shown that more thoughtful code reviews identify larger densities of defects than reviews that are too quick and/or last a duration greater than 60-90 minutes.

3. **Review with the following questions in mind:**
    - Does the code accomplish the purposes set forth by the code author?
    - Is the code legible and does it follow the team's style guides?
    - Is the code optimized for efficient performance?
    - Does the code need integration tests with downstream systems?
    - Was the code's documentation updated to reflect the changes made (e.g., README file or data dictionary)?

4. **Provide code review responses in the Pull Request on GitHub.**
    - Even if there are no changes deemed necessary (which would be suspect), the code reviewer is required to supply a review comment stating what actions went into the code review and that the code is approved "as-is".
    - When changes are requested, provide solid recommendations on how the change request can be resolved.
    - Indicate whether or not the code needs to be re-reviewed by the code reviewer after suggested changes are made
    - Provide code review responses that avoid possessive pronouns (e.g., "your code", "my method") and abosolute judgements (e.g., "never works", "always happens").

5. **Provide all code review change requests with one of the following 3 labels:**
    - "Suggestion": These are suggestions that are based on the reviewer's personal experience, but final discretion is in the author's hands.
    - "Required Change": These are items that prevent code review approval, if not resolved. The code reviewer should always supply solid reasoning and/or reference when communicating a required change. Examples include policy issues, security issues, compilation issues, misalignment of code products or business objectives.
    - "Clarification Needed": These are items that are too ambiguous for the code reviewer to make a determination on with the code in its current state.

# Additional Rules of Engagement

1. **Code reviews are to be approached by both parties AS a collaborative effort towards jointly creating an optimal work product.**
    - The code author accepts code review feedback AS an objective assessment of the code and an opportunity to improve the output.
    - The code reviewer provides helpful feedback in a concise, amiable, and actionable manner with positive intent.

2. **Once the code reviewer has submitted their review, the code author is required to respond to every comment.** Simple responses like "acknowledged" or "done" are appropriate.

3. **When the code author does not agree with the code reviewer, the code author is expected to:**
    - Comment in the Pull Request why the original decision(s) were made.
    - Engage the code reviewer in real-time communication.
    - Submit follow-up comments in the Pull Request.
    - IF the steps listed above are not able to resolve the differences, then engage management together for additional counsel.
