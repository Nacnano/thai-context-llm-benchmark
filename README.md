# Individual Study

## Implementing GQA Question engine for Thai language

### [Final Presentation Slide](https://docs.google.com/presentation/d/1aU7nGrlz9hOWeAyrhA-63w8jmNGYY1dNA_LiVluOIXI/edit#slide=id.g3211a13ede1_0_171)

### References

- https://paperswithcode.com/paper/gqa-a-new-dataset-for-compositional-question

### Updates

- 13/9/2024: Find how GQA datasets are generated (from the paper), convert them to Thai's context and translate them again
- 11/10/2024: Try implement the GQA Question Engine with Thai Language
- 18/10/2024: Got stuck with the classses (objects, attributes, relation). Try playing with more classes (aside from colors). Example: https://gemini.google.com/app/0796b71c54fd5067
- 25/10/2024: Successful corrected the generated questions using Gemini. Try implementing Thai questions from Scene Graph with Thai words (manually add คำไทยๆ หรือ context ไทยๆ) and then generate with the current question engine method.
- 1/11/2024: Add question templates in the prompts and add pipelines for evaluation (Check the question-answer correlation, Check the check the correct answer, Check how beautiful it is?)
- 8/11/2024: Check the criterias with some ground truth (pure bruteforce for every score) then use some stat model to evaluate the model accuracy. Maybe intentionally add wrong result to see whether it can detect the wrong ones
- 15/11/2024: Used paired t-test (got insignificant for all criterias) and RMSE (around 20%) to evaluate the generated questions and found out that the LLMs (Gemini, ChatGPT, Claude) can't detect context-based criterias. Maybe use Recall to specify just the incorrected questions. Maybe use in-prompt context to tell the model "these are the exmaples of the wrongs" while grading

### Advisor

- Assoc. Ekapol Chuangsuwanich
