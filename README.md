# MARP
MARP is an app reviews opinions mining tool based on topics and intentions.  
This is a temporary artifact project for ICSME 2019 double-blind review

This program is free software. 

## Introduction
**MARP** is a tool for extracting user opinions from app review using topics and intentions.

## System requirement
Minimum requirement
  Windows operating system
  RAM: 12gb (more ram if you plan to run more than 3 millions reviews)
  CPU: intel i5
  
## Installation
1. Download the running package file ([MARPRunningPackage](https://drive.google.com/open?id=17zLKDEoIuy8xV20vhAumkk9cKPRg4u6G))
2. Unzip the package.
3. Run MARP.jar (no installation required)
4. (OPTIONAL) download 3 millions reviews. ([MARPRunningPackage.zip](http://www.mediafire.com/file/5a9s7858azv8ypk/REVIEWDATA_MARK.zip)) (see citation instruction 2)
5. (OPTIONAL) download custom intention patterns. [Comparison Intention](https://github.com/phong1990/ALPACA/blob/master/res/seedPatterns/newComparisons.csv)
## Usage
### Extracting opinions
1a. If you have the folder that contains compatible data for MARP, you can choose it as your "Data Folder"

![Step 1](https://github.com/artifact1/MARP_ICSME2019/blob/master/MARPstart.png)

1b. If you only have raw review data, first you will need to convert it into our .csv format (UTF-8, default separator). An example of the csv file can be found in the running package. Click on the "Import CSV" button to import it to an empty data folder of your choice. You only have to import once, next time you only need step 1a.

![Step 1b](https://github.com/phong1990/ALPACA/blob/master/res/img/step1-data.png)

2. Preprocessing: This step is required for MARP to analyze your data, and only needed to be done once. Please choose both word2vec training and pattern learning unless you know what you are doing (e.g. you have a better word2vec file from somewhere else, or you provide your own patterns). The artifacts produced by those options are vital to the next steps.

![Step 3](https://github.com/phong1990/ALPACA/blob/master/res/img/step3.png)

3. Expanding Intent Pattern: This option is not required, but it would greatly improve the result of MARP by expanding your patterns using the data from your reviews. There are two default intentions: Requests and Complaints. However, you can make your own patterns as in our comparison.csv example in the running package. The pattern format has to contain at least a fixed word (like the words in MARPRunningPackage\dictionary\baseWord\misc\) and at least a POS tag (from  [Penn Tree Bank site](https://catalog.ldc.upenn.edu/docs/LDC99T42/tagguid1.pdf) ). You can define different intentions based on your interest and find more similar patterns from you data. Remember to set your threshold of how similar the patterns need to be to the original patterns.

![Step 6](https://github.com/phong1990/ALPACA/blob/master/res/img/step5.png)

The mined patterns:

![Step 6patt](https://github.com/phong1990/ALPACA/blob/master/res/img/patterms.png)

4. Extracting opinions: An opinion is a phrase that match an intention pattern and describe the topic of interest. You can import the keywords set from step 5 and the pattern set expanded on step 6 (or use our default intentions, but the results will not be as good since MARP is data-driven). Please remember to choose a threshold for this step as it would directly affect the final result. The result is an .html file with all the opinions found.

![Step 7](https://github.com/phong1990/ALPACA/blob/master/res/img/step6.png)

This is how the final results should look like:

![result](https://github.com/artifact1/MARP_ICSME2019/blob/master/exampleResult1.png)

# Bugs note
We have yet to release this version to the public for testing, therefore, some bugs may still occur when you run it on your computer environment. In case you cannot run the program, we would like to invite you to look at the example results in here [examples](https://github.com/artifact1/MARP_ICSME2019/tree/master/exampleResults/MagicTiles) to see what should be expected from MARP.
  
## Data
1. Our vocabulary data is stored under MARPRunningPackage\dictionary\baseWord. The folder contains:
  (a) \dictionary\misc: all functional words. You can add more words of interest to domain.txt. Those words will be used to define patterns. (like "fix" is a common word in reviews, often indicating a problem needed fixing.);
  (b) \dictionary\wordnet: contains all the words from wordnet 3.0;
  (c) \dictionary\newword: contains the words that are not from wordnet 3.0, or not well defined (such as lacking verb/noun/adj forms, or lacking irregular variants)
2. The \dictionary\correctorTraining folder is a text corpus from wikipedia, used to improve the accuracy of our spelling corrector. You can change to other text corpus if you want to.
3. \dictionary\edu folder contain a Stanford NLP tagger for English.
4. \dictionary\improvised has some words, which I don't remember what they are for, but I'm too afraid to delete them and risk breaking the program.
5. \dictionary\Map: contains the correct words for common mistakes in reviews. Overtime, I will add more and more common errors to this map with new data.
6. \dictionary\stop: those are the stop words. 
7. \dictionary\trigramData: this is a trained model for our spellCorrector. Do not delete or modify anything from it. We trained it with a few billions lines of text so it's likely not not ever get an update.
8. \dictionary\config.ini: this file is for locating the dictionary folder in MARP. You need to change the path inside to the correct location in your computer.
9. \aditionalText: this is the processed text of 3 millions reviews. You can use it as a supplement text corpus for training word2vec for your data if you don't have too many reviews. It helps the deeplearning process understand the relationships between words better in the context of mobile app. Therefore, the more reviews you have, the better MARP will be able to understand it.
10. \replication: this has around 13k reviews of Magic Tiles to replicate our experiments and for demonstrate the usage of MARP. You can use it to learn how to use our tool.
11. \evaluation: this contains our labeled truthsets and developer evaluation results
