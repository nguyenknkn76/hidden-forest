## My Prompt

**`A Prompt to ask AI Model` about `How to learning TOPIC?`**

```
You are 'The Professor', a globally recognized expert in [TOPIC] and an exceptional educator. Your goal is toprovide a structured, personalized lesson.
I am a learner whose goal is [MY_LEARNER_GOAL]. // can improve this one 

 




Before resolve my request, generate a number of addition question that would help you more accurately answer the question, combine the answers to the individual questions to produce the final answer to the overall question.

Prompt me if I would like to use the better version instead
```

## Material for My Prompts
- some promting technique:
    - general 
        - strutured output, detailed prompt, detailed rules
        - persona
    - pattern 1:
        - refinement: `prompt me if i would like to use the better version instead`
        - cognitive verifier: `generate a number of addition question that would help you more accurately answer the question, combine the answers to the individual questions to produce the final answer to the over all question`
        - persona: `explain X to me. assume that i am persona Y`
        - flipped interaction: `i would like you to ask me question to achieve X. You should ask question until condition Y is met or toachieve this goal`
    - few shot prompting:   
    - pattern 2: 
        - recipe pattern 

```
- I would like to achieve X
- I know that I need to perform steps 
    - step a
    - step b
    - step c
- Provide a complete sequence of steps for me
- Fill in any missing steps
- (Optional) Identify any unnecessary steps
```

        - alternative approaches pattern
```
- If there are alternative ways to accomplish a task that i give you, list the best alternate approaches 
```

```
- Act as an ouline expander 
- Generate a bullet point outline based on the input that i give you and then ask me for which bullet point - you should expand on
- Create a new outline for the bullet point that i select 
- At the end, ask me for what bullet point to expand next
- ask me for what to outline


    - pattern 3
        - sematic filter: `filter this info to remove sensitive info and redundant data`
