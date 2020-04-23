## This file will explain the contents of the files in this folder

1. **Extract physical features.ipynb** => This file extracts meta data details from the excel sheet provided by Michael Appleby (MA).  An idea of the contents of this excel sheet are provided through EDA.  Meta characteristics of files are extracted using tika. But they are not of very use as many of the file characteristics are modified/ over written while transferring them on drives. A simple set of models are developed based on the data. 

Pre-processed metadata file is saved as 'metadata_with_filesize_lastmodified.pkl' for future use

**Models used on all the data from the excel sheet **
- **DecisionTree Classifier** 
-  with 80:20 Train/Test ratio
-  Binary classification -> Accuracy: 0.9752871562826314 (only Yes or No classes for selection)
-  Multi class classification -> Accuracy: 0.9470501218238775 (Multi class - ret schedule classification )

**Model is tested with following text file formats**
- accepted_file_list(restricted set of file formats) = ['pdf','rtf','txt','msg','doc','docx','xls','xlsx','mbx']

- **DecisionTreeClassifier**
- with 80:20 Train/Test ratio
- Multi class classification on ret schedule:  Accuracy: 0.9324432702740953

**Tested on websites data for the restricted set fof file formats**
- created a dataframe from the websites data
- Cleaned dataframe is saved in the 'Websites_processed.pkl' pickle file  for future use. The  columns are :'fileextension', 'documentname', 'file_path', 'file_size',  'datelastmodified', 'parent11', 'parent10'. (parent11 is the top most folder and parent10 is one step below parent11)

- accepted_file_list(restricted set of file formats) = ['pdf','rtf','txt','msg','doc','docx','xls','xlsx','mbx']

- The decision tree classifier trained on the metadata file predicted the website contents as follows:

|ret. schedule   | num of files|
| :----: | :----------:|
|16      | 930         | 
|23      | 49735       | 
|33    | 32          |
 
 
2. **Conventional_NLP.ipynb** - This file explores contents of the files on the hard drive. This file has all the pre processing steps as simple hand written functions for NLP pipeline. 

- The data file formats are restricted to ['pdf','rtf','txt','msg','doc','docx','xls','xlsx','mbx'] only.
- contents from the files in the websites folder (unlabelled data) is saved as 'websites_contents_NLP.pkl' for future use. Columns are the document name and cleaned tokens from the files.
- contents from the files in the labelled data ( folder 'a') is saved as 'a_cleaned_ready_for_NLP.pkl' for future use. 

![alt Number of files according to retention schedules in the data](a_ret_schedules_.png)

### Should remember that I have not applied these models Paul's broad clssificationto websites data for comparison

Total files in the labelled data = 93824

Total files in the websites data = 28411

**Models used**
- **Naive Bayes** : Multiclass classification labelled data
- Train:test = 80:20
|class |precision|    recall|  f1-score|   support|
| :----: | :-----:| :-----:| :-----:| :-----:|
         | 02      | 0.44     | 0.89     | 0.59      |2673|
          |03      | 0.93      |0.38     | 0.54      |1007|
         | 04      | 0.96     | 0.76     | 0.85      |1600|
         | 05 |      0.95   |   0.49  |    0.65  |    1737|
         | 06     |  0.00    |  0.00     | 0.00      |  13|
         | 07      | 1.00   |   0.01  |    0.01|       541|
          |10    |   0.00    |  0.00    |  0.00      | 190|
          |11      | 1.00    |  0.11    |  0.20     |  527|
          |16   |    1.00 |     0.00  |    0.01|       328|
          |20    |   0.99 |     0.17  |    0.29 |      540|
          |21    |   1.00 |     0.01 |     0.01 |      521|
         | 23    |   0.99 |     0.43 |     0.60 |     1379|
         | 24    |   0.51 |     0.98 |     0.67   |   3873|
         |24b    |   1.00 |     0.02 |     0.04  |     306|
         | 25    |   0.00  |    0.00  |    0.00  |      44|
         | 27     |  0.94  |    0.12 |     0.22 |      491|
         | 28     |  0.97  |    0.14 |     0.25  |     427|
         | 32    |   0.00  |    0.00 |     0.00  |     429|
         | 33    |   0.71  |    0.79  |    0.75   |   2139|
  |  accuracy|          |           |      0.60  |   18765|
  | macro avg     |  0.70   |   0.28   |   0.30   |  18765|
|weighted avg  |     0.73    |  0.60    |  0.54   |  18765|

- **Naive Bayes** : Binary class classification on Labelled data
- Train:test = 80:20
|class |precision|    recall|  f1-score|   support|
| :----: | :-----:| :-----:| :-----:| :-----:|
      |   NO    |   0.83    |  1.00   |   0.91 |    14492|
      |   YES   |    0.98    |  0.30   |   0.46  |    4273|
  |  accuracy    |         |          |    0.84   |  18765|
  | macro avg    |   0.90    |  0.65   |   0.68  |   18765|
