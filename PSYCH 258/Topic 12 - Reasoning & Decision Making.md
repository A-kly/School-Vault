
# Reasoning & Decision Making

## Learning Outcomes

1. What are four kinds of logical rules?
2. Describe the propositional calculus in deductive reasoning.
3. How are normative and descriptive models different?
4. Describe the following heuristics and biases in decision making:
	- representativeness
	- availability
	- anchoring and adjustment
	- framing
	- overconfidence
	- hindsight bias
	- illusory correlation
	- confirmation bias
5. Can we make better decisions without thinking consciously?
6. What are some fallacies that occur in real-life situations?
7. What is the paradox of choice, and how do we avoid it?

---

## Deductive Reasoning

### Logical Rules

- apply logical relations to relate stimulus attributes, to determine whether a given item is a category member
- **==Conjunction== rule**: applies AND operator
	- e.g., child safety seat must be rear-facing until child is 1 year old AND weighs 10 kg

- **==Disjunction== rule**: applies OR operator
	- e.g., Archie can marry either Betty OR Veronica

- **==conditional== rule**: applies IF, THEN operator
	- e.g., IF a man is a bachelor, THEN he is unmarried

- **==biconditional== rule**: applies conditional rule in both directions; IFF (“IF AND ONLY IF” or XNOR)
- an item is a member of the category if it has both attributes, or neither attribute
	- e.g., J.D. has the flu IF AND ONLY IF Turk has it

### Conditional Reasoning

- states relation between conditions: **==antecedent==** and a **==consequent==** (“IF -p-, THEN -q-.”)
	- e.g., “If the Oilers win the game, then I will cheer.”

- may be affirmed (true) or denied (false): is the conclusion true, false, or indeterminate?
- **the ==propositional calculus==**: system for categorizing conditional reasoning statements

1. affirming the ==antecedent== (-modus ponens-: “mode that affirms”):

“The Oilers won the game.”

- produces valid conclusion: (consequent=true) “I am cheering.”
- easiest to evaluate

2. affirming the ==consequent==:

“I am cheering.”

- produces invalid conclusion: (antecedent=indeterminate): you don’t know if the Oilers won the game or not
- maybe I’m cheering because I found $20!
- next easiest to evaluate

3. denying the ==antecedent==:

“The Oilers did not win the game.”

- produces invalid conclusion: (consequent=indeterminate): you don’t know if I’m cheering or not
- maybe I’m cheering anyway, because I found $20!

4. denying the ==consequent== (-modus tollens-: “mode that denies”):

“I am not cheering.”

- produces valid conclusion: (antecedent=false): “The Oilers did not ==not== the game.”
- most difficult to evaluate
- try: “If there is a solar eclipse, then the streets will be dark".
- problems with negatives more difficult to solve

---

## Perspectives on Decision Making

- **==normative== model**: how a decision -*should*- be made, given unlimited resources (e.g., memory, time, information) to devote to the decision
	- -*homo economicus*- (“economic human”) concept in neoclassical economics views humans as rational decision-makers
- **==descriptive== model**: how people -*really*- reach decisions, given limited memory abilities, time, information, etc.
	- **behavioural economics** includes social, emotional, and cognitive factors

“I’m going to roll a die. If a 6 appears, you win $5, otherwise you win nothing. It costs $1 to play.”

Is it worth it to play?

- **expected ==value==**: objective, statistical value of outcome

= (*p* (W) × *v* (W)) + (*p* (L) × *v* (L))

= ((1/6) × $4) + ((5/6) × -$1) = -$1/6 (average loss of ~17¢ each roll)

- does not always ==accurately== predict behaviour
- **expected ==utility==**: subjective value of an outcome

= (*p* (W) × *u* (W)) + (*p* (L) × *u* (L))

= ((1/6) × $6) + ((5/6) × -$1) = +$1/6 (average gain of ~17¢ each roll)

- better at predicting/explaining behaviour (gambling is fun,  ==insurance== protects you against high potential loss)
- **subjective expected ==utility==**: subjective value of an outcome according to subjective assessment of probability

