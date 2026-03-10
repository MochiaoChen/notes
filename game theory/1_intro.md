---
tags:
  - game-theory
  - course-notes
  - economics
aliases:
  - Game Theory Introduction
date: 2026-03-09
---
# Game Theory: An Introduction 

## 1. What is Game Theory? 

Game Theory is a systematic study of strategic interactions among a group of rational decision makers. 
### Strategic Interaction 

* Each individual's actions have an effect on the outcome of interest to all. 
* Decision makers are aware of that their actions have an effect on others as well. 
* They act accordingly. 
### Rationality 

* Rational choices: a decision-maker chooses the best action according to her preferences, among all the actions available to her. 
* A set of actions or outcomes. 
* **Well-defined** (i.e. complete and transitive) **preference** over the set of actions. 
* Completeness and transitivity are necessary for presentation of utility (payoff) functions. 
* Decision maker can choose the best action/outcome according to her preference. 
* The action chosen is at least as good, according to her preferences, as every other available action. 
### Realistic? 

* "Strategic interaction" is more loaded than it seems.  One needs to assume that the rules of the game, including how actions affect the participants and individuals' rationality, are **common knowledge.** 
* A fact X is **common knowledge** if everybody knows it, if everybody knows that everybody knows it, if everybody knows that everybody knows that everybody knows it, and so on.  A interesting puzzle about common kenowledge is [[The Red Eyes Logic Puzzle]].
* "Rationality" is more demanding than it appears. 
* A limiting case of **bounded rationality**. 
	* Always optimizing?  Common knowledge is ideal in mathematics, but challenging in practice. 
		* Guess the average game (and higher order belief). 
		* Challenging in multi-stage games. 
	* Expected utility?  
		* Allais Paradox; 
		* Framing Effect.
### Then Why? 

* The objective of game theory is to organize our knowledge and increase our understanding of the outside world (not to model the world per se). 
* The best analytical models are based on rationality for lack of better alternatives. 
* The bottom line.  Proof of the pudding is in the eating: if a model enhances our understanding of the world, then it serves its purpose. 
* "When our task is to look for potential flaws in a social institution, it can be very helpful to analyze the institution under an assumption that the agents in the institution are not themselves flawed." (Myerson, 1999) 
## 2. Why Should We Study It? 

* Strategic interactions are pervasive in economics, politics, biology, etc. 
* Firms competes for business. 
* Bidders competes in an auction. 
* Political candidates competes for votes. 
* Workers and managers and so on. 
* A rigor training of logics.  Be trained to be better at thinking (about the real world). 
## 3. How Can We Study It? 

* Mathematics. 
* Logics. 
* Algebra. 
* Probability Theory. 
* Calculus. 
* Real analysis and functional analysis(\*). 
* Models. 
* Abstractions that we use to understand our observations and experiences. 
## 4. History of Game Theory

* Ideas of game theory can be traced back to ancient times. 
* Ancient China: Horse Racing; Confucianism; Mohism; etc. 
* Division of marital property in Talmud. 
### Early Studies of Game Theory 

* Cournot (1838): quantity competition of oligopolies. 
* Bertrand (1883): price competition. 
* Zermelo (1913): the first formal theorem of game theory; the idea of backward induction. 
* Emile Borel (1921-1927): two-person zero-sum games, methods of play, mixed strategy. 
* John von Neumann (1928): strategy (German "Spielmethode" from French "methode de jeu"); min-max solution to zero-sum games. 
* John von Neumann (1941): normal form game and extensive form game; expected utility. 
### Starting Point of the Modern Game Theory 

* John von Neumann and Oskar Morgenstern (1944): Theory of Games and Economic Behavior. 
* Many fundamental concepts are formally proposed: strategic form games, extensive form games, etc. 
### Fast Development of Game Theory: 1950s-1970s 

