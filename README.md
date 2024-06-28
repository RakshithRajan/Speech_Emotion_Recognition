# <center>Emotional Speech Recognition</center>

## <center>Emotions Speech Datasets</center>

**Content:**
Data set contains files from RAVDESS, CREMA-D, SAVEE, and TESS.

Out of all files, data sets make up:
- CREMA-D: 7,442 files
- TESS: 2,800 files
- RAVDESS: 2,076 files
- SAVEE: 480 files

We extract the path of all emotions from each dataset and create separate CSV files for male and female voices.

## Introduction

Emotion in speech depends significantly on pitch and tone. Variations in these elements can convey different emotions, making it possible to recognize emotions from audio signals. This project aims to leverage these variations to classify emotions using machine learning techniques.

## <center>Data Visualization</center>

First, we will plot the number of emotions (proportions of each emotion). Then, using Librosa, we will create waveplots for each emotion.

## Data Definition

- **Data Augmentation:**
  - Data augmentation involves creating new synthetic training samples by adding small changes to the initial training set.
  - The goal is to make our model invariant to these changes and enhance its ability to generalize.
  - Perturbations must preserve the original label.
  - For images, augmentation includes shifting, zooming, and rotating.
  - For audio, we add noise, stretch and roll, pitch shift, higher speed, and lower speed.

## Feature Extraction

Audio data needs to be converted into a format that models can understand, which is done through feature extraction. The audio signal is a three-dimensional signal where the axes represent time, amplitude, and frequency.

Waveforms alone may not provide clear class-identifying information. One of the best tools for feature extraction from audio waveforms is **Mel Frequency Cepstral Coefficients (MFCCs)**. Below is a brief technical discussion on how MFCCs work.

## References
- Information about feature extraction and audio processing is taken from [this Medium article](https://medium.com/comet-ml/applyingmachinelearningtoaudioanalysis-utm-source-kdnuggets11-19-e160b069e88).
- Special thanks to Nicolò Malatesta for sharing invaluable knowledge through his projects and works!

### Audio Features:
- **Zero Crossing Rate:** Identifies the noisiness of a signal. Higher rates can indicate more noise or higher frequencies.
- **Energy:** Measures the loudness of the audio. High energy corresponds to louder sounds.
- **Entropy of Energy:** Detects variations and changes in energy. High entropy can indicate a more complex or unpredictable sound.
- **Spectral Centroid:** Identifies the "brightness" of a sound. Higher centroids usually mean a sound is brighter or sharper.
- **Spectral Spread:** Indicates the bandwidth of the signal. A wide spread can signify a mix of low and high frequencies.
- **Spectral Entropy:** Measures the complexity of the spectral distribution. High entropy indicates a more uniform spread of frequencies.
- **Spectral Flux:** Measures how quickly the power spectrum of a signal is changing. Useful for detecting the onset of notes or beats.
- **Spectral Rolloff:** Helps in distinguishing between voiced and unvoiced sounds, and detecting high-frequency noise.
- **MFCCs (Mel Frequency Cepstral Coefficients):** Capture the timbral (tone quality) aspects of the audio. Widely used in speech and music recognition.
- **Chroma Vector:** Represents the harmonic and melodic content of the music. Useful for identifying chords, tonality, and musical key.
- **Chroma Deviation:** Measures the stability of the harmonic content. High deviation indicates a more varied pitch content.

## Data Preparation

- Using OneHotEncoder for labels.
- Preparing the data for model training and testing.
- Splitting the data.

We will scale our features using the StandardScaler module, which standardizes the features into a **normal curve**, i.e.,

<center> $Z = \frac{X - \mu}{\sigma}$ </center>

*Standardization is essential for many machine learning estimators as they might perform poorly if the features do not resemble standard normally distributed data (e.g., Gaussian with 0 mean and unit variance).*

## Model Architecture

- The model consists of 4 1D convolution layers with ReLU activation.
- The first three layers have 256 filters, and the last layer has 64 filters.
- The Adam optimizer is used with categorical_crossentropy for loss.
- ReduceLROnPlateau is used as a callback.
- Training is performed with a batch size of 32 and for 75 epochs.

## Results

- Mixed-gender emotions training accuracy: 96.80%
- Mixed-gender emotions testing accuracy: 88.07%
- Female emotions training accuracy: 99.38%
- Female emotions testing accuracy: 93.54%

## Conclusion

This project demonstrates that by leveraging pitch and tone variations in speech, we can effectively recognize emotions using machine learning techniques. The high training and testing accuracies indicate that the model generalizes well to new data. This approach can be further refined and applied to various applications, such as enhancing human-computer interaction and aiding in psychological studies.
