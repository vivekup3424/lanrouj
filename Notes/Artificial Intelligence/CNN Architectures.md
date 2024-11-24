# CNN with sliding window
### CNN with Sliding Window

A **Convolutional Neural Network (CNN)** with a **sliding window** approach is used when you want to apply a CNN to detect objects or patterns in an image by analyzing smaller portions (or windows) of the image rather than processing the entire image as a whole. 

> [!NOTE]
>  This approach was widely used before modern object detection methods like YOLO and Faster R-CNN became popular.

![[Pasted image 20241123195933.png]]

---

### **What is the Sliding Window Approach?**
The **sliding window** technique involves dividing an image into smaller regions or patches using a window of fixed size. This window is "slid" across the image, typically with some overlap, and a classifier (like a CNN) is applied to detect patterns in each patch.

---

### **How it Works in CNNs**
1. **Define a Window Size**:
   - Decide on a fixed size for the window (e.g., $64 \times 64$ or $128 \times 128$).
   - This window size should match the input size expected by the CNN.

2. **Slide the Window Across the Image**:
   - Move the window across the image, both horizontally and vertically, with a fixed **stride** (e.g., 8, 16, or 32 pixels).
   - For each position, extract the patch of the image covered by the window.

3. **Pass Each Patch Through the CNN**:
   - Feed the patch into the CNN to classify or detect objects within that patch.

4. **Aggregate Results**:
   - After processing all patches, aggregate the CNN’s outputs to determine if and where objects are detected in the image.
   - This aggregation could involve:
     - Non-Maximum Suppression (NMS) to eliminate redundant detections.
     - Combining overlapping results to refine the prediction.

---

### **Advantages**
1. **Localized Detection**:
   - Enables the CNN to focus on smaller regions of the image for localized object detection.
   
2. **Straightforward Approach**:
   - Works with any standard CNN architecture without modifications.

---

### **Disadvantages**
1. Computationally Expensive
2. Fixed Window Size
3. Overlapping windows lead to redundant computations

---

### **Applications**
1. **Object Detection (Traditional)**:
   - Before modern methods like YOLO or Faster R-CNN, sliding windows were used to detect objects in images.
   
2. **Face Detection**:
   - Early face detection systems used sliding windows with CNNs to locate faces.

3. **Scene Analysis**:
   - Detecting specific features or patterns in specific regions of an image.


---

### **Example of Sliding Window in CNN**
Let’s assume we have a $512 \times 512$ image and a CNN that expects $64 \times 64$ input patches:
1. Window size: $64 \times 64$.
2. Stride: $32$ pixels (50% overlap).
3. Total patches to process:
   - Horizontally: $\frac{512 - 64}{32} + 1 = 15$.
   - Vertically: $15$.
   - Total patches: $15 \times 15 = 225$.

For each of these 225 patches, the CNN is run independently, and the outputs are combined.

---
# **U-Net**

U-Net is a convolutional neural network architecture specifically designed for **image segmentation**, where the goal is to classify each pixel of an image into a category. Developed in 2015 for *biomedical image segmentation*, it has since become one of the most popular architectures in various domains requiring ==semantic segmentation.==

---
### **Why U-Net is Needed?**

1. **Loss of Spatial Information**: Regular CNNs use pooling layers, which reduce the resolution of the image. You lose pixel-level detail, making it hard to map back to the original image.
2. **Global Context Missing**: While CNNs extract features well, they don’t combine global (whole image) and local (pixel-level) information effectively.

> [!NOTE]
> U-Net solves these issues by:
> Preserving spatial details using **skip connections**.
>  Combining local and global context for precise segmentation 

### **Key Features of U-Net**

1. **Symmetrical U-Shape**:
    
    - The architecture has a symmetrical "U" shape, consisting of two main parts:
        - **Encoder (Contracting Path)**: Extracts feature representations while reducing spatial dimensions.
        - **Decoder (Expanding Path)**: Reconstructs spatial dimensions to generate a pixel-wise segmentation map.
    - This structure ensures both context (global information) and localization (pixel-level details) are preserved.
