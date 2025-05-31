#  Model Card for Meow Meow Translator
A model built on an audio feature extractor and CNN that helps translate cat sounds into emotions for people to better understand what their furry friends are feeling and take better care of them.

## Model Details 
### Model Description
- Developed by: Ziqian Liao, Joanna Shen, Haoheng Tang
- License: MIT License

### Model Structure
The model is designed with two main components: an audio feature extractor and a CNN classifier, working together to classify emotional states from cat sounds.

#### Audio Feature Extractor
We used traditional audio processing techniques to convert raw waveforms into meaningful features using the `librosa` library. The following features were extracted for each audio clip:
- Zero Crossing Rate – Indicates how frequently the signal changes sign, related to sound roughness.

- Chroma Frequencies – Captures pitch-related content.

- MFCCs (Mel-Frequency Cepstral Coefficients) – Represents timbre and texture.

- Spectral Rolloff – Shows the frequency below which most of the energy is concentrated.

- Spectral Bandwidth – Measures the range of frequencies with most of the energy.

- RMS Energy – Reflects loudness.

- Mel-Spectrogram – Transforms sound into a frequency scale that aligns with human perception.

Each feature was averaged over time to reduce dimensionality while keeping key characteristics. These were concatenated into a single vector representing the audio clip.

#### CNN Classifier
The processed audio vectors were reshaped and passed into a deep 1D CNN. The architecture includes:

- 4 convolutional layers with increasing filter sizes (128 → 1024) and kernel size of 3, each followed by a max pooling layer to reduce spatial dimensions.

- A Flatten layer to convert the 3D output into 1D for the dense layers.

- Three dense layers (512 → 256 → 128 units) with ReLU activation and dropout (0.5, 0.3, 0.2) for regularization.

- A final softmax layer with 10 units for multi-class emotion classification.

The output of the model is a probability distribution across 10 emotion classes, with the highest value indicating the predicted emotional state of the cat sound.

### Methodology
#### Data Collection 
We used a dataset of cat sounds curated for better understanding of cat behavior, or more specifically, the emotion classification of cats. This dataset is organized to include a total of 10 categories, each representing a different emotional state of a cat: happiness, fighting, defensive behavior, anger, warning, resting, pain, calling for its mother, mating, and hunting desire, which will be used as class labels for the classifier.

##### Data Source
Yagya Raj Pandeya, Dongwhoon Kim and Joonwhoan Lee, Domestic Cat Sound Classification Using Learned Features from Deep Neural Nets (https://www.mdpi.com/2076-3417/8/10/1949)
Yagya Raj Pandeya and Joonwhoan Lee, Domestic Cat Sound Classification Using Transfer Learning (http://www.ijfis.org/journal/download_pdf.php?doi=10.5391/IJFIS.2018.18.2.154)

#### Data Handling
During preprocessing, we have transformed the audio in the form of .mp3 files to .wav files to comply with the python packages. We also converted the stereo input (2 channels) into mono (1 channel). There is no missingness in our dataset.

#### Model Training
A deep 1D CNN was used for classification. The model was trained for up to 50 epochs using the Adam optimizer (learning rate 0.0005) and categorical cross-entropy loss. We used a batch size of 256 and early stopping to monitor training loss, with a patience of 3 epochs and a minimum delta of 0.05. Validation was performed on a separate hold-out set.

### Evaluation Results
The model demonstrated strong overall performance in classifying cat vocalizations by emotional state. It achieved a training accuracy of 98.36%, indicating effective learning on the training data. On the validation set, the model reached an accuracy of 87.45%, and it maintained a comparable test accuracy of 85.15% when evaluated on a separate 20% subset of the original dataset. The relatively small gap between validation and test performance suggests that the model performance is generalizable. 




