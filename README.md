# virajapalleti-langsmith-MAT496

## INSIGHTS:

### **Module01:**

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

### **Module02:**

_Lesson01:_  
Datasets are fundamentally a list of examples.  
Created a custom dataset using the LangSmith SDK and client. Uploaded examples to LangSmith as a new dataset, both manually and by generating AI examples with OpenAI.

- Datasets contain input/output pairs for evaluation and few-shot examples
- Examples can be added individually or in bulk
- Generated 5 unique examples using GPT-4o-mini instead of using the provided examples
- split the dataset for crucial exampels
