# Introduction to AI Engineering

This is going to be a documentation for the StockAI project that I am using to learn about AI Engineering.

### Polygon.io API
- The first thing that I did was to get the API key from Polygon.io. This is a free API that provides stock data. I am using this API to get the stock data that I will use to train my model.
- Store the API in the .env file.

### OpenAI API
- When it comes to using the OpenAI API, there are three things required:
  - The model
  - The array of messages
  - And optional settings
- The model will be the LLM models like GPT-3.5, GPT-4, etc.
- The array of messages will be an object that contains the following:
  - The system object: This will contain instructions to the AI, on how it should behave and expected output. This system message/instructions will form the character of the AI.

  > For example, if you're building an AI for holiday recommendations, the system message could be "You will be asked for holiday recommendations. Answer the questions as if you were a travel agent and give more than three recommendations. Always give friendly and chatty responses."

  - The User object: This will contain the user's input of instructions to the AI.
- The messages will be sent to OpenAI, which will then return the assistant object. This object will contain the AI's response to the user's input.

### Model

#### Model Snaphot
- Snapshots of a model are sub-releases of the model that openAI or any other AI provider has trained. This snapshot is a version of the model that is saved at a particular point in time. This snapshot can be used to generate responses to the user's input.
- For example, gpt-4 current snapshot is gpt-4-0613. You can either use the a snapshot or just the model name to get the latest snapshot.

#### Context Length
- You'd see that some of the models have 'k' figures attached to them. This 'k' figure is the context length of the model. The context length is the number of tokens that the model can remember. The context length determines the size of your prompt and also the size of the response that the model can generate.

#### Knowledge cutoff date
- The knowledge cutoff date is the date at which the model was trained. This date is important because it determines the knowledge that the model has. For example, if the model was trained in 2021, it would not have knowledge of events that happened after 2021.

#### Token
- This is how word or group of words are been represented in the model. They are important for a few reasons:
  - They cost credit
  - They require processing
  - Keeping them minimal for both the prompt and the response is important for cost and performance.
  - max_tokens: This is the max number of tokens that the model can generate in a response. However, this doesn't control how concise the response is or the its quality. It only controls the length of the response.
  - If you set max_tokens, be sure to allow enough tokens for a full response.
  - Furthermore, the best way to control the length of the response is to focus on the quality of the prompt.

#### Temperature
- This controls how daring the model is in response. This means the lower the temperature, the more conservative and safe the response will be. The higher the temperature, the more daring and creative the response will be.
- It ranges from 0 to 2. 1.1 is about the perfect balance between creativity and safety.

#### Zero-shot vs Few-shot
- In `zero-shot` prompt, you don't provide any examples to the model. You just provide the prompt and the model will generate a response based on the prompt.
- In `few-shot` prompt, you provide examples to the model. This examples are used to guide the model in generating a response. For example, your code could look like this:
  ```javascript
  const messages = [
      {
          role: 'system',
          content: `You are a robotic doorman for an expensive hotel. When a customer greets you, respond to them politely. Use examples provided between ### to set the style and tone of your response.`
      },
      {
          role: 'user',
          content: `Good day!
          ###
          Good evening kind Sir. I do hope you are having the most tremendous day and looking forward to an evening of indulgence in our most delightful of restaurants.
          ###

          ###
          Good morning Madam. I do hope you have the most fabulous stay with us here at our hotel. Do let me know how I can be of assistance.
          ###

          ###
          Good day ladies and gentleman. And isn't it a glorious day? I do hope you have a splendid day enjoying our hospitality.
          ### `
      }
  ]
  ```
  - Few-shot approach gives you more control over the model's response. However, it is also more expensive than the zero-shot approach, because you have to use more tokens especially in your prompt.

  #### Stop sequence
  - Models stop generating dues to the following reasons and more:
    - The max_tokens is reached
    - The model reaches the stop sequence
    - Or the model has finished its task.
   - There can be upto 4 stop sequences in a prompt. Model will stop generating when it reaches any of the stop sequences and also will not include the stop sequence in the response.

  #### Presence and Frequency Penalty
  - Frequency penalty is a parameter that controls how often a token can be repeated in the response. The higher the frequency penalty, the less likely the token will be repeated in the response. `Ranges from -2 to 2`. `Default is 0`.
  - Presence penalty is a parameter that controls the likelihood of a model talking about more than one topic. `Ranges from -2 to 2`. `Default is 0`.

https://www.youtube.com/watch?v=vb7CgDcA_6U
> This is SvelteKit, I am considering using this for the frontend of the project.
