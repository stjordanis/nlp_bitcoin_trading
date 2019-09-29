# Bitcoin Topic Modeling/Sentiment Analysis Using NLP and Trader Using LSTM
I applied **natural language processing (NLP)** on news articles to perform **topic modeling** using bag-of-words approach and **sentiment analysis** using open source modules. Topic modeling gives a very consie visual for the user to understand topics and trends revolving around Bitcoin and cryptocurrency over time. Also, features created from sentiment analysis were combined with other features (Bitcoin's open price, close price, volume, etc.) to build a **LSTM model to predict Bitcoin price**.

## Project Intro/Objective
I specifically chose Bitcoin over traditional stocks to apply NLP because Bitcoin only has two analysis components (technical and sentimental) and is missing the fundamental, which traditional stocks all have. This is good since it means that sentimental analysis has greater power of affecting Bitcoin price. However, the difficulty of sentimental analysis has always been limited by human factors. There are 3.2 million online articles and 500 million tweets **daily**, and it is **impossible** for humans to process this much information. Using state-of-the-art machine learning algorithms, it has become possible to not only process this much information but to use it as features for prediction models to provide highly advanced guidances.

Refer to presentations for more lighter intro to my project  
* [Presentation Link - Google Slides](https://docs.google.com/presentation/d/1v__ZPV--fQRT2HkwEQG_ULtZ8vP9zDoMuestRkisUOg/edit?usp=sharing)  
* [Presentation Link - Hard Copy](https://github.com/silvernine209/bitcoin_trader/raw/master/presentation.pptx)

## Datasets Used
* RAVDESS : [Download the Data](https://zenodo.org/record/1188976#.XVDlOi2ZO3V)
* TESS : [Scrape the Data](https://github.com/silvernine209/voice_emotion_classifier/blob/master/download_tess_dataset_scraper.ipynb)

## Methods Used
* Audio Signal Processing
* Feature Engineering
* LightGBM Classifier
* Data Visualization
* Flask App for Production Deployment : [Demo Link - YouTube](https://youtu.be/6blqy-s0VpM)

## Notable Technologies Used
* Python 3, Jupyter Notebook
* Pandas, Numpy, Matplotlib, Seaborn # Data Processing/Visualization tools
* LightGBM, Scikit-learn # Models
* RandomizedSearchCV # Automatic hyperparameter tuning & Cross validation
* Libroa # Audio signal processing
* etc. 

## Feature Engineering
Overall, I had very clean and fairly balanced dataset between 8 different emotions. After evaluating most of files for each emotion, I determined emotions "neutral" and "calm" could be combined into one emotion since they were very similar. It also improved class imbalance. Below is a quick look at my data.
![Data Stat](img/data_stat.PNG)


* **Truncating Silences**- Get rid of useless data
* **Auto Correlation** - Attempt to remove noise and find fundamental frequency
* **Pitch Tracking** - Used root mean square of energy to find strong timbres of voice to find true fundamental frequencies.
* **Mel-frequency cepstral coefficients** - Similar to fingerprints of audio files. Best if used in moderation in order to generalize.
* **Percentiles** - Took different percentile values of time-domain signals so that it's time insensitive. Losing info, but helps to generalize.

## Model 
Logistic regression was used as baseline model for this multi-class classification project. For the final model, LightGBM with RandomizedSearchCV was used for hyperparameter tuning and cross validation with 5 folds on the training data. While lacking in explainability compared to the logistic regression, LightGBM is preffered for its better scores as shown below.  
![Models](img/models.PNG)


## Result 
Below is confusion matrix generated from LightGBM model. It performed very well on the test dataset as already shown in the various scores from the Model section. Although very surprising, I contribute this too-good-to-be true results to my dataset. First of all, all audio files in the dataset were recorded with minimal noises. Secondly, very similar sentences repeated in the dataset, which was not optimal.  
![Confusion Matrix](img/confusion_matrix.PNG)

## Conclusion
Overall, I was very happy that I was able to build a classifier that would classify different emotions using raw audio files (.wav) without using neural network as base. I pitched my model(LightGBM) as lighter and quicker, but true comparison has to be made in terms of time and performance since quicker execution time might not be able to justify significant performance boost you could potentially get with NN-based architecture. However, with the current model, I'm pretty confident in its ability to generalize due to the pre-processing and feature engineering performed. Furthermore, with more robust and diverse data, LightGBM model will be able to generalize even better.

Again, here is a demo of a working flask app : [Demo Link - YouTube](https://youtu.be/6blqy-s0VpM)