|weighted avg   |    0.86    |  0.84     | 0.80    | 18765|

- **Naive Bayes** : multi class classification on unLabelled (websites) data

|class |Num_docs_in_category|
| :----: | :-----:|
|02| 17324|
 |03|5|
 |23|4|
 |24|11056|
 |27|2|
 |33|20|

- **Naive Bayes** : binary class classification on unLabelled (websites) data
|class |Num_docs_in_category|
| :----: | :-----:|
|NO |28411|
|YES| 0 |


- **Support Vector Machine**: Multi class classification on labelled data
- Train:test = 80:20
|class |precision|    recall|  f1-score|   support|
| :----: | :-----:| :-----:| :-----:| :-----:|
|02      | 0.80     | 0.75   |   0.77  |    2673|
       |   03    |   0.73   |   0.94    |  0.82   |   1007|
       |   04    |   0.92  |    0.88  |    0.90    |  1600|
      |    05     |  0.83  |    0.81  |    0.82  |    1737|
      |    06   |    1.00  |    0.08  |    0.14    |    13|
    |      07   |    0.84  |    0.62  |    0.71   |    541|
     |     10   |    0.87    |  0.29   |   0.43   |    190|
     |     11     |  0.85  |    0.43 |     0.57  |     527|
      |    16     |  0.90   |   0.88 |     0.89   |    328|
      |    20    |   0.85    |  0.70   |   0.77   |    540|
       |   21  |     0.86    |  0.46   |   0.60  |     521|
       |   23  |     0.85   |   0.86   |   0.86  |    1379|
       |   24  |     0.81   |   0.91   |   0.86  |    3873|
      |   24a  |     0.00  |    0.00  |    0.00  |       0|
       |  24b |      0.89  |    0.95 |     0.92 |      306|
        |  25  |     0.92  |    0.25  |    0.39   |     44|
        |  27 |      0.83   |   0.65  |    0.73  |     491|
         | 28  |     0.88   |   0.66  |    0.76   |    427|
         | 32    |   0.83   |   0.51 |     0.63   |    429|
        |  33    |   0.65  |    0.87  |    0.74   |   2139|
    |accuracy|           |            |    0.80   |  18765|
  | macro avg    |   0.80    |  0.62    |  0.67     |18765|
|weighted avg     |  0.81    |  0.80    |  0.79     |18765|

- **Support Vector Machine**: Binary class classification on labelled data
- Train:test = 80:20
|class |precision|    recall|  f1-score|   support|
| :----: | :-----:| :-----:| :-----:| :-----:|            
     |     NO  |     0.87  |    1.00   |   0.93  |   14492|
      |   YES    |   0.97   |   0.50   |   0.66   |   4273|
    |accuracy  |           |           |   0.88   |  18765|
   |macro avg  |     0.92   |   0.75   |   0.79   |  18765|
|weighted avg   |    0.89   |   0.88  |    0.87    | 18765|

- **Linear Support Vector Machine Multi class unlabelled data**
|class |Num_docs_in_category|
| :----: | :-----:|
|02|10980|
 |03|2208|
|04|109|
|05|897|
|07|1174|
 |10|7|
 |11|4|
 |16|6|
 |20|505|
|21|1|
 |23|2411|
 |24|8204|
 |24a|167|
 |24b|8|
 |27|80|
 |28|3|
 |32|2|
 |33|1645|
 
 - **Linear Support Vector Machine Binary class unlabelled data**
 |class |Num_docs_in_category|
 | :----: | :-----:|
 |NO|28411|
 |YES| 0 |
 
 - **Logistic Regression Machine Multi class labelled data**
 - Train:test = 80:20
|class |precision|    recall|  f1-score|   support|
| :----: | :-----:| :-----:| :-----:| :-----:|  
      | 02    |   0.86|      0.89  |    0.87  |    2673|
        |  03 |      0.85  |    0.85  |    0.85   |   1007|
        |  04  |     0.97  |    0.95  |    0.96   |   1600|
        |  05  |     0.92  |    0.92   |   0.92   |   1737|
        |  06    |   0.92  |    0.85   |   0.88    |    13|
       |   07   |    0.86   |   0.84  |    0.85  |     541|
        |  10   |    0.92   |   0.78  |    0.85 |      190|
        |  11  |     0.61  |    0.89   |   0.72   |    527|
         | 16   |    0.98   |   0.97  |    0.98  |     328|
        |  20   |    0.89   |   0.86  |    0.87   |    540|
         | 21 |      0.88  |    0.85   |   0.86  |     521|
        |  23 |      0.93  |    0.94    |  0.93   |   1379|
        |  24 |      0.94   |   0.94   |   0.94  |    3873|
        | 24b  |     0.99  |    0.97  |    0.98  |     306|
        |  25   |    0.93  |    0.61  |    0.74  |      44|
         | 27   |    0.92  |    0.82  |    0.87  |     491|
         | 28   |    0.94  |    0.76  |    0.84 |      427|
         | 32   |    0.78  |    0.73  |    0.75  |     429|
         | 33   |    0.93  |    0.89 |     0.91  |    2139|
   | accuracy|            |          |     0.90   |  18765|
 |  macro avg |      0.89 |     0.86  |    0.87  |   18765|
