# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Namra Schazil

```
Please write your explanation here...

Question: Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.


Answer: The following list mentions the stages in the Whitby-covid tracing code where sampling is occurring:
1.	Creating data-frame for people at social events:
In the Whitby-covid tracing code, a data-frame is created for people at social events with initial infection and traced status. At this stage of the experiment, sampling is done to get a sample of the population who attended social events i.e., weddings and brunches. The sampling method used is stratified sampling as the population is divided into groups called ‘strata’ i.e., people who attended weddings and brunches. Thereafter, a proportionate number is randomly taken from each of the two categories of events. This is an example of random sampling as any group of N individuals is as likely to be chosen as any other group of N individuals. 
The function used in python is “def simulate_events(m):” which represents individuals attending weddings and brunches in a community. The sample size is 1000 individuals and the sampling frame is the list of people attending weddings and brunches in a single time period. 
The procedure outlined in the blog post assumes that out of a community of 1000 people, every person attends exactly one event from either one of two weddings each with 100 attendees (total 200) or one of 80 brunches each with 10 attendees (total 800). 

2.	Infecting a subset of the data-frame of people attending events:
The second stage of sampling takes place following the creation of data-frame i.e. infecting a random subset of people. Simple random sampling is used to randomly select the number of individuals which have all have an equal chance of getting selected and infecting them on a pre-defined attack-rate of 0.10. The function used for this sampling is “np.random.choice”. The sample size is 10% of the sample of people attending events so that is 100 individuals, and the sampling frame is sampled population attending weddings and brunches. The sampling procedure outlined in the blog post at this stage of sampling assumes 10% of people at every events are infected keeping in mind that there are more people attending each wedding (100 attendees) compared to the number of people attending each brunch (10 attendees)

3.	Primary contact tracing:
Following infection stage, simple random sampling is again carried out to randomly decide which of the infected people get traced. The simple random sampling is carried out on the sampling frame of the randomly selected individuals who were infected within the population who attended weddings and brunches. The function used for this sampling is “np.random.rand” and the trace rate is 0.20 which means 20% of the 100 people infected are traced i.e., 20 people. The sampling frame is 100 randomly infected individuals who either attended weddings or brunches within the original sample of 1000. The primary contact sourcing stage is outlined in the blogpost as the infection which only has 20% chance of being traced to a source event. This is due to faulty recall of patients or staff shortages etc. which makes the contact tracing imperfect and only 20% cases of covid are traced. 

Andrew whitby’s blog discusses how contact tracing can lead to biased sampling by disproportionately testing contacts of known cases rather than random members of the population. This bias affects the estimation of disease parameters and dynamics. 

Question: 
Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Answer: the results obtained from the whitby-covid tracing code shares some similarities and differences from the result in the original blog post. The true proportion of cases from weddings are around the same for both the results i.e. 20% but the mean observed proportion is around double the true proportion for the graph is the original blog post. Whereas in the python script result, the traced cases of infections to weddings is around the same as that of the true infections from weddings. In the blogpost result, one is likely to overestimate the proportion of cases that result from weddings whereas in the python script result one might reflect that the number of observed and true cases from originating due to weddings are around the same but their frequency is less than true cases. The frequency of the true proportions of infections resulting from weddings in also much higher than the observed proportion in the results from the blogpost. 

Question: 
Modify the number of repetitions in the simulation to 1000 (from the original 50000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Answer: when the code is run with fewer iterations the frequency of the proportion of observed and true cases decreases but the differences between the observed and true proportion of cases remain the same. Reproducibility refers to the instances in which the original researcher’s data and codes are used to regenerate the results. The results are reproducible in this case as when the existing data is reanalysed using the same research methods using fewer iterations, it yields the same cases of infection. Therefore the results are consistent across different runs but with fewer frequency. 

Question: Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

The code was edited to include the random seed element at the beginning of the code after downloading the libraries which introduces a number for the random seed generator and sets it to a certain value so that whenever the code is run, it produces the same result. This makes the result reproducible. 

import random
# Set random seeds for reproducibility
 np.random.seed(10) 
random.seed(10)



```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `HH:MM AM/PM - DD/MM/YYYY`
* The branch name for your repo should be: `sampling-and-reproducibility`
* What to submit for this assignment:
    * This markdown file (sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `sampling-and-reproducibility`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
