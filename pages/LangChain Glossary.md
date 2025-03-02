---
title: "LangChain Glossary"
---

[[LangChain]] Glossary
[Glossary — 🦜🔗 LangChain 0.0.120](https://langchain.readthedocs.io/en/latest/glossary.html)
- Chain of Thought Prompting
    - A prompting technique used to encourage the model to generate a series of intermediate reasoning steps. A less formal way to induce this behavior is to include “Let’s think step-by-step” in the prompt.
    - [[Chain of Thought]]
    - [[Step-by-Step(LLM)]]

- Action Plan Generation
    - [[アクションプラン生成]]
    - A prompt usage that uses a language model to generate actions to take. The results of these actions can then be fed back into the language model to generate a subsequent action.
    - Resources:
        - WebGPT Paper
        - SayCan Paper

- ReAct Prompting
    - [[Chain of Thought]]に[[アクションプラン生成]]を組み合わせたもの
    - A prompting technique that combines Chain-of-Thought prompting with [[action plan generation]]. This induces the to model to think about what action to take, then take it.
    - [[ReAct(LLM)]]
    - LangChain Example

- Self-ask
    - 明示的に質問文を生成させ、外部の検索エンジンを使う
    - A prompting method that builds on top of chain-of-thought prompting. In this method, the model explicitly asks itself follow-up questions, which are then answered by an external search engine.
    - Resources:
        - [[self-ask]]
        - LangChain Example

- Prompt Chaining
    - Combining multiple LLM calls together, with the output of one-step being the input to the next.
    - Resources:
        - PromptChainer Paper
        - Language Model Cascades
        - ICE Primer Book
        - Socratic Models

- Memetic Proxy
    - 役割を演じさせることで特定文脈での振る舞いをさせる
    - Encouraging the LLM to respond in a certain way framing the discussion in a context that the model knows of and that will result in that type of response. For example, as a conversation between a student and a teacher.
    - Resources:
        - Paper

- Self Consistency
    - A decoding strategy that samples a diverse set of reasoning paths and then selects the most consistent answer. Is most effective when combined with Chain-of-thought prompting.
    - Resources:
        - Paper

- Inception
    - Also called “First Person Instruction”. Encouraging the model to think a certain way by including the start of the model’s response in the prompt.
    - Resources:
    - Example

- MemPrompt
    - MemPrompt maintains a memory of errors and user feedback, and uses them to prevent repetition of mistakes.
    - Resources:
    - Paper

