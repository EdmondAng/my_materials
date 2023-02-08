# Project 3: Multiclass Classification of SIA Enquiries
Author: Edmond Ang

## 1. Problem Statement

Every week, the customer service centre of Singapore Airlines (SIA) receives thousands of feedback, questions, compliments and complaints from its customers and the public. As part of SIA's digitalisation effort to reduce manual labour and speed up response time, the SIA management hired me to (1) develop a predictive model to automatically sort incoming messages and into their top 2 most-frequently-asked topics and others, and (2) to identify the top key words from these messages and their sentiments.

SIA's top 2 most-frequently-asked topics and others:
- KrisFlyer and PPS Club<sup>1</sup> (KF)
- Lounges, catering and amenity kits (LCA)
- Others

## 2. Methodology

1. <b>Prepare data for model training</b> by scraping the 3 abovementioned topics' text data from SQTalk<sup>2</sup>

2. <b>Develop baseline model</b> using CountVectoriser and Multinomial Naives Bayes model

3. <b>Determine the best pre-processing and vectorizer combination</b> by comparing the performance of different techniques (e.g. further remove duplicated words, use TFIDF vectoriser)
    
4. <b>Develop improved models</b> by using the best pre-processing and vectoriser combination

5. <b>Conduct sentiment analysis</b> to identify the sentiments of comments containing top words from KF and LCA 

## 3. Conclusion

A predictive model with good performance was successfully developed for SIA. The customer service centre can use the model to sort incoming messages into (1) KF, (2) LCA, and (3) other categories automatically. The areas of strength for KF and LCA were also identified through sentiment analysis, where SIA can then incorporate into their marketing campaigns. SIA was also advised to continuously monitor the model's performance, and to conduct model re-training when the ROC AUC and f1 scores dip to 0.8 and 0.7 respectively to maintain good predictive performance.

1. Findings:
    - The TFIDF-vectorised SVM model performed the best in both macro-average ROC AUC (0.925) and f1-scores (0.815) across all the above models
    - The sentiments of comments containing the top 3 words from KrisFlyer and PPS Club, and LCA are largely positive. Hence, the top 3 words can be deemed as areas of strength for the respective topic (i.e. areas where people are satisfied with)
        - The top 3 words for KrisFlyer and PPS Club are 'miles', 'PPS', 'KF'
        - The top 3 words for LCA are 'lounge', 'SQ', 'served'
        
2. Areas for further improvement:

    - With further software and GUI development, the model can be used as a chatbot engine to sort incoming enquiries to the correct customer service teams. Additionally, the sentiment analysis can sort incoming enquiries into the correct enquiry type (e.g. neutral: feedback, negative: complaints, positive: compliments)
    - Further sentiment analysis can be done to find top words with negative sentiments, to identify and improve on areas of weaknesses
    - To expand the model prediction into more than these 3 topics, scraping of other SQTalk topics and model re-training can be done
    - Further model performance improvement may be achieved by grid-searching over more parameters of SVM and XGBoost<sup>3</sup> (both models outperformed other models substantially)

## 4. References

1. The KrisFlyer and PPS Club memberships are reward programmes for regular and frequent travellers of SIA respectively. Privileges of such memberships include earning points as you spend which can be exchanged for flight upgrades, membership-only deals and offers, and discounts on flight add-ons. [(KrisFlyer and PPS Club)](https://www.singaporeair.com/en_UK/us/ppsclub-krisflyer/)

2. SQTalk is a local forum where travel enthusiasts share and discuss the latest news, deals and more about SIA, Star Alliance Partners and other airlines. [(SQTalk)](http://www.sqtalk.com/forum/index.php)

3. Both SVM and XGBoost can potentially be further optimised through hyperparameter tuning. [(SVC tuning)](https://medium.com/all-things-ai/in-depth-parameter-tuning-for-svc-758215394769) [(XGBoost tuning)](https://towardsdatascience.com/xgboost-fine-tune-and-optimize-your-model-23d996fab663) 

\*Note: Due to the upload size limitation of GitHub, the data source have been separated - they can be found [here](https://drive.google.com/drive/folders/1IIywNaOOiJ_y2l8D7Nyv5xLrEFBGb0C7?usp=sharing).
