# Developing Algorithmic Trading Strategies
Project for MSDS692, Data Science Practicum I

John Holub

__________________________________________________________________________________________________________________________________________

## Table of Contents
- Summary & Project Goals
- File Descriptions
- Exploratory Analysis
- Algorithmic Systems
- System Performance Results
- Challenges & Findings
- Acknowledgments and References

___
## Summary

In recent years cloud computing environments has made previous very cumbersome and expensive intraday financial time series data much more accessible than it has ever been. In addition to the data becoming more accessible, cloud computing has also made working with the data much easier as well with online environments, docker images and IDEs.

It is estimated over &quot;80% of daily trades in United State are machine-led&quot;1 which is up from an estimated 15% in early 2000s1. This suggests a growth market for algorithmic trading and possibly extending its benefits to the non-professional. With this project I intend to explore the possibilities of algorithmic trading, not only in the short-term, but also for long-term investments and development of capital preservation methods applied to traditional portfolio allocations.

## Project Goals
1. Gain familiarity with large price/time series financial data and defining, developing, testing, optimizing and implementing (bring to Production Stage) algorithmic trading strategies.
2. Develop method(s) for rapid Exploratory Data Analysis (EDA) and Feasibility Analysis (FA) of potential algorithms.
3. Bring algorithm(s) to production and test performance in live real-time environment (paper trading).
4. Summarize, visualize and communicate results in useful and attractive format.

___
## File Descriptions
- Binary Classifier 1.ipynb
  - CNN model that predicts healthy lungs vs. abnormal lungs using PNG images (Independent of other models)
- Binary Classifier 2.ipynb
  - CNN model that predicts healthy lungs vs. abnormal lungs using PNG images (Independent of other models)
- Bounding Box Predictor (CNN).ipynb
  - CNN model that predicts the location of pneumonia in DICOM files
- Classifier Image Processing.ipynb
  - DICOM to PNG converter
  - Training/Validation Split
  - Establishes Directory Architecture
- Detailed Class Categorical Classifier 1.ipynb
  - CNN model that predicts healthy lungs vs. abnormal lungs/without pneumonia vs. abnormal lungs/with pneumonia
- Pneumonia Exploratory Analysis.ipynb
  - Explores the data for the present competition

___
## Exploratory Analysis

It's important to understand the data in our DICOM files before we dive in. Here is an example of a method one can employ to view the contents of a dicom file:

```python
import pydicom
dcm_file = path/to/dicom/file.dcm
dcm_data = pydicom.read_file(dcm_file)
print(dcm_data)
```
![alttext1](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_1.PNG "Image 1")

Understanding the data from the DICOM files is imperative to being able to ensure one's coneptualization of bounding boxes on the arrays from those files. After all, I am not a radiologist and do not have medical training. Therefore, I need to visualize those boxes in order to augment my knowledge regarding the visual aspects of pneumonia:

![alttext2](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_2.PNG "Image 2")

Now that we have visualized the bounding boxes and the XRAYs, we should take a look at the demographics of our study participants.

#### Frequency Chart of Detailed Class (Colored by Binary Class)
![alttext3](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_3.PNG "Image 3")

#### Frequency Chart of Binary Class (Colored by Binary Class)
![alttext4](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_4.PNG "Image 4")


#### Frequency Chart of Sex (Colored by Binary Class)
![alttext5](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_5.PNG "Image 5")

Ensuring that we maintain reasonably consistent demographic spreads when determining training and test sets will be imperative. Exploratory analysis will assist in that effort.

Making sure we understanding the pneumonia spread in these images will help us to identify anomalies in our predictions.
#### Heatmap of Pneumonia Presence in the Sample Images
![alttext6](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_6.PNG "Image 6")

For a look at some more of the exploratory analysis, please see the *Pneumonia Exploratory Analysis.ipynb* file.

___
## Model Results

As mentioned in the summary section, the bounding box detector is vastly superior, in terms of classification, compared to any of my classification models. All models in this repository are convolutional neural networks. The following are some of the most important details from the models here.
#### Key Metrics from the Bounding Box Detector *(Bounding Box Predictor (CNN).ipynb)*
![alttext7](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_7.PNG "Image 7")

#### Key Metrics from a Binary Classifier *(Binary Classifier 2.ipynb)*
![alttext8](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_8.PNG "Image 8")


It's pretty clear that, for now, the Bounding Box Detector *does not* need any help from my current classifiers. 

___
## Algorithmic Systems

___
## System Results

___
## Challenges & Findings

___
## Challenges & Findings

___
## References

- [Dr. Nathan George](https://www.regis.edu/CCIS/Academics/Departments-and-Faculty/Data-Sciences/George-Nate.aspx) 
  - For helping with all things df.iterrows
- [Shervine Amidi](https://stanford.edu/~shervine/blog/keras-how-to-generate-data-on-the-fly)
  - For providing detailed work creating generators with keras that I referenced in my bounding box model
- [Vivek Kumar](https://medium.com/@vivek8981/dicom-to-jpg-and-extract-all-patients-information-using-python-5e6dd1f1a07d)
  - For providing inspiration for my DICOM/PNG converter
- [Kevin Mader](https://www.kaggle.com/kmader/lung-opacity-overview/notebook)
  - For inspriation and code for portions of my exploratory analysis
- [Guy Zhavi](https://www.kaggle.com/zahaviguy/what-are-lung-opacities/notebook)
  - For exploratory code and explaining the nuance of lung opacity
- [Jonne](https://www.kaggle.com/jonnedtc/cnn-segmentation-connected-components/notebook)
  - For code framework used in Bounding Box Predictor
- An anonymous radiologist
  - For looking at my bounding boxes and for explaining where my shortcomings were
___ 