2. **Skip Connections**:
    
    - Connections between layers in the encoder and decoder allow the network to combine high-level semantic information from the encoder with fine-grained spatial information from earlier layers.
    - These skip connections are critical for accurate segmentation, as they help retain detailed features lost during downsampling.

---

### **Architecture of U-Net**

![[Pasted image 20241123183503.png]]

1. **Encoder (Downsampling/Contracting Path)**:
    
    - Consists of repeated **Convolutional Layers**, **ReLU activations**, and **Max-Pooling Layers**.
    - Purpose:
        - Extract features.
        - Reduce spatial resolution (dimensionality reduction) to focus on "what" is present in the image.
    - At each level, the number of feature channels is increased to capture richer information.
3. **Decoder (Upsampling/Expanding Path)**:
    
    - Consists of **Upsampling Layers** (like transposed convolutions or bilinear upsampling) followed by **Convolutional Layers**.
    - Purpose:
        - Reconstruct the spatial resolution of the input image.
        - Use features extracted by the encoder to create a pixel-wise segmentation map.
4. **Skip Connections**:
    
    - Features from the encoder are concatenated with features in the decoder at corresponding spatial resolutions.
    - This helps preserve fine details and context lost during downsampling in the encoder.
5. **Final Output Layer**:
    

---

### **Workflow of U-Net**

1. Input:
    - A 2D/3D image (e.g., medical scans).
2. Forward Pass:
    - The image passes through the encoder, which extracts features and reduces spatial resolution.
    - The bottleneck captures context-rich features.
    - The decoder reconstructs the segmentation map, combining low-resolution semantic features with high-resolution spatial details using skip connections.
3. Output:
    - A segmented image where each pixel is labeled with a specific class.

---

### **Advantages of U-Net**

1. **Effective for Small Datasets**:
    - Due to its encoder-decoder structure and skip connections, U-Net works well with relatively small datasets, making it ideal for domains like medical imaging.
2. **Preservation of Fine Details**:
    - Skip connections help preserve spatial details critical for precise segmentation.
3. **Flexible and Generalizable**:
    - While originally designed for 2D biomedical images, U-Net has been extended to 3D segmentation and other tasks like satellite image segmentation and scene parsing.

---

### **Applications of U-Net**

1. **Biomedical Image Segmentation**:
    - Example: Segmenting cells, tissues, or lesions in medical scans like CT or MRI.
2. **Autonomous Driving**:
    - Semantic segmentation of roads, vehicles, and pedestrians.
3. **Agriculture**:
    - Analyzing satellite images for crop monitoring or land use segmentation.
4. **Aerial and Satellite Imagery**:
    - Detecting objects or segmenting geographical features like rivers or forests.

---

### **Key Innovations**

- U-Net introduced **skip connections** for semantic segmentation, which later influenced many state-of-the-art architectures (e.g., ResNet, Feature Pyramid Networks).
- Its focus on pixel-level accuracy and efficient use of data has made it a cornerstone in deep learning for segmentation.

In summary, U-Net is a highly efficient architecture for image segmentation tasks, excelling in preserving both fine details and high-level context, making it a staple in applications requiring pixel-wise predictions.

# Res-Net
I am not going to prepare this shit

# Alex-Net
**AlexNet** is a deep convolutional neural network (CNN) architecture that was proposed by **Alex Krizhevsky**, **Ilya Sutskever**, and **Geoffrey Hinton** in their 2012 paper "ImageNet Classification with Deep Convolutional Neural Networks." It became famous for significantly outperforming other models in the **ImageNet Large Scale Visual Recognition Challenge (ILSVRC)** in 2012. AlexNet is often credited with sparking the deep learning revolution in computer vision.

### **Key Features of AlexNet:**
![[Pasted image 20241123190433.png]]


