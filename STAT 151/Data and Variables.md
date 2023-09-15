# Statistics Process
Goal: to take a sample of a very large population, Analyze and come to conclusion about the full population
## Descriptive Statistics
- Gathering data
- Summarize and present the data
	- **Summarize**: Mean, standard dev, median
	- **Present**: Histogram, graphs, tables
- Analyze and interpret the data
	- What does the data (median, mean, standard deviation, histogram) mean?
## Inferential statistics
- Make generalisations of the population

# Data types
## Categorical
No granularity, only categories	

- **Nominal**: No method to compare between categories, we have simply given *Names* to categories
	- Eg: Gender, Blood type
- **Ordinal**: We can made an order to each category, One observation/category comes before (or is better than) another category
	- Eg: Letter grades
- **Center of data:** Mode
### Nominal vs Ordinal
Ask: Is one data better than another?
- Phone area code -> Number is not ordered -> Nominal
## Numerical
No distinct categories, more continuous

- **Discrete**: described with *integers* only
	- Counted, not measured
	- eg: \# of customers
- **Continuous**: Fractions of a unit are allowed
	- Measured, not counted
	- Eg: Height
- **Center of data**: Mean, Median
## Categorical vs Numerical
Ask: Does the data descibe a category or a value?
- Phone area code -> Category of location ->Categorical
# Sampling
**Good sample data**: Small, representative subset of population, random sampling
**Bias**: Result of non-representative sample
## 5 Ws of Sampling
1. Who is in the sample data?
2. When is the data collected?
3. Where is sample data collected?
^ ==These are to make sure sample is representative!==
4. Why is the data collected?
5. What is in the Study?
6. How is data taken?

## Random Sampling
Only way to get unbiased sample data
### Simple random sampling
- Randomly pick one individual from entire population repeatedly until we get desired sample size
- Every individual has an equal chance of being picked
### Stratified random sampling
- Divide population into groups based on characteristics. Choose samples from each group using simple random sampling. ==Sample size of each group is proportional to group's size in entire population.==
### Cluster Sampling
- Divide population into groups randomly, *Not* by characteristics. Select a few groups randomly to be sample.

## Bias Avoidance
We must avoid the following to have representative data:
### Voluntary response sample
- respondents decide whether to be included in sample.
	- eg. Internet polls
### Non - response:
- Only a small fraction of randomly selected people choose to respond.
	- eg. Mail in polls where only 20% of sent mail gets a response
### Convenience sample
- Accessible individuals are more likely to be included in sample.
	- eg. Instructor asks front row if his voice is loud enough (convenient but not helpful to those in the back)

# Data Sources
## Observational Study
- Observe & measure characteristics
- Determines Association, *Not* Causation
### Retrospective
- Look at (and gather) data after the event happened
	- eg. data of patients before Covid-19
### Prospective
- Look at (and gather) data of ongoing event as it's happening
	- eg. data of patients since 2010 *and ongoing*
# Organizing and presenting data
## For [[#Categorical]] data
### Frequency table
- Listing of values and their frequencies

| Grade | Count |
| ----- | ----- |
| A     | 20    |
| B     | 80    |
| C     | 60    |
| D     | 30    |
| F     | 10    |
| Total | 200  |

Alternatively, We can use relative frequencies

| Grade | Count | Percentage (can replace count) |
| ----- | ----- | ------------------------------ |
| A     | 0.1   |          10%                      |
| B     | 0.4   |            40%                    |
| C     | 0.3   |              30%                  |
| D     | 0.15  |                15%                |
| F     | 0.05  |                  5%              |
| Total | 1.0   |                   100%             |
### Bar chart
![[Pasted image 20230912112115.png|500]]
### Pie chart
![[Pasted image 20230912112200.png|400]]
### Marginal and Conditional relative frequency
#### Contingency table
| Treatment   | Relapse | No Relapse | Total |
| ----------- | ------- | ---------- | ----- |
| desipramine | 10      | 14         | 24    |
| lithium     | 18      | 6          | 24    |
| Placebo     | 20      | 4          | 24    |
| Total       | 48      | 24         | 72    |
- Table that shows data for two variables.
- Two categorical variables are said to be independent or not associated if the conditional distributions of one variable is the same in each category of the other variable.
	- When two variables are not associated, then we say one of the variables is homogeneous with respect to the other variable.
- **Marginal:** Along the bottom and right border of the table
- **The *marginal* relative frequency** distribution of Treatment is is 24/72 for desipramine, 24/72 for Lithium, and 24/72 for Placebo.
	- `(Relapse + No Relapse) / Total for each treatment`
- **The *conditional* relative frequency** distribution of Treatment for the Relapsed group is 10/48 for desipramine, 18/48 for Lithium, and 20/48 for Placebo.
	- `Relapse for each treatment/total relapse`
	- If each column's conditional relative frequencies are identical, *Variable 1 anf Var*
## For [[#Numerical]] data
### Histogram
- Roughly equivalent to Bar chart
- Bars touch each other
- Can have curve drawn
![[Pasted image 20230912112409.png|500]]
![[Pasted image 20230912112540.png|300]]
### Stem-and-leaf 
- Like a histogram but shows individual values
- Example: For the data {56, 60, 64, 64, 64, 68, 68, 68, 68, 72, 72, 72, 72, 76, 76, 76, 76, 80, 80, 80, 80, 84, 84, 88 }

| Stem                      | Leaf                       |
| ------------------------- | -------------------------- |
| (This is the first digit) | (This is the second digit) |
| 5                         | 6                          |
| 6                         | 04444                      |
| 6                         | 8888                       |
| 7                         | 2222                       |
| 7                         | 6666                       |
| 8                         | 000044                     |
| 8                         | 8                          |