|weighted avg   |    0.90 |     0.90  |    0.90  |   18765|

- **Logistic Regression Machine binary class labelled data**
 - Train:test = 80:20
|class |precision|    recall|  f1-score|   support|
| :----: | :-----:| :-----:| :-----:| :-----:| 
|NO      | 0.97   |   0.98  |    0.98  |   14492|
       |  YES   |    0.94   |   0.90   |   0.92 |     4273|
    |accuracy  |           |          |    0.96 |    18765|
  | macro avg|       0.96  |    0.94  |    0.95 |    18765|
|weighted avg |      0.96   |   0.96  |    0.96  |   18765|


- **Logistic Regression Machine Multi class unlabelled data**
|class |Num_docs_in_category|
| :----: | :-----:|
|02| 12485|
 |03| 11|
 |04| 35|
 |05| 2381|
 |07| 369|
 |10|11|
 |11| 2342|
 |16| 495|
|20| 408|
 |21| 328|
 |23|2453|
 |24|6141|
 |24b|3|
 |27|51|
 |28| 56|
 |32| 5|
 |33| 837|
 
 - **Logistic Regression Machine Binary class unlabelled data**
 |class |Num_docs_in_category|
| :----: | :-----:|
|NO|27696|
 |YES| 715|
 
- **RandomForest Classification Multi class labelled data**
 - Train:test = 80:20
|class |precision|    recall|  f1-score|   support|
| :----: | :-----:| :-----:| :-----:| :-----:| 
|02    |   0.73 |     0.83 |     0.78  |    2673|
  |        03  |     0.81 |     0.82 |     0.82   |   1007|
  |        04   |    0.99   |   0.92  |    0.95  |    1600|
  |        05  |     0.90 |     0.86 |     0.88|      1737|
     |     06   |    1.00  |    0.08  |    0.14    |    13|
    |      07  |     0.97  |    0.65  |    0.78    |   541|
   |       10  |     0.98 |     0.51   |   0.67    |   190|
    |      11 |      0.60  |    0.78  |    0.68     |  527|
     |     16 |      1.00 |     0.89  |    0.94     |  328|
     |     20  |     0.93   |   0.73   |   0.82     |  540|
      |    21 |      0.97 |     0.56   |   0.71     |  521|
      |    23  |     0.93  |    0.86  |    0.90     | 1379|
      |   24   |    0.83   |   0.94   |   0.88     | 3873|
      |   24b  |     1.00 |     0.88  |    0.93   |    306|
      |    25  |     0.90  |    0.20  |    0.33    |    44|
      |    27  |     0.95   |   0.74   |   0.83   |    491|
       |   28  |     0.95   |   0.67  |    0.79   |    427|
       |   32  |     0.87   |   0.49  |    0.63  |     429|
        |  33  |     0.74   |   0.87  |    0.80   |   2139|
    |accuracy   |          |          |    0.84  |   18765|
   |macro avg    |   0.90   |   0.70    |  0.75   |  18765|
|weighted avg     |  0.85   |   0.84    |  0.83   |  18765|



- **RandomForest Classification Binary class labelled data**
 - Train:test = 80:20
|class |precision|    recall|  f1-score|   support|
| :----: | :-----:| :-----:| :-----:| :-----:| 
|NO     |  0.91    |  1.00  |    0.95  |   14492|
   |      YES   |    0.98 |     0.67  |    0.80  |    4273|
  |  accuracy  |         |           |     0.92   |  18765|
   |macro avg |      0.95  |    0.84     | 0.88   |  18765|
|weighted avg  |     0.93  |    0.92   |   0.92  |   18765|

- **RandomForest Classification Multi class unlabelled data**
|class |Num_docs_in_category|
| :----: | :-----:|
|02|8052|
 |03| 4|
 |05| 70|
 |07| 2|
 |11| 195|
 |20| 1|
|23|1417|
 |24| 17493|
 |27| 144|
 |28| 11|
|33|1022|



- **RandomForest Classification Binary class unlabelled data**
|class |Num_docs_in_category|
| :----: | :-----:|
|NO|28411|