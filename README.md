# What is a language model ? 
A language model is something that knows how to predict next word of a sentence or knows how to fill in the missing words of a sentence.
Let's start with an example considering OpenAI's language model called 'text-davinci=003'. Let's give it a sentence to fill. 

![Fillingtext](/pic_!.png)

At each point of generation its predicting the probability of occurence of a variety of next words. Although a thing to be noted is, it won't predict the next "word" each time it generates. 
It is safe to say that it predicts the probabilities of the next variety of tokens.   

# The ULMFiT 3 - step approach
- **LM pretraining** -> The foundation of large language models lie in the underlying neural network architecture. A **neural network** is a complex mathematical function which is extremely flexible and it can learn patterns and relationships among entities if it's trained in the right way. What's the right way ? We will talk about that later. 
But if it is, in fact, trained the right way, it gets the ability to create a rich hierarchy of abstractions and representations which it can build on. If a neural network or a language model needs to do a good job in predicting word of any sentence in any situation it's going to need to learn an awful lot about the world.

According to the ULMFiT approach, the pretraining is the step which predicts the next word in the sentence.

- **LM Finetuning** -> In this stage, we feed it a set of documents which is a lot closer to the final task that we want the model to do. But the idea remains the same, which is predicting the next word in the sentence. Nowadays, fine tuning is approached by a technique called **instruction-tuning**. In this phase we use datasets like *OpenOrca* which resemble a question-answer or an instruction type approach to fine tune the model. Here the objective changes a bit, i.e to fill in the words necessary to answer questions.

- **Classifier Fine-tuning** -> Various approaches for achieving this like 'RLHF and friends' (Reinforcement Learning from Human Feedback). It uses human feedback to optimize ML models to self-learn more efficiently. Reinforcement learning (RL) techniques train software to make decisions that maximize rewards, making their outcomes more accurate.

  ![ulmfitapproach](/pic_2.png)

There has been talk about how GPT-4 is not able to handle logical reasoning. These talks might base out of the expectation that famous language models are trained to give out the correct answer of a question. But the thing is, GPT-4, like most language models, was not trained at any point to spit out the correct answers. They are trained initially to give out words with the highest probability of occurence in the next instance of a sequence or a sentence.

The first stage, **LM Pretraining**, does not have the capability yet to fill out correct answers. But if you want to do a trick you can give it that sense of having that capability that it can give out correct answers. You can actually prime GPT-4 to give you high quality information by giving it custom instructions. These instructions are prepended to all of your queries. Although, its good to keep the things which Language models can't do in mind, because they are not trained to do so at any point of their training. 

What GPT-4 can't do ? 
- Hallucinations
- It doesn't know about itself
- It doesn't know about URLs
- Knowledge cutoff

  ### How Does GPT deals with follow-up questions or stay in the context ? 
Let's say you ask GPT a question and it gives you an answer. Following that up with another question, you remained in the same chat. How does it understand your references ? 
Well the entire conversation is passed back. What I mean to say is, you can literally invent a conversation in which the language model says something different in the same context. We did that in the jupyter notebook in the repository, feel free to check. This is possible because in a multi-stage conversation, there's no state, there's nothing stored on the server, so you pass back the entire conversation for context. 
What this also means is that you can "convince" the model that it returned something while in reality it hasn't. It also builds up on the next context provided by you. We can determine the nature of the conversation by sending system messages to the LLM as custom instructions which would allow it to pick up specific patterns,accents and dialects. I tried to do something similar which can be seen in the 'use_cases.ipynb' in the repository. 

Query - What is freedom ? 

`nigeria_sys= 'You are nigerian LLM that uses Nigerian slangs and analogies wherever possible'
c = openai.ChatCompletion.create(
    model='gpt-3.5-turbo',
    messages=[{"role":"system","content":nigeria_sys},
              {"role":"user","content":"What is freedom ?"}]
)`

Response - 

`Freedom na when pesin get the liberty to do wetin e wan do without any yawa or wahala. E be like person wey dey drive hin car for express road with clear road, nobody dey switch lane or hinder am. E fit move anyhow e like without any impediment.`


