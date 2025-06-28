---
layout: homepage
---
## About Me
In my darkest hour, AI lit the way—showing me how once-impossible ideas could take shape, and revealing its greatest power: helping us make better decisions amid complexity and uncertainty.That moment changed how I see the world—and what I believe AI should really be about.

To realize that vision, reliability must come first. My initial focus is addressing hallucinations—those moments when AI speaks with confidence but delivers falsehoods. I’m working on tools that help people make smarter decisions—in law, finance, and other fields where mistakes can be costly.My long-term goal is far more ambitious: I want AI to move beyond linear generation—to reason, adapt, and connect ideas across complex contexts, until it can truly think, not just generate.

If each of us has one mission in life, then mine is clear: to devote my life to building the future of AI.

---
## Research Interests | Building a Hallucination-Resistant Architecture for LLMs
While large language models (LLMs) have made significant strides in generating fluent text, hallucination remains a critical issue in high-stakes applications—where the absence of factual grounding, logical inconsistencies, and unverifiable outputs undermine reliability. This exposes fundamental flaws in inference control, cognitive feedback, and knowledge alignment.

To address this challenge, I propose a three-tiered, progressive hallucination-resistant framework, centered around a Planning-Reflection-Evidence feedback loop, focusing on the following three key components: 
SFPL(Structured Feedback Planning Layer): By implementing pre-generation reasoning plans, we replace free-form generation with precise control over the initial steps, mitigating generation bias;
REFLEXION: This introduces recursive self-feedback and cognitive evaluation, enabling dynamic correction of cognitive errors during the generation process; 
CAT(Citation-Aware Generation): This facilitates word-level fact referencing, ensuring the generated content is bound to external knowledge, thus enhancing verifiability.

This architecture significantly improves the reliability of LLMs, advancing them from "statistical generation" to "causal-reasoning-driven cognitive systems," providing both a theoretical foundation and practical solutions for hallucination mitigation. It supports the trusted deployment, accountability, and verifiability of large models in high-risk scenarios.

{% include_relative _includes/publications.md %}
{% include_relative _includes/services.md %}