1. **Architecture Overview**: AlexNet consists of **8 layers**:
    
    - **5 Convolutional layers** (conv layers)
    - **3 Fully connected layers** (fc layers)
    
    These layers are followed by **ReLU activations**, **max-pooling**, and **dropout** for regularization.
    
2. **Layers in Detail**:
    
    - **Input Layer**: The input image is of size **227x227x3** (RGB image).
        
    - **First Convolutional Layer**:
        
        - 11x11 kernel size, with 96 filters, with a **stride of 4** and **padding**.
        - This produces an output of size **55x55x96**.
    - **Second Convolutional Layer**:
        
        - 5x5 kernel size, with 256 filters.
        - Output size: **27x27x256**.
    - **Third Convolutional Layer**:
        
        - 3x3 kernel size, with 384 filters.
        - Output size: **13x13x384**.
    - **Fourth Convolutional Layer**:
        
        - 3x3 kernel size, with 384 filters.
        - Output size: **13x13x384**.
    - **Fifth Convolutional Layer**:
        
        - 3x3 kernel size, with 256 filters.
        - Output size: **13x13x256**.
    - After the convolutional layers, **max-pooling** is applied after certain layers to downsample the feature maps and reduce their dimensionality.
        
    - **Fully Connected Layers**:
        
        - The first two fully connected layers have **4096 neurons** each.
        - The third fully connected layer has **1000 neurons**, corresponding to the **1000 classes** in the ImageNet dataset.
    - **Softmax Layer**:
        
        - The final output layer applies a **softmax activation** function to classify the image into one of 1000 possible categories.
3. **Activation Functions**:
    
    - AlexNet used **ReLU (Rectified Linear Unit)** activation functions, which were a key factor in its success. ReLU is computationally simpler than traditional activation functions like sigmoid or tanh, and it helps to mitigate the vanishing gradient problem.
4. **Regularization (Dropout)**:
    
    - **Dropout** was used in the fully connected layers to reduce overfitting during training. With dropout, a random set of neurons are turned off during each iteration, forcing the network to learn more robust features.
5. **GPU Training**:
    
    - AlexNet utilized **two GPUs** to train the model efficiently. The training process was parallelized across these GPUs to speed up computation and to handle the large dataset (ImageNet).
6. **Data Augmentation**:
    
    - **Data augmentation** techniques, like **flipping**, **cropping**, and **color jittering**, were used to artificially increase the size of the training dataset. This helps prevent overfitting by exposing the model to more varied examples.
7. **Optimization**:
    
    - **Stochastic Gradient Descent (SGD)** was used with **momentum** to update the weights during training. The learning rate was initially set to 0.01 and then adjusted.

### **Impact of AlexNet**:

- **Breakthrough Performance**: AlexNet significantly reduced the error rate in the **ImageNet Challenge** from **25.7%** to **16.4%**, which was a huge leap in performance. It outperformed traditional computer vision methods by a large margin and showed the power of deep learning in image classification.
    
- **ReLU**: The use of **ReLU** helped AlexNet avoid the vanishing gradient problem, making it easier to train deep networks. This was a key innovation that allowed for deeper networks to be trained efficiently.
    
- **GPU Acceleration**: The use of GPUs for training deep networks helped demonstrate the feasibility of large-scale training and contributed to the shift towards using GPUs in deep learning.
    
- **Inspiration for Future Networks**: AlexNet's success laid the foundation for more advanced CNN architectures, such as **VGG**, **ResNet**, **Inception**, and **DenseNet**. It demonstrated the importance of large datasets, deeper networks, and powerful hardware in achieving state-of-the-art results.
    

### **Numerical of AlexNet Architecture**:

Let’s go step-by-step through each layer of AlexNet, breaking down the numerical details, and explaining how the spatial dimensions (height and width) and depth (number of channels) change at each stage.

---

### **Input Layer**
- **Input size**: $227 \times 227 \times 3$ (RGB image with height $227$, width $227$, and 3 color channels).
- No processing occurs here; this is just the raw input size.

---

