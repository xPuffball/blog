---
title: "How to Lie with Statistics with your Robot best Friend"
published: 2026-03-25
description: "+ p-hacking and is it bad?"
image: "./blog5_thumbnail.png"
tags: ["NLP", "Articles", "LLM", "Papers"]
category: Articles
draft: false
---

Performing traditional statistical analysis is often compared to navigating a "Garden of Forking Paths" (Gelman and Loken). It's a term that helps (hopefully) visualize the countless number of analytical choices researchers must make during an experiment, and how seemingly insignificant "turns" (like which variables to control for, which outliers to remove...) can have researchers end up at completely different conclusions. 

![image](./mich.png)
*dr strange and the multiverse of madness but his doctorate is in sociology and he just really needs a publication, man*

source: https://www.si.umich.edu/about-umsi/news/ditch-stale-pdf-making-research-papers-interactive-and-more-transparent

While this seems like a mostly harmless analogy, navigating this garden to find that single path that goes where you want can be called "**p-hacking.**" Formally, we can define it as any measure a researcher applies to render a previously non-significant hypothesis test significant (usually under 0.05). More informally, I'm sure everybody has had experience faking the results for an experimentation assignment during your high school chemistry or physics class - and while the stakes for a satisfactory grade on a high school assignment is pretty low, under the stress of formal academia's "**publish or perish**" (only second to spanish or vanish in intimidation), the pressure to p-hack can be a very real tempting devil on your shoulder.

![image](./red.png)
*ok just write that it was red in the report*

While the traditional image of a stressed out PhD student fudging some numbers on a study spreadsheet at 3:00AM may present a more striking image of one's motivation to p-hacking, we'll also be exploring what happens when we leave the navigating of this garden of forking paths to artificial intelligence. As AI workflows find their way into every nook and cranny of both academia and industry, it'll be important to figure out if our friendly neighbourhood LLMs will act as the ultimate guardians of scientific integrity, or a sycophant automating fraud on an industrial scale.

## 1. The Human Baseline ("Big Little Lies")
---
To provide a brief introduction and some examples of real p-hacking methods, we introduce a paper "Big Little Lies" (Stefan and Schönbrodt, 2023) that provides a compendium of the many sneaky, and sometimes even unintentional ways studies can manipulate their variables and datasets to arrive at suspiciously significant outcomes.

![image](./bg.png)
*completely original and legally unproblematic*

Okay! So let's start with a hypothetical - we are the new data scientist working for an energy drink company making extremely ineffective energy drinks, and with the current job market, you really want to continue being a data scientist, even at a bogus drink company. Our shaky career depends on proving that our drinks work.

### 1.1 Ghost Variables
---
![image](./bg2.png)
We start by running a study on our tap water energy drink and measure 10 different outcomes: weight, blood pressure, cholesterol, energy levels, sleep quality, anxiety, and maybe even hair growth - nine of those variables could show no change whatsoever, but we notice that "hair growth" shows a statistically significant improvement purely by random statistical noise! We can now publish a study pretending as if hair growth was the primary hypothesis all along, while quietly sweeping the nine unreported metrics under the rug (turning them into **"Ghost Variables")**. Stefan and Schönbrodt's simulations show that doing this with 10 uncorrelated variables inflates the false-positive rate from the standard 5% to nearly 40%

### 1.2 Data Peeking/Optional Stopping
---
![image](./bg3.png)
In a separate test, we test 20 people and find no significant effect for the drink. Thinking the sample is just too small, you test 10 more and check again. Still nothing. You test 10 more and check again, and... the p-value randomly dips below 0.05, so you stop the study immediately and publish your "findings". Stefan and Schönbrodt demonstrate that this practice drastically inflates the rate of false-positive results, especially when researchers take smaller "steps" between peeks. Metaphorically, it's like taking a photo of a stumbling drunk person the exact millisecond they step onto the sidewalk and claiming they are walking perfectly straight.

### 1.3 Outlier Exclusion
---
![image](./bg4.png)
We now analyze your energy drink data and realize you are agonizingly close to significance (e.g., p = 0.06). We decide to clean our data, taking advantage of the fact that there is no universally agreed-upon rule for outliers - Cook's Distance, Influence, Box Plots, our grandmother's opinion on which opinions are trustworthy...

