# Visual-Question-Answer-Using-Medical-Imaging
Developed a transformer-based model that combines Vision Transformer (ViT) for image feature extraction and BERT for question embedding, achieving high accuracy on datasets like VQA-RAD and PathVQA for both closed and open-ended clinical question answering.

**This project is an integrated application of Deep Learning with Computer Vision and Natural Language Processing.**

## Introduction
The application of the VQA Medical Imaging is to assist medical professionals in analyzing medical Images such as X-rays, MRI scans and CT Scans.

It provides answers  to questions related to the content of these images . This can significantly aid in diagnosis, treatment planning nd medical research.

## Model Architecture

The model consists if a seperate encoder for each input modality followed by a decoder, hence there are 3 parts:

1. Image Encoder
2. Language Encoder
3. Answer Decoder

## 1. Image Encoder

<ul>
  <li>ViT32 based model</li>
  <li> composed of 12 identical layers. Each block is preceded by a normalization layer and a residual connection to the next block.</li>
  <li>MSA Encoder: to find the correlation between different patches of the medical image.</li>
</ul>

The result of the attention heads are concatenated together and then passed to the Feed Forward Neural Network block. The FFN consists of two fully connected layers with a Gaussian error linear Unit (GeLU) activation function applied in between.

## 2. Text Encoder

<ul>
  <li>BERT like architecture to generate the question's textual features.</li>
  <li>Two tokens: <CLS> and <SEP> are appended to the sequence to mark its beginning and end,</li>
  <li>MSA Encoder: to capture the dependencies within the question tokens.</li>
</ul>

The output of the questions encoder is the question feature representation of size 77 x 512. This representation holds information about the semantics of the question and the relationships between words.

## 3. Answer Decoder

The image features f<sub>xi</sub> and the question features f<sub>qi</sub> are concatenated (f<sub>i</sub> =f<sub>xi</sub> XOR f<sub>qi</sub> ). The representation f<sub>i</sub>, which aggregates the relevant information from the two modalities is sulied as input to the answer generator which decodes it into an answer.

## Multi model representation

The decoder layer is composed of the same MSA and FFN block present in the encoder. However the decoder uses a masked self attention block that learns the dependencies within the answer tokens without considering future tokens.