### **Conv1: First Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $11 \times 11$.
   - **Number of filters**: 96 (each filter extracts a different feature, so the depth increases to 96).
   - **Stride**: $4$ (the filter shifts by 4 pixels at each step).
   - **Padding**: None (valid convolution, $P = 0$).

2. **Formula for Output Dimensions**:
	$$
   H_{out} = \left( \frac{H_{in} - K + 2P}{S} \right) + 1
   $$
   $$
   H_{out} = \left( \frac{227 - 11 + 2(0)}{4} \right) + 1 = 55
   $$

   Similarly, $ W_{out} = 55$.

3. **Output size**:
   - Spatial dimensions: $55 \times 55$.
   - Depth: $96$ (one for each filter).
   - **Output tensor**: $55 \times 55 \times 96$.

4. **ReLU Activation**: Applies the ReLU activation function, introducing non-linearity.

5. **Max Pooling**:
   - **Kernel size**: $3 \times 3$.
   - **Stride**: $2$.
   - Pooling reduces dimensions:
     $$
     H_{out} = \left( \frac{H_{in} - K}{S} \right) + 1 = \left( \frac{55 - 3}{2} \right) + 1 = 27
     $$

     Similarly, $W_{out} = 27$.

6. **Output size after Conv1 + Max Pooling**:
   - $27 \times 27 \times 96$.

---

### **Conv2: Second Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $5 \times 5$.
   - **Number of filters**: 256.
   - **Stride**: $1$ (default stride for convolution unless specified otherwise).
   - **Padding**: $2$ (to maintain spatial size using "same" padding).

2. **Formula for Output Dimensions**:
   $$
   H_{out} = \left( \frac{H_{in} - K + 2P}{S} \right) + 1 = \left( \frac{27 - 5 + 2(2)}{1} \right) + 1 = 27
  $$

   Similarly, $W_{out} = 27$.

3. **Output size**:
   - Spatial dimensions: $27 \times 27$.
   - Depth: $256$.
   - **Output tensor**: $27 \times 27 \times 256$.

4. **ReLU Activation**: Applies the ReLU function.

5. **Max Pooling**:
   - **Kernel size**: $3 \times 3$.
   - **Stride**: $2$.
   - Pooling reduces dimensions:
     $$
     H_{out} = \left( \frac{H_{in} - K}{S} \right) + 1 = \left( \frac{27 - 3}{2} \right) + 1 = 13
     $$

     Similarly, $W_{out} = 13$.

6. **Output size after Conv2 + Max Pooling**:
   - $13 \times 13 \times 256$.

---

### **Conv3: Third Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $3 \times 3$.
   - **Number of filters**: 384.
   - **Stride**: $1$.
   - **Padding**: $1$ (to maintain spatial size).

2. **Formula for Output Dimensions**:
   $$
   H_{out} = \left( \frac{H_{in} - K + 2P}{S} \right) + 1 = \left( \frac{13 - 3 + 2(1)}{1} \right) + 1 = 13
   $$

   Similarly, $W_{out} = 13$.

3. **Output size**:
   - Spatial dimensions: $13 \times 13$.
   - Depth: $384$.
   - **Output tensor**: $13 \times 13 \times 384$.

4. **ReLU Activation**: Applies the ReLU function.

---

### **Conv4: Fourth Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $3 \times 3$.
   - **Number of filters**: 384.
   - **Stride**: $1$.
   - **Padding**: $1$ (to maintain spatial size).

2. **Output size**:
   - Spatial dimensions: $13 \times 13$.
   - Depth: $384$.
   - **Output tensor**: $13 \times 13 \times 384$.

3. **ReLU Activation**: Applies the ReLU function.

---

### **Conv5: Fifth Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $3 \times 3$.
   - **Number of filters**: 256.
   - **Stride**: $1$.
   - **Padding**: $1$ (to maintain spatial size).

2. **Output size**:
   - Spatial dimensions: $13 \times 13$.
   - Depth: $256$.
   - **Output tensor**: $13 \times 13 \times 256$.

