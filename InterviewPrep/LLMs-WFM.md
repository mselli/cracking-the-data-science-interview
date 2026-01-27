# LLMs

# Stanford  CS295 LLMs and Transformers

## Tokenization

 just a way to represent language

    could be word-wise or sub-word wise

you build a vocabulary from this tokenization process



single language vocabulary: ~10Ks words

multilanguage: ~100Ks words

multi task language (llm + code): > 100Ks



end of sequence token is there to know when the sequence ends.



## Embedding representation

an NN with a proxy task over millions of tokens to learn the representation of the language.

**proxy tasks:**

contnous bag of words - predicts words around a set of words

skip gram - predicts the next token



**word2vec:**

one hot encoding representation passes thru an NN, after a soft max layer, it predicts the prob for the next token. 

process: for every word,  you represent it as a one hot encoding, passes thru an NN, make a prediction about the first word, compute the loss, update weights and move to the next token. 



hidden layer size: depends on the complexity of your task. 100s or 1Ks size in practicallity. usually ppl use: 768

--> the representations you learn are token specific

## RNNs

RNNs, instead of processing words one at a time, they keep the hidden rep of the sentence sofar and consider tokens one at the time. 

have the issue of not retaining previous knolwedge. vanishing gradient. 

in order to predict the last word, you are dependent on every hidden state that came before that. because of this, you get vanishing gradients

LSTM help in this way. 



## Attention

originated in 2014. having a way to know which word you are trying to predict. 

**Attention is all you need** - 2017 paper. state of the art translation mechanisms.

**self attention:** move away from sequential ways of processing text and direct connections to all parts of the text at once.



you use attention mechanism in order to compute the representation of a word that is unique to the context of the text. the representation has contextual information as well. 



## Query, Key, Value:

![](/Users/xonxis/Library/Application%20Support/marktext/images/2026-01-15-09-01-05-image.png)



**GOAL:** you want to quantify how similiar your **QUERY** is to a given KEY, **and** then you get that **VALUE**

**Process:** compare the query to all other keys, compare similiarity and weight it and then take that asociated value.



pros: can be computed in a matrix format. 

![](/Users/xonxis/Library/Application%20Support/marktext/images/2026-01-15-09-04-23-image.png)



the quantities are learned. 

the key is there for you to figure out which key is most similiar to the query. **these things are learned by the model**



## Architecture

Attention layer (MHA)

encoder-decoder 



compute meaningful embeddings by passing that thru the layer 

input text + tokens will attent to one another



use all the representation of your input sentence to predicvt the next word. 



goal: what are the words that i;ve used so far are relevant to predict the next one.

![](/Users/xonxis/Library/Application%20Support/marktext/images/2026-01-15-17-36-36-image.png)

 

attention layer: 

comuting embeddings from the input sentences as a function of itself. 

maskes self attentionL: express something 



you dont have any sense of order. so you have positional encodings to know 



# LLM Architecture

Last Updated : 28 Oct, 2025

Large Language Models (LLMs) are AI systems designed to understand, process and generate human-like text. They are built using advanced neural network architectures that allow them to learn patterns, context and semantics from vast amounts of text data. LLMs are used in applications like chatbots, translation systems, content generation and text summarization.

- They are based mainly on transformer architectures which allow efficient learning of relationships between words in a sequence.
- LLMs require large datasets and significant computational power for training.
- These models can be fine-tuned for specific tasks making them adaptable to different domains.
- Despite their power, LLMs can inherit biases from training data and require careful monitoring.

## Architecture

