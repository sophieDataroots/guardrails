# Use Guardrails with LLM APIs

Guardrails' `Guard` wrappers provide a simple way to add Guardrails to your LLM API calls. The wrappers are designed to be used with any LLM API.


Here are some examples of how to use the wrappers with different LLM providers and models:

## OpenAI

### Completion Models (e.g. GPT-3)

```python
import openai
import guardrails as gd


# Create a Guard class
guard = gd.Guard.from_rail(...)

# Wrap openai API call
raw_llm_output, guardrail_output = guard(
    openai.Completion.create,
    prompt_params={"prompt_param_1": "value_1", "prompt_param_2": "value_2", ..},
    engine="text-davinci-003",
    max_tokens=100,
    temperature=0.0,
)
```

### ChatCompletion Models (e.g. ChatGPT)

```python
import openai
import guardrails as gd

# Create a Guard class
guard = gd.Guard.from_rail(...)

# Wrap openai API call
raw_llm_output, guardrail_output = guard(
    openai.ChatCompletion.create,
    prompt_params={"prompt_param_1": "value_1", "prompt_param_2": "value_2", ..},
    system_prompt="You are a helpful assistant...",
    model="gpt-3.5-turbo",
    max_tokens=100,
    temperature=0.0,
)
```


## Using a custom LLM API

```python
import guardrails as gd

# Create a Guard class
guard = gd.Guard.from_rail(...)

# Create a PromptCallable function that takes in the prompt as a string and returns the LLM output
def my_llm_api(prompt: str, **kwargs) -> str:
    # Call your LLM API here
    return ...


# Wrap your LLM API call
raw_llm_output, guardrail_output = guard(
    my_llm_api,
    prompt_params={"prompt_param_1": "value_1", "prompt_param_2": "value_2", ..},
    **kwargs,
)
```