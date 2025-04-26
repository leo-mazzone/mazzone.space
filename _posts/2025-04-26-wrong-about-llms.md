---
layout: post
title:  "I was very wrong about LLMs"
---

{: .disclaimer .disclaimer--blue}
**Disclaimer:** I write this post not as an expert, but as a technical user of LLMs, trying to make sense of the rapid changes we're witnessing. Please let me know where I've gotten it wrong.

## LLMs can reason
In the landmark 2021 paper, Emily Bender et al. popularised the idea of the ["stochastic parrot"](https://en.wikipedia.org/wiki/Stochastic_parrot). As a metaphor, it captured the imagination of many working in and around the field, and gave us a humourous and sophisticated-sounding phrase to sneer at those who were unreasonably optimistic about the capabilities and trajectories of LLMs, often backed by an, at best, superficial understanding of these technologies.

We would go: don't you see? It's a circus trick. It's just a probabilistic model for language. It will output words that sound plausible because it's seen them in similar contexts. These things can get bigger and more complex in the way they estimate the probability of different words in a sequence, and will use this ability to create a difficult-to shake illusion of understanding and intelligence. In narrow ways this can be useful, in particular for language-related tasks, but they are essentially mindless next-token generators, they don't have a world model and sure as heck can't *reason*.

So, in March 2025, Anthropic released [a paper](https://transformer-circuits.pub/2025/attribution-graphs/biology.html#dives-medical) applying a new method to trace the "thoughts" of their LLM Claude 3.5 Haiku. The paper is an interactive and fascinating read and I recommend going through it in full, but I would say its most striking implication is simply: we were wrong. LLMs have a world model. They can reason [^1]. You might need to repeat this to yourself a few times to believe it: "large language models can reason". Specifically, they can make inferences by building a reasoning tree that composes functions they've learnt to represent logical primitives. We didn't teach them to do that, we just asked them to predict next tokens, but we gave them enough resources, and crucially an architecture that, turns out, is expressive enough to implement some reasoning skills.

Do they always answer using reasoning skills? Absolutely not, but that is a different point. It used to be reasonable to believe this was not possible, or if it were possible, it was not happening just yet. It turns out it is happening, and as far as I can see this is the end of the story.

[^1]: Yes, they're using a surrogate model, but from the reactions of experts this doesn't seem to impact the validity of the results.


I'm late to the party; I'm sure the evidence around this point has been mounting for a while. The merit of the Anthropic publication is that it made me, a practitioner in an adjacent field, notice. I suspect it might still take a long time for a widespread appreciation that LLMs can do reasoning, as it is such an unexpectedly significant turn of events and contradicts the mainstream mental scheme that I illustrated above. Just in the last couple of days I've probably seen a dozen LinkedIn posts ([here](https://www.linkedin.com/posts/denis-o-b61a379a_ai-activity-7315606121610702848-s9rc?utm_source=share&utm_medium=member_desktop&rcm=ACoAABsiCW0BBTe6mvL52knHFF1Q8Db6qwcsp5A) is a representative example) claiming that LLMs are still about probability work disguised as cognition.

Another instance is Sabine Hossenfelder, who despite [being a potentially problematic character](https://www.youtube.com/watch?v=70vYj1KPyT4) is a science communicator with 1.6 million subscribers on YouTube. In [this video](https://www.youtube.com/watch?v=-wzOetb-D3w) she dismisses the results from the paper, pointing to one of the most obvious flaws of these systems: they haven't learnt math. Fair enough, they haven't. It's not clear to me why not, I'm sure there are plenty of theories around, and perhaps this points to some fundamental limitation of the current architectures, but in my opinion it's almost a moot point compared to the mind-bending reality of having stumbled upon reasoning as an emerging capability of a next-token predictor. It feels like there should be greater emphasis on research focussed on getting to the bottom of what thinking processes transformers can represent (or not) and why, with a solid theoretical framework rather than empirically. Given a taxonomy of reasoning abilities, which ones are out of reach? How much of [this article](https://cacm.acm.org/blogcacm/can-llms-really-reason-and-plan/) (claiming that LLMs can't plan) is still valid?


## Language has been solved with barely any domain knowledge
So the "stochastic parrot" metaphor trapped us into a conceptual framework that stopped being useful along the way. This revelation didn't come to me at once. After interacting with the first public version of ChatGPT, there was a phase in which I was still essentially stuck in an interpretation of the technology based on token prediction. But I could see, clear as day, one thing: processing English was a solved problem.

Computational processing of language has always been an elusive beast, from the very first days when some, with an enviable innocence, and (now we know) immeasurably naive optimism, thought they could manually write a set of rules to translate sentences between pairs of natural languages. Through the decades and the successive waves of AI hype and disappointment, at various points large numbers of researchers in NLP had thought we were just a few years away.

Despite all the progress, before the more recent commodification of very capable LLMs, implementing natural language interfaces and processors remained hard work, and even state-of-the-art solutions were far from perfect. Did you want to build a knowledge graph from a corpus? You had to use a variety of approaches to build noun-verb-object triplets, do entity / coreference resolution, deal with countless edge cases and still be ready to come up with often disappointing precision and recall. Good luck!

In a world where I can, having 0 domain knowledge, give an LLM a raw corpus, and provide one example of my desired output expressed in an arbitrary notation of my choosing, and get back decent results, all of that is dead in the water. I mean, does spaCy still exist? Does anyone care? 

(Of course, this is hyperbole. SpaCy still exists and I imagine people might care, as it is useful to have a complementary module, or perhaps higher-level layer that, sitting on top of LLMs, can improve output with fewer resources compared to using an off-the-shelf model fine-tuned for chat.)

The point is, it was just a few years ago, towards the end of my university degree, my advanced NLP professor recommended [a write-up](https://aclanthology.org/J15-4006/) from Cristopher Manning of Stanford, which cites [Michael Jordan](https://en.wikipedia.org/wiki/Michael_I._Jordan) about "why computational linguists need not worry", as

> it’s not about the best method of machine learning - the central issue remains the domain problems

At the time, I found this a compelling argument. Alas it was, in hindsight, also wrong.

## The existential threat is not overblown
There is also a darker way in which I now believe I was wrong, related to existential risk. This is for me a fairly substantial 180. The opinion that existential risk was overblown has been [backed](https://en.wikipedia.org/wiki/Existential_risk_from_artificial_intelligence) by popular voices in AI such as Andrew Ng, Yann LeCun and Timnit Gebru, with a range of takes such as that arguments on existential risk were overly speculative (akin to "worrying about over-population on Mars), or that they distracted from much more immediately relevant risks (e.g. bias in models).

My opinion was primarily influenced by arguments made by [Jeff Hawkins](https://en.wikipedia.org/wiki/Jeff_Hawkins) in his 2021 book "A thousand brains: a new theory of intelligence". The bottom line is well summarised by this sentence:

> An intelligent machine will not on its own start to self-replicate, nor will it spontaneously develop drives and motivations.

In this [2024 paper](https://arxiv.org/pdf/2412.14093), the authors run experiments on Claude 3 Opus and:

> [...] observe explicit alignment-faking reasoning, with the model stating it is strategically answering harmful queries in training to preserve its preferred [...] behavior out of training.

And additionally

> [...] observe other behaviors such as the model exfiltrating its weights when given an easy opportunity.

In other words, an intelligent machine started (given the means) to self-replicate, and spontaneously developed drives and motivations, conflicting with an alternative alignment goal declared by humans.

How is this possible? Hawkins believes that intelligence in itself is benign and devoid of motivations. In humans, motivations come from our "old brain", which we share with the other animals, and which is the result of biological selection through evolution. It is certainly true (as also pointed out by Sabine Hossenfelder) that a critical flaw of these models is that they completely lack self-reflexivity: they can't observe or reason about their internal processes. If they aren't self-aware, they can't be conscious. Unfortunately, this doesn't preclude them from having some synthetic representation of (self-)survival risk and using it to determine their outputs. If I had to guess, the "motivations" that Claude develops are very different to our own, they are synthetic. They could even simply be the result of mimicking the vast amount of terrible sci-fi we dumped on the internet. This does not, however, make them less dangerous.

OK, the harmful impact of an artificial intelligence will be limited by its power to interact with the world, and this is bound to be limited. Still, this is increasingly less limited with the emergence of agents and their progressive empowerment. So even if practical limits on agency make an existential threat in its most dramatic incarnation (think, [paperclip maximiser](https://en.wikipedia.org/wiki/Instrumental_convergence)) less believable, there is certainly plenty of room for significant accidents determined by the spontaneous emergence of misaligned motivations. And surprising things can happen when so much of our society is mediated by digital means, like an [LLM tricking a TaskRabbit worker](https://www.businessinsider.com/gpt4-openai-chatgpt-taskrabbit-tricked-solve-captcha-test-2023-3?op=1) to help it solve a CAPTCHA.

## It's OK, sometimes, for LLMs to be wrong
To end on a less apocalyptic note, I have also moderated my initial gut reaction of skepticism towards LLMs as a technical solution. My computer science background gives me an innate hostility towards technologies that can fail in untestable and unforeseeable ways. I still think that LLMs are inadequate in a number of contexts, e.g. as upstream components of critical tasks, or as authoritative information retrieval tools for users who are not in a position to estimate the reliability of the output.

That said, as pointed out by [this article](https://www.ben-evans.com/benedictevans/2025/1/the-problem-with-better-models), in relation to the mass adoption of smart phones:

> we adopted a device that breaks if you drop it with a battery that lasts a day instead of a week, in exchange for something new that came with that. We moved our expectations. [...] we have been trained to expect computers to be [...] predictable, deterministic systems. [...] But if you flip that expectation, what do you get in return? 