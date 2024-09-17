# Getting Started with Code Execution in Genkit

## intro

The Code Execution feature of Google AI was added in version 0.5.8 of Genkit. This allows the execution and return of Python code.

## Initializing a Genkit Project

Let's initialize a Genkit project. The Genkit version must be 0.5.8 or higher, so let's start by installing Genkit.

```sh
% npm i -g genkit
% mkdir genkit-code-execution-sample
% cd genkit-code-execution-sample

% genkit init
? Select a runtime to initialize a Genkit project:
❯ Node.js
? Select a model provider:
❯ Google AI
? Select a model provider: Google AI

? Would you like to generate a sample flow? Yes
✔ Successfully generated sample file (src/index.ts)
Genkit successfully initialized.
```

## Enabling Code Execution

You can enable it by simply adding `codeExecution: true` to the arguments of the generate method. Also, the `prompt` will be modified to pass the input text as is.

```typescript
const llmResponse = await generate({
  model: gemini15Flash,
  prompt,
  config: {
    temperature: 1,
    codeExecution: true, // Add this line
  },
});
```

## Actual Behavior

Run the following to launch the Developer Tool.

```
% genkit start -o
```

Select the implemented Flow from the Flow menu.

First, let's try requesting the following prompt:
"Simulate the ratio of heads to tails after flipping a coin 100,000 times."

[img]()

By selecting View Trace, you can see that the code has actually been executed.

Next, let's try a more direct request:
"Execute the following code in Python: print('Hello World')"

[img]()

As with the previous request, selecting View Trace shows that the code has been executed.

Finally, let's try a general request unrelated to code.

[img]()

You can see that no code was executed. This is because Code Execution is specified as one of the tool options, and the generative AI only executes Code Execution when necessary.

## Summary

With just one additional line, you could easily try out Code Execution. This expands the possibilities of what can be done with Genkit. Please give it a try.

Here is the actual code on GitHub.

https://github.com/tanabee/genkit-code-execution-sample

## References

- Code Execution: https://ai.google.dev/gemini-api/docs/code-execution?lang=node