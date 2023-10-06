# Rare Event Rule for Inferential Statistics
- If, under a given assumption, the probability of a particular observed event is extremely small, we conclude that the assumption is probably not correct.
- eg. 
	- Under the assumption of a fair coin, if we get 98 heads out of 100 flips, we have to reject the assumption that the coin is a fair coin.
- Statisticians use the rare event rule for inferential statistics.

# Basic Concepts of Probability
- An **experiment** (or a random process) is an action *whose outcome cannot be predicted with certainty*.
- Eg.
	- Tossing a coin
	- Randomly selecting a card from 52 playing cards
	- Drawing a lottery ticket
	- Selecting a sample

- An **event** (denoted by A, B, C) is any *collection of results or outcomes of an experiment*.
	- eg. Getting at least one head in tossing a coin twice. i.e. {HH, HT, TH}
	- *Circle part of venn diagram*
- A **simple event** is an outcome or an event that *cannot be further broken down into simpler components*.
	- eg. Getting two heads in tossing a coin twice (i.e. {HH}) is a simple event.
	- Getting at least one head in tossing a coin twice (i.e. {HH, HT, T H}) is **not a simple event**.
- The **sample space** for a procedure consists of all possible simple events.
	- eg. The collection of all 52 cards is the sample space in randomly selecting a card in a deck of 52 playing cards.
	- *Box part in a venn diagram, denoted Ω*
## Interpretations of P(A)
==Notation: Probability of event A is denoted by P (A).==
- The probability of an outcome is the proportion of times the outcome would occur if we observed the random process an infinite number of times. ![[Pasted image 20230927101559.png]]
- P(Ω (sample space)) = 1 = area of the Box in a venn diagram
- P(A) = Area of A region
## Properties of Probability
1. The probability of an event that can not occur (impossible event) is 0.
2. The probability of an event that is certain to occur is 1.
3. For any event A, the probability of A is between 0 and 1 inclusive. i.e 0 ≤ P (A) ≤ 1
## Law of Large Number
As a random process is repeated again and again, the relative frequency probability of an event tends to approach the actual probability.
- **Example:** In a large number of fair coin tosses, one can get approximately half heads H and half tails T.
	- But this should not be misunderstood that random processes are supposed to compensate for whatever happened in the past (called Gambler’s fallacy or law of averages).
## Disjoint Events (Mutually exclusive events)
Events A and B are **disjoint** (or mutually exclusive) if they *cannot occur at the same time*.
![[Pasted image 20230927102021.png|300]]
### Examples of disjoint events
- In a coin toss, the events {H} and {T } are disjoint.
- A student can not fail and pass a course.
- A single card drawn from a deck cannot be an ace and a queen.

==MISSED 3 LECTURES beacuse of moving and stuff== #COMEBACKTOTHIS 

# Random Variables
- A **random variable** is a variable (denoted by X or Y ) that has a single numerical value, determined by chance, for each outcome of a procedure.
	- A **discrete random variable** has either a finite number of values or a countable number of values.
		- eg. Rolling a pair of dice,
	- A **continuous random variable** has infinitely many values, and those values can be associated with measurements on a continuous scale without gaps or interruptions.
		- e. flashlight battery life remaining
- **Notation:** The probability of a random variable assuming value x is denoted by P (x) or P (X = x).
- A **probability distribution** is a description that gives the probability for each value of the random variable.
	- It is often expressed in the format of a *graph, table, or formula*. i.e. A listing of the values of X and the probabilities P (X = x) or *A graph where x on the horizontal axis and P (x) on the vertical axis*.
	- Example: let X denote the number of siblings of a randomly selected student in professor Weiss’ Introductory Stat class in a previous example. The following is the probability distribution of X.![[Pasted image 20231006100114.png|300]]
## Criteria for Probability Distribution
- A probability distribution must satisfy the following two criteria:
1. ∑ P (x) = 1 where x assumes all possible values. (That is, the sum of all probabilities must be 1.)
2. 0 ≤ P (x) ≤ 1 for every individual value of x. (That is, each probability value must be between 0 and 1 inclusive.)
## Probability Histogram
- A **probability histogram** is very similar to the relative frequency histogram but the vertical scale shows probabilities instead of relative frequencies. ![[Pasted image 20231006100302.png|300]]
## Mean, Variance, and Standard Deviation