![input_data](https://media.geeksforgeeks.org/wp-content/uploads/20251027113102226370/input_data.webp)

Flow

### 1. Input Layer: Tokenization

- Input text is broken into tokens which are smaller units like words, subwords or characters.
- Tokens are converted into numerical representations that the model can process.

### 2. Embedding Layer

- Word embeddings map tokens to dense vectors representing their meanings.
- [Positional embeddings](https://www.geeksforgeeks.org/nlp/positional-encoding-in-transformers/) are added to indicate the order of tokens, since [transformers](https://www.geeksforgeeks.org/machine-learning/getting-started-with-transformers/) cannot process sequences in order naturally.

### 3. Transformer Architecture

- [Self-Attention](https://www.geeksforgeeks.org/nlp/self-attention-in-nlp/) calculates how each word relates to others in the input. It uses Query (Q), Key (K) and Value (V) vectors.
- [Multi-head attention](https://www.geeksforgeeks.org/nlp/multi-head-attention-mechanism/) allows the model to focus on multiple relationships simultaneously.
- A feedforward network processes attention outputs independently for each token.
- Layer normalization and residual connections help stabilize training and allow deeper networks.

### 4. Stacking Layers

- Transformers are composed of multiple blocks stacked together.
- Each block contains attention and feedforward layers to capture complex relationships and hierarchical patterns in text.

### 5. Output Layer: Decoding

- In autoregressive models like GPT, the model predicts the next word in a sequence.
- In masked models like BERT, the model predicts missing words in a sequence.
- The final softmax layer converts outputs into probability distributions over the vocabulary.

## Training and Fine-Tuning

### ****1. Pre-training****

LLMs start by learning from massive datasets like books, articles, websites and other text sources. The model is trained to predict missing words or the next word in a sequence, helping it understand language patterns. This phase demands powerful GPUs or TPUs and distributed computing, since the models often contain billions of parameters.

### ****2. Fine-tuning****

After pre-training, the model can be refined on specific datasets for particular tasks like translation, sentiment analysis or question-answering. During this step, hyperparameters such as learning rate and batch size are carefully adjusted to get the best performance on the target task.

### ****3. Optimization and Scaling****

During training, the model minimizes a loss function that is usually a cross-entropy by adjusting its weights using [backpropagation](https://www.geeksforgeeks.org/machine-learning/backpropagation-in-neural-network/) and [gradient descent](https://www.geeksforgeeks.org/machine-learning/gradient-descent-algorithm-and-its-variants/).

To handle large models efficiently, different scaling strategies are used:

- Data parallelism and model parallelism allow the workload to be split across multiple devices.
- Techniques like quantization, pruning and distillation help shrink the model size and speed up inference without losing much accuracy.

## Ethical Considerations

- ****Bias and Fairness****: LLMs can reflect biases in their training data, requiring evaluation and mitigation.
- ****Misinformation and Safety****: They may generate incorrect or misleading content, so oversight and filters are needed.
- ****Privacy and Data Security****: Training data can include sensitive information, making anonymization and secure handling crucial.
- ****Environmental Impact****: Large models consume significant energy, so efficiency and optimization are important.
- ****Responsible Deployment****: Guidelines and monitoring are necessary to prevent misuse of the model.

---

# Gemini workflow

**Context Retrieval (Memory)** Gemini doesn't just look at your current question; it looks at the conversation history so it knows what "it" refers to if you say "Explain *it* again."

- **The Look-up:** The system queries a low-latency database (likely Spanner or an in-memory cache) to pull the last few turns of your conversation.

- **The Append:** It stitches your new question to the end of this history to create a single "Prompt Context."

**4. The Safety Shield (Input Filtering)** Before the AI ever sees your text, it passes through a **Classifier Model** (a smaller, faster AI).

- **The Check:** This model scans for prohibited content (CSAM, hate speech, severe harassment, malware injection attacks).

- **The Verdict:** If your input triggers a hard block, the process stops here, and you get a "I can't help with that" error. If it passes, it moves to the brain.

### Phase 3: The Brain (Inference & Reasoning)

**5. Tokenization (Translation)** The model doesn't understand English letters; it understands numbers.

- **The Process:** Your text is broken down into **Tokens** (chunks of characters, roughly 4 characters per token).

- **Example:** "Show me the code" becomes `[Show] [ me] [ the] [ code]`. These are converted into a long string of integers (vectors).

**6. The Orchestrator (Tool Use Decision)** This is where Gemini differs from a basic text generator. A "Router" or "Orchestrator" analyzes your intent.

- **Decision:** Does this question need external data?
  
  - *If "What is the capital of France?"* -> **Pure Generation** (Go straight to model).
  
  - *If "What is Google's stock price right now?"* -> **Tool Use**. The Orchestrator pauses the model, calls Google Search (Grounding), retrieves the snippets, and *then* feeds those snippets to the model.

**7. Inference (The TPUs)** The request is sent to a **TPU Pod** (Tensor Processing Unit). These are Google's custom-built AI chips (likely TPU v4 or v5e/p).

- **The Calculation:** The model (a massive Transformer neural network with billions of parameters) processes the input vectors. It performs matrix multiplications to predict the **most likely next token** in the sequence.

- **Decoding:** It doesn't just pick the #1 most likely word every time (which would be boring). It uses **Temperature** and **Top-K/Top-P** sampling to add a tiny bit of variation so the language sounds natural.

### Phase 4: Verification (Output Processing)

**8. The Safety Shield (Output Filtering)** As the model generates the answer, it is scanned again.

- **The Check:** The system checks if the *AI's* answer violates safety policies (e.g., did it accidentally generate instructions for a dangerous act?).

- **The Recitation Check:** It also checks if the output is a verbatim copy of copyrighted text (like a whole page from a Harry Potter book) and suppresses it if necessary.

**9. Detokenization & Streaming** The numbers (tokens) are converted back into human-readable text.

- **Streaming:** Instead of waiting for the whole paragraph to finish, the system sends chunks of text back to you as they are generated. This is why you see the "typing" effect.

### Phase 5: Feedback Loop

**10. Rendering & Logging**

- **Client Side:** Your browser receives the stream and renders Markdown (making bold text **bold**, code blocks look like code).

- **Logging:** The interaction is logged (anonymized, depending on your privacy settings) for system health monitoring and potentially for future fine-tuning (RLHF - Reinforcement Learning from Human Feedback) if you give it a "Thumbs Up" or "Thumbs Down."

## Text embeddings

### Part 1: Encoding (Text to Numbers)

The goal of encoding is to turn your sentence into a format the model can process mathematically while preserving the *meaning* of the words.

#### Step 1: Tokenization (The "Chop Shop")

The model does not read word-by-word; it reads **token-by-token**. A "token" can be a whole word, part of a word, or even a single character.

- **The Algorithm:** Most modern LLMs use a method called **BPE (Byte-Pair Encoding)**. It is efficient: common words like "apple" remain one token, but complex or made-up words like "GPT4o" might be split into `[GPT]`, `[4]`, `[o]`.

- **The Indexing:** The model has a fixed vocabulary (e.g., 100,000 specific tokens). Each token has a permanent, unique ID number.

> *Example:* **Input:** "Helping" **Tokens:** `[Help]` + `[ing]` **IDs:** `[4521]` + `[98]`

#### Step 2: Embedding (The "Meaning" Layer)

This is the most critical step. If we just fed the computer the number `4521`, it would treat it like a quantity (math). But `4521` isn't a quantity; it's a concept.

To solve this, the model looks up ID `4521` in a massive **Embedding Matrix**. This converts the single integer into a **Vector**—a list of thousands of floating-point numbers (e.g., `[0.02, -0.41, 0.99, ...]`).

- **Why do this?** In this vector space, words with similar meanings are mathematically close to each other. The vector for "King" minus the vector for "Man" plus the vector for "Woman" will mathematically equal the vector for "Queen."

- **Result:** Your simple text question is now a massive multi-dimensional matrix of floating-point numbers ready to be processed by the Neural Network.

### Part 2: Processing ( The "Black Box")

Once encoded, these vectors pass through the model's layers (the Transformer architecture). The model doesn't just look at one token; it looks at **all of them at once** (Self-Attention mechanism).

It calculates how much the word "bank" relates to "money" versus "river" based on the other words in your sentence. It transforms the vectors layer by layer until it reaches the final layer.

### Part 3: Decoding (Numbers to Text)

The model has finished thinking. Now it needs to speak. It doesn't just spit out a word; it spits out **probabilities**.

#### Step 1: Logits and Softmax

The final layer of the model produces a raw score (called a **Logit**) for every single token in its vocabulary (all 100,000 of them).

- It might give a high score to the token for "Java" and a low score to "Pizza" if you asked about coding.

- A **Softmax function** turns these raw scores into percentages (probabilities) that add up to 100%.

> *Example Output for the next word:*
> 
> - "Python": 80% chance
> 
> - "Java": 15% chance
> 
> - "The": 0.01% chance

#### Step 2: Sampling (The Choice)

The model must pick one.

- **Greedy Decoding:** It picks the #1 highest percentage every time. This is robotically accurate but can be repetitive and boring.

- **Temperature Sampling:** If you set the "Temperature" higher, the model rolls the dice. It might pick "Java" (the 15% chance) just to be creative.

#### Step 3: Detokenization (The Assembly)

Once the ID is chosen (e.g., ID `774`), the system looks up `774` in the dictionary, finds the text snippet associated with it, and appends it to the response stream.

#### Step 4: Autoregressive generation

This cycle (Predict Probability → Pick Token → Detokenize) repeats for every single word generated until the model outputs a special **[STOP]** token, signaling the answer is complete.

The LLM does not produce the whole sentence at once; it produces it **one word at a time**, extremely fast. This process is called **Autoregressive Generation**. The "output" of step 1 becomes the "input" of step 2.

Here is the exact loop that happens for every multi-word answer:

#### The "Loop" Mechanism

1. **Step 1:** You feed the model your question: *"What is the capital of France?"*
   
   - The model runs the math and predicts the single most likely next token: **"Paris"**.
   
   - *System outputs "Paris" to your screen.*

2. **Step 2 (The Trick):** The system takes the new word ("Paris") and **pastes it onto the end of your original question.**
   
   - New Input: *"What is the capital of France? Paris"*
   
   - The model runs the math again on this *new, longer* sequence.
   
   - It predicts the next likely token: **"is"**.

3. **Step 3:** The system appends "is".
   
   - New Input: *"What is the capital of France? Paris is"*
   
   - The model predicts: **"the"**.

4. **Step 4:** The system appends "the".
   
   - New Input: *"What is the capital of France? Paris is the"*
   
   - The model predicts: **"capital"**.

This loop repeats—predict, append, predict, append—<mark>until the model finally predicts a special invisible token called **[EOS]** (End of Sequence) or **[STOP]**. </mark>Once that token appears, the loop breaks, and the generation finishes.

### Why does it feel instantaneous?

Modern GPUs (Graphics Processing Units) and TPUs can perform this "predict and append" cycle hundreds of times per second. To you, the text flows out smoothly, but under the hood, the model is furiously re-reading the entire conversation plus the new word it just wrote, over and over again, for every single word it generates.

### The Memory Trick (KV Caching)

You might wonder: *"Does it really have to re-read the whole book every time it adds one word?"*

Ideally, yes, but that would be slow. To speed this up, engineers use **KV Caching (Key-Value Caching)**.

- The model remembers the mathematical "state" of the previous words.

- When generating word #50, it doesn't need to re-calculate words #1–49 from scratch; it just retrieves their calculated states from memory and only does the heavy lifting for the new word.

#### Auto-regressive token prediction

At its core, **auto-regressive token prediction** is the mechanism Large Language Models (LLMs) use to generate text one piece at a time.1 The term "auto-regressive" comes from statistics and simply means "predicting future values based on past values.

In plain English, the model reads what it has written so far to decide what to write next. Here is the step-by-step breakdown of how this process works inside an LLM.

### 1. The Core Loop

An LLM does not write a whole sentence at once.5 It writes the first word, reads it, writes the second word, reads *both*, and so on. This happens in a continuous loop:6

+1

1. **Input:** The model takes a sequence of text (the "context").7

2. **Prediction:** It calculates the probability of every possible next token (word or character chunk) in its vocabulary.8

3. **Selection:** It picks one token from those probabilities.9

4. **Update:** It adds that new token to the end of the sequence.10

5. **Repeat:** This new, longer sequence becomes the input for the next step.11

### 2. Under the Hood: From Math to Words

While the loop is simple, the decision-making process for *which* word to pick involves several mathematical steps.12

#### Step A: Processing the Context

When you type "The cat sat on the...", the model turns these words into numbers (embeddings) and passes them through its neural network (Transformer layers).13 The **Attention Mechanism** allows the model to look back at previous words to understand relationships (e.g., knowing "sat" relates to "cat").14

+1

#### Step B: Logits and Probabilities

At the very end of the network, the model produces a list of raw scores called **Logits** for every single word in its dictionary (which can be 50,000+ words).15

- **Logits:** Raw, unnormalized scores.16 (e.g., "mat": 15.2, "roof": 10.1, "banana": -5.0).

- **Softmax:** A mathematical function that squashes these logits into **probabilities** that add up to 100%.

| **Token**  | **Logit** | **Probability** |
| ---------- | --------- | --------------- |
| **mat**    | 15.2      | **85%**         |
| **rug**    | 12.1      | **10%**         |
| **floor**  | 8.5       | **4%**          |
| **banana** | -5.0      | **0.0001%**     |

#### Step C: Sampling (Making the Choice)

This is where the "personality" of the model comes in. The model doesn't always just pick the #1 most likely word (Greedy Decoding), as that can make text sound robotic and repetitive.17 Instead, it **samples** from the list.18

+1

- **Temperature:** A setting that adjusts the probabilities.19 High temperature (e.g., 1.0) flattens the curve, giving lower-probability words a higher chance of being picked (more creative/random).20 Low temperature (e.g., 0.1) sharpens the curve, making the #1 choice almost guaranteed (more deterministic/focused).21
  
  +1

- **Top-K / Top-P:** These settings force the model to only consider the top few options (e.g., "only look at the top 5 words") to prevent it from choosing something nonsensical like "banana" in the example above.

### 3. Why This Matters

Understanding this explains many behaviors of LLMs:

- **No Planning:** The model generally doesn't know how a sentence will end when it starts writing it.22 It is improvising word by word.23
  
  +1

- **Hallucinations:** If the model picks a slightly wrong token early on, the "auto-regressive" nature means it must now stick to that mistake and generate the next token based on it, often leading to a runaway error.24

- **Context Window Limits:** Since every new word is added to the input history, the input eventually becomes too long for the model to process, which is why LLMs have a maximum "context window" size.25

### Summary

1. **Read** text so far.

2. **Calculate** odds for the next word.26

3. **Roll the dice** (based on Temperature) to pick one word.

4. **Add** the word to the text.

5. **Repeat** until a "Stop" token is generated.27

### Self attention mechanism

Here is a technical deep dive into the **Self-Attention Mechanism** (specifically within a Transformer architecture).

To understand this technically, we must view the model not as a reader, but as a series of **vector matrix operations**. The "memory" is actually a process of **weighted aggregation** of information across the entire sequence.

### 1. The Setup: Embeddings & Positional Encoding

Before the attention mechanism starts, the input text is converted into a matrix $X$.

- **Token Embeddings:** Each token is turned into a high-dimensional vector (e.g., a list of 4,096 numbers).

- **Positional Encodings:** Since the attention mechanism treats all words simultaneously (permutation invariant), we must inject information about order. We add a positional vector to the token embedding so the model knows that "dog bites man" is different from "man bites dog."

### 2. The Linear Projections (The Learnable Part)

This is where the "intelligence" lives. For every token vector $x$, we apply three separate learned linear transformations (matrix multiplications) to project the input into three different subspaces.

We multiply the input $x$ by three weight matrices ($W_Q, W_K, W_V$) that were learned during training:

$Q = x \cdot W_Q \quad (\text{Query})$

$K = x \cdot W_K \quad (\text{Key})$

$V = x \cdot W_V \quad (\text{Value})$

- **Technical Note:** These projections allow the model to encode the token in three different ways for three different roles. The vector used to *ask* for context ($Q$) should be different from the vector used to *provide* context ($K$).

### 3. Scaled Dot-Product Attention (The Equation)

The core of the mechanism is defined by this specific formula:

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{Q K^T}{\sqrt{d_k}}\right) V$$

Let's break down the operations inside this formula:

#### A. The Dot Product ($Q K^T$)

We take the Query vector of the current token and perform a **Dot Product** with the Transposed Key vectors ($K^T$) of every other token in the sequence.

- **Geometric meaning:** The dot product measures the **cosine similarity** (alignment) between vectors.

- **Result:** A raw score indicating how "relevant" token A is to token B. If the vectors point in the same direction, the score is high (high relevance).

#### B. Scaling ($\frac{1}{\sqrt{d_k}}$)

We divide the raw scores by the square root of the dimension of the key vectors ($d_k$).

- **Why?** If the vectors are large, the dot products can become huge numbers. When fed into the Softmax function (next step), huge numbers cause **vanishing gradients** (the model stops learning effectively). Scaling keeps the variance stable.

#### C. Softmax

We apply the Softmax function to the scaled scores.

- **Result:** This converts raw scores (logits) into an **Attention Weight Distribution** (probabilities that sum to 1.0).

- **Interpretation:** "For the word 'Bank', pay 85% attention to 'River', 10% to 'The', and 5% to 'overflowed'."

### 4. The Weighted Sum (Context Integration)

Finally, we multiply these attention weights by the **Value ($V$)** vectors.

$$\text{Output} = \sum (\text{Attention Weight} \times V)$$

This is the critical "memory" step. The output for the token "Bank" is no longer just the vector for "Bank." It is a **weighted sum** of the vectors for "River", "Flooded", and "Bank" combined.

- **Information Flow:** The semantic meaning of "River" (contained in its $V$ vector) has effectively flowed into the representation of "Bank."

### 5. Multi-Head Attention (Parallel Subspaces)

Standard transformers don't just do this once; they use Multi-Head Attention.

The model splits the embedding dimension into multiple smaller "heads" (e.g., 8 or 12 heads). Each head has its own unique $W_Q, W_K, W_V$ matrices.

- **Head 1** might learn syntactic relationships (subject-verb agreement).

- **Head 2** might learn semantic relationships (synonyms).

- **Head 3** might learn causal relationships (if-then structures).

The outputs of all heads are concatenated and projected back to the original dimension.

### Summary of Technical Context Retention

The model "remembers" context because the mathematical representation of every token at layer $N$ is actually a **composite vector** containing information aggregated from every other relevant token at layer $N-1$.

By the time the signal passes through dozens of layers (Deep Learning), the final vector for the last token contains a rich, compressed "memory" of the entire preceding sequence, allowing the auto-regressive head to predict the next token accurately.

--- 

# Diffusion models

Diffusion models are a class of generative AI that work on a principle of **"systematic destruction and learned restoration."1**

While GANs (Generative Adversarial Networks) try to "trick" a discriminator, and VAEs (Variational Autoencoders) try to compress and decompress data, Diffusion models learn to reverse the flow of entropy.2

Here is the breakdown, starting with the intuition and moving into the architecture suitable for a data scientist.

### 1. The High-Level Intuition: "The Fog"

Imagine you have a clear photograph.

1. **Forward Process:** Over 1,000 steps, you add a tiny amount of static (Gaussian noise) to the image.3 By step 1,000, the image is destroyed; it is just pure random static.

2. **Reverse Process:** You train a neural network to look at step 1,000 (pure static) and predict what step 999 looked like. Then from 999, it predicts 998, and so on.

3. **Generation:** Once trained, you can give the model *new* random static it has never seen before, and it will "hallucinate" a clear image out of it by iteratively removing the noise.4

---

### 2. The Technical Workflow

The process is divided into two distinct phases: the fixed forward process (which has no learnable parameters) and the learnable reverse process.5

#### Phase A: Forward Diffusion (The Corruption)

We take a data sample 6$x_0$ (an image) and gradually add noise over 7$T$ timesteps.8

This is modeled as a Markov Chain.9 The transition from one step to the next is fixed and mathematically defined:

$$q(x_t | x_{t-1}) = \mathcal{N}(x_t; \sqrt{1 - \beta_t} x_{t-1}, \beta_t \mathbf{I})$$

- $\beta_t$ is the "noise schedule" (how much noise to add at each step).10

- Eventually, at 11$x_T$, the data is indistinguishable from isotropic Gaussian noise 12$\mathcal{N}(0, \mathbf{I})$.13

#### Phase B: Reverse Diffusion (The Denoising)

This is where the Deep Learning happens. We cannot mathematically reverse the noise because we lost information. So, we train a neural network to **approximate** the reverse distribution:

$$p_\theta(x_{t-1} | x_t) = \mathcal{N}(x_{t-1}; \mu_\theta(x_t, t), \Sigma_\theta(x_t, t))$$

- The network (14$\theta$) takes the noisy image 15$x_t$ and the current timestep 16$t$ as input.17

- **Crucially, the network does not predict the image directly.** It predicts the **noise** (18$\epsilon$) that was added to the image.19

- We then mathematically subtract that predicted noise to get a slightly cleaner image.20

### 3. The Architecture: U-Net and Attention

The neural network used for the reverse process is almost always a **U-Net**.21

1. **U-Net Backbone:** The noisy image is downsampled (compressed) into features and then upsampled (decompressed) back to the original size.

2. **Time Embedding:** Since the "amount of noise" changes at every step, the network needs to know which timestep 22$t$ it is looking at.23 A sinusoidal time embedding (similar to Transformers) is injected into the network.24

3. **Cross-Attention (The "Prompt"):** If this is a text-to-image model (like Stable Diffusion), the text prompt is tokenized (using CLIP or T5) and injected into the U-Net layers via Cross-Attention mechanisms.25 This "guides" the denoising so that when the model sees a vague shape in the noise, it resolves it into a "cat" rather than a "car" because the text prompt says "cat."26

### 4. Latent Diffusion (Why it's fast)

Early diffusion models (like Google's original papers) operated in **Pixel Space**. To generate a 1024x1024 image, the U-Net had to process 1024x1024 pixels at every single step (often 50-100 steps). This was computationally incredibly expensive.

**Stable Diffusion** introduced **Latent Diffusion Models (LDM)**:27

1. **Compression:** They use a VAE (Variational Autoencoder) to compress the image into a "Latent Space" (e.g., 64x64 vector representation) that preserves the *semantic* meaning but discards high-frequency pixel details.

2. **Diffusion:** The diffusion process (adding/removing noise) happens in this small 64x64 latent space. It is much faster.

3. **Decoding:** Once the latent noise is cleaned into a latent image, the VAE Decoder blows it back up to a high-resolution 1024x1024 pixel image.

### 5. Why is this relevant to AV (Autonomous Vehicles)?

Since you are looking at roles in AV simulation:

- **Scene Editing:** Diffusion is used to modify drive logs. You can take a daytime drive log, encode it, and use a diffusion model to "denoise" it back into a nighttime scene or a rainy scene while keeping the geometry (cars, roads) identical.

- **Corner Case Generation:** You can use diffusion to generate synthetic images of rare obstacles (e.g., "a kangaroo jumping on a highway") to train perception models on data that is hard to capture in reality.

---

# NeRFs vs. Gaussian Splatting

To understand **NuReC** (NVIDIA's Neural Reconstruction Engine), you need to understand the two core technologies it uses to turn flat video into 3D worlds: **NeRFs** and **3D Gaussian Splatting**.

Think of them as two different ways to "paint" a 3D world:

- NeRF (Neural Radiance Field): The "Voxel Fog" Approach
  
  Imagine a 3D block of air (a volume). For every tiny point in that air, you ask a Neural Network two questions: "Is there anything here?" (Density) and "What color is it if I look from this angle?" (Radiance). To make an image, you shoot a ray of light through this "fog." The neural network tells you how much light gets blocked or reflected at every step.
  
  - *Pros:* Incredible lighting details (reflections, transparency).
  
  - *Cons:* Very slow. The computer has to ask the neural network millions of questions just to render one frame.

- Gaussian Splatting: The "Fuzzy Blob" Approach
  
  Instead of a fog, imagine millions of tiny, translucent, colored 3D ellipsoids (like flattened footballs). Each blob has a position, a color, a size, and an orientation. To make an image, you just take all these blobs and "splat" them onto the screen. It’s like a point cloud, but instead of single hard dots, the points are fuzzy and blend together to form smooth surfaces.
  
  - *Pros:* Extremely fast. It doesn't need a neural network to *render*, it just needs a standard video card to draw shapes.
  
  - *Cons:* Can sometimes struggle with complex reflections (mirrors) compared to NeRF, though it is rapidly catching up.

---

### Technical Implementation Details

When NVIDIA NuReC runs on a drive log, it is performing an **Inverse Rendering** problem. It starts with the 2D answer (the video) and tries to calculate the 3D question (the scene).

#### 1. The NeRF Implementation (Older/High-Fidelity Path)

- **Input:** 3D Coordinates $(x, y, z)$ and Viewing Direction $(\theta, \phi)$.

- **The Network:** A simple Multi-Layer Perceptron (MLP) acts as the "scene memory." It is overfitted to *one specific scene*.

- **Ray Marching:** To render a pixel, the engine shoots a ray from the virtual camera. It samples hundreds of points along that ray.

- **Volumetric Rendering Equation:** It integrates the color and density along the ray to produce a final pixel color.

- **Training:** It compares the rendered pixel to the real pixel from the dashcam video. If they don't match, it backpropagates the error to update the MLP weights.

#### 2. The Gaussian Splatting Implementation (Newer/Real-Time Path)

- **Initialization:** It starts with a sparse point cloud (often from the AV's LiDAR or Structure-from-Motion data) to guess where "stuff" roughly is.

- **The Attributes:** Each Gaussian carries parameters:
  
  - **Mean ($\mu$):** Position in 3D space.
  
  - **Covariance ($\Sigma$):** The shape/stretch of the blob (is it a thin wall or a round ball?).
  
  - **Spherical Harmonics:** A mathematical way to store color that changes based on viewing angle (shiny things look different when you move).
  
  - **Opacity ($\alpha$):** How transparent it is.

- **Adaptive Density Control (ADC):** This is the "magic" step. During training, if the model sees a blurry area, it **splits** one big blob into two smaller ones. If it sees empty space with a useless blob, it **prunes** (deletes) it.

- **Rasterization:** Unlike NeRF's heavy ray-marching, 3DGS uses a tile-based rasterizer that sorts the blobs by depth and draws them instantly.

--- 

# Nvidia NuRec

While NeRFs and Gaussian Splatting are the *rendering techniques* (the "engine"), **NuReC** is the **end-to-end industrial pipeline** that wraps these techniques to turn messy real-world data into clean, usable simulation assets.

It solves the biggest problem with raw NeRFs: **The real world is full of moving junk (cars, pedestrians) that you don't want baked into your map.**

### The NuReC Pipeline: From Dashcam to Digital Twin

NuReC works in four distinct stages:

#### 1. Ingestion & Alignment (The "Sensor Fusion" Step)

NuReC doesn't just look at video; it looks at the **entire sensor stack** of the recording vehicle.

- **Inputs:** It takes synchronized streams from multiple cameras (front, side, rear), LiDAR point clouds, and the vehicle's highly accurate trajectory (IMU/GPS).

- **Pose Optimization:** Before it builds 3D geometry, it runs an optimization pass to ensure it knows *exactly* where every camera was for every millisecond of the drive. If the camera position is off by even a millimeter, the resulting 3D world will be blurry.

#### 2. Reconstruction (The "3D Gaussian" Step)

This is where the core technology we discussed earlier applies.

- It uses the optimized sensor data to train a **3D Gaussian Splatting** model (or NeRF) of the static environment.

- It builds the roads, buildings, trees, and traffic signs as millions of 3D blobs.

- **The Problem:** At this stage, the reconstruction also includes the "ghosts" of the cars and pedestrians that were driving next to you during the recording. If you used this for simulation, your AV would crash into these "ghost cars" that are frozen in time.

#### 3. The "Fixer" (The AI Cleanup Crew)

This is the specific value-add of NuReC over open-source tools. NVIDIA uses a secondary AI model (often a Transformer-based vision model or a Diffusion in-painting model) called the **NuReC Fixer**.

- **Dynamic Object Removal:** The AI identifies and **deletes** all moving objects (other cars, pedestrians) from the 3D scene.

- **In-Painting:** When you delete a car, you leave a "hole" in the road behind it. The Fixer "hallucinates" the missing road texture to fill in that hole, ensuring the pavement looks continuous.

- **Result:** You are left with a **clean, empty stage**—a perfect 3D replica of the city streets, but completely devoid of traffic.

#### 4. Export & Simulation (The "Interactive" Step)

Finally, the clean model is packaged for use.

- **USD Format:** The scene is exported as a **USD (Universal Scene Description)** file, the standard format for NVIDIA Omniverse.

- **Physics Layers:** NuReC doesn't just export visuals; it can align with HD Maps (OpenDRIVE) to add "invisible" physics layers. This ensures that when you put a *virtual* car into this scene, its tires interact with the road surface, not just the visual blobs.

#### 5. Inference

At **inference time**, NuReC is not "predicting" in the traditional sense (like a classifier predicting "cat"). Instead, inference refers to **Real-Time Neural Rendering**.

When you "run" NuReC in a simulator (like NVIDIA DRIVE Sim), the engine is asking the model: *"If a camera were at exactly these coordinates $(x, y, z)$ looking in this direction, what pixels would it see?"*

### 1. How NuReC Works at Inference Time (The Runtime Mechanics)

The process must happen incredibly fast (typically <10ms per frame) to keep up with the AV's "brain" in a Hardware-in-the-Loop (HIL) test.

- **The Query (The Trigger):** The simulator (e.g., CARLA or Isaac Sim) sends a "pose" (position and rotation) to the NuReC engine via an API (often gRPC).1

- **The Rasterization (The Action):**
  
  - If the model is **3D Gaussian Splatting**: The engine takes the millions of 3D colored blobs (Gaussians) and essentially "sorts" them based on their distance to the camera. It then projects them onto the 2D screen, blending their colors based on transparency. This happens on the GPU using a highly optimized rasterizer (faster than traditional game rendering).
  
  - If the model is **NeRF** (older/high-fidelity): The engine shoots "rays" from the virtual camera pixels into the 3D volume, querying the neural network for density and color at points along the ray. (This is often too slow for real-time, so Gaussian Splatting is preferred for inference).

- **The Output (The Result):** NuReC returns a **Synthetic Sensor Frame**. This isn't just a JPEG image; it is raw sensor data (e.g., GMSL camera packets) that is fed directly into the AV's computer, tricking the car into thinking it is seeing the real world.

**Key Technical Enabler:** NVIDIA caches the heavy neural processing into a format (like USD) that allows the inference to be just a "sorting and projecting" task rather than a "deep learning" task, enabling **100+ FPS** performance.

---

### 2. The Core Use Cases

Why go through the trouble of Neural Reconstruction instead of just using a game engine like Unreal Engine 5?

#### A. Closed-Loop "Resimulation" (The Safety Killer)

This is the #1 money-maker use case.

- **Scenario:** A real AV disengages (driver grabs the wheel) because a van cut it off.

- **The NuReC Workflow:**
  
  1. The logs from that real drive are fed into NuReC to build a 3D digital twin of that exact highway stretch.2
  
  2. The "van" is removed (using the Fixer) and replaced with a *virtual* van.
  
  3. **Inference:** You now run the simulation 1,000 times, tweaking the virtual van's speed and aggression to see if your *new* AV software code can handle the cut-off safely.

- **Why NuReC?** The road geometry, lane lines, and visual clutter (trees, barriers) are **pixel-perfect matches** to the real world, so the test is valid. A "hand-made" game world is never accurate enough to debug specific sensor failures.

#### B. Data Augmentation (Training Perception)

You need to train your car to detect children running into the street, but you can't film that in real life.

- **Workflow:** You take a NuReC scan of a quiet suburban street. You insert a 3D asset of a child running.

- **Inference:** You render 10,000 frames of this scene from different angles and lighting conditions.

- **Value:** You generate "Synthetic Training Data" for your perception models (YOLO/Transformer) to learn from dangerous scenarios that rarely happen in reality.

#### C. Auto-Labeling (Ground Truth Generation)

Labeling data (drawing boxes around cars) is expensive and slow.

- **Workflow:** Since NuReC builds the world in 3D, it *knows* what every object is (road, tree, sky).

- **Inference:** When NuReC renders the RGB image (for the car to look at), it can simultaneously render a **Semantic Segmentation Mask** (a color-coded map where pink=road, blue=sky).

- **Value:** You get pixel-perfect labels for free, instantly, without paying humans to click points.

#### D. Sensor Layout Validation

- **Scenario:** An OEM wants to move the LiDAR from the roof to the bumper.

- **Workflow:** Instead of building a prototype car, they load a NuReC world and move the *virtual* sensor to the bumper.

- **Inference:** They check the simulated camera/LiDAR feeds. "Oh, the bumper blocks the view of the curb."

- **Value:** They save millions by finding hardware mistakes before bending metal.

**For developers working on autonomous vehicle software, the open-source CARLA simulator supports NuRec. When you
run the NuRec launcher script, it loads a curated set of pre-reconstructed scenes from the nvidia physical AI dataset and renders them in CARLA replay thru an integration with the nurec gRPC API**

NVIDIA’s business model for autonomous driving (AD) is a **"full-stack" ecosystem play**.1 They do not just sell chips; they sell the infrastructure to develop, train, and deploy AI.2

Regarding **NuReC** specifically: It is not a standalone consumer product but a **development tool** within the NVIDIA Omniverse ecosystem.3

Here is the breakdown of the business model behind NuReC and the broader AD software suite.

### NVIDIA NuReC: Accuracy & Runtime Specs

NVIDIA NuReC (Neural Reconstruction) is essentially an enterprise-grade wrapper around these techniques, optimized for the automotive use case.

#### Accuracy: "Perception-Grade" vs. "Visual-Grade"

NuReC models are tuned for **metric accuracy** rather than just "looking good."

- **Geometric Accuracy:** Because NuReC often uses LiDAR data to initialize the Gaussians/NeRF, the static geometry (buildings, road surface) is typically accurate to within **<5 cm** of the real world. This is critical because you are testing if a car stays in its lane; if the lane is 10cm off, the simulation is useless.

- **Photometric Accuracy (PSNR):** NuReC models typically achieve a Peak Signal-to-Noise Ratio (PSNR) of **30dB+**, which is considered high quality.

- **Artifacts:** A common issue is "floaters" (ghostly blobs in the air) or dynamic objects (a walking pedestrian getting frozen into the static background). NuReC uses a "Fixer" model (a Transformer-based in-painting tool) to remove dynamic objects (cars/people) from the background so you have a clean, empty stage to run your simulation in.

#### Runtime: The "Real-Time" Requirement

This is where the business model (Omniverse/DGX) meets the tech.

- **Training Time (The Cost):** Creating *one* Digital Twin of a complex intersection used to take days with NeRF. With 3D Gaussian Splatting on NVIDIA DGX Cloud (H100 GPUs), a scene can now be reconstructed in **minutes to roughly 1 hour** depending on the size (e.g., a 2km stretch of highway).

- **Inference Time (The Value):** This is critical for **Hardware-in-the-Loop (HIL)** simulation.
  
  - **NeRF:** Runs at ~1-5 FPS (Frames Per Second) natively. Too slow for a car computer that needs data at 30Hz.
  
  - **Gaussian Splatting (NuReC):** Runs at **100+ FPS** at 1080p/4K resolution.
  
  - **Why this matters:** The AV stack (the brain of the car) expects camera frames every 33 milliseconds. If the simulation lags, the AV stack crashes. NuReC using Gaussian Splatting is fast enough to feed "fake" camera data to the real car computer in real-time.
  
  - 

### 1. The Value Proposition

**NuReC** stands for **Neural Reconstruction**.4 It is an AI toolset that takes raw sensor data (video, LiDAR) from real-world drives and automatically reconstructs it into a 3D, interactive simulation environment (a "Digital Twin").5

- **The Problem it Solves:** Manually building 3D simulation worlds is slow and expensive. NuReC automates this, allowing automakers to turn one real-world drive into infinite simulated test scenarios.6

- **Where it fits:** It is part of **NVIDIA Omniverse** and feeds into **DRIVE Sim**.7

### 2. The Business Model: "Hardware as the Trojan Horse, Software as the Rent"

NVIDIA's AD revenue comes from three distinct layers. NuReC falls into the "Development & Training" layer.

#### Layer A: Development & Training (Where NuReC Lives)

- **Customer:** Automakers (OEMs like Mercedes, JLR), Tier 1 suppliers (Bosch), and AV startups (Zoox, Waabi).8

- **Model:** **Enterprise Subscription & Cloud Usage.9**
  
  - **Omniverse Enterprise:** To use tools like NuReC or DRIVE Sim, companies pay substantial licensing fees for the Omniverse platform.
  
  - **DGX Cloud / Compute:** Reconstructing 3D worlds using neural networks (NeRFs/Gaussian Splatting) requires massive computing power.10 NVIDIA monetizes the *compute* time used to run NuReC, often selling access to their DGX Cloud supercomputers.
  
  - **Data Generation:** By selling the tool that generates synthetic training data, NVIDIA ensures automakers need *more* NVIDIA GPUs to train their models on that data.

#### Layer B: In-Vehicle Compute (The Hardware Anchor)

- **Customer:** OEMs (buying parts for production cars).

- **Model:** **Direct Hardware Sales.**
  
  - NVIDIA sells the "brain" of the car (e.g., **NVIDIA DRIVE Orin** or **Thor** SoCs).11
  
  - This is the traditional "one-off" sale, but it locks the car into NVIDIA's software architecture (CUDA).

#### Layer C: In-Vehicle Software (The Recurring Revenue)

- **Customer:** OEMs and End-Consumers.

- **Model:** **Licensing & Revenue Share.**
  
  - **The Stack:** NVIDIA offers a full software stack called **DRIVE OS**, **DriveWorks**, and applications like **DRIVE Chauffeur** (AI driving) and **DRIVE Concierge** (AI cockpit).
  
  - **Revenue Share:** For some partners (like Mercedes-Benz), NVIDIA has moved to a **revenue-sharing model**. If a car owner pays a subscription for "Level 3 Autonomy" on their Mercedes, NVIDIA takes a percentage of that recurring fee (often termed a "software-defined vehicle" agreement).

### 3. The "Flywheel" Strategy

NVIDIA’s goal is to become the unavoidable operating system of the car. NuReC is a strategic piece of this flywheel:

1. **Capture:** Real cars (running NVIDIA hardware) collect data.

2. **Reconstruct (NuReC):** That data is processed (on NVIDIA Cloud) to create simulations.

3. **Train:** New AI models are trained (on NVIDIA DGX) inside those simulations.

4. **Deploy:** The improved AI is flashed back to the car (running NVIDIA Orin/Thor).

### Summary Table

| **Product**         | **Category**     | **Business Model**                                                                              |
| ------------------- | ---------------- | ----------------------------------------------------------------------------------------------- |
| **NuReC**           | Development Tool | **SaaS / Enterprise License** (Part of Omniverse/Isaac/DRIVE Sim) + **Cloud Compute Fees**.     |
| **DRIVE Orin/Thor** | Hardware (SoC)   | **Unit Sales** (Traditional hardware margin).                                                   |
| **DRIVE Chauffeur** | In-Car Software  | **Recurring Licensing** or **Revenue Share** (NVIDIA takes a cut of the driver's subscription). |
| **DGX Cloud**       | Infrastructure   | **Usage-based / "AI Factory"** rental fees for training models.                                 |

**The Bottom Line:** NVIDIA doesn't just want to sell the chip in the dashboard; they want to monetize the entire lifecycle of the car's intelligence—from the server rack where the AI is born (using tools like NuReC) to the monthly subscription the driver pays for autopilot features.

---

# KV Cache Hits 🎯 vs. Misses ⛔ in LLM Inference

In long-context use-cases, the KV cache is essentially a high-value memory pool the model queries on every incoming token. And the difference between a hit and a miss is where major prefill performance is won or lost.  

🎯Cache Hit: The required K/V tensors are already resident in the pool.  
The attention block performs a fast read → no recompute, lower latency.  

⛔Cache Miss: The tensors aren’t in the pool. Either they were never cached or were evicted due to memory pressure. The model must regenerate them → added compute, higher latency, and potential evictions of older entries.  

Scale this over millions of tokens in prefill and the hit rate becomes multiplicative. High hit rates collapse attention cost; low ones turn prefill into a major bottleneck for long-context use-cases.  

Bottom line: In prefill, you're either doing cheap memory lookups… or paying the K/V compute price. Hit rate decides which world you live in.

![diagram](https://media.licdn.com/dms/image/v2/D5622AQEfD1-ea-eLGg/feedshare-shrink_800/B56ZsT_cFKIEAg-/0/1765566956662?e=1767225600&v=beta&t=Q7PKT829pIo7eUieWuziwDJF90fd7-9KaCUcvcKANUc)

# Chain of Thought

To understand how **Chain of Thought (CoT)** is implemented "in reality," you have to look at it from two different perspectives: the **Model User** (how you implement it via API/prompt) and the **Model Creator** (how it is baked into the model via training).

In reality, CoT is rarely a change to the "physical" architecture of the model (the neural network layers usually remain the same). Instead, it is a manipulation of the **data flow** and **token sequence**.

Here is the detailed breakdown of how CoT is actually implemented.

---

### 1. The Inference Layer (How it works at Runtime)

When you use a model like GPT-4 or Claude, CoT is implemented purely as **text injection**. The model does not have a separate "reasoning brain"; it simply predicts the next word. CoT works by effectively "hacking" the autoregressive nature of the LLM.

#### The Mechanism: "Compute via Tokens"

An LLM has a fixed amount of computation it can do *per token*. If you ask a complex question and demand an immediate answer, the model has to solve the logic, math, and syntax all in a single forward pass.

- **Without CoT:** Input $\rightarrow$ [1 forward pass] $\rightarrow$ Output "42".

- **With CoT:** Input $\rightarrow$ [Forward pass 1] $\rightarrow$ "First," $\rightarrow$ [Forward pass 2] $\rightarrow$ "we" $\rightarrow$ ... $\rightarrow$ "42".

By forcing the model to generate 100 tokens of reasoning before the answer, you are granting it 100x more "compute time" (forward passes) to process the problem.

#### The "Zero-Shot" Implementation (Trigger Phrases)

This is the simplest implementation, famously discovered by Kojima et al. (2022). It involves appending a specific string to the input.

- **Implementation:** You concatenate the string `"\nLet's think step by step."` to the user's prompt.1

- **Reality:** This string shifts the probability distribution of the next token. In the model's training data (textbooks, Stack Overflow), the phrase "step by step" is usually followed by a logical derivation. The model mimics this pattern.2

#### The "Few-Shot" Implementation (In-Context Learning)

This is the standard engineering implementation. You prepend "exemplars" (examples) to the prompt context window.

**Structure of the Input sent to the API:**

Plaintext

```
Q: Roger has 5 tennis balls. He buys 2 more cans of tennis balls. Each can has 3 tennis balls. How many does he have now?
A: Roger started with 5 balls. 2 cans * 3 balls = 6 new balls. 5 + 6 = 11. The answer is 11.
###
Q: [User Input]
A: 
```

**Reality:** The model attends to the previous examples via its **Self-Attention Mechanism**. It copies the *structure* of the reasoning (Breakdown $\rightarrow$ Calculation $\rightarrow$ Answer) and applies it to the new `[User Input]`.

---

### 2. The Training Layer (How it is "baked in")

Modern models (like Llama 3, Orca, or GPT-4) don't just rely on you asking them to think; they are **fine-tuned** to do it automatically. This is the "hard" implementation.

#### Dataset Curation (The "CoT Collection")

Developers create massive datasets specifically for CoT. They don't just scrape the web; they synthetically generate reasoning chains.

1. **Question:** "Is a dove a mammal?"

2. **Standard Label:** "No."

3. **CoT Label:** "A dove is a bird. Birds lay eggs and have feathers. Mammals give birth to live young and have fur. Therefore, a dove is not a mammal. Answer: No."

#### Instruction Tuning (SFT)

During the Supervised Fine-Tuning (SFT) phase, the model is penalized if it jumps straight to the answer. The loss function is calculated on the *reasoning tokens* as well as the *answer tokens*.

- **Implementation:** The model weights are updated to maximize the probability of the *explanation* sequence.

- **Result:** When you ask a question later, the model's internal probability distribution now favors outputting the "explanation" tokens first, even without a "Let's think step by step" prompt.

---

### 3. The "System" Implementation (The Hidden Layer)

When you use ChatGPT or Claude via their web interfaces, there is often an invisible layer of CoT implementation known as **System Prompt Injection**.

Before your message reaches the model, the backend wraps your prompt in a meta-template.

- **Hidden System Prompt:** `You are a helpful assistant. When asked a math or logic question, you must break down the problem step-by-step before answering.`

- **User sees:** Just the answer.

The "Hidden Chain" (New Frontier):

Newer "reasoning models" (like OpenAI's o1 series or research like Quiet-STaR) implement a more radical version:

1. **Hidden Tokens:** The model generates reasoning tokens that are visible to the system but *hidden* from the user.

2. **Reinforcement Learning:** The model is trained using Reinforcement Learning (RL) where the reward is given only for the correct final answer, but the model is allowed to generate "thought tokens" in between to get there.

3. **Implementation:** The inference engine runs the model until it outputs a special `<end_of_thought>` token, filters out the thought text, and streams only the result to the user.

---

### 4. Advanced: Program-Aided CoT (PAL)

In high-reliability implementations (e.g., inside financial agents), CoT is implemented not as text, but as **code**.

- **Prompt:** "Write a Python script to solve this step by step."

- **Implementation:**
  
  1. Model generates Python code (The "Chain of Thought").
  
  2. System halts generation.
  
  3. System executes Python code in a sandbox.
  
  4. System appends the result to the context.
  
  5. Model generates the final answer based on the code execution.

### Summary Table: Implementation Types

| **Type**       | **Where it lives** | **How it works**                                                      |
| -------------- | ------------------ | --------------------------------------------------------------------- |
| **Zero-Shot**  | Prompt String      | Appending "Let's think step by step".                                 |
| **Few-Shot**   | Context Window     | Pre-pending Q&A examples with reasoning steps.                        |
| **Fine-Tuned** | Model Weights      | Training on datasets (like FLAN or Orca) containing reasoning traces. |
| **System 2**   | Inference Engine   | Hiding "thought tokens" from the user (e.g., OpenAI o1, Quiet-STaR).  |
