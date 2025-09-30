# virajapalleti-langsmith-MAT496

## INSIGHTS:

### Module01:

_Lesson01: Tracing Basics_  
Learnt about tracing: projects -> traces -> runs === run trees  
Learnt about metadata and how to use it for organizing traces.  
My tweaks: Changed the project name, modified rag prompt, added custom metadata tags.  
[module01/TracingBasics.ipynb](module01/TracingBasics.ipynb)

_Lesson02: Types of Runs_
Learnt abotu the different types of Runs.  
Learnt how to invoke an LLM, retrive documents related and Tool calling  
[module01/RunTypes.ipynb](module01/RunTypes.ipynb)

_Lesson03: Alternative Ways to Trace_

- LangGraph = automatically does the tracing, manual setup like @tracing is not required. (best for graph based workflows)
- trace() = to manually control what gets traced and to specify the exact input/outputs to log.
- wrap_openai = wraps OpenAI SDK calls and auto-logs API interactions. (also captures token usage and costs)
- RunTree API = for lowest level control. (LANGCHIAN_TRACING_V2 has to be set to false)
  [module01/AlternativeTracingMethods.ipynb](module01/AlternativeTracingMethods.ipynb)
