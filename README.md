# Training_session_interval_detection
## Project Overview : 
The Training Session Interval Detection project is aimed at developing a machine learning model to detect intervals in a cycling training session. This detection is based on a clustering method that utilizes power, cadence, and heart rate data, subsequently compiling these intervals into a structured table..

## Librairies used
- pandas
- numpy
- scikit-learn (Kmeans, DBSCAN)
- matplotlib
- seaborn

## Skills : 
- Machine Learning Models for clustering: We employ K-means and DBSCAN machine learning models for clustering data points, which helps identify intervals within training sessions.
- Hyperparameter Tuning: Hyperparameter tuning is implemented to optimize the Kmeans model's performance by finding the best values for hyperparameters.
- Time Series Analysis: Handling and analyzing time-based data to uncover temporal trends and variations.

## 1. Overview of the data
We utilize two cycling activity data for this project. Both datasets contain interval training, with the first consisting of 3 sets of 10-minute intervals and the second comprising a similar structure but with the last 5 minutes of the second and third sets following a (20/40) interval pattern.

## 2. Model Used
Two machine learning algorithms are used to split data point into cluster

- Kmeans : We generate an inertia vs. the number of clusters plot to assist users in selecting the optimal number of clusters, using the elbow method.
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/e2f7af9f-a34c-4567-82d4-1c8a429072e5)

- DBSCAN : For DBSCAN, we fix the parameters as eps=0.05 and min_samples=10 after conducting several tests.

## 3. Interval creation
Based on the clusters determined by the two models, we create intervals. To prevent numerous short-duration intervals, we merge intervals with less than 15 data points into the surrounding clusters. A summary table is then generated, highlighting intervals with a Normalized Power above a certain threshold for easy retrieval.

## 4. Results
Here are the resulting clusters and intervals for the first activity (3x10' constant intervals):

K-means produces coherent results for long and constant interval training sessions:
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/7f1a8a9e-03e9-410e-aa35-1263bdc06ca2)
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/e1dd6cfc-928a-456d-a6ee-a30d3a9e5039)

DBSCAN also performs well, generating various clusters; however, it may place the start of intervals (approximately 30 seconds) in different clusters than the rest of the interval:
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/56f14365-2964-497c-8e85-53ab66d1d987)
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/bdb3da17-a8c0-4bc8-9e31-e0415f949ca6)

For the second activity (3x10' with the last 2 sets having 5*(20/40)), we observe: 

K-means works reasonably well for this activity but may not accurately identify the 20/40 intervals at the end of the 10-minute sets:
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/628229ef-71de-4b77-8a42-937d17cf5733)
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/da1dc7a0-b427-465e-9068-e669401df377)


DBSCAN, on the other hand, performs better on the 20/40 intervals, capturing most of the intervals : 
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/7f8d52ad-f1cc-4761-bf32-bf5b5d4cb7da)
![image](https://github.com/VioleauPierre/Training_session_interval_detection/assets/129098391/2a96a8a1-62ab-4911-924b-eab56fd361df)

## 5. Further work
Future work on this project aims to enhance interval detection, making it applicable to racing data. The goal is to identify key points in races and provide feedback on the required capacity to achieve victory.
