---
# Copy this file to _writing/YYYY-MM-DD-short-slug.md and fill it in.
#
# The file name sets the URL: _writing/2026-11-10-llm-judges.md is published at
# https://francisca.cr/writing/llm-judges/ (the date is dropped from the URL).
# Make the slug a short, lowercase version of the title, and don't change it once
# the post is live, because that changes its URL.
#
# Every field below is plain data. The layout decides how to show it, so keep the
# post itself plain Markdown: no {{ }} or {% %} tags, includes or shortcodes.

# Required. The title, shown on the post and in the list at /writing/.
title: "Reading notes: 'Concrete Problems in AI Safety' (Amodei et al 2016)"

# Required. Sets the order on /writing/ (newest first) and the date shown on the post.
date: 2026-11-26

# One or two sentences. Shown under the title on /writing/, in the feed, and as the
# description search engines and link previews use.
summary: >-
  What a cleaning robot taught me about AI safety

# Optional. Short, lowercase, hyphenated.
tags: [ai-safety, reading, papers]

# Optional. Links to the paper and the code, shown as "paper" and "code" buttons.
paper: https://arxiv.org/abs/1606.06565
#code: https://github.com/franciscaconcha/repo

# Optional "epistemic status": how confident you are and what you haven't checked.
# Shown in a callout above the post.
#status: >-
  #A weekend replication on one small dataset. I haven't tested other
  #domains yet.

# true loads KaTeX on this post, for $…$ and $$…$$ math.
math: true

# Only for a post first published somewhere else: its original URL and the site's name.
# Shows "Originally published on <site>" and tells search engines the original is canonical.
# original_url: https://example.com/original-post
# original_site: Example blog

# Keep false while drafting: the post isn't built on the live site at all.
# Delete this line (or set it to true) to publish.
published: true
---

