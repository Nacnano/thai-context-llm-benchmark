# Individual Study

## Implementing GQA Question engine for Thai language

### [Final Presentation Slide](https://docs.google.com/presentation/d/1aU7nGrlz9hOWeAyrhA-63w8jmNGYY1dNA_LiVluOIXI/edit#slide=id.g3211a13ede1_0_171)

### References

- https://paperswithcode.com/paper/gqa-a-new-dataset-for-compositional-question

### Advisor

- Assoc. Ekapol Chuangsuwanich

### Reports

- [Semester 1 report](https://docs.google.com/document/d/13lc5IbdQh5jjwDDPc_1fTkfclUWYRmRs9VRCPYoRFsc/edit?usp=sharing)
- [Semester 2 report](https://docs.google.com/document/d/1orgQmQnmjxz6QXle6dZQsBUTEgMlME6XUlAAQIvALYE/edit?tab=t.0)

### Updates

#### Year 3 semester 1

- 13/9/2024: Find how GQA datasets are generated (from the paper), convert them to Thai's context and translate them again
- 11/10/2024: Try implement the GQA Question Engine with Thai Language
- 18/10/2024: Got stuck with the classses (objects, attributes, relation). Try playing with more classes (aside from colors). Example: https://gemini.google.com/app/0796b71c54fd5067
- 25/10/2024: Successful corrected the generated questions using Gemini. Try implementing Thai questions from Scene Graph with Thai words (manually add คำไทยๆ หรือ context ไทยๆ) and then generate with the current question engine method.
- 1/11/2024: Add question templates in the prompts and add pipelines for evaluation (Check the question-answer correlation, Check the check the correct answer, Check how beautiful it is?)
- 8/11/2024: Check the criterias with some ground truth (pure bruteforce for every score) then use some stat model to evaluate the model accuracy. Maybe intentionally add wrong result to see whether it can detect the wrong ones
- 15/11/2024: Used paired t-test (got insignificant for all criterias) and RMSE (around 20%) to evaluate the generated questions and found out that the LLMs (Gemini, ChatGPT, Claude) can't detect context-based criterias. Maybe use Recall to specify just the incorrected questions. Maybe use in-prompt context to tell the model "these are the exmaples of the wrongs" while grading

#### Year 3 Semester 2

- 15/1/2025: Try adding the in context prompt and split the question input into mini batch (10 questions per batch). Not really have any progress.

- 24/1/2025:

  - Done: Finish correction and grading. Some of the grading and correction are still weird maybe because of the context parse in (bad reproducibility, criteria, memory, LLMs forgets very long context). Aj. Ekapol approved the results.
  - TODO: Read SEA-VQA paper to implement the Thai GQA question set and try the implementation

- 31/1/2025:

  - Done: Review SEA-VQA paper. Got that some generated questions are not that accurate
  - TODO: implement some automatic segmentation on Thai-Cultural image (SAM, SAM2, etc.), read more about the visual genome paper

- 21/2/2025:

  - Done: Read visual genome paper, designed framework for image annotation using tools (VIA, Bounding Box, etc.), combined the annotations (object, attribute, relationship, region, QA pair, canonicalization)
  - TODO: Try generating relationships between objects using LLMs (just to test how good it is)

- 14/3/2025:

  - Done : Generated image scene graphs from LLMs
    - GPT 4o : weird attributes (use verb as atrributes)
    - Sonnet 3.7 : detailed attributes (adjectives) and relations
    - Gemini 2.0 Flash : no additional attribute, too simple relations
    - Good overall positioning (both position and size)
  - TODO :
    - Generate Thai image scene graph with text enrichment using SEA VL (https://huggingface.co/datasets/SEACrowd/sea-vl_crowdsourced)
    - Plot the bounding box from the image scene graph data (+ maybe try scaling a bit)

- 21/3/2025:

  - Done : Generated various data using the Thai language.
    - Attempted "more in detail" reply => Got more detail but hallucinate after too many tries
    - Gemini is better than Claude and GPT-4o but all still fail in some contexts
    - Context enrichments from SEA-VL are useless in most cases but helpful in some very niche photos (very few)
  - TODO :
    - Implement pipeline for generating image scene graphs from list of images
    - Implement pipeline for generating instructions
    - Plot bounding box from generated image scene graph

- 28/3/2025: Earthquake (No update)

- 4/4/2025:
  - Done :
    - Plotted the bounding boxes from the generated image scene graph. The result is not accurate at all
    - Tried implementing the pipeline for generating image scene graphs from plain images (use gemini api)
  - TODO :
    - Use image segmentation (ex. SAM) for segmenting the image before generating the image scene graph (because using the bounding box from the generated image scene graph is inaccurate)
    - Implement the rest of the automation pipeline from the Photo to the Question
- 11/4/2025:
  - Done:
    - Use SAM for finding segmentation for the bounding boxes of an image. The result is not accurate.
  - TODO:
    - Use some YOLO model to detect objects for finding the bounding boxes. Then use eye to validate the result (not automate).
    - If the YOLO result is bad, then use SAM to handle those cases.
- 18/4/2025:
  - Done:
    - Use YOLOv8 for doing object detection instead of SAM. The result is not accurate. It cannot find some specific Thai objects or small objects.
  - TODO:
    - Combine both SAM segmentation and YOLO bounding boxes to see if it is working or not.
    - Combine everything (SAM+YOLO if possible but maybe too hard) into a pipeline
    - Benchmark (use eyes) the generated questions (make sense mai?)
- 12/05/2025 (After final exam):

  - Slide

- 13/05/2025:
  - DONE:
    - Presentation
  - TODO:
    - Write a detailed documentaion for everything (code/prompt/steps for running the pipeline)
    - List what to do next (any ideas) and (probably) will talk to Aj. next

Capstone?

Present after final exam (online/onsite)

## Prompts

- Image Scene Graph generation:

```
Generate a detailed image scene graph of this image using the Thai language based on this template

{
       "width": 640,
       "height": 480,
       "location": "living room",
       "weather": none,
       "objects": {
           "271881": {
               "name": "chair",
               "x": 220,
               "y": 310,
               "w": 50,
               "h": 80,
               "attributes": ["brown", "wooden", "small"],
               "relations": {
                   "32452": {
                       "name": "on",
                       "object": "275312"
                   },
                   "32452": {
                       "name": "near",
                       "object": "279472"
                   }
               }
           }
       }
   }
```

- Image Scene Graph generation (continue): Add more detail

```
Please be more detailed and focus more on Thai contexts
```
