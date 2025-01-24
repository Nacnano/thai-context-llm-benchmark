# Prompt

I want to correct questions generated from the Thai GQA question engine. They are still wrong. Please correct the questions based on the contexts given.
Object, Attribute, Relation, Target, Question Template?Answer Template

Also, after correcting each question, please grade how good or bad your correction is based on these 5 criteria to number score (1 to 5).

Grammatical - Correct grammar?
Relevance - Question related to the answer?
Clarity - Clear understanding? (not ambiguous)
Specificity - Has only one correct answer?
Prettiness - Easy to read by human?

Score criteria:
5 - Perfect
4 - Some room for improvement
3 - So so
2 - Bad
1 - Unacceptable

Here is the input csv with format
Object, Attribute, Relation, Target, Question Template?Answer Template

Please output in csv format with
Original Question,Corrected Question,Grammatical,Relevance,Clarity,Specificity,Prettiness,Average Score,Reason for Corrections
