# Text Summarizer

Text Summarization helps in summarizing and shortening the text. It can be done with the help of an algorithm that can help in reducing the text bodies while keeping their original meaning intact or by giving insights into their original text.

## Two different approaches are used for Text Summarization

**Extractive Summarization**

In Extractive Summarization, we are identifying important phrases or sentences from the original text and extract only these phrases from the text. These extracted sentences would be the summary.

<p align="center">
  <img src="https://user-images.githubusercontent.com/64821137/209453332-0d0a5801-3dff-4061-b682-7c7a3b1007d2.png"/>
</p>

**Abstractive Summarization**

In the Abstractive Summarization approach, we work on generating new sentences from the original text. The abstractive method is in contrast to the approach that was described above. The sentences generated through this approach might not even be present in the original text.

<p align="center">
  <img src="https://user-images.githubusercontent.com/64821137/209453340-37f4b597-14bc-4afd-83eb-518fe8a3c122.png"/>
</p>

## Understanding the Encoder-Decoder Architecture

The Encoder-Decoder architecture is mainly used to solve the sequence-to-sequence (Seq2Seq) problems where the input and output sequences are of different lengths.

Let’s understand this from the perspective of text summarization. The input is a long sequence of words and the output will be a short version of the input sequence.

<p align="center">
  <img src="https://user-images.githubusercontent.com/64821137/209453396-4981856c-3c8f-49d8-a6b8-a6694720dd1f.png"/>
</p>

Generally, variants of Recurrent Neural Networks (RNNs), i.e. Gated Recurrent Neural Network (GRU) or Long Short Term Memory (LSTM), are preferred as the encoder and decoder components. This is because they are capable of capturing long term dependencies by overcoming the problem of vanishing gradient.

We can set up the Encoder-Decoder in 2 phases:

* Training phase
* Inference phase

**Training phase**

In the training phase, we will first set up the encoder and decoder. We will then train the model to predict the target sequence offset by one timestep. Let us see in detail on how to set up the encoder and decoder.

 
**Encoder**

An Encoder Long Short Term Memory model (LSTM) reads the entire input sequence wherein, at each timestep, one word is fed into the encoder. It then processes the information at every timestep and captures the contextual information present in the input sequence.

<p align="center">
  <img src="https://user-images.githubusercontent.com/64821137/209453437-62b152ac-59cf-4117-bef8-2159dbbe988d.png"/>
</p>

The hidden state (hi) and cell state (ci) of the last time step are used to initialize the decoder. Remember, this is because the encoder and decoder are two different sets of the LSTM architecture.

**Decoder**

The decoder is also an LSTM network which reads the entire target sequence word-by-word and predicts the same sequence offset by one timestep. `The decoder is trained to predict the next word in the sequence given the previous word.`

<p align="center">
  <img src="https://user-images.githubusercontent.com/64821137/209453459-1ca3a411-6d10-41d8-a84a-9f867eddd81d.png"/>
</p>

<start> and <end> are the special tokens which are added to the target sequence before feeding it into the decoder. The target sequence is unknown while decoding the test sequence. So, we start predicting the target sequence by passing the first word into the decoder which would be always the <start> token. And the <end> token signals the end of the sentence.

**Inference Phase**

After training, the model is tested on new source sequences for which the target sequence is unknown. So, we need to set up the inference architecture to decode a test sequence

<p align="center">
  <img src="https://user-images.githubusercontent.com/64821137/209453468-4c6b0c97-35f1-493f-b432-036954c2a0c9.png"/>
</p>

**How does the inference process work?**

1.Encode the entire input sequence and initialize the decoder with internal states of the encoder
2.Pass <start> token as an input to the decoder
3.Run the decoder for one timestep with the internal states
4.The output will be the probability for the next word. The word with the maximum probability will be selected
5.Pass the sampled word as an input to the decoder in the next timestep and update the internal states with the current time step
6.Repeat steps 3 – 5 until we generate <end> token or hit the maximum length of the target sequence

## Model Architecture

![image](https://user-images.githubusercontent.com/64821137/209453629-97e7cbe6-8186-4aa9-add3-4cf6210269b6.png)

## Results

![image](https://user-images.githubusercontent.com/64821137/209453573-35c2c38e-f6cd-4efc-aab9-163c6b13d961.png)

## How can we Improve the Model’s Performance Even Further?
Your learning doesn’t stop here! There’s a lot more you can do to play around and experiment with the model:

* Try Attention Mechanism
* I recommend you to increase the training dataset size and build the model. The generalization capability of a deep learning model enhances with an increase in the training dataset size
* Try implementing Bi-Directional LSTM which is capable of capturing the context from both the directions and results in a better context vector
* Use the beam search strategy for decoding the test sequence instead of using the greedy approach (argmax)
* Evaluate the performance of your model based on the BLEU score
* Implement pointer-generator networks and coverage mechanisms
