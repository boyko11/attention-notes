# Transformer Model Overview

This document provides an overview of the Transformer model architecture as detailed in the "Attention is All You Need" paper. It breaks down the key components of both the Encoder and Decoder parts of the Transformer model.

## Encoder

### Input Processing
- **Tokenization**: Input text is tokenized into individual tokens.
- **Embedding**: Tokens are converted into embedding vectors.
- **Positional Encoding**: Embeddings are positionally encoded to retain sequence order information.

### Multi-Head Attention Mechanism
- **Distribution to Heads**: Positionally encoded embeddings are distributed to each head.
- **Breakdown into Q, K, V**: Embeddings transformed into Query (Q), Key (K), and Value (V) vectors.
- **Attention Calculation**: Dot product of Q and K, followed by softmax for attention weights.
- **Weighted Sum of Values**: Attention weights create a weighted sum of V vectors.
- **Combining Head Outputs**: Concatenation of outputs from all heads, followed by a linear transformation.

### Residual Connection and Layer Normalization
- **First Residual Connection**: Output from multi-head attention added to original embeddings.
- **First Layer Normalization**: Normalization of the sum across features.

### Feed-Forward Network
- **Independent Processing**: Each embedding processed through a feed-forward network.
- **Second Residual Connection**: Output of the network added back to its input.
- **Second Layer Normalization**: Another layer normalization applied.

### Output to Next Layer or Decoder
- Passed to the next encoder layer or to the decoder in sequence-to-sequence models.

## Decoder

### Decoder Input Preparation
- **Decoder Input Sequence**: Receives a sequence of tokens (e.g., starting with a `<start>` token).
- **Embedding and Positional Encoding**: Similar to the encoder process.

### Masked Multi-Head Attention
- **Masked Attention Mechanism**: Predictions dependent only on known outputs at prior positions.
- **Creating Q, K, V Vectors and Attention Calculation**: Similar to the encoder, with an added mask.

### First Residual Connection and Layer Normalization
- **Residual Connection**: Output from masked multi-head attention added to its input.
- **Layer Normalization**: Sum normalized across features.

### Cross-Attention Layer
- **Interaction with Encoder Output**: Decoder attends to encoder's output.
- **Attention Calculation**: Using decoder's Q and encoder's K and V for attention.

### Second Residual Connection and Layer Normalization
- **Residual Connection and Layer Normalization**: Similar to previous layers.

### Position-Wise Feed-Forward Network
- **Feed-Forward Network**: Independent processing of each embedding.
- **Structure similar to the encoder's feed-forward network**.

### Third Residual Connection and Layer Normalization
- **Residual Connection and Layer Normalization**: Additional layers of processing.

### Output Generation
- **Final Linear Layer and Softmax**: Generating probabilities for the next token.
- **Token Generation**: Selection of the highest probability token, repeated for subsequent tokens.

### Additional Notes
- **Repeated Layers**: Decoder consists of multiple layers with the above structure.
- **End Token**: Generation continues until an end-of-sequence token is generated or a maximum length is reached.

# Data Flow and Learnable Parameters in a Transformer Model (GPT-3/GPT-4)

This document summarizes the data flow and identifies the learnable parameters at each stage of a forward pass in a transformer model, specifically in the context of next token generation tasks like those performed by GPT-3 or GPT-4.

## Summary of Steps and Parameters

1. **Input Text & Tokenization**:
   - Text input is tokenized into a sequence of tokens.
   - No learnable parameters in tokenization.

2. **Embedding Layer**:
   - Each token is mapped to an embedding vector.
   - Learnable Parameters: Embedding matrix mapping each token to its embedding.

3. **Positional Encoding**:
   - Positional encodings are added to the embeddings to provide order information.
   - Typically no learnable parameters; fixed sinusoidal encodings are used.

4. **Multi-Head Attention Mechanism**:
   - Each embedding is transformed into Query (Q), Key (K), and Value (V) vectors for each attention head.
   - Attention scores are calculated, scaled, and normalized (softmax).
   - Attention is applied to Value vectors, and results are combined.
   - Learnable Parameters: Separate Q, K, V linear transformation matrices for each head.

5. **Concatenation and Linear Transformation After Attention**:
   - Outputs from all heads are concatenated and linearly transformed.
   - Learnable Parameters: Linear transformation matrix for processing concatenated output.

6. **First Residual Connection**:
   - Output of the multi-head attention is added to the original input embeddings.
   - No learnable parameters in the residual connection.

7. **First Layer Normalization**:
   - Normalization of the combined output from the first residual connection.
   - Learnable Parameters: Scale and shift parameters in the layer normalization.

8. **Feed-Forward Neural Network (FFNN)**:
   - Consists of two linear layers with a non-linear activation function in between.
   - Learnable Parameters:
     - First Linear Layer: Weights and biases, typically projecting to a higher-dimensional space.
     - Non-Linear Activation Function (e.g., ReLU, GELU): No learnable parameters.
     - Second Linear Layer: Weights and biases, projecting back to the original dimensionality.

9. **Second Residual Connection**:
   - Output of the FFNN is added back to its input (post-first layer normalization).
   - No learnable parameters in the residual connection.

10. **Second Layer Normalization**:
    - Normalization of the combined output from the second residual connection.
    - Learnable Parameters: Scale and shift parameters in the layer normalization.

11. **Final Linear Layer for Token Generation**:
    - Linear transformation of the output to match the vocabulary size.
    - Learnable Parameters: Weights and biases in the final linear layer.

12. **Softmax Layer**:
    - Converts the output of the final linear layer into a probability distribution over the vocabulary.
    - No learnable parameters in the softmax function.

## Conclusion

This overview provides a comprehensive understanding of the key stages and components in the forward pass of a transformer model like GPT-3 or GPT-4. It highlights the complex interplay of different elements that enable these models to perform sophisticated language tasks, from input processing to token generation.