= (*sp* (W) × *u* (W)) + (*sp* (L) × *u* (L))

= ((6/6) × $6) + ((0/6) × -$1) = +$6 (average gain of $6 each roll)

- what people do is not always statistically the best decision

---

## Decision Making

**Prospect Theory** (Kahneman & Tversky, 1979)

Daniel Kahneman (b.1934-d.2024, won Nobel prize in Economics, 2002) & Amos Tversky (b.1937-d.1996); both shared Grawemeyer Award in Psychology in 2003

- describes how potential gains and losses are evaluated, using heuristics and biases
- cognitive features (Kahneman, 2011):
- evaluation is made with respect to a reference point or baseline
	- e.g., winning $10 is worth more to you than to a billionaire

- principle of diminishing sensitivity
	- e.g., winning $1,000 is good; winning $1,010 is not much better

- loss aversion: people are more sensitive to losses than gains
	- e.g., winning $10 is good; losing $10 is really, really bad

- value function:

![Prospect Theory](PSYCH%20258/Attachments/p258s13-1.png)

e.g., public service announcements about breast self-exams that emphasize benefits of early cancer detection (gains) are less effective than those that emphasize costs of late detection (losses)

e.g., energy conservation appeals that focus on savings (gains) are less powerful than those that focus on added costs of using energy (losses)

**Framing Effect** (Tversky & Kahneman, 1981)

- judgments can be affected by the way information is presented
	- e.g., Which would you choose?

a) sure ---- of $10,000

b) 50% chance of ------- $20,000 and 50% chance of getting $0
	- e.g., Which would you choose?

a) sure ---- of $10,000

b) 50% chance of ------ $20,000 and 50% chance of losing $0

- if framed in terms of gains, people are risk-------; if framed in terms of losses, people are risk--------

Kahneman & Tversky (1984):

Gp 1: Imagine that you decided to see a play and you paid $20 for the admission price of one ticket. As you enter the theatre, you discover that you have lost the ticket. The theatre keeps no record of ticket purchasers, so the ticket cannot be recovered. Would you pay $20 for another ticket?

Gp 2: Imagine that you decided to see a play where the price of one ticket is $20. As you enter the theatre, you discover that you have lost a $20 bill. Would you still pay $20 for a ticket to the play?

- only --% of gp. 1 chose another ticket (cost of play perceived to be -------)
- 88% of gp. 2 chose to buy the ticket
- background context affects choice:

Which would you prefer, saving $500 on tuition, or saving $500 on a new ---?

**Representativeness Heuristic** (Kahneman & Tversky, 1972)

- judging likelihood by how well something matches the ---------
	- e.g., Is (a) finding 600 boys in a sample of ----- children as likely as (b) finding 60 boys in a sample of --- children?

(assuming even distribution of sexes, --- is far less likely)

- **------------ fallacy**: assuming that small samples will be representative of population; this violates the law of large numbers
	- e.g., There is a disease that has an incidence of 1 in 1,000. A test to detect it has a false positive rate of 5%. What are the chances that someone with a positive result actually has the disease?

(mean response = ----%; mode = --%; correct = --%)

(1 in 1,000 has disease, 999 do not; 5% of --- = --

 -- test positive; only ---- actually has disease = --%)

- **---- rate fallacy**: reasoning based on distinctive features, not probability in the population
	- e.g., Linda is 31 years old, single, outspoken, and very bright. As a student, she majored in philosophy, and was deeply concerned with issues of discrimination and social justice, and also participated in anti-nuclear demonstrations.

Which is more probable, that she is a bank teller, or that she is a bank teller who is an ------ --------?

(there are ---- bank tellers than -------- bank tellers)

- **----------- fallacy**: probability of a conjunction is less than that for a single condition
	- e.g., Flip a coin: H T H H H H H H

What will come up next?

(each side has 50% chance of coming up, each toss)

- **--------- fallacy**: reasoning based on expectation, not probability

