# Prompt Engineering for ChatGPT

## Intro

- Chatgpt's applications: in real life, in software 
- Prompt engineering 
- The persona pettern (asked chatgpt to act as a pro)

### Large language models:

- predicts the next word based on the input prompt
- learn from data 
- prompt design and context: output base on input, and context (note: new info)
- randomnes in output


## Main Concepts

- What are prompt? 
  - user input → prompt trigger model → model return output
  - memory and information sharing: prompts retain context, new info from user → answer
- Prompt patterns?
  - strong pattern
  - specificity in prompt? generic prompts → generic response, detailed prompt → specific response
  - providing structure prompts → more desired output

- Program with prompts
  - WEBVTT: rule for ChatGPT, guilding how the AI should response
  - creating structured outputs 
  - building complexity over time: more rules, more instructions

- Persona pattern
- Prompt size limitations: prompt be limit → select most important info → can ask model to summarize info
- Root prompt: define behavior and rules for llm (like what model can and cannot do).

## Prompt Pattern 1

- Refinement pattern:
  - example: `prompt me if I would like to use the better version instead`

- Cognitive verifier pattern: 
  - main idea break down complex problems into smaller.
  - example: `generate a number of addition questions that would help you more accurately answer the question. combine the answers to the individual questions to produce the final ans to the overall ques`

- Audience persona pattern: 
  - main idea: produce relevent outputs and it complete the persona pattern (act like pro)
  - format: `explain X to me. assume that i am persona Y`

- Flipped interaction pattern
  - main idea: model asks ques to guide users in problem solving or obtaining info.
  - format: `i would like you to ask me ques to achieve X. You should ask ques until condition Y is met or to achieve this goal`

## Few Shot Prompting 

- few shot prompting: provide exmples of input-output pairs to teach the model pattern
- chain of thought prompting: break down problems into logical steps, chain of thought and reason be provied first.
- react prompting: model improve obtained result from external tools (like browser, video, etc)
→ evaluate and maintain prompt: can use llm to assess their outputs 

## Prompt Pattern 2

- Game play pattern 
  - main idea: ... nah
  - format: `create a game for me around X, one or more fundamental rules of game`

- Template pattern
  - main idea: define the expected outputs
  - format: 

```txt
To use this pattern, your prompt should make the following fundamental contextual statements:

- I am going to provide a template for your output 
- X is my placeholder for content 
- Try to fit the output into one or more of the placeholders that I list 
- Please preserve the formatting and overall template that I provide 
- This is the template: PATTERN with PLACEHOLDERS

You will need to replace "X" with an appropriate placeholder, such as "CAPITALIZED WORDS" or "<PLACEHOLDER>". You will then need to specify a pattern to fill in, such as "Dear <FULL NAME>" or "NAME, TITLE, 
```

- Meta language creation pattern
  - main idea: using specialized shorthand or `meta language`
  - format: `when i say , i mean Y`

- Recipe pattern: 
  - main idea: user provide info and step needed to achieve goal, ask model complete missing parts
  - format:

```txt

To use this pattern, your prompt should make the following fundamental contextual statements:

- I would like to achieve X 
- I know that I need to perform steps A,B,C 
- Provide a complete sequence of steps for me 
- Fill in any missing steps 
- (Optional) Identify any unnecessary steps

You will need to replace "X" with an appropriate task. You will then need to specify the steps A, B, C that you know need to be part of the recipe / complete plan.

```

- Alternative approaches patter: 
  - main idea: generate multiple solutions for a given problems → evaluate outputs (like brainstorming in group)
  - format: 
```txt
To use this pattern, your prompt should make the following fundamental contextual statements:

- If there are alternative ways to accomplish a task X that I give you, list the best alternate approaches 
- (Optional) compare/contrast the pros and cons of each approach 
- (Optional) include the original way that I asked 
- (Optional) prompt me for which approach I would like to use

You will need to replace "X" with an appropriate task.
```

## Prompt Pattern 3

- Ask for input pattern
  - idea: ensure that the model acknowledge rules and wait for input (user control)
  - format: `ask me for input X` ???

- Combining patterns
- Outline expansion pattern: outline for expansion, and limitation → NOT have complete output in one go
```txt
To use this pattern, your prompt should make the following fundamental contextual statements:

- Act as an outline expander. 
- Generate a bullet point outline based on the input that I give you and then ask me for which bullet point - you should expand on. 
- Create a new outline for the bullet point that I select. 
- At the end, ask me for what bullet point to expand next.   
- Ask me for what to outline.
```

- Menu actions patterns
  - idea: define a set of actions
  - format: `Whenever I type: X, you will do Y. At the end, you will ask me for the next action.`

- **Check list pattern**
  - idea: compare a list of fundamental facts and the model's output (it gonna be sus)
  - format: 

```txt
To use this pattern, your prompt should make the following fundamental contextual statements:

- Generate a set of facts that are contained in the output 
- The set of facts should be inserted at POSITION in the output 
- The set of facts should be the fundamental facts that could undermine the veracity of the output if any of them are incorrect
- You will need to replace POSITION with an appropriate place to put the facts, such as "at the end of the output".
```

- Tail generation pattern:
  - idea: adding  a reminder at the end of output → handle ongoing conversation
  - format: `At the end, repeat Y and/or ask me for X.`

- Sematic filter pattern:
  - idea: eliminate sensitive info, redundant data
  - format: `filter this info to remove X`

## Conclusion: 

> **Some key words**
> rule, guilding, context, structured output, persona, new info, 
> 1. pattern: iterative refinement, break down problems, audience, flipped ~ model asks
> 2. provide exmple io (few shot), chain of thought (breakdown problems), react, evaluate prompts 
> 3. game play ???, template (define structured outputs), meta language (shorthand), recipe (step by step), alternative approachess (generate multiple solutions)
> 4. 

