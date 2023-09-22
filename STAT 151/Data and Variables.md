# Statistics Process
Goal: to take a sample of a very large population, Analyze and come to conclusion about the full population
## Descriptive Statistics
- Gathering data
- Summarize and present the data
	- **[[#Summary of data|Summarize]]**: Mean, standard dev, median
	- **Present**: Histogram, graphs, tables
- Analyze and interpret the data
	- What does the data (median, mean, standard deviation, histogram) mean?
## Inferential statistics
- Make generalisations of the population
# Data types
## Categorical
No granularity, only categories	

- **Nominal**: No method to compare between categories, we have simply given *Names* to categories. 
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
	- ==`For every row in table: (entry in chosen column / total for column)`
	- If each column's conditional relative frequencies are identical, *Variable 1 and Variable 2 are not associated / Are independent variables*

#### Segmented bar chart
- Segmented Bar charts can also be used to see the association between two categorical variables. (Rows from table on bottom, )
![[Pasted image 20230915101553.png|400]]
#### Double bar chart 
For the following contingency table:
![[Pasted image 20230915103016.png|300]]
We can generate the following double bar chart:
![[Pasted image 20230915103038.png|300]]

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

# Summary of data
### Definitions
Calculations based on *population data* is called a **parameter.**
Calculations based on *sample data* is called a **Statistic.**
## Center of Data
==Most typical value==
![[Pasted image 20230918100228.png]]
- **Skewed to the Left:** Pushed towards the right from the left. Extremes to the left.
	- Mean < Median < Mode
- **Skewed to the Right:** Pushed towards the left from the right. Extremes to the right.
	- Mode < Median < Mean
- **Symmetric:** No skewing.
	- Median = Mean = Mode
### For [[#Numerical]] data
Example data = `{0,100,100,100}`

- Mean
	- $$\overline x \space in \space sample = M \space in \space population= Mean = \frac{\sum(xi)}{n}$$
	- (n = Number of values, xi = the ith data value)
	- *Add all values, divide by number of values*
	- Uses all values
	- For example data, Mean = `(0 + 100 + 100 + 100) / 4 = 75`
	- *Symetrical data*
	- If there are two datasets with respective sample sizes and averages n1, x1 and n2, x2, then the average of the two combined datasets is given by:![[Pasted image 20230921134013.png]]
- Median
	- *Middle value* after sorting data in increasing order
	- **If n is odd:** median is middle value
	- **If n is even:** median is average (mean) of two middle values
	- Uses only middle values
	- *Skewed data*
	- *Divides area under curve in half equally*
	- For example data, Median  = `(100 + 100) / 2 = 100`

==For skewed data, the median is more appropriate than the mean==
- eg. Some CEOs make Millions, Some make BILLIONS
### For [[#Categorical]] data
Example data = `{F, M, F, F, M}`
- Mode
	- The most frequent value in the data
		- Value that repeats the most frequently
	- appropriate for categorical data
		- We cannot use mean (eg. averaging gender) or median (eg. gender is not ordered)
	- For example data, `M` shows up 2 times, `F` Shows up 2 times Therefore *Mode = F*
## Measures of variation
### Range
$$Range = Maximum \space value - Minimum \space value$$

### Standard deviation
Measures the variation of values around the mean
#### For population
$$Standard\space Deviation \space for \space a \space population = \sigma = \sqrt {\frac{\sum{(x-\mu)^2}}{N}}$$
**Where ==N== is the population size**
**Where ==Mu== is mean**
#### For sample
$$Standard \space deviation \space for \space a \space sample = s = \sqrt {\frac{\sum{(xi-\overline {x})^2}}{n-1}}$$ ![[Pasted image 20230918100935.png|400]]
**Where ==n== is the sample size**
**Where ==x bar== is mean**
**Where ==xi== is a given datum**
$$ (xi-\overline{x}) = Mean \space deviation$$
### Variance 
$$ Sample \space variance = s^2 = (std \space dev)^2$$


### Inter quartile range (IQR)
- **Quartiles:** Denoted Q1 --> Q3, Divides the sorted data into four equal parts.
	- *Remember, median divides data into two halves*
	- *Quartiles are an extension of the median*
#### Estimating Quartiles
- **Q2** is exactly the median of the entire data set.
- **Q1** is the median of the bottom 50% of the data.
	- Median from lowest value to Q2 (excluding Q2 if it is not part of the original data).
- **Q3** is the median of the top 50% of the data.
	- Median from Q2 to highest value (excluding Q2 if it is not part of the original data).
#### Interquartile range
$$IQR = Q3-Q1$$
IQR gives us the range that covers the *middle 50%* of the data.
## More summary tools
### Upper fence & Lower fence
**Used to set a cut-off for *outlier* values.**
- Upper fence/limit:
$$ Upper \space Fence = Q3 + 1.5 \space IQR$$
 - Lower fence/limit:
$$ Lower \space Fence = Q1 - 1.5 \space IQR$$
- Values *above upper fence* or *below lower fence* are outliers.
- **Adjacent values:** Values right before cut-offs.
### The five-number summary
- The five-number summary of a data set is Min, Q1, Q2, Q3, Max.
### Box plot
To Construct a Boxplot:
1. Determine the quartiles, potential outliers and the adjacent values.
2. Draw a horizontal axis on which the numbers obtained in Steps 1 can be located. Above this axis,  mark the quartiles and the adjacent values with vertical lines.
3. Connect the quartiles to make a box, and then connect the box to the adjacent values with lines.
4. Plot each potential outlier with an asterisk
![[Pasted image 20230920101230.png]]
- Remember, Q2 is median.
**Note:** Boxplots can can be used to compare two data sets as shown in the following example.
Researchers measured skinfold thickness, an indirect indicator of body fat, of samples of runners and non-runners in the same age group. The sample data, in millimetres (mm), are presented below. Use boxplots to compare these two data sets, paying special attention to center and variation. ![[Pasted image 20230920101809.png]]
- Boxplot can also be used to identify the approximate shape of the distribution of a data set. ![[Pasted image 20230920102632.png]]
### Percentiles
- denoted P1, P2, . . ., P99, which partition the data into 100 groups with about 1% of the values in each group.
![[Pasted image 20230920103337.png]]
- Same role as quartiles
## Relative Standing and Normal Model
- A **z-score** (or standardized value), is the number of standard deviations that a given value x is above or below the mean.
	- Shows the relative standing of x in the data (around mean).
- For a sample: $$ Z = \frac {x−\overline x} {s}$$
- For a population: $$ Z = \frac {x−\mu} {\sigma}$$Rounded to 2 decimal places
- *Used to compare two values in two different groups.*
	- If you have two data sets, `data1` and `data2`
	- How do we compare a given `x1` from `data1` with a given `x2` from `data2`?
	- We use the Z-score do do it!
	- eg. compare two students across two different midterms
## Density curves
![[Pasted image 20230922100831.png|300]]
- Always above horizontal axis
- Uses relative frequency as y axix
- `P(a<x<b)` = Area under the curve between `a` and `b`.
	- Percentage of observational data between `a` and `b`.
### Normal curve (special type)
![[php6pVJmc.png|300]]
- ` X ~ N(M,σ)` = The variable `X` has a Normal distribution (`N`) with mean  `M` and standard dev `σ`
	- eg. X = midterm scores of stat 151, `X ~ N(70%, 9%)`
		- Mean of midterm scores = 70%
		- Standard deviation = 9%
![[2880px-Standard_deviation_diagram_micro.svg.png]]
- `P(M-σ<X<M+σ) = 68.2%`
- `P(M-2σ<X<M+2σ) = 95.45%`
- `P(M-3σ<X<M+3σ) = 99.73%`
![[Pasted image 20230922102241.png]]
