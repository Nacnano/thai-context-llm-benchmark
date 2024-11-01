# Individual Study

## Implementing GQA Question engine for Thai language

Setup

1. Download Scene Graph data from the [GQA Website](https://cs.stanford.edu/people/dorarad/gqa/download.html) and move it into `data/sceneGraphs` folder

### References

- https://paperswithcode.com/paper/gqa-a-new-dataset-for-compositional-question

### Updates

- 13/9/2024: Find how GQA datasets are generated (from the paper), convert them to Thai's context and translate them again
- 11/10/2024: Try implement the GQA Question Engine with Thai Language
- 18/10/2024: Got stuck with the classses (objects, attributes, relation). Try playing with more classes (aside from colors). Example: https://gemini.google.com/app/0796b71c54fd5067
- 25/10/2024: Successful corrected the generated questions using Gemini. Try implementing Thai questions from Scene Graph with Thai words (manually add คำไทยๆ หรือ context ไทยๆ) and then generate with the current question engine method.
- 1/11/2024: Add question templates in the prompts and add pipelines for evaluation (Check the question-answer correlation, Check the check the correct answer, Check how beautiful it is?)
