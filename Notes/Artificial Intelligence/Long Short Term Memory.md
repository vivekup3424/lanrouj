### What is LSTM?

LSTM is a type of Recurrent Neural Network (RNN) designed to overcome the **vanishing gradient problem** encountered during training of standard RNNs. It can **learn long-term dependencies** in sequence data, making it suitable for tasks like time-series prediction, language modeling, and speech recognition.

LSTM introduces **gates** to control the flow of information, enabling it to retain or forget information over long periods.

---

### LSTM Architecture
![[Pasted image 20241124213302.png]]

An LSTM cell consists of the following key components:

1. **Cell State ($C_t$)**:
    - The **long memory** of the cell that carries information across time steps.
    - Callled as cell state
    
> [!NOTE]
> On the basis of $x_{t}$ you decide what to remove from cell state or add to cell state.
> All the values are vectors here.



2. **Hidden State ($h_t$)**:
    - Also called as short-term memory
    - Represents the **current output of the cell** and is passed to the next time step.

3. **Input Gate ($i_t$)**:
    - Controls *how much of the new input should be written to the cell state.*

4. **Forget Gate ($f_t$)**:
    - Decides *what information to forget from the cell state.*

5. **Output Gate ($o_t$)**:
    - Determines the output based on the cell state.

6. **Candidate State ($\tilde{C}_t$)**:
    - A potential update to the cell state based on the input and hidden state.
    
![[Pasted image 20241124214212.png]]
---

### LSTM Equations

At each time step $t$, the LSTM performs the following computations:

1. **Forget Gate**:  
![[Pasted image 20241124230003.png|300]]
   Determines which parts of the previous cell state to forget:  
   $$f_t = \sigma(W_f \cdot [h_{t-1}, x_t] + b_f)$$

2. **Input Gate**:  
   Decides what new information to store in the cell state:  
   
   ![[Pasted image 20241124230231.png|300]]
   
   
   
   
   $$i_t = \sigma(W_i \cdot [h_{t-1}, x_t] + b_i)$$
     
   Compute the candidate state:  
   $$\tilde{C}_t = \tanh(W_C \cdot [h_{t-1}, x_t] + b_C)$$

3. **Update Cell State**:  
   Combine old and new information:  
   $$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$$

4. **Output Gate**:  
   Compute the output and update the hidden state:  
   
   ![[Pasted image 20241124230730.png|300]]
   
   
   $$o_t = \sigma(W_o \cdot [h_{t-1}, x_t] + b_o)$$  
   $$h_t = o_t \odot \tanh(C_t)$$

Where:
- $\sigma$ is the sigmoid activation function.
- $\odot$ is element-wise multiplication.

---

### Key Features of LSTM

1. **Memory Capability**:  
   LSTM can retain long-term dependencies due to the cell state.

2. **Gating Mechanisms**:  
   Gates control the flow of information, enabling the network to learn when to remember or forget.

3. **Avoids Vanishing Gradients**:  
   Gradients flow more effectively through the cell state, allowing the network to learn long-term dependencies.

---

### Advantages of LSTM

1. Captures both long-term and short-term dependencies in data.
2. Effective for tasks with sequential data, such as time-series forecasting, speech recognition, and language translation.
3. Handles gradient problems better than vanilla RNNs.

---

### Limitations of LSTM

1. **Computational Complexity**:
   - LSTMs are computationally expensive due to their internal structure.
   - ![[Pasted image 20241124212239.png]]
   
1. **Training Time**:
   - Longer training times compared to simpler architectures.
2. **Overfitting**:
   - Tends to overfit if not regularized, especially with small datasets.

---

### Applications of LSTM

1. **Natural Language Processing (NLP)**:
   - Sentiment analysis, machine translation, and text generation.
2. **Speech Recognition**:
   - Sequence-to-sequence modeling for audio data.
3. **Time-Series Analysis**:
   - Stock price prediction, weather forecasting, and sensor data analysis.
4. **Anomaly Detection**:
   - Detecting outliers in sequential data.