* John Nash (1950-1951): was awarded Nobel Prize in 1994.  
	* Nash Equilibrium: Equilibrium Points in N-person Games; 
	* Nash Bargaining Solution: The Bargaining Problem. 
* Harold Kuhn (1950, 1953): reformulate extensive form and behavioral strategy. 
* Lloyd Shapley (1952-1953): was awarded Nobel Prize in 2012.  
	* Shapley value; 
	* Core. 
* Thomas Schelling (1960): was awarded Nobel Prize in 2005.  
	* The Strategy of Conflicts. 
* Reinhard Selten (1965): was awarded Nobel Prize in 1994.  
	* Subgame Perfect Equilibrium; 
	* Trembling Hand Equilibrium. 
* John Harsanyi (1967-1968): was awarded Nobel Prize in 1994.  
	* Harsanyi transformation; 
	* Bayesian Equilibrium of incomplete information. 
* Robert Aumann (1959-1976): was awarded Nobel Prize in 2005.  
	* Common knowledge; 
	* Correlated Equilibrium. 
* David Kreps and Robert Wilson (1982): Robert Wilson was awarded Nobel Prize in 2020. 
	* Sequential Equilibria. 
## 5. Examples 

### Example 1.1 (A Single Person Decision Problem) 

Suppose Ali is an investor who can invest his $100 either in a safe asset, say government bonds, which brings 10% return in one year, or he can invest it in a risky asset, say a stock issued by a corporation, which either brings 20% return (if the company performance is good) or zero return (if the company performance is bad). 

| State | Good | Bad |
| :--- | :--- | :--- |
| Bonds | 10% | 10% |
| Stocks | 20% | 0% |


### Example 1.2 (An Investment Game) 

Now, suppose Ali again has two options for investing his $100.  He may either invest it in bonds, which have a certain return of 10%, or he may invest it in a risky venture.  This venture requires $200 to be a success, in which case the return is 20%, i.e., $100 investment yields $120 at the end of the year.  If total investment is less than $200, then the venture is a failure and yields zero return, i.e., $100 investment yields $100.  Ali knows that there is another person, let's call her Beril, who is exactly in the same situation, and there is no other potential investor in the venture.  Unfortunately, Ali and Beril don't know each other and cannot communicate.  Therefore, they both have to make the investment decision without knowing the decisions of each other. 

| Ali \ Beril | Bonds            | Venture          |
| :---------- | :--------------- | :--------------- |
| Bonds       | **110**, **110** | 110, 100         |
| Venture     | 100, 110         | **120**, **120** |


### Example 1.3 (Prisoners' Dilemma) 
Probably the best known example, which has also become a parable for many other situations, is called the Prisoners' Dilemma.  The story goes as follows: two suspects are arrested and put into different cells before the trial.  The district attorney, who is pretty sure that both of the suspects are guilty but lacks enough evidence, offers them the following deal: if both of them confess and implicate the other (labeled C), then each will be sentenced to, say, 5 years of prison time.  If one confesses and the other does not (labeled N), then the "rat" goes free for his cooperation with the authorities and the non-confessor is sentenced to 6 years of prison time.  Finally, if neither of them confesses, then both suspects get to serve one year. 

| Player 1 \ Player 2 | C              | N         |
| :------------------ | :------------- | :-------- |
| C                   | **-5**, **-5** | **0**, -6 |
| N                   | -6, **0**      | -1, -1    |


### Example 1.4 (Rebel Without a Cause) 

Game of Chicken.  In the classic 1955 movie Rebel Without a Cause, Jim, played by James Dean, and Buzz compete for Judy, played by Natalie Wood.  Buzz's gang members gather by a cliff that drops down to the Pacific Ocean.  Jim and Buzz are to drive toward the cliff; the first person to jump from his car is declared the chicken whereas the last person to jump is a hero and captures Judy's heart.  Each player has two strategies: jump before the other player (B) and after the other player (A).  If they jump at the same time (B, B), they survive but lose Judy.  If one jumps before and the other after, the latter survive and gets Judy, whereas the former gets to live, but without Judy.  Finally, if both choose to jump after the other (A,A), they die an honorable death. 

