## Turn 1 — document page 5 (rank 1 of 20)

Figure 4. The comparison between MMMU and other existing benchmarks. MMMU excels in both its breadth to cover a wide range of disciplines and its depth to test LMMs' reasoning abilities. In the image format, V means visual input, OC means optical characters, MC means multi-choice. Repurposed means the benchmark is a compilation of prior datasets.

The text below the figure states: "From the breadth perspective, the prior benchmarks are heavily focused on daily knowledge and common sense. The covered image format is also limited. Our benchmark aims to cover college-level knowledge with 30 image formats including diagrams, tables, charts, chemical structures, photos, paintings, geometric shapes, music sheets, medical images, etc. In the depth aspect, the previous benchmarks normally require commonsense knowledge or simple physical or temporal reasoning. In contrast, our benchmark requires deliberate reasoning with college-level subject knowledge."

The table lists datasets including VQA, GQA, VisWiz, TextVQA, OKVQA, SEED, MMBench, MM-Vet, ScienceQA, and MMMU, with their sizes, image formats, sources, and answer types.

## Turn 2 — document page 1 (rank 2 of 20)

Figure 1 on this page provides an overview of the MMMU dataset, highlighting its four key challenges. The first challenge is "comprehensiveness," which states that MMMU presents 11.5K college-level problems across six broad disciplines and 30 college subjects. This is presented as a core feature of the benchmark. The figure also lists "Heterogeneous Image Types" and "Interleaved Text and Images" as other challenges, but the "comprehensiveness" challenge is explicitly tied to the breadth of disciplines and subjects covered.

## Turn 3 — document page 2 (rank 3 of 20)

- The page contains Figure 2, which shows sampled MMMU examples from each of the six disciplines: Art & Design, Business, Science, Health & Medicine, Humanities & Social Science, and Tech & Engineering.
- Each example includes a question, image, subject, subfield, image type, and difficulty level, demonstrating the breadth of knowledge covered.
- The text explains that MMMU is designed to cover college-level knowledge across six disciplines and 30 subjects, aiming for breadth.
- The text contrasts MMMU with ScienceQA, noting that while ScienceQA covers diverse disciplines (breadth), its questions are at elementary to middle school level, lacking the depth needed for Expert AGI benchmarking.
- The text states that MMMU consists of 11.5K questions covering 30 diverse subjects and 183 subfields, meeting the breadth goal.

## Turn 4 — document page 3 (rank 4 of 20)

Figure 3 on this page visually breaks down the 30 subjects and 183 subfields across the six broad disciplines of MMMU. The breakdown shows:
- Art & Design (11%): Includes Art, Design, Music, Art History.
- Business (14%): Includes Accounting, Finance, Management, Marketing.
- Science (23%): Includes Biology, Chemistry, Physics, Mathematics, Geography.
- Health & Medicine (17%): Includes Basic Med. Sci., Clinical Med., Diagnostics, Pharmacy, Public Health, Public Health.
- Humanities & Social Science (9%): Includes History, Literature, Psychology, Sociology.
- Tech & Engineering (26%): Includes Agriculture, Architecture, Computer Science, Electronics, Energy Power, Materials, Mechanical Eng.

The text below the figure reiterates that MMMU contains 11.5K multimodal questions covering six broad disciplines, 30 subjects, and 183 subfields. It also states that MMMU is designed to cover college-level knowledge across these six disciplines and 30 subjects, aiming for breadth.

## Turn 5 — document page 7 (rank 5 of 20)

Figure 5 and Table 3 on this page analyze model performance across different image types and difficulty levels. The text states that models perform relatively better in disciplines like Art & Design and Humanities & Social Sciences (where images are more "natural" and reasoning is less complex) and worse in Science, Health & Medicine, and Technology & Engineering (which require intricate perception and complex reasoning). The text also notes that for less common image types like Geometric shapes, Music sheets, and Chemical structures, all models obtain very low scores, indicating poor generalization. Table 3 shows GPT-4V's overall accuracy is 55.7%, significantly higher than open-source models.

## Turn 6 — document page 4 (rank 6 of 20)

Table 1 on this page provides key statistics of the MMMU benchmark, including:
- Total Questions: 11,550
- Total Disciplines/Subjects/Subfields: 6/30/1830
- Image Types: 30
- Dev:Validation:Test split: 150:900:10500
- Difficulties (Easy: Medium: Hard): 28%:45%:27%
- Multiple-choice Questions: 10,861 (94.03%)
- Open Questions: 689 (5.97%)
- Questions with an Explanation: 2,035 (17.62%)
- Image in the Question: 11,264 (97.52%)
- Images at the beginning: 2,006 (17.81%)
- Images in the middle: 4,159 (36.92%)
- Images at the end: 5,679 (50.42%)
- Image in Options: 389 (3.37%)
- Example with Multiple Images: 854 (7.39%)
- Average question length: 59.33
- Average option length: 9.17
- Average explanation length: 107.92

The text confirms MMMU covers 30 subjects across 6 disciplines: Art, Business, Health & Medicine, Science, Humanities & Social Science, and Tech & Engineering. It is designed to measure perception, knowledge, and reasoning, and to evaluate models' ability to apply reasoning with subject-specific knowledge.
