## Project Title: Identifying ID Submissions using Computer Vision
#### Improving the customer experience in applying for a new digital bank account

\*For a more detailed read, please view the PDF under the presentation folder.\*

---
### 1. Introduction
---
#### Problem Statement: 
Scenario: A digital bank in Singapore wants to expand its banking business into Indonesia, but faced the challenge of Indonesia not having digital national ID cards. The bank wants to avoid manual ID verification for account opening, because it leads to a poor customer experience.
- Opportunities:
    - Large underserved market: Indonesia is the 4th most populous nation, and has the 3rd largest unbanked population
    - Young, tech-savvy population: the median age in Indonesia is median age is 30 years, and its population has the 2nd highest interest level in digital financial services in Southeast Asia\
- Challenge:
    - No national digital ID: for bank account opening, laborious and time consuming ID verification must be done with digital submission of physical documents (i.e. photos)

#### Objective: 
To enable process automation & process acceleration (reducing the image verification task from 3-5 working days to <30 seconds), the bank tasked me to develop a model to distinctly identify ID cards and passports (multiclass object detection in images).

#### Approach:
1. Label and analyse data: as proof of concept, to use artificially-generated ID cards and passports from East Europe, North-West Asia (source: [Informatique Image Interaction](http://l3i-share.univ-lr.fr/MIDV2020/midv2020.html))
2. Model training: use YOLOv5 for its state-of-the-art inference speed, good accuracy performance & ease of use
3. Model deployment via streamlit: Use Streamlit to illustrate model prediction speed and capability – users can choose from a selected set of photos, or upload their own

---
### 2. EDA
---
A total of 1,000 photos from East Europe and North-West Asia were used:
- Training (total 600 photos)
    - 100 digitally generated photos of ID cards from Slovakia, Spain and Finland each (total 300)
    - 100 digitally generated photos of passports from Latvia, Russia and Greece each (total 300)
- Validation (total 200 photos)
    - 100 digitally generated photos of ID cards from Estonia
    - 100 digitally generated photos of passports from Serbia
- Test (total 200 photos)
    - 100 digitally generated photos of ID cards from Albania
    - 100 digitally generated photos of passports from Azerbaijan

Through scatterplot of boundary box centres, histrogram of boundary box area and aspect ratios, it was found that:
1. Objects are usually in centre of photo, and missing from the corners of photos --> models trained on this dataset may be weak in identifying objects in photo corners
2. No objects are near the full 640 * 640 pixel size --> models trained on this dataset may be weak in identifying close-up objects
3. Most objects hover around their original aspect ratios --> models trained on this dataset may be weak in identifying rotated passports

EDA takeaway: data augmentation should be explored for training dataset to increase sample variations.

---
### 3. Modelling & Deployment
---
#### Modelling: 
The below models were trained and tested: 

|                                         |    <br>Baseline Model                                                                                      |    <br>Improved Model 1                                                                       |    <br>Improved Model 2                                                                                          |    <br>Improved   Model 3<br>\*Best performance\*                                               |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
|    <br>Dataset                          |                            <br>1000 photos (600 train, 200 validation, 200 test)                           |                                        Same as baseline                                       |                                                 Same as baseline                                                 |                     <br>1600 photos (1200 train, 200 validation, 200 test)                    |
|    <br>Augmentation on training data    | None                                                                                                       | - Colours: hue, saturation, brightness<br>- Image translation, scale, flip left-right, mosaic | - Colours: hue, saturation, brightness<br>- Image translation, scale, flip left-right, mosaic<br>- Rotate, shear | - Colours: hue, saturation, brightness<br>- Image translation, scale, flip left-right, mosaic |
|    <br>Model training, validation       | - YOLOv5l<br>- Batch size = 8<br>- Epochs = 100<br>- Starting weights = pretrained weights on COCO2017     |                                        Same as baseline                                       |                                                 Same as baseline                                                 |                                        Same as baseline                                       |
|    <br>Model testing                    | - Best-weight from training-validation<br>- Confidence threshold = 0.7<br>- Test-time augmentation enabled |                                        Same as baseline                                       |                                                 Same as baseline                                                 |                                        Same as baseline                                       |
| Test results                            | Correctly identified 99 ID cards, 62 passports                                                             | Correctly identified 95 ID cards, 99 passports                                                | Correctly identified 95 ID cards, 98 passports                                                                   | Correctly identified 96 ID cards, 100 passports                                               |

#### Deployment: 
The best model was deployed at [Streamlit](https://id-card-passport-detection.streamlit.app/).

---
### 4. Conclusion
---
As tasked by the bank, an object detection model was successfully developed with a test accuracy of 96% for ID cards and 100% for passports. The streamlit deployment also achieved a classification speed of ~3 seconds for each photo submission.

#### Limitations
- Dataset used is too small even for transfer learning, likely leading to poor generalisation
- Possibly limited performance on Southeast Asian ID documents (due to nature of dataset)
- Current model is unable to discern quality of submissions (e.g. blur, too dark, too bright etc.)

#### Areas for Improvement
- Conduct proof-of-concept using real data (>= 1,500 images per class)
- Use transfer learning to train on local dataset (i.e. start from developed weights)
- Develop a multi-head14 model to conduct quality classification (each head to classify 1 type of quality)

Notes:
- The model training and inference output cells were cleared due to their long printout - this is to improve the readability of the notebooks.
- The original and labelled datasets are too large to upload on Github. You may find the original dataset at [Informatique Image Interaction](http://l3i-share.univ-lr.fr/MIDV2020/midv2020.html) by La Rochelle Universite.
- In the case where Github fails to load the notebooks (error: unable to render rich display), please use the free [nbviewer](https://nbviewer.org/) to view the notebooks instead.