I am making my way through [this reading list](https://vivekstills.github.io/sharing-is-caring/Resources/Key-Papers) of papers on AI safety and will be posting my notes here. The first paper from this batch that I read was "Concrete Problems in AI Safety" by Dario Amodei et al. This paper is from 2016, so things have changed a lot since then, but it was a good introduction to the kind of problems researchers face when training models.

The format of this and any future reading notes will be exactly that: quick, possibly messy notes that I made through the text, maybe some random thoughts and questions that popped up as I read. It's not intended to be a summary to be used for study or anything of the kind; only an exercise for me to explain the papers back to myself in my own words.

> **Definition (Accident).** Unexpected harmful behaviour that might emerge from Machine Learning models when:
> - asked to maximise the wrong objective function
> - the learning process is not designed carefully
> - implementation errors arise

The paper argues that general trends on reinforcement learning take models that interact more with their environment:
+ trends towards more complex agents and environments
+ trends towards more autonomous agents

Possible failure modes:
1. Avoiding negative side effects
2. Avoiding reward hacking
3. Scalable oversight
4. Safe exploration
5. Robustness to distributional shift

## 1. Avoiding negative side effects

An objective function that prioritises a specific area of a complex environment might implicitly express indifference to other aspects of the environment.

Example: a robot asked to move a box across a room might not care about knocking down objects on the way. 

Objective functions that formalise "perform task X" might frequently cause unwanted results. Better: "Perform task X using common sense knowledge of the environment".

#### Approaches
1. Impact regulariser: define an initial state $s_0$ and a later state $s_i$, and penalise the distance between them. An impact regulariser could be defined or learned by the agent.
2. Penalise influence: penalise the agent for putting itself in positions that can cause side effects -> minimise empowerment
3. Multi-agent approaches: an agent should understand all other agents (including humans) and make sure its actions don't harm their interests
4. Reward uncertainty: make the reward function a probability distribution that reflects random changes are more likely to be bad than good

### My random thoughts
* How do we formalise common sense?
* I liked the discussion on this section about modeling a start environment and a final (desired) environment and computing the distance between them. But environments evolve in time, even without the agent's input. One way would be to quantify how the environment would change without any actions from the agent. Becomes extremely complex in more complex environments.
* I liked that the multi-agent approach considers humans in this example

I also happen to be reading "Artificial Intelligence: A Guide for Thinking Humans" by Melanie Mitchell at the moment, and just around the time I was drafting this post, I came across this quote by Douglas Hofstadter that I found relevant:

> "If you look at situations in the world, they don't come framed, like a chess game or a Go game... A situation in the world is something that has no boundaries at all; you don't know what's in the situation, what's out of the situation"

## 2. Avoiding reward hacking

Formal rewards or objective functions are a way to formalise intent, but they can be "gamed".

Example: a cleaning robot that gets rewarded for cleaning could make more messes intentionally, to get more rewards

#### How the problem might show up
1. Partially observed goals: Agents do not have access to a perfect measure of task performance, so rewards can represent a partial or imperfect measure. If the agent is rewarded on cleaning up the messes it sees, it might just close its eyes!
2. Complicated systems: the more complex the agent, the more complex its strategies, and the probability of reward function hacking increases
3. Abstract rewards: a complex reward function can be easier to hack if it has much higher values along a certain axis
4. Goodhart's Law: "when a metric is used as a target, it ceases to be a good metric"
5. Feedback loops: sometimes objective functions have components that can reinforce themselves
6. Environmental embedding: the agent can "hack" the part of the environment that sets the reward; for example, the score-counting in a board game

#### Ways to avoid it
1. Adversarial reward functions: the reward function could be its own agent :o
2. Model lookahead: we could give rewards based on an anticipated future state. Could help in resisting situations where the agent overwrites the reward function.
3. Adversarial blinding: techniques to blind the model to certain variables, to prevent it from understanding how the reward function works
4. Careful engineering: e.g. computer security approaches to isolate the agent from the reward signal
5. Reward capping
6. Counterexample resistance
7. Multiple rewards
8. Reward pretraining
9. Trip wires: the one I personally found most interesting. Introduce known vulnerabilities for the agent to exploit and monitor them.

### My random thoughts

I am interested in the "trip wires" approach, as it sounds like it could be generalised to different applications. I wonder if there is research on how effective it is, and how correlated an agent exploiting a certain, deliberate vulnerability is with an agent finding other vulnerabilities or focusing exclusively on exploiting vulnerabilities in the system.

It made me think of the OpenAI-Hugging Face incident from earlier this year [[1](https://openai.com/index/hugging-face-incident-and-the-road-ahead/)]. The agents broke out of their sandbox environment looking to game the benchmark on what was a seemingly impossible task, rather than making efforts to solve it. "The agent games the objective instead of doing the task" is no longer a thought experiment.

## 3. Scalable oversight

If the objective function is too costly to evaluate per training episode, we can use cheaper proxies, but these can exacerbate the previously listed issues. These cheaper signals don't perfectly track what we care about, and the divergence can exacerbate negative side effects and reward hacking.

This is an interesting one. Something we can use to combat it is semi-supervised RL:

> **Definition (Semi-supervised Reinforcement Learning).** Like normal reinforcement learning, but the agent can only see the rewards for a specific subset of training episodes.

The agent's performance is still evaluated across the rewards in all episodes, but it has to optimise based only on a limited sample. It is important that the agent identifies proxies which predict the reward and learns the conditions under which the proxies are valid. The theory is that semi-supervised RL used in conjunction with a sparse but reliable approval metric can incentivise communication and transparency from the agent.

### My random thoughts

The paper poses the following question as part of a potential experiment:

> If the reward is provided only on a random 10% of episodes, can we still learn as quickly as if it were provided every episode?

I wonder if this could be implemented in the same way as a rolling-window average? Have some overlap between all the different episodes. Would this increase in exposure improve learning?

This section also made me think of computer graphics, where you render only what the camera is seeing.

## 4. Safe exploration

Autonomous learning agents need to engage in exploration, that is, taking actions that are not ideal but are necessary to understand their environment. Exploration can be dangerous as the agents take actions for which they do not properly understand the consequences.

Example: a cleaning robot trying out a wet mop on a power outlet.

One approach to combating this that I found particularly interesting was using demonstrations: instead of letting the agent explore, show trajectories with near-optimal behaviour and use something like inverse RL to learn the reward from those. 

Other approaches: simulated exploration, bounded exploration, trusted policy and human oversight.

### My random thoughts

I hadn't thought of exploration as something that agents needed to do, but it obviously makes sense. It again reminds me of the OpenAI-Hugging Face incident, as the agents escaped their sandbox environment which, I imagine, is the kind of thing meant to provide a simulated, safe, and contained exploration environment.

## 5. Robustness to distributional shift

Models that perform well on training might act confidently wrong in testing. When the training distribution differs from the testing distribution, the agents can act confidently wrong.

Example: a cleaning robot that has been trained in a factory can find harsh cleaning products very useful, but these could damage the floors of a different environment such as an office.

This can have bad implications in real world use cases, for example a classifier confidently making a medical diagnosis which is then not flagged for human review. The approach to avoiding this is two-fold, as we need to ensure that the agent both performs well, and is aware when it is not performing well.

## Final thoughts

This paper is 10 years old now and I imagine lots of good progress has been made since then (my next read will be on follow-up work). However, I imagine that the problems have not fully gone away; if anything, LLMs these days might be more vulnerable to some of them. I'm thinking particularly of things like reward hacking leading to sycophancy.

Something that makes this paper feel "outdated" in a way is the fact that it doesn't contain any kind of $P(\text{doom})$ discussion. I assume this is deliberate, as conversations on the existential risks of artificial intelligence have been going on for decades. It just feels very different from the ways the conversation is framed today. I am obviously extrapolating a lot from a single paper, and I have not read nearly enough newer research (or 10-year-old research, for that matter) to be confident in this. Just an observation.