**Availability Heuristic** (Tversky & Kahneman, 1973)

- judging probability by how ------ examples are retrieved
	- e.g., Are there more words that begin with “k,” or have “k” as the third letter?

- causes:
- **-----------**: more familiar items more easily retrieved
- **-------**: retrieving more recent items causes overestimation of probability
- **---------- heuristic**: probability judgment affected by ability to imagine an event

**Anchoring and Adjustment Heuristic** (Tversky & Kahneman, 1974)

- initial approximation (------) may affect later judgments (----------)
	- e.g., How long is the Mississippi?

|   |   |
|---|---|
|**“Greater or less than...**|**Average response:**|
|...500 miles?”|------ miles|
|...5,000 miles?”|------ miles|

(initial number influenced estimates; answer = ----- miles)

**Overconfidence** (Fischhoff, Slovic, & Lichtenstein, 1977)

- overestimating the accuracy of one’s knowledge and judgments
	- e.g., weaker tournament chess players believe they can beat someone with the same skill level more than two-thirds of the time (Chabris et al., 2014)

- causes:
- people unaware their knowledge is based on unreliable information
- ------ effect: difficulty in recalling information
- includes confirmation bias

**Hindsight Bias** (Fischhoff & Beyth, 1975)

- tendency to consistently exaggerate what could have been anticipated in foresight, when looking back in hindsight
	- e.g., physicians were given a clinical case history

- foresight group had to make a diagnosis
- hindsight group were given a plausible diagnosis in advance
- hindsight group were 2-3 times more likely to agree with the given diagnosis than the foresight group (Arkes et al., 1981)
- causes (Roese & Vohs, 2012):
- memory distortion
- beliefs about events’ objective likelihoods (-------------)
- subjective beliefs about one’s own prediction abilities (--------------)

**Illusory Correlation** (Chapman, 1967)

- judging a correlation where none exists (or vice-versa)
	- e.g., Is there a relationship between height and temperament?

|   |   |   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|---|---|
|height:|80|63|61|79|74|69|71|75|77|60|
|temperament:|75|66|60|90|60|42|31|60|81|39|

(correlation: -r- = -----; -p- = .08)

**Confirmation Bias** (Wason, 1960) ==IMPORTANT==

- seeking evidence confirming a belief--even to the exclusion of contradictory information

Assuming that each card has a letter on one side and a number on the other, which card(s) must be turned over to test this statement?

“If a card has a vowel on one side, then it has an even number on the other side.”

|   |   |   |   |
|---|---|---|---|
|E|J|6|7|

(results: 33% chose positive evidence alone; only 4% chose positive and negative evidence; Wason, 1966)

Criticisms of Prospect Theory:

- [c] runs counter to traditional economic view of people as rational

- [c] relies on “stated preferences” in surveys, not “revealed preferences” of behaviours

- [c] “demonstration approach” seems designed to show flaws in decision making; are we really that bad?

- [c] lacks ==explanation== of underlying mechanisms

---

## Unconscious Thought Theory

(Dijksterhuis & Nordgren, 2006)

Principles of unconscious thought:

- occurs outside of ==attention==
- capacity not limited by working memory
- applies bottom-up processing
- superior at weighting importance of choice attributes
- uses ==associative== thinking, not rule-based thinking
- is divergent, not convergent

Dijksterhuis (2006):

- participants given positive and negative information about apartments or roommates
- choice conditions:
- immediate decision
- conscious thought: given 3 minutes to analyze their preferences
- unconscious thought: performed digit-manipulation task for 3 minutes
- dependent variable: selection of best alternative
- results:

![unconscious thought experiment](PSYCH%20258/Attachments/p258s13-2.png)

- unconscious thinkers made the best decisions

Criticisms (Newell, 2015; Nieuwenstein et al., 2015):

- [c] some findings not replicable; meta-analysis found no advantage

- [c] some studies failed to include control (i.e., immediate) condition

- [c] giving participants as much time as they needed to think consciously led to superior performance

