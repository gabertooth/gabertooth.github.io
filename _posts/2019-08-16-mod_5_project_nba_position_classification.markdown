---
layout: post
title:      "Mod 5 Project NBA Position Classification"
date:       2019-08-16 11:12:35 -0400
permalink:  mod_5_project_nba_position_classification
---



__Project Background:__ The following Jupyter Notebook uses different classification machine learning modeling techniques to try and correctly identify a NBA players position based off of their physical traits and game stats. Due to the NBA shifting into a position-less basketball style of play, I thought it would be interesting to apply statistical python code to solve this problem. 

__Approach:__ The approach is simple, take data obtained from a kaggle open source data set that dates back to 1950 up until the 2017 NBA season. Using this data I will create four different types of models (KNN, SVM, RandomForest, Adaboost) and try to optimize each model using the modeling techniques learned in module 5. 

A __OSEMN framework__ was followed for this project:  

__Obtain:__ the data from the relevant resources and stakeholders  
__Scrub:__ Cleaning the data into formats that can be digested in Python packages such as Sklearn or Statsmodels Remember the "Garbage in, garbage out".  
__Explore:__ Using statistical methods and data analytic techniques explore the data to find significant patterns or trends  
__Model:__ Construct models to predict and forecast the data. Here we focus on our target variable which is price!  
__Interpret:__ Take the results of the analysis and model and create meaningful visualizations or presentations


This project was eye opening. It cemented many of the Machine Learning techniques learned throughout module 5. I truly believe I have both a technical and fundamental grasp on the following models, Random Forest, KNN, and SVM. I finally got to choose a topic for a project. Of course I chose the NBA. I am a very passionate Lebron James fan and will always say he is the GOAT. Anyway, I thought it would be perfect to classify NBA positions especially in the era of positionless basketball we see in todays game. I will now walk you through my analysis with code snippets that were necessary for the success of this project. 

The data set used can be found here, https://www.kaggle.com/drgilermo/nba-players-stats. It is a file with three different csv files. I used the player data and player stats csv's to run classification models on. The first step was to divide the data into different eras as not every year has the same stats. I decided to divide the data into the following:

 1. 1950-1956
 2. 1957-1979
 3. 1980-1998
 4. 1999-2017

From here I cleaned each of the data frames and ensured all of the data was digestible by the models I wanted to build. The four models I came up with were K-Nearest Neighbors, Adaboost, Random Forest, and Support Vector Machine. Below are the functions I built which were used for modeling each of the four data sets.

__Random Forest__
```
def random_forest(df,X,y): #Random Forest model
    X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=.2) #train test split
    clf= RandomForestClassifier(random_state=0) #classifier defined
    clf.fit(X_train, y_train) #fitted data
    preds= clf.predict(X_test) #predictions of model using test data
    acc = round(accuracy_score(preds, y_test) * 100,2) #basic accuracy score
    print("Accuracy is :{0}%".format(acc))
    feat_importances = pd.DataFrame(clf.feature_importances_, index=X.columns, columns=['Score']) #creating a list of top 10 features from RF model
    feat_importances = feat_importances.sort_values(by='Score',ascending=True) #sorting values
    feat_importances.plot(kind='barh') #plotting the features in a horizontal bar chart
    plt.show()
    pd.crosstab(y_test, preds, rownames=['Actual Result'], colnames=['Predicted Result']) #confusion matrix to show where the model predicted what positions
    
    Refined_X=feat_importances.index[-10:] #rerunning the model again this time using only the top 10 features
    X_key_features=df[Refined_X]
    y_key_features=df['Pos']

    X_train, X_test, y_train, y_test = train_test_split(X_key_features,y_key_features, test_size=.2)
    clf= RandomForestClassifier()
    clf.fit(X_train, y_train)
    preds= clf.predict(X_test)
    acc = round(accuracy_score(preds, y_test) * 100,2)
    print("Accuracy is :{0}%".format(acc))
    feat_importances = pd.DataFrame(clf.feature_importances_, index=X_key_features.columns, columns=['Score'])
    feat_importances = feat_importances.sort_values(by='Score',ascending=True)
    feat_importances.plot(kind='barh')
    plt.show()
    print(classification_report(y_test,preds))
    return pd.crosstab(y_test, preds, rownames=['Actual Result'], colnames=['Predicted Result'])
```

__SVM__
```
def SVM(df,X,y): #Support Vector Machine Model
    X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=.2) #train test split
    svclassifier = SVC(kernel='linear') #defining classifier
    svclassifier.fit(X_train, y_train) #fitting SVM classifier
    y_pred = svclassifier.predict(X_test) #predicting y values using classifier and X_test
    pd.crosstab(y_test, y_pred, rownames=['Actual Result'], colnames=['Predicted Result']) #confusion matrix again
    acc = round(accuracy_score(y_pred, y_test) * 100,2) #accuracy score
    print("Accuracy is :{0}%".format(acc))
    print(classification_report(y_test,y_pred)) #classification score with recall, precision, and F1 score
```

__KNN__
```
def KNN(X, y): #K Nearest Neighbor Model
    
    X_train, X_test, y_train, y_test = train_test_split(X,y, test_size=.2) #train test split

    clf= KNeighborsClassifier() #classifier defined
    clf.fit(X_train, y_train) #classifier fitted
    test_preds= clf.predict(X_test) #predicting y values using classifier and X_test
    acc = round(accuracy_score(test_preds, y_test) * 100,2) #accuracy score
    print("Accuracy is :{0}%".format(acc))
    print(classification_report(y_test,test_preds)) #classification score with recall, precision, and F1 score

    k_range =range(1,25) #Finding the optimal k
    scores= {} #accuracy scores dictionary
    scores_list= [] #scores list

    for k in k_range: #for loop to get each of the accuracy scores for different values of k
        knn = KNeighborsClassifier(n_neighbors=k)
        knn.fit(X_train, y_train)
        test_preds=knn.predict(X_test)
        scores[k] = accuracy_score(y_test, test_preds)
        scores_list.append(accuracy_score(y_test, test_preds))

    plt.plot(k_range, scores_list)
    plt.xlabel('Value of K')
    plt.ylabel('Testing Accuracy')
    plt.show() #graph to show how the accuracy changes as K increases from 1 to 25

    max(scores.items(), key=operator.itemgetter(1))[0] , max(scores.items(), key=operator.itemgetter(1))[1] #max accuracy 

    optimal_k= max(scores.items(), key=operator.itemgetter(1))[0] #best k variable created

    clf= KNeighborsClassifier(n_neighbors=optimal_k) #rerunning the model with the optimal k value
    clf.fit(X_train, y_train)
    test_preds= clf.predict(X_test)
    acc = round(accuracy_score(test_preds, y_test) * 100,2)
    print("Accuracy is :{0}%".format(acc))
    print(classification_report(y_test,test_preds))
    return pd.crosstab(y_test, test_preds, rownames=['Actual Result'], colnames=['Predicted Result'])
```

__Adaboost__
```
def ADABOOST(X, y):
    X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=.2) #train test split
    adaboost_clf = AdaBoostClassifier() #adaboost classifier 
    adaboost_clf.fit(X_train, y_train) #fit the model
    y_pred= adaboost_clf.predict(X_test)#predict the value of y using X_test
    acc = round(accuracy_score(y_pred, y_test) * 100,2) #accuracy score
    print("Accuracy is :{0}%".format(acc))
    print(classification_report(y_test,y_pred)) #classification report
    return pd.crosstab(y_test, y_pred, rownames=['Actual Result'], colnames=['Predicted Result']) #confusion matrix
```