3. **ReLU Activation**: Applies the ReLU function.

4. **Max Pooling**:
   - **Kernel size**: $3 \times 3$.
   - **Stride**: $2$.
   - Pooling reduces dimensions:
     $$
     H_{out} = \left( \frac{13 - 3}{2} \right) + 1 = 6
     $$

     Similarly, $W_{out} = 6$.

5. **Output size after Conv5 + Max Pooling**:
   - $6 \times 6 \times 256$.

---

### **Flatten Layer**
- The 3D tensor ($6 \times 6 \times 256$) is flattened into a 1D vector.
- Number of elements: $6 \times 6 \times 256 = 9216$.
- **Output**: A 1D vector with $9216$ elements.

---

### **Fully Connected Layers**
1. **First Fully Connected Layer**:
   - Input: $9216$.
   - Neurons: $4096$.
   - ReLU activation.
   - Dropout applied to reduce overfitting.

2. **Second Fully Connected Layer**:
   - Input: $4096$.
   - Neurons: $4096$.
   - ReLU activation.
   - Dropout applied.

3. **Third Fully Connected Layer**:
   - Input: $4096$.
   - Neurons: $1000$ (for the 1000 classes in ImageNet).
   - Softmax activation for classification.

---

### **Summary of AlexNet Dimensions**
Here is the modified text with all the replacements applied:


Let’s go step-by-step through each layer of AlexNet, breaking down the numerical details, and explaining how the spatial dimensions (height and width) and depth (number of channels) change at each stage.

---

### **Input Layer**
- **Input size**: $227 \times 227 \times 3$ (RGB image with height $227$, width $227$, and 3 color channels).
- No processing occurs here; this is just the raw input size.

---

### **Conv1: First Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $11 \times 11$.
   - **Number of filters**: 96 (each filter extracts a different feature, so the depth increases to 96).
   - **Stride**: $4$ (the filter shifts by 4 pixels at each step).
   - **Padding**: None (valid convolution, $P = 0$).

2. **Formula for Output Dimensions**:
   $$
   H_{out} = \left( \frac{H_{in} - K + 2P}{S} \right) + 1
   $$
   $$
   H_{out} = \left( \frac{227 - 11 + 2(0)}{4} \right) + 1 = 55
   $$

   Similarly, $W_{out} = 55$.

3. **Output size**:
   - Spatial dimensions: $55 \times 55$.
   - Depth: $96$ (one for each filter).
   - **Output tensor**: $55 \times 55 \times 96$.

4. **ReLU Activation**: Applies the ReLU activation function, introducing non-linearity.

5. **Max Pooling**:
   - **Kernel size**: $3 \times 3$.
   - **Stride**: $2$.
   - Pooling reduces dimensions:
     $$
     H_{out} = \left( \frac{H_{in} - K}{S} \right) + 1 = \left( \frac{55 - 3}{2} \right) + 1 = 27
     $$

     Similarly, $W_{out} = 27$.

6. **Output size after Conv1 + Max Pooling**:
   - $27 \times 27 \times 96$.

---

### **Conv2: Second Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $5 \times 5$.
   - **Number of filters**: 256.
   - **Stride**: $1$ (default stride for convolution unless specified otherwise).
   - **Padding**: $2$ (to maintain spatial size using "same" padding).

2. **Formula for Output Dimensions**:
   $$
   H_{out} = \left( \frac{H_{in} - K + 2P}{S} \right) + 1 = \left( \frac{27 - 5 + 2(2)}{1} \right) + 1 = 27
   $$

   Similarly, $W_{out} = 27$.

3. **Output size**:
   - Spatial dimensions: $27 \times 27$.
   - Depth: $256$.
   - **Output tensor**: $27 \times 27 \times 256$.

4. **ReLU Activation**: Applies the ReLU function.

5. **Max Pooling**:
   - **Kernel size**: $3 \times 3$.
   - **Stride**: $2$.
   - Pooling reduces dimensions:
     $$
     H_{out} = \left( \frac{H_{in} - K}{S} \right) + 1 = \left( \frac{27 - 3}{2} \right) + 1 = 13
     $$

     Similarly, $W_{out} = 13$.

6. **Output size after Conv2 + Max Pooling**:
   - $13 \times 13 \times 256$.

---

### **Conv3: Third Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $3 \times 3$.
   - **Number of filters**: 384.
   - **Stride**: $1$.
   - **Padding**: $1$ (to maintain spatial size).

2. **Formula for Output Dimensions**:
   $$
   H_{out} = \left( \frac{H_{in} - K + 2P}{S} \right) + 1 = \left( \frac{13 - 3 + 2(1)}{1} \right) + 1 = 13
   $$

   Similarly, $W_{out} = 13$.

3. **Output size**:
   - Spatial dimensions: $13 \times 13$.
   - Depth: $384$.
   - **Output tensor**: $13 \times 13 \times 384$.

4. **ReLU Activation**: Applies the ReLU function.

---

### **Conv4: Fourth Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $3 \times 3$.
   - **Number of filters**: 384.
   - **Stride**: $1$.
   - **Padding**: $1$ (to maintain spatial size).

2. **Output size**:
   - Spatial dimensions: $13 \times 13$.
   - Depth: $384$.
   - **Output tensor**: $13 \times 13 \times 384$.

3. **ReLU Activation**: Applies the ReLU function.

---

### **Conv5: Fifth Convolutional Layer**
1. **Operation**: Convolution with:
   - **Kernel size**: $3 \times 3$.
   - **Number of filters**: 256.
   - **Stride**: $1$.
   - **Padding**: $1$ (to maintain spatial size).

2. **Output size**:
   - Spatial dimensions: $13 \times 13$.
   - Depth: $256$.
   - **Output tensor**: $13 \times 13 \times 256$.

3. **ReLU Activation**: Applies the ReLU function.

4. **Max Pooling**:
   - **Kernel size**: $3 \times 3$.
   - **Stride**: $2$.
   - Pooling reduces dimensions:
     $$
     H_{out} = \left( \frac{13 - 3}{2} \right) + 1 = 6
     $$

     Similarly, $W_{out} = 6$.

5. **Output size after Conv5 + Max Pooling**:
   - $6 \times 6 \times 256$.

---

### **Flatten Layer**
- The 3D tensor ($6 \times 6 \times 256$) is flattened into a 1D vector.
- Number of elements: $6 \times 6 \times 256 = 9216$.
- **Output**: A 1D vector with $9216$ elements.

---

### **Fully Connected Layers**
1. **First Fully Connected Layer**:
   - Input: $9216$.
   - Neurons: $4096$.
   - ReLU activation.
   - Dropout applied to reduce overfitting.

2. **Second Fully Connected Layer**:
   - Input: $4096$.
   - Neurons: $4096$.
   - ReLU activation.
   - Dropout applied.

3. **Third Fully Connected Layer**:
   - Input: $4096$.
   - Neurons: $1000$ (for the 1000 classes in ImageNet).
   - Softmax activation for classification.

---

### **Summary of AlexNet Dimensions**
1. Input: $227 \times 227 \times 3$.
2. Conv1 + Pool: $27 \times 27 \times 96$.
3. Conv2 + Pool: $13 \times 13 \times 256$.
4. Conv3: $13 \times 13 \times 384$.
5. Conv4: $13 \times 13 \times 384$.
6. Conv5 + Pool: $6 \times 6 \times 256$.
7. Fully Connected Layers: $4096 \rightarrow 4096 \rightarrow 1000$.


Let me know if you'd like further adjustments!
### **Key Takeaways**:

- **AlexNet** demonstrated the power of deep learning in image classification tasks.
- Its innovations like **ReLU activations**, **GPU training**, **dropout**, and **data augmentation** were crucial for its success.
- AlexNet's architecture is relatively shallow compared to modern architectures, but it was revolutionary at the time and remains a classic example of a CNN for image classification.