---

## Practical Logic

Fong, Krantz, & Nisbett (1986):

- students in statistics course called for phone survey
- asked question about sports, not “statistics” (e.g., why baseball Rookie of the Year tends to do worse in his second year)
- non-statistical answer: ==pressure== causes poorer performance
- statistical answer: conjunction of talent and ==luck==
- students contacted early in term: 16% gave statistical answer; those contacted later: 37%

Mill, Gray, & Mandel (1994):

- undergraduate training in social sciences: no improvement in applying critical thinking to reasoning in everyday situations

Damer (2012): -Attacking faulty reasoning: A practical guide to fallacy-free arguments-

- teaches people to avoid fallacies or errors in real-life situations
- **==illicit== contrast**: if one thing lacks a certain property, any contrasting object must have that property (or vice-versa)
	- e.g., “The provincial government is crooked. I’m glad I’m a member of the opposition.”

- **argument by ==innuendo==**: directing one to a particular (suggestive) conclusion by choice of words
	- e.g., “Is the president a good guy? Well, he’s never been convicted of anything.”

- **fallacy of the ==continuum==**: assuming that small differences are always unimportant
	- e.g., “I know your monthly payments are high. But what’s another $20 a month?”
	- e.g., The ==Latte== Factor®: difference between spending $3/latte/day vs. saving your money = $5855 over 5 years

- **==loaded== question**: using language that presupposes a certain conclusion
	- e.g., “When are you going to stop cheating on exams?”

- **fallacy of the ==composition==**: assuming that what is true of the parts is true of the whole
	- e.g., “You like potatoes. You like chicken. You like ice cream. So you’ll love this potato-chicken-ice cream casserole.”

---

## The Paradox of Choice

More is not better:

- students given a large number of topics for an extra-credit essay were less likely to write one than those given a small number of topics (they also wrote essays of lower ==quality==)
- when convenience stores reduced the variety of soft drinks and snacks available, sales volume increased (as did customer satisfaction)
- more matches made in an evening of “speed dating” in which young adults met 8 potential partners than when they met 20
- Swedes were less likely to save money using a government retirement plan when a greater variety of investment options was presented to them
- these are examples of the choice overload effect (or choice paralysis)

Iyengar & Lepper (2000):

- set up sample table of Wilkin & Sons exotic jams in a grocery store

e.g., Strawberry & Champagne, Cranberry & Cointreau, Rhubarb & Ginger

- gave samples of 6 or 24 jams on different days; all 24 available for purchase
- tasters were given $1-off coupons
- more customers attracted to larger tasting array, but same number of tastings in both conditions (about 1.5/person)
- results: ==30==% of customers exposed to small array made a purchase versus 4% of those exposed to large array

Why does greater choice make people miserable?

- **==Missed== opportunities**: options not chosen have positive qualities
- **The curse of high ------------**: with many options, your final selection should be perfect (or at least extraordinary)
- **------**: if your final selection is not perfect, disappointment results
- **----------**: in a world of abundant choice, disappointing results attributed to your poor selection

How do you make decisions?

- **----------**: choose the optimal alternative by evaluating pros and cons of every option
- **-----------** (“satisfy” and “suffice”): choose the alternative sufficiently good to satisfy you
- career decisions made by college seniors: maximizers got better salaries, but felt worse about their selection (Iyengar, Wells, & Schwartz, 2006)
- maximization correlated with ---------- (-r- = .34)

Lessons on choice (Schwartz, 2004; 2016):

- choose when to ------: restrict your options when decisions are not crucial
- learn to accept “---- ------”: pick an alternative that meets your core requirements, not the elusive “best”
- don’t worry about what you’re -------: forget about the attractive features of the alternative you reject; focus on the positives of your selection
- control ------------: lower expectations mean less disappointment

---

This document copyright © 2000-2024 Karsten A. Loepelmann. All rights reserved. Viewing this page is taken as acceptance of the [copyright agreement](https://sites.ualberta.ca/~kloepelm/copy.html).