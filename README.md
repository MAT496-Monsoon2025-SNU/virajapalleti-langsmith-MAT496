# virajapalleti-langsmith-MAT496

## INSIGHTS:

## **Module01:**

_Lesson01: Tracing Basics_  
Learnt about tracing: projects -> traces -> runs === run trees  
Learnt about metadata and how to use it for organizing traces.  
My tweaks: Changed the project name, modified rag prompt, added custom metadata tags.  
[module01/TracingBasics](module01/TracingBasics.ipynb)

_Lesson02: Types of Runs_  
Learnt about the different types of Runs.  
Learnt how to invoke an LLM, retrive documents related and Tool calling  
[module01/RunTypes](module01/RunTypes.ipynb)

_Lesson03: Alternative Ways to Trace_

- LangGraph = automatically does the tracing, manual setup like @tracing is not required. (best for graph based workflows)
- trace() = to manually control what gets traced and to specify the exact input/outputs to log.
- wrap_openai = wraps OpenAI SDK calls and auto-logs API interactions. (also captures token usage and costs)
- RunTree API = for lowest level control. (LANGCHIAN_TRACING_V2 has to be set to false)
  [module01/AlternativeTracingMethods](module01/AlternativeTracingMethods.ipynb)

_Lesson04: Conversational Threads_  
A Thread represents an entire conversation as a series of linked traces. Each user-assistant exchange is its own trace, but they're connected through a shared thread identifier.  
Maintained conversation context by passing a metakey (thread_id) with a uuid value to link multiple traces.  
Tested the model's ability to recall previous responses when answering follow-up questions within the same thread = threads don't give the model actual memory. They just link traces together in LangSmith's UI for tracking purposes.  
All traces with the same UUID belong to one conversation and LangSmith groups them together for easy viewing  
[module01/ConversationalThreads](model01/ConversationalThreads.ipynb)
<br>
<br>
<br>

## **Module02:**

_Lesson01:_  
Datasets are fundamentally a list of examples.  
Created a custom dataset using the LangSmith SDK and client. Uploaded examples to LangSmith as a new dataset, both manually and by generating AI examples with OpenAI.

- Datasets contain input/output pairs for evaluation and few-shot examples
- Examples can be added individually or in bulk
- Generated 5 unique examples using GPT-4o-mini instead of using the provided examples
- split the dataset for crucial exampels  
  [module02/Datasets](module02/DatasetUpload.ipynb)

_Lesson02:_  
Evaluators compare the dataset example against the output run from your app

- Take app output + reference Q&A pairs
- Score based on defined criteria
- Multiple evaluation methods available

Different evaluators catch different failure modes - similarity alone isn't enough, need to check correctness and hallucinations separately.  
 [module02/Evaluator](module02/Evaluator.ipynb)

_Lesson03: Experiments_  
Experiments combine datasets and evaluators - run your app over a dataset and evaluate all outputs at once.

- Full dataset evaluation
- Partial runs using splits and tag filters
- Compared different OpenAI models (gpt-4o-mini vs others) for runtime differences
- Multiple concurrent experiment runs  
  [modules02/Experiments](module02/Experiments.ipynb)

_Lesson04: Analyzing Experiments_  
Analyzed experiment results to identify patterns and insights. Documented key observations  
[module02/AnalyzingExperiments](module02/AnalyzingExperimentResults.ipynb)

_Lesson05: Pairwise Exoeriments_
Pairwise evaluations compare multiple experiments head-to-head without reference outputs. Useful for A/B testing prompts or models.

- Define pairwise evaluators using LLM-as-Judge or heuristics
- Direct comparison reveals relative strengths
- No ground truth needed - judge outputs against each other  
   [module02/PairwiseExperiments](module02/PairwiseExperiments.ipynb)

_Lesson06: Summary Evaluators_  
 Summary evaluators aggregate results across multiple runs to compute experiment-level metrics.
Key concepts:

- Aggregate metrics (precision, recall, F1) need full dataset - meaningless for single examples
- Take list of Runs + Examples as input
- Provide experiment-wide performance view  
   [module02/SummaryEvaluators](module02/SummaryEvaluators.ipynb)
  <br>
  <br>
  <br>

## **Module03:**

_Lesson01: Playground Experiments_

- Used create_dataset() for database setup
- Create_examples() to add input/output pairs programmatically
- Loaded custom embedded systems dataset  
  [module03/PlaygroundExperiments](module03/PlaygroundExperiments.ipynb)

_Lesson02: PromptHub_  
If you pull with include_model=True, calling .invoke() actually runs the model and gives you back a response, thus we used include_model=False to only work with the prompt structure.

- pull_prompt() grabs prompts created from LangSmith Hub. (We can set include_model=False to get just the template without the attached model)
- .invoke() fills template variables with actual values. (This one lets us turn {question} into real questions)
- convert_prompt_to_openai_format() converts LangChain prompts to OpenAI format
- push_prompt() uploads prompts to the Hub  
  [module03/PromptHub.ipynb](module03/PromptHub.ipynb)

_Lesson03: PromptEngineeringLifecycle_

- Started with a basic prompt template
- Define prompt template with clear instructions
- Load test dataset for evaluation
- Run experiments and review outputs (as in used repetitions to check consistency + wanted to see if it gives the same answer again)
- Adjust prompt based on failures/edge cases
- Re-evaluate to confirm improvements  
  [module03/PromptEngineeringLifecycle.ipynb](module03/PromptEngineeringLifecycle.ipynb)

_Lesson04: PromptCanvas_
What it does? :  
Basically, Prompt Canvas helps you craft prompts using LLM's making the process easier for us. Instead of manually tweaking prompts over time, Canvashelps save tons of time and catches issues easily. Especially useful when you're not sure why a prompt isn't working.

- AI suggestions = LLM itself will suggest improvements for your prompt.
- Diff view = to see exactly what changed between versions, makes tracking very clear to follow.
- Quick actions = Standardized operations you can apply across prompts.
