# The Data Science Lifecycle

The phases described below are combined to create the roadmap process that our Data Science team uses for product delivery. Although all projects are different, the outlined process is general enough to be applicable in most situations. Additionally, the lifecycle is presented below in a linear fashion, but the actual work takes place iteratively, often bouncing back and forth from one section to another. The entire (scrollable) process can be found [here](https://github.com/b-shelton/team_processes/blob/master/files/images/ds_lifecycle.jpg) and a downloadable Visio version can be found [here](https://github.com/b-shelton/team_processes/blob/master/files/ds_lifecycle.vsd).


![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/dsl_ideation.png)

The Ideation phase of any data science project begins with the team's business customers describing a problem, then working together with the Data Science team to understand (a) if a viable solution already exists, (b) if there would be substantial business value in solving the problem, and (c) how difficult it would be to build the necessary solution.

If a project is deemed worthwhile, the data science team works with the business to develop a charter and plan to develop a solution.


![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/dsl_getdata.png)

The Data Science team starts actual product development by assessing what data it thinks will be necessary _*and*_ what data it thinks will be readily available. If the data is already available within the organization, it needs to be placed in a location accessible to the tools used on the Data Science team (e.g., R, Python, Spark, Impala, Tableau). The location generally used by our team is HDFS, leveraging Hive as an infrastructure for structured data.

If the data is not readily accessible, the Data Science team works with the business to understand if the data could be made available at all and, if so, if it would require creation or purchasing. If the data is not obtainable, or is deemed to costly to create or purchase, then expectations need to be reset with the team's customer.

Once available, the team spends time understanding the data through exploratory data analysis, which then leads to data documentation and appropriately transforming the data from its raw state into an analytics-ready state. Prior art review is critical during the Data Acquisition & Exploration phase because so much time and frustration can be spared by leveraging the prior efforts of others on the team. Our Data Science and Business Insights teams continually contribute to an "analytics data layer" that contains commonly-used data in a flexible and easy-to-use state, accompanied by an updated dictionary.


![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/dsl_development.png)

When the data is transformed and ready-for-use, models are iteratively built, trained/tested/validated (if supervised), and assessed. This step is what most people often consider true "data science". Although the most technical phase of the lifecycle, it is one of the least time consuming parts of the process, and no more important than any other step.


![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/dsl_validation.png)

All customer-facing work that the Data Science and Business Insights teams develop must go through our [code review process](https://github.com/b-shelton/team_processes/blob/master/code_review.md) to ensure accuracy, efficiency, and interpretability. The product must then be presented to its intended end-users to test its usability. Finally, I.T. engineering and administration assess the product workflow in order to justify and provide the necessary compute resources for operationalization in our production environment.


![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/dsl_delivery.png)

The workflow of the product's customer often dictates the method of delivery. For customers who are small teams that are still standing up their own processes, daily email results may suffice initially. Other customers consist of larger teams or need custom interactivity with the results. Other customers need data science scores fed directly into their existing work platforms.


![alt text](https://github.com/b-shelton/team_processes/blob/master/files/images/dsl_monitoring.png)  

Our Data Science team stays just as focused on its products once the solutions are deployed. The Data Science UX specialist solicits on-going feedback from end-users, enhancements are continually required to off-set model deterioration, and value is tracked and reported to business stakeholders.  
