# Classifying horse activities with big data using machine learning

- [Introduction](#introduction)
- [Pipeline](#pipeline)
- [Approach](#approach)

# Introduction 
This is the repository of the experimantal side of our published article named **Classifying horse activities with big data using machine learning**, in *Kuwait Jurnal of Science* that is fully available [here](https://journalskuwait.org/kjs/index.php/KJS/article/view/19571).

We obtained very good results in means of accuracy to classify the horse activities, namely (94.62%) by using **Extra Trees** algorithm. Below the approach we developed will be shared in short. Also, the code has self explanatory thanks to the comment lines. For more information, reader is referred to the article.

Please do not hesitate to contact us for any reason about the publication or code, here is our e-mails.

Derya Birant: derya.birant@deu.edu.tr

Emircan Tepe: emircan.tepe@ceng.deu.edu.tr

# Pipeline

First of all we give our pipeline. The code is consist of several parts, that can also be seen from our pipeline. 


![Figure1_eski](https://user-images.githubusercontent.com/73601642/175987903-c950580e-e9f5-4876-94df-53e596035a9a.png)


The dataset we worked on is publicly avilable, shared by (*Kamminga et all.*, available [here](https://www.mdpi.com/2306-5729/4/4/131)).

Here is the abstract definition of the data set.

>Movement data were collected at a riding stable over seven days. The dataset comprises data from 18 individual horses and ponies with 1.2 million 2-s data samples, of which 93,303 samples have been tagged with labels (labeled data). Data from 11 subjects were labeled. The data from six subjects and six activities were labeled more extensively. Data were collected during horse riding sessions and when the horses freely roamed the pasture over seven days. Sensor devices were attached to a collar that was positioned around the neck of horses. The orientation of the sensor devices was not strictly fixed. The sensors devices contained a three-axis accelerometer, gyroscope, and magnetometer and were sampled at 100 Hz. (*Kamminga et all.*)

As the above paragraph refers, the dataset contains null and unlabeled rows and we need to disard them for supervised learning algorithms. the commonly labeled six horses (namely Bacardi, Driekus, Galoway, Happy, Patron, and Zafir) and five activities (walking, standing, grazing, galloping, and trotting) were used to provide sufficient accelerometer data for training. Also the data coming from other than accelerator sensor is accapted as **unreliable**, so also these columns were discared. This work is done in the notebook named **DataPreprocessing**. 

Feature extraction progress, consisting of 
- Filtering
- Windowing
- Adding statistics as features extracted from the data

In the filtering process, the low-pass Butterworth filter method with a cut-off frequency of 30 Hz was used and the features were extracted with a sliding window of two seconds with 50% overlap. Below you can find the features extracted from the data.

| **ID** | **Feature**             |
|--------|-------------------------|
| F1     | Min                     |
| F2     | Max                     |
| F3     | Mean                    |
| F4     | Median                  |
| F5     | Standard Deviation      |
| F6     | Covariance              |
| F7     | Percentile(25)          |
| F8     | Percentile(75)          |
| F9     | Number of Zero Crossing |
| F10    | Peak-to-Peak Value      |
| F11    | Root Mean Squared(RMS)  |
| F12    | Kurtosis                |
| F13    | Skewness                |
| F14    | Crest Factor            |
| F15    | Sample entropy          |
| F16    | Spectral Entropy        |
| F17    | Energy                  |

All these work conducted in the notebook named **FeatureExtraction**.

The rest is all about splitting the dataset for creating the model and testing, which were all conducted using the functions where are in the notebook named **Machine Learning**.

Also, there is another notebook named **ActivityPlot**, that consists of the functions used for plotting purposes. 

These flow of pipeline procedure can be easily followed in the notebook named **main**. 

As comment lines indicates, if you never run it locally, you may need to unblock some of the codes in the **main** notebook, then you will have them in your local set up.  
# Approach and Results

The approach we developed is based on taking individual features (age, gender, etc.) of horses into account, not in a way of adding them as features to the dataset (Unfortunately, these were not available.) but creating model per horse. Because the characteristics of an horse, or an animal in a more general manner depends on the specific features of it. 

As an overall result, this approach gives a better accuracy that can also be observed from the below figure.
![image](https://user-images.githubusercontent.com/73601642/175988137-e28d72cb-f4d9-4d99-9b5b-1f4b38e8133c.png)

## Future Work
>In future studies, the proposed model can be extended by using different sensors such as a gyroscope
and magnetometer. Even for the same activity, different horses have distinct movement modes since
their physical conditions (i.e., age, weight, height, and gender) and habits affect their movements. This
means that only a horse’s own movement data can reflect his own activity completely and accurately. The
fact that we got the best performance in the per-subject (personalized) model can be evidence to support
this conclusion. This conclusion brings us another question: can we identify horses according to their
movements? In other words, can we extract the activity fingerprint for authentication? This question
(horse identification) can be explored in future work. Furthermore, in the future, different predictive
models can be built for other animal species such as sheep or dogs.






 