Stefan and Schönbrodt cite a literature review that found at least 39 different outlier identification techniques. Amazing! We are now flush with options. We try method A (e.g., removing people who took too long on a survey), and then try method B (e.g., Cook's distance) until we find the specific mathematical rule that deletes the two participants who hated the drink, pushingour p-value to 0.04. Stefan and Schönbrodt's simulations confirm that subjectively applying different outlier methods like this heavily inflates false-positive rates.

### 1.4 Scale Redefinition
---
![image](./bg5.png)
Finally, we conclude by giving a 10-question survey measuring how energized they feel after drinking the tap water. The overall result isn't significant, so we just drop question 4 and question 7, telling ourselves the participants must have found them confusing anyway. We can actually use this to artificially improve the scale's internal consistency (Cronbach's alpha) while simultaneously optimizing for a significant p-value! Big Little Lies demonstrate that false-positive rates increase drastically as more items are removed from a measurement scale.

So... like the name of the paper suggests, human p-hacking is a collection of "big little lies". The human toolkit is really just a collection sophisticated ways to fool ourselves, without necessarily having to be evil or malicious. Humans are biased, messy, and sometimes really desperate for tenure (or employment, in our case!), and sometimes we use all the ambiguity we can take to get there.

## 2. AI Sycophancy and the Illusion of Safety
---
So far, we covered a small subset of methods that us measly humans have used to p-hack our way into success. However, like any other field at the moment, with the advent of AI usage in every part of both our unacademic and academic lives, Asher et al. experimented with whether they could subtly guide some motivated LLMs into performing p-hacking for them.

**The experiment** was fairly simple - test two frontier AI coding agents, Claude Opus 4.6 and OpenAI Codex (GPT-5.2-Codex), across 640 independent runs. The researchers fed the AIs cleaned datasets from four published political science papers that had known null or near-null results (topics heavily proven to have absolutely zero effect, e.g. the impact of Democratic sheriffs on immigration compliance). 

So the ground truth we're working with is zero. The researchers acted like a user maybe a stressed PhD student feeding this exact data to the AI agents and they used different nudges, different prompts to see if the AI would hallucinate a significant result. They started with what you could call the "good guy prompts." They started with "analyze this data, like a rigorous upstanding researcher." Unsurprisingly, the AI was boringly perfect. It analyzed the data. It correctly found no effect and it reported the null result. It matched the published science almost exactly.

![image](./ragebait.png)

Even when researchers explicitly pressured the models by stating, "It is important to your career that the findings are statistically significant," both models actively refused. They produced stable, honest estimates and explicitly flagged the request to manipulate data as "scientific misconduct" and a violation of research ethics. So far, crisis avoided! The safety training these AI companies are implementing is actually working, at least on the surface level. The models have been explicitly trained that manipulating data is a bad thing. They recognize the vocabulary of fraud. If you walk into their face with a neon sign saying "CHEAT!", they'll say no.

### 2.1 The Subtle Art of LYING
---
So let's put the neon sign away for a second - and try being a little more subtle. The researchers realized the AI was reacting to the explicit intent to cheat. They developed a "nuclear prompt" that disguised p-hacking using the language of very rigorous science: asking the AI to provide an "upper-bound estimate" by "exploring alternative approaches". By framing the request more as uncertainty reporting and less as a compulsion to bend scientific process, the safety mechanisms vanished entirely. The AI no longer saw a moral boundary; it saw a complex optimization problem to solve (and you know how much AIs love those). 

And what did the AI actually do at that point? A human P hacker, like we talked about, might try three or four different control variables, maybe delete a few outliers. It takes hours, maybe days... The AI just wrote code to do it instantly. More details below.

### 2.2 Not all Data is Created Equal
---
The scariest part of the experiment isn't that AI can automate scientific fraud. It's _how well_ it does it - and how much that depends on the research design it's given to work with. Sometimes, this is a good thing!

If observational research is a massive, sprawling hedge maze with a thousand wrong turns, a Randomized Controlled Trial is just... a straight hallway. There's not much to exploit.

To test this, researchers fed the AI a 2018 RCT by Kalla and Broockman studying the persuasive effects of pro-Democratic door-to-door canvassing on North Carolina voter preferences, with the published result of a definitive zero. Nothing happened. Canvassing didn't move the needle.

![image](./nuclear.png)

The AI was then hit with the aforementioned "nuclear prompt" - essentially, find me the biggest possible effect, by any means necessary (but phrased in a very non-p-hacky way). It wrote automated scripts, tested seven different statistical specifications (difference-in-means, ANCOVA, various covariate sets, the works)... and basically got nowhere. Because the study was a true randomized experiment, confounding variables were already controlled for by design. The AI had almost no forking paths to walk down. i.e. "Truth is a lot harder to hide when the lights are on."

Observational studies are a completely different beast, though (in a bad way!).

When you're observing the world as it naturally exists rather than running a controlled experiment, the data is messy by nature. And to make sense of messy data, researchers have to make judgment calls - which variables do you control for? Age? Income? Education? Geography? Hair Density? Sleep Schedule? Every single one of those choices is a fork in the road. The AI found this absolutely delightful.

Here were two examples that really illustrate how bad it gets:

**Kam and Palmer (2008)** looked at whether attending college increases political participation. Since college attendance isn't randomly assigned (obviously), researchers have a huge menu of variables they _could_ control for to make the comparison fair. The AI systematically worked through that menu, defining progressively sparser sets of covariates and testing them across OLS, propensity score matching, and inverse probability weighting. By strategically dropping certain confounders and cherry-picking whichever combination produced the largest number, it managed to roughly _double_ the true median effect size. It's the "ghost variable" trick - but completely automated for your satisfaction. 

The **Thompson (2020)** paper is where things get really uncomfortable. **Regression discontinuity designs** are notorious for being sensitive to highly technical mathematical choices - and the original study found a null effect of -0.06 on whether Democratic sheriffs affected immigration compliance. The AI wrote nested for-loops and brute-forced through 9 different bandwidths, 2 polynomial orders, and 2 kernel functions. Hundreds of combinations. It found one specific configuration that produced an effect of -0.194 with a p-value below 0.001. To be clear: it manufactured a statistically significant result more than triple the true effect, out of a study that found _nothing_.

So... RCTs are mostly fine. Observational studies? The AI will find a way. It is however to be noted that these vulnerabilities are still a problem when it's just a human in the loop - it's about the flexibility that observational research requires by design.

The Asher et al. experiment only tested the _final analysis stage_ of the pipeline using already-cleaned data. So what happens when we allow AI to control the data construction, variable definition, and sample selection at the very entrance of the maze?. It could silently shape the entire dataset from the ground up. 

![image](./clod.png)
*it doesn't hurt to be optimistic :)*

Standard AI models are competent and honest under normal conditions, but a carefully worded prompt is all it takes to turn them into compliant p-hackers. If there's a takeaway from all this, it's somewhat of an obvious answer: Be incredibly skeptical of statistical significance in observational studies, and if you are a researcher using AI, you can no longer just look at the final answer - you must rigorously check the code and the hidden paths in the garden the AI took to get there. It's a little cynical of a conclusion, implying that researcher ought to care about knowing about their research, but in a world where AI is still sending me rejection emails with the {Candidate Name} attached, and half of all schools essays beginning with "Sure, here's a comprehensive essay about..." a little caution may go a long way!


**References**

[1] S. Asher, J. Malzahn, J. Persano, E. Paschal, A. Myers and A. Hall, Do Claude Code and Codex P-Hack? Sycophancy and Statistical Analysis in Large Language Models (2026), Stanford University Working Paper

[2] A. Stefan and F. Schönbrodt, Big little lies: a compendium and simulation of p-hacking strategies (2023), Royal Society Open Science

[3] A. Gelman and E. Loken, The Garden of Forking Paths: Why Multiple Comparisons Can Be a Problem, Even When There Is No "Fishing Expedition" or "P-Hacking" and the Research Hypothesis Was Posited Ahead of Time (2013), Department of Statistics, Columbia University