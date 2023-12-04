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

