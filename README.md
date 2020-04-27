# DeepLearning

[Our notebook can be found online via Google Colab](https://colab.research.google.com/drive/1u6GA0axP2lsY2ozk0VPUU-LCZrf2Aoxk)

## Overview
Theoretically, you should be able to load our python notebook into Google Collab, copy our dataset into your drive, hit run all and be good, but our code isn't fool-proof so you may still need to understand a little bit about it to get it to work.  Our model itself is discussed from a high level in our final report and our code has a fair amount of inline comments noting what particular lines do, but I'd like this to be a guide explaining our architecture as a whole.

Our "main" code is fairly short, only a couple dozen lines, and most of the work is done in our many many helper functions.  The ones you might want to know are:

```
def labelconvert(labels, target):
```
This helper function formats our labels for binary classification

```
def train(data, labels, file, user, loud=0):
```
This functions trains our CNN with data using labels as the what user we are counting as a match.  The model is saved locally ti file.h5

```
def evaluate(test,file):
```
Given an array of test data and the filename of the model it will return the matrix of our guesses.  For binary classification this is a list of percentages, one for each test email, and the percentage is our confidence that we think that given email is from our targeted user

```
def fin(filedir, emails, verbose=1):
```
This function reads our data in.   emails=number of emails from each user to read in.

```
def score(evaluation, labels, v):
```
This functions takes our data from evaluate and prints it in a more easily digestable form

```
def getStatsModel(file_name, threshold=0.25):
```
This function takes our data saved to disk and performs statistical analysis on it

## Working With Google Drive
As we worked in colab, the data we used is currently stored in Google Drive.  You can gain access to our dataset [here](https://drive.google.com/drive/folders/1AZryWUTrIoCvF-mwNqw0wUdrXisvtAEt?usp=sharing), although the zipped and cleaned dataset is also included in the github repo in case that link doesn't work or you'd rather access the data some other way.  If you don't simply add the above folder to your drive be sure to change the filepaths in the code to wherever you put the data and wherever you want the models saved
You can add this to your own Google Drive.  If you save it under the same name and you're running this in Collab then you shouldn't need to change any code.  If you rename anything you'll need to update the filenames in our "main" (the final block).  Regardless of if you rename it or not, you'll need to connect your Google Drive.  The very first block does this, just click the link and follow the instructions.  Unfortunately, file IO is very slow, taking over an hour to read in all of the training data (on account of the +28K files in our processed dataset)

## If Running Locally
If you're running this on a non-Collab machine, you'll need at minimum the following libraries:
Tensorflow, matplotlib, pandas, collections,  Install using pip, source, or whatever other method you prefer.  It is also strongly recommended to have the appropriate CUDA libraries installed if you plan on training locally otherwise it will take quite a long time.  You also may want to remove the first block (the google collab one) if you plan on reading your files locally.  File IO this way is very fast, taking only a few seconds.

## Canned Models
The models we discussed in our report will also be included in our submission in a zipped archive.  You're free to train yourself, but between reading in the data then training this will take a few hours.  If you want to use our models instead you can set the "train_bool" variable in our "main" to 0 and change the lines of code that read
e=evaluate(data, "/content/drive/My Drive/TEST/Models/SingleCNN/enronsat_"+str(i))
To whatever path you put the models in.

## Evaluation Error
We've had some runtime related weirdness with evaluating our data.  We can train just fine but we sometimes crash during our evaluation.  The first one almost always works, but after that there's a small chance that our code will halt.  If this happens you can resume evaluation where you left off by following these instructions:
1. Restart the runtime
2. Change train_bool flag to 0
3. Change the range of users to eval.  We default with range(0, 10) for 0-9, if you failed on user 3 set this to range(3, 9)
4. Run all.


