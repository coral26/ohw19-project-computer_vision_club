# ohw19-project-computer_vision_club
computer vision club project for ocean hackweek 2019

Welcome to the computer vision club at OHW 2019. Please join us in the slack channel #computervisionclub-2

## Rules
RULE 1: name notebooks and files with lower case letters and _ for spaces.  
RULE 2: have fun and don't freak out.

## Structuring the repo

Improve the `README.md` by filling individual sections from the project guidelines:

[https://oceanhackweek.github.io/wiki/project_guidelines.html](https://oceanhackweek.github.io/wiki/project_guidelines.html)

#### Project title

*Underwater currency counter: Kickass AI to count sandollars*

#### Discussion Participants

Jordan Pierce  

Dimitris Politikos  

Massimo Di Stefano
...  
...  
...  
...  

#### The Problem

Annotating imagery data by hand is time consuming, mundane and costly which is only exacerbated with larger datasets. What if you could use AI to help you with the brunt of the workload, leaving you with the simple task of going over its predictions and ensuring it is correct?

This project aims to use benthic habitat imagery data collected from ROVs to train a deep object recognition algorithm. With a learned model, its task will then be used to make predictions on non-annotated data. Predictions with high enough confidences will be retained as per the users discretion.

### Workflow at a glance:

1.) Parsing/cleaning existing annotation data   
2.) Extracting and organizing training data   
3.) Preprocessing and augmenting training data   
4.) Train object recognition/image classification network  
5.) Apply trained model to new data, take *good* predictions and add to training data  

#### Application example

*put words here*    


#### Specific tasks

1.) Currently we have *some* annotations in XML format, how can we clean and parse that data into a format that can be used to then extract the individual annotation instances? 
- Which class(es) should we be paying attention to and what is the distribution?
- Go through all XML annotations and record all of the different number of organisms annotated; ~find the majority class~ __Sand Dollars!__
- Create new annotations that only contain the class that we're interested in __not completed__

*Secondary task: how can you adjust your function(s) to incorporate multiple classes instead of just the single class?*

Notebook with first step for [data preparation](https://gist.github.com/f750d04fca54251f67d0b42aad849ffb)   
which generates: 

[test.csv](https://gist.github.com/4d651a9b3ac205da83a4d16ef236bf04)

[train.csv](https://gist.github.com/db7dc567eaa7118ea3de425d58337cad)

Along with the `tf_records` (dataset.tfrecords)


##### Edit: this can *mostly* be done using existing scripts to save time! Still need to find a way to parse *just* the majority class

  
2.) With all these new, cleanly parsed XML files, we then need to convert ALL of the annotation data into another data structure that could then be used to extract the individual patches from the original images.
- Create a function(s) that will convert XML into some easy to work with data structure. __completed__
- Attributes of each instance/annotation should have annotation id, original image filename, xmin, ymin, xmax, ymax, area (any others?) __completed__
- The last step is to convert to .csv format into a TFRecord (refer to Slack page for information) or see [here](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/using_your_own_dataset.md) __not completed__

*Secondary task: how can you adjust your function(s) to incorporate multiple classes instead of just the single class? How should you organize the folder heiarchary? Are there any other attributes you can think of that might help to create cool graphics?*

##### Edit: this *can* be done using existing scripts to save time! Refer to [raccoon tutorial](https://github.com/datitran/raccoon_dataset) (e.g. `xml_to_csv.py`)

  
3.) We now have a TFRecord file for both the training and testing data; these are essentially the instructions for how the training data will be fed into the model for the training. However, we need to provide further instructions for how the training images will be preprocessed in a way so that they'll be learnable/acceptable as input. Things to look at:

- Zero-mean, normalizing, standardizing and rescaling the images, which do we do?
- Data augmentation (flipping, flopping, rotating, blurring, sharpening, pixel dropout)
- How do we actually feed the data into the model for training? (python generators?)

  
4.) Object recognition consists of two parts: object detection, followed by image classification. The framework thus consists of two components. 
- Which framework should we use and why? (see [model zoo](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md) for all of the easy to grab frameworks)
- Which convolutional neural network architecture should we use?
- Transfer learning? (e.g. use weights of previously trained networks to assist in our training)
- HYPER PARAMETERS!!! (loss, optimization and metrics)


  
5.) With a trained model, what can we do with it to assist us in annotatating data in the future?
- What is the prediction output exactly?
- How can that be used to create annotations?
- What about prediction confidence? How sure are we that it is right?

  
6.) Additional tasks:  
- Make everything go faster  
- Create secondary data visualizations that'll make people poo their pants (e.g. [Tensorboard](https://itnext.io/how-to-use-tensorboard-5d82f8654496))  
- Add images to github README.md file (*very important*)

#### Existing methods
  
*put words here*    

#### Proposed methods/tools

Keras - for building and training the network   
OpenCv - image processing and augmentation  
Scikit image - image processing and augmentation  
Pandas - data science  
Numpy and/or Cupy - data science  
Numba - SPEED  
labelImg -- has to be installed in your cloud environment. Use pip to install labelImg in your terminal. 

#### Background reading/watching

YOLO: https://www.youtube.com/watch?v=Cgxsv1riJhI   

### Project Organization

Name : Task

### Longterm project objective 
  
Help our robot overlords achieve world domination

![](robot_overlord.gif)


