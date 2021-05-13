# Simple Neural Network on Excel Sheet

## Neural Network Diagram
<img src="./images/1. Neural Network Diagram.JPG" />

## FeedForward : Calculate Errors
Feedforward equations based on the diagram above.

<img src="./images/2. Forward pass.JPG"  />

## Backpropagation Equations : Get Gradients
<img src="./images/3. Backward Pass solving gradients.JPG" />

1. We start with w5 and calculate the error delta for w5 and similarly solve error gradients for w6, w7 and w8.

2. Using the chain rule and above calculated gradients we calculate gradients for W1, w2, w3 and w4 too. Here we break the equation into two parts:

   a. output  ----> hidden layer

   b. hidden layer  ---> input layer.

---

## Training the Network
<img src="./images/4. Training.JPG" width="1000"/>

1. Initialize weights as the values given in diagram above.
2. Calculate the hidden node values and output values.
3. Calculate the Total Error by comparing outputs with Targets.
4. Get total error.
5. Use backward pass equation to get gradients for each weight against the error.
6. Reduce the weight values by the corresponding gradient values.
7. Move to next iteration with the weights from step6.
8. Repeat until you are tired.

## Results

<img src="./images/5. Error vs Iterations.JPG" width="500"/>

<img src="./images/6. Impact of Learinging rate.JPG" width="500"/>

