# language-model-training-on-habana
Training Million parameter language model on AWS Habana EC2 instance with Gaudi Accelerator to help people in a war zone to reduce their mental issues.
## Inspiration
Since Russia launched a full-scale military invasion into Ukraine on February 24, 2022, fighting has caused over one hundred civilian casualties and pushed tens of thousands of Ukrainians to flee to neighboring countries—including Poland.  During war, people can be exposed to many different traumatic events. That raises the chances of developing mental health problems—like post-traumatic stress disorder (PTSD), anxiety, and depression—and poorer life outcomes as adults.
Sometimes all they need is someone to talk, someone to make them feel better, and someone to share their feelings. 
# Installation and Run
## Local Installation
1. Select the Habana base AMI which contain the OS image and the Habana driver and SynapseAI Software Stack. [link](https://aws.amazon.com/marketplace/search/results?searchTerms=Habana)
2. After launching the EC2 instance, install PyTorch using [link](https://github.com/HabanaAI/Setup_and_Install/tree/main/installation_scripts/PyTorch)
3. Install Jupyter Notebook on root using command
```sh
sudo pip install jupyter notebook
```
4.clone this repository. After setting the AWS inbound rule, opened to 8888 port run
```sh
git clone https://github.com/kishorkuttan/language-model-training-on-habana.git
cd language-model-training-on-habana
sudo jupyter notebook --ip=* --allow-root
```
go to **https://your_instance_public_ip4 :8888**

5. run train.ipynb

## Custom Dataset Sample
```sh

text:I am feeling really sad?   labels:why are you feeling sad?
text:A war is going on here in Ukrain?   labels:yes, I know. Russia and Ukraine have had no formal diplomatic relations since 24 February 2022. The Russian Federation and Ukraine are currently in a state of war: the Russo-Ukrainian War began in 2014 following the Russian annexation of Crimea from Ukraine. In February 2022, Russia invaded Ukraine across a broad front.
text:Indeed. When will it end  labels:Hope it end soon
text:I am feeling really scared   labels:Don't be scared. Be strong and be brave
text:How can I feel secured, feeling so insecured now   labels:I am here for you. Don't feel scared. We will get through it.
text:I am in a bunker now   labels:That is scary. But things will be better soon. Don't lose hope.
text:thank you   labels:you are welcome. Hope everything works fine.
text:bye   labels:bye.   episode_done=True
```
# Language Model Architecture
Open-Domain chatbots are the need of the hour. Most of the enterprise chatbots are closed domain chatbots and are not capable of understanding deep human conversational context and don't have any persona. The main difference between a closed domain and an open domain is the understanding of complex sentences and long conversational engagement. The framework is called Blender. It has **3 distinctive features.**

**1. Consistent persona throughout the conversation.**

**2. Empathetic conversation**

**3. Factual information. Eg: Wikipedia**

## Recipes of an open-domain chatbot

**1. Blended Skill Talk(BST)**

**2. Generation Strategy**

BST mainly focuses on understanding the user's emotions, knowledge and switching tasks according to the conversation of the user. Like Serious to funny. Generation Strategy is to minimize perplexity during training the neural network. It measures how well the model can predict or generate the next words. Short text can be considered dull while long text can be considered as an arrogant response. An optimal beam length is chosen and the value is between 1-3.
## Transformer architectures
Three types of transformer-based architectures.

**1. Retriever** - Find the next best dialogue. Eg: Poly-Encoder

![alt text](https://github.com/kishorkuttan/language-model-training-on-habana/blob/main/blenderbot.png)

**2. Generative** - A seq2seq architecture is used for generating responses instead of picking from a fixed set.

**3. Retrieve-and-refine** - A new approach for reading or accessing external knowledge other than what is embedded in our model. it is also sub-categorized as 

1. dialogue retrieval
2. knowledge retrieval

The response will be retrieved for utterance based on the retrieval mechanism and then passed the input sequence to the generator by adding a special separator token in the sequence. This is the flow of **Dialogue retrieval**. Generators are more capable of producing vibrant language than high probability utterances. **Knowledge retrieval**, retrieves from the large knowledge base. They used the proposed model Wizard of Wikipedia task.


# Benchmarking Habana Gaudi Accelerator Vs Tesla P100 from Google Colab
## Training

<p float="left">
  <img src="habana_interface.png" width="480" />
  <img src="colab_interface.png" width="480" /> 

</p>

## Hardware Usage
<p float="left">
  <img src="habana.png" width="480" />
  <img src="colab-2.png" width="480" /> 
  <img src="colab-3.png" width="480" /> 

</p>

**After benchmarking we closely monitored the performance and we got far better performace of Habana Gaudi AWS instance compared to Colab Pro.**

## ParlAI
A unified platform for sharing, training and evaluating dialogue models across many tasks. 
![alt text](https://github.com/kishorkuttan/language-model-training-on-habana/blob/main/parlai.png)
# Datasets Used For Fine-Tuning
1. BlenderBot 90 M.[link](https://huggingface.co/facebook/blenderbot-90M)
2. Empathetic.[link](https://arxiv.org/abs/1811.00207)
3. Paper.[link](https://arxiv.org/abs/1811.00207) 
# TO DO
1. The trained language model can be deployed as an API. Which means we can even built a mental health helpline number with our trained conversational AI as backend to help them feel connected.
![alt text](https://github.com/kishorkuttan/language-model-training-on-habana/blob/main/diagram.png)

