![[Pasted image 20241014055221.png]]

We are doing parameter sharing here, shared weights have equal value

## What is Parameter Sharing in RNNs?

Parameter sharing in Recurrent Neural Networks (RNNs) refers to the use of the same set of weights across all time steps in the network. This means that the parameters (weights and biases) that transform the input and the hidden state at one time step are reused at all other time steps.

---

### Why Do We Use Parameter Sharing?

1. **Efficiency**: It significantly reduces the number of parameters, making the model computationally and memory-efficient.
2. **Generalization**: It helps the model generalize better by enforcing a temporal consistency, as the same transformation is applied across time steps.
3. **Sequence Learning**: It captures patterns in sequential data, such as speech, text, or time series, by processing inputs in a recurrent manner.

---

### How Does It Work?

In RNNs, for each time step tt, the following equations are used:

1. **Hidden State Update**:  
    $$
    h_t=f(W_h h_{t-1}+W_{x}x_{t}+b)
    $$
    where:
    - $W_h$: Recurrent weight matrix (shared across all time steps).
    - $W_x$: Input weight matrix (shared across all time steps).
    - b : Bias (shared across all time steps).
    - f : Activation function.
2. **Output**:  
    $$y_t=g(W_yh_{t}+c)$$
    where $W_y$ and c are also shared.

---

### Where Can Engineers Encounter It?

1. **Natural Language Processing (NLP)**: Sentiment analysis, machine translation, and text generation.
2. **Time-Series Analysis**: Forecasting stock prices, weather prediction.
3. **Speech Recognition**: Sequence-to-sequence models.
4. **Reinforcement Learning**: In agents for sequential decision-making.

---

## What is Backpropagation Through Time (BPTT)?

**Backpropagation Through Time (BPTT)** is the algorithm used to train Recurrent Neural Networks (RNNs). It extends standard backpropagation to account for the sequential nature of RNNs by unrolling the network over all time steps and computing gradients for each step. These gradients are then used to update the shared weights of the RNN.

---

### How Does It Work?

1. **Unrolling the RNN**:  
    The RNN is "unrolled" for a fixed number of time steps (or the entire sequence) into a feedforward-like network.
    
    At each time step tt, the network computes:
    
	- Hidden state:  
	  $h_t = f(W_h h_{t-1} + W_x x_t + b)$  
	- Output:  
	  $y_t = g(W_y h_t + c)$


2. **Loss Computation**:  
    The total loss is calculated as the sum over all time steps:
    $L = \sum_{t=1}^{T} L_t$
    1. **Backward Pass**:  
    Gradients are calculated backward through the unrolled network:
    
    - Gradients are propagated backward through time from $t = T$ to $t = 1$.
    - At each time step, partial derivatives of the loss with respect to $W_h$, $W_x$, $b$, and other shared parameters are computed.

2. **Weight Update**:  
    Once the gradients are calculated, weights are updated using gradient descent (or a variant):
    
    $$W \leftarrow W - \eta \cdot \frac{\partial L}{\partial W}$$
    
    Here, $\eta$ is the learning rate.

---

### How Do Shared Weights Get Updated?

Since the weights $W_h$, $W_x$, $W_y$, and biases $b$, $c$ are shared across time steps:

1. Gradients for these parameters are accumulated across all time steps:  
    $$\frac{\partial L}{\partial W} = \sum_{t=1}^{T} \frac{\partial L_t}{\partial W}$$
2. The accumulated gradients are used to update the shared parameters once after the backward pass.

---

### Limitations of BPTT

1. **Vanishing and Exploding Gradients**:
    - For long sequences, gradients can diminish (vanishing gradients) or grow uncontrollably (exploding gradients), making it difficult to train the network effectively.
    - **Mitigation**: Use variants like LSTM or GRU and gradient clipping.

2. **High Computational Cost**:
    - Unrolling and backpropagating through many time steps require significant memory and computation, making BPTT slow for long sequences.

3. **Difficulty in Capturing Long-Term Dependencies**:
    - Due to vanishing gradients, RNNs struggle to learn long-term dependencies in data.

