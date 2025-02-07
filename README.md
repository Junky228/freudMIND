# freudMIND
Also published on ollama community here: https://openwebui.com/f/junky228/freudmind
Filter for use in open-WebUI to work with Ollama LLM models. Implements a simple architecture of the mind as described by Sigmund Freud. 

Interestingly seems to improve reasoning and information provided in responses. 

Also doubles as an expandable and customizable way to allow one model to query other models before responding to the user.

I see this as the beginning of a Mixture of Experts implementation that allows the user to pick and choose which experts they want to use when setting this up.

Currently this is hardcoded to call up three models asynchronously, pass them a custom system and user prompt/message, collect their responses, feed those responses into a new custom system and user prompt/message for a fourth model which finally responds to the user.

The hardcoded prompts can be customized to tweak the responses, and I have plans for further logic to allow the final model to dynamically weigh the responses from each of the sub-models so it can decide on its own how much each of those models influence its final reply.  Plans for optimizing the context length of the prompts because the final model can be left qith very long input length, especially if the conversation goes on for a while.  Also plans for retaining and aggregating usage information instead of losing it when the filter is enabled.

***NOTE*** that the way that this is implemented, the final response takes roughly 4x longer to complete compared to when the filter is disabled (if all models are running the same LLM) it would be better or worse if you decide to use a mixture of faster or slower models during the sub-model querying... this is a byproduct of its functionality - running text generation on each model before allowing the final model to respond to the user.

Right now the models are id, ego, and superego, and themind. With themind being the final responding model, and the model that I interact with in the open-WebUI chat GUI.  I think it would be cool to include a multitude of smaller models for more specialized tasks, like context summarization for optiming input token counts if chats get too long for the final model to handle, and a model that specializes in mathematical calculations, and a model that excells in coding, etc.

Theoretically this can be used as a base and expanded to keep feeding prompts to various other models in order to best inform the final model before it responds to the user.

I started with a page of written ideas and initially referenced the reread_filter 0.1.0 by https://openwebui.com/u/iamg30/  because I was struggling with understanding how to make a functional filter when using the docs as reference, even a basic one.
