1. We can't use ANN for sequential data, because the size of data input for a time-series data is not definite, its polynomial.

### Summary Table

| **Aspect**                | **ANN**                                | **RNN**                                      |
|---------------------------|----------------------------------------|----------------------------------------------|
| **Sequence Handling**      | No built-in ability for sequences      | Designed for sequential data                 |
| **Variable-Length Input**  | Requires fixed-length input            | Can handle variable-length input sequences   |
| **Temporal Dependencies**  | Can’t capture temporal dependencies    | Captures short- and long-term dependencies   |
| **Context Awareness**      | Treats inputs independently            | Maintains context across time steps          |
| **Parameter Efficiency**   | Different parameters per input         | Shares parameters across time steps          |
| **Efficiency**             | Inefficient for sequences              | Efficient for processing sequences           |

---


**RNNs** are much better suited than **ANNs** for tasks that involve sequences of data or temporal dependencies because they are specifically designed to remember and use past inputs when making predictions. This makes RNNs the go-to architecture for tasks like speech recognition, language modeling, and time series forecasting, where order and context are crucial.
