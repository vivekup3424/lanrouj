Let's break down how we calculate the output dimensions after applying a convolutional layer, step by step, using the details you provided for AlexNet's first convolutional layer.

### **Convolutional Layer Formula**:

For a given convolutional layer, the output dimensions ($H_{out} \times W_{out}$) can be calculated using the following formulas:

$$
H_{out} = \left( \frac{H_{in} - K + 2P}{S} \right) + 1
$$
$$
W_{out} = \left( \frac{W_{in} - K + 2P}{S} \right) + 1
$$

Where:
- $H_{in}$ and $W_{in}$ are the height and width of the input image, respectively.
- $K$ is the size of the kernel (filter).
- $P$ is the amount of **padding**.
- $S$ is the **stride** (how much the filter moves at each step).
- $H_{out}$ and $W_{out}$ are the height and width of the output image after the convolution.

### **Given Information** for AlexNet's First Convolutional Layer:
- **Input Image Dimensions**: $ 227 \times 227 \times 3 $ (RGB image).
    - $H_{in} = 227$
    - $W_{in} = 227$
    - 3 color channels (RGB), but the formula for height and width doesn't depend on the number of channels.

- **Kernel Size** ($K$): 11x11 (square kernel).
    - $K = 11$

- **Stride** ($S$): 4.
    - $S = 4$

- **Padding** ($P$): Usually, padding is chosen to ensure the output feature map has a reasonable size. For AlexNet's first convolutional layer, we typically apply **valid padding**, which means no padding. So, $ P = 0 $.

- **Number of Filters**: 96 filters.
    - The number of filters doesn't affect the spatial dimensions (height and width) of the output. It only changes the depth of the output (i.e., the number of channels).

---

### **Calculating Output Dimensions**:

#### Step 1: Calculate Output Height ($H_{out}$)
$$
H_{out} = \left( \frac{227 - 11 + 2(0)}{4} \right) + 1
$$
$$
H_{out} = \left( \frac{227 - 11}{4} \right) + 1
$$
$$
H_{out} = \left( \frac{216}{4} \right) + 1
$$
$$
H_{out} = 54 + 1 = 55
$$

#### Step 2: Calculate Output Width ($W_{out}$)
Since the input image is square, the width calculation will be the same as the height calculation:
$$
W_{out} = 55
$$

#### Step 3: Output Depth (Number of Channels)
The output depth is equal to the number of filters used in the convolution:
$$
\text{Output Depth} = 96
$$

---

### **Final Output Dimensions**:
The output of the first convolutional layer will be:
$$
55 \times 55 \times 96
$$

This means:
- The height and width of the output feature map are **55x55**.
- The depth (number of feature maps) is **96** because we used **96 filters**.

### **Summary**:

The dimensions of the output after the first convolutional layer are calculated by applying the formula for the height and width, considering the kernel size, stride, and padding. The depth of the output is simply the number of filters used in that layer.