| Jim \ Buzz | B | A |
| :--- | :--- | :--- |
| B | 2, 2 | 1, 3 |
| A | 3, 1 | 0, 0 |

### Example 1.5 (Entry Game) 
In this game Pepsi (P) first decides whether to enter a market currently monopolized by Coke (C).  After observing Pepsi's choice Coke decides whether to fight the entry (F) by, for example, price cuts and/or advertisement campaigns, or acquiesce (A). 

Game Tree Mapping:
* Player P chooses "Out": Payoff is 0, 4. 
* Player P chooses "In": Player C decides next. 
  * Player C chooses "A": Payoff is 2, 2. 
  * Player C chooses "F": Payoff is -1, 0. 
### Example 1.6 (Voting) 
Suppose that there are two competing bills, A and B, and three legislators, voters 1, 2 and 3, who are to vote on these bills.  The voting takes place in two stages.  They first vote between A and B, and then between the winner of the first stage and the status-quo, denoted S.  The voters' rankings of the alternatives are given as follows. 

| Voter 1 | Voter 2 | Voter 3 |
| :--- | :--- | :--- |
| A | B | S |
| B | S | A |
| S | A | B |
### Example 1.7 (Investment Game with Incomplete Information) 
Let us go back to Example 1.2, which we modify by assuming that Ali is not certain about Beril's preferences.  In particular, assume that he believes (with some probability p) that Beril has the preferences represented in Example 1.2, and with probability 1-p he believes Beril is a little crazy and has some inherent tendency to take risks, even if they are unreasonable from the perspective of a rational investor. 

**Normal (p)** 

| Ali \ Beril | Bonds | Venture |
| :--- | :--- | :--- |
| Bonds | 110, 110 | 110, 100 |
| Venture | 100, 110 | 120, 120 |


**Crazy (1-p)** 

| Ali \ Beril | Bonds    | Venture  |
| :---------- | :------- | :------- |
| Bonds       | 110, 110 | 110, 120 |
| Venture     | 100, 110 | 120, 120 |

### Example 1.8 (Signalling) 
Suppose that Ali takes Beril out on a date.  Beril is going to decide whether she is going to have a long term relationship with him (call that marrying) or dump him.  However, she wants to marry a smart guy and does not know whether Ali is smart or not.  However, she thinks he is smart or dumb with equal probabilities.  Ali really wants to marry her and tries to show that he is smart by cracking jokes and being funny in general during the date.  However, being funny is not very easy.  It is just stressful, and particularly so if one is dumb, to constantly try to come up with jokes that will impress her. 

Game Tree Mapping:
* God assigns Ali as "smart" or "dumb". 
* If Smart: 
  * Ali chooses "quite", Beril chooses "marry" (2, 1) or "dump" (0, 0). 
  * Ali chooses "funny", Beril chooses "marry" (1, 1) or "dump" (-1, 0). 
* If Dumb: 
  * Ali chooses "quite", Beril chooses "marry" (2, 0) or "dump" (0, 1). 
  * Ali chooses "funny", Beril chooses "marry" (-1, 0) or "dump" (-3, 1). 
## 6. Methodology 
* Try to find general principles that apply to all games. 
* To analyze abstract games and suggest "reasonable" solutions. 
* A classification based on two dimensions: (1) the order of moves; (2) information. 
* Other classifications. 

| Order of Moves | Complete Information | Incomplete Information |
| :--- | :--- | :--- |
| **Simultaneous** | Strategic Form Games with Complete Information (Example 1.2) | Bayesian Games (Example 1.7) |
| **Sequential** | Extensive form Games with Complete Information (Example 1.5) | Extensive form Games with Incomplete Information (Example 1.8) |