4. **Truncation Issues**:
    - Often, BPTT is truncated to a fixed number of steps (Truncated BPTT), which can limit the network's ability to capture dependencies across distant time steps.

5. **Online or Real-Time Scenarios**:
    - BPTT is not well-suited for online learning since it requires the entire sequence to compute gradients.

---

### Practical Improvements

1. **LSTMs and GRUs**:
    - Replace vanilla RNNs with LSTMs or GRUs to handle long-term dependencies better.

2. **Gradient Clipping**:
    - Limit the magnitude of gradients during backpropagation to prevent exploding gradients.

3. **Truncated BPTT**:
    - Process a fixed number of time steps to reduce computational overhead:
        - Example: Instead of unrolling $T$ steps, unroll $k$ steps where $k \ll T$.

4. **Optimizers**:
    - Use advanced optimizers like Adam to speed up convergence and stabilize training.

## Teacher Forcing in RNNs

### What is Teacher Forcing?

**Teacher Forcing** is a training strategy for Recurrent Neural Networks (RNNs) where the actual target output from the training data at the current time step is used as the input for the next time step, instead of the output generated by the model.

In standard RNN training, the model predicts the next output based on its own previous predictions, which can lead to compounding errors if early predictions are incorrect. Teacher forcing mitigates this issue by "forcing" the model to use the ground truth data during training.

---

### How Does It Work?

1. At each time step $t$:
    - The model takes the current input $x_t$ and the hidden state $h_{t-1}$ to predict the output $\hat{y}_t$.
    - During training, instead of feeding $\hat{y}_t$ to the next step, the ground truth value $y_t$ is fed as the next input.

2. The loss is calculated based on the difference between the predicted output $\hat{y}_t$ and the ground truth $y_t$.

---

### Why is It an Improvement Over BPTT?

1. **Faster Convergence**:
    - Teacher forcing helps the model learn more quickly by directly exposing it to the correct sequence during training, reducing the error accumulation seen in standard BPTT.

2. **Reduction in Gradient Vanishing/Exploding Issues**:
    - Since the model is trained using the ground truth at each step, the compounding of incorrect predictions is avoided, leading to more stable gradients.

3. **Improved Learning of Short-Term Dependencies**:
    - By providing the true target at every step, the model focuses on learning short-term patterns more effectively.

---

### Limitations of Teacher Forcing

1. **Exposure Bias**:
    - During inference, the model no longer has access to the ground truth and must rely on its own predictions. This mismatch between training and inference can lead to errors during deployment.

2. **Difficulty in Capturing Long-Term Dependencies**:
    - While it improves short-term predictions, teacher forcing does not inherently address the vanishing gradient problem for long-term dependencies.

---

### Practical Use and Implementation

Teacher forcing is typically used during the training phase, while during inference, the model generates its own outputs sequentially without access to the ground truth.

---

### Code Example of Teacher Forcing

```python
import torch
import torch.nn as nn

# Define RNN model
class RNN(nn.Module):
    def __init__(self, input_size, hidden_size, output_size):
        super(RNN, self).__init__()
        self.rnn = nn.RNN(input_size, hidden_size, batch_first=True)
        self.fc = nn.Linear(hidden_size, output_size)
    
    def forward(self, x, h):
        out, h = self.rnn(x, h)
        out = self.fc(out)
        return out, h

# Initialize model, criterion, and optimizer
model = RNN(input_size=10, hidden_size=20, output_size=10)
criterion = nn.MSELoss()
optimizer = torch.optim.Adam(model.parameters(), lr=0.01)

# Sample data
inputs = torch.randn(5, 10, 10)  # Batch size=5, Sequence length=10, Input size=10
targets = torch.randn(5, 10, 10)

# Training with teacher forcing
h = None
for epoch in range(10):  # Number of epochs
    optimizer.zero_grad()
    outputs, h = model(inputs, h)
    
    # Use teacher forcing: feed ground truth instead of predicted output
    loss = criterion(outputs, targets)
    loss.backward()
    optimizer.step()
    print(f"Epoch {epoch + 1}, Loss: {loss.item()}")
