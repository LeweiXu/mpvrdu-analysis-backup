## Turn 1 — document page 3 (rank 1 of 10)

The current page describes a system called QACHECK, which consists of five key modules: Verifier $\mathcal{D}$, Question Generator $\mathcal{Q}$, Question-Answering Model $\mathcal{A}$, Validator $\mathcal{V}$, and Reasoner $\mathcal{R}$. The text states that these five modules are implemented using large language models (LLMs) such as InstructGPT and GPT-4. Specifically, the Claim Verifier, Question Generator, and Question Answering Model are explicitly built based on InstructGPT. The Validator and Reasoner are also part of the system and are implied to be implemented with LLMs, as the text describes the entire system as leveraging LLMs for in-context learning.

## Turn 2 — document page 7 (rank 2 of 10)

## Limitations
The text states that "several modules of our QACHECK currently utilize external API-based large language models, such as InstructGPT." This confirms that multiple modules rely on LLMs, but does not specify the exact number. The page does not contradict or add new information about the count of LLM-backed modules.

## Turn 3 — document page 2 (rank 3 of 10)

The current page describes the QACHECK system, which is composed of five principal modules: 1) a claim verifier, 2) a question generator, 3) a question-answering module, 4) a QA validator, and 5) a reasoner. The page states that the system is designed to manage a reasoning process by guiding the model to self-generate questions and answer them, and that it outputs a final veracity label. It also mentions that the system offers adaptability, allowing users to customize each module by integrating with different models, such as retriever–reader, FLAN-T5, or GPT3-based models. However, this page does not specify which of these five modules are implemented with Large Language Models (LLMs) as their backbone.

## Turn 4 — document page 4 (rank 4 of 10)

- The page describes three implementations of the Question Answering (QA) module: Retriever–Reader, FLAN-T5, and GPT Reciter–Reader.
- The Retriever–Reader uses a BM25-based retriever and a RoBERTa-large reader, which are not LLMs.
- The FLAN-T5 is described as a Seq2Seq model pretrained on 1.8K tasks with instruction tuning, which is an LLM.
- The GPT Reciter–Reader uses InstructGPT, which is explicitly identified as an LLM.
- The QA Validator module is implemented by prompting InstructGPT, which is an LLM.
- The page does not explicitly state that the Claim Verifier or Question Generator modules use LLMs, but previous pages (Turn 1) state that these modules are implemented with LLMs.

## Turn 5 — document page 1 (rank 5 of 10)

This page introduces the QACHECK system and its five key modules: claim verifier, question generator, question-answering module, QA validator, and reasoner. It describes the system's purpose and provides an example of question-guided reasoning. However, it does not specify which of these modules are implemented with Large Language Models (LLMs) as their backbone. The page does not contradict or add new information about the count of LLM-backed modules.

## Turn 6 — document page 6 (rank 6 of 10)

The current page discusses the QACHECK system and its evaluation results, mentioning that users can select between three different QA models (Retriever–Reader, FLAN-T5, and GPT Reciter–Reader) in the demo interface. It also states that the system leverages in-context learning, document retrieval, and question-answering techniques. However, this page does not provide any new information about which specific modules of the system are implemented with Large Language Models (LLMs) as their backbone, nor does it contradict or add to the count established in previous pages.
