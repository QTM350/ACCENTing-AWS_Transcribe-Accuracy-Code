<p align="center">
  
 <img width="800" height="400" src="https://github.com/QTM350/ACCENTing-AWS_Transcribe-Accuracy-Code/blob/main/pics/awsT.jpeg">
 
</p>

---
# ACCENTing Transcribe’s Accuracy-Code
This project uses AWS Transcribe to make transcriptions out of English scripts recited in different accents. 

In combination with AWS Transcribe, we used Amazon S3 buckets to store our data output from AWS Transcribe. These tools allow us to do all the necessary conversions in order to make our project successful. 

In order to measure the accuracy of AWS Transcribe's speech-to-text, we took 3 different texts varying in syntax complexity and converted them into fifteen various audio files that contained a combination of one of the three difficulty ratings as well as one of the five accents (United States, United Kingdom, China, Spain, and India). 

One control we decided to account for is to only look at female voices. This helps control for other variations in the data. We tested these multiple transcripts from various scripts, using Transcribe that is within Sagemaker.

Our data analysis included using Levenshtein distances and a confidence review on Transcribe. The Levenshtein distances was used to measure the difference between two sequences. This helps to determine the amount of single character edits between two scripts. We have included this data in the repo for the user to view.

Anyone who is interested in replicating this project can access our data in this github repository. We also provide a [blog](https://colab.research.google.com/drive/1Zh4zfuPF4tj4p5B_aoUTPWHOtjMij6og?usp=sharing#scrollTo=tFOEa9EF71wM) on Google Colab that provides the motivation behind the project, explanations in our analysis (including what the Levenshtein distance is) and a visual for the confidence rating from Amazon Transcribe.

---

### ttsreader.com

We decided to use ttsreader.com for converting our original transcripts to speech due to the service’s “natural multilingual voice” feature. This webpage offers male & female voices, in different accents and different languages. It also allowed us to export and save the synthesized speech from our data text. 

*Our project limited the speeches to female voices to minimize the external noise that may have arisen from our analysis.*

![tss](pics/tts_reader.jpg)

---

# Navigating the Repository

#### To see the transcripts that are being used for transcription: [actual-transcript-for-comparison folder](https://github.com/QTM350/ACCENTing-AWS_Transcribe-Accuracy-Code/tree/main/actual-transcripts-for-comparison). This folder contains three text files/initial data that we input into ttsreader.com to generate into audio recordings. The scripts that we used were excerpts from the following:

##### - "Easy" Difficulty - A Pep Talk from Kid President by Kid President (SoulPancake)
##### - "Medium" Difficulty - Inside the Mind of a Master Procrastinator by Tim Urban (TedTalk)
##### - "Hard" Difficulty - The ability to estimate knowledge and performance in college: A metacognitive analysis by Howard T. Everson & Sigmund Tobias.

###### Links to the actual webpages and source of these excerpts are also provided at the bottom of the README. 

---
#### Because TTSReader is a paid service, we have provided a collection of all processed recordings in a [google drive](https://drive.google.com/drive/folders/1XMca6gJVa3iX1yEqHoQxlFnAMySBhFmX?usp=sharing). These files can also be located in the [audio-files-for-transcription folder](https://github.com/QTM350/ACCENTing-AWS_Transcribe-Accuracy-Code/tree/main/audio-files-for-transcription). However, we recommend accessing the **google drive** for the audio recordings as each file is organized by name and difficulty rating. The audio-files-for-transcription folder only contains the URLs of the recordings from Amazon S3 in a txt format without any discernernability within each URL. 

###### *All audio recordings are formatted as .wav files*

---
#### The result of a completed transcription job links to an Amazon Simple Storage Service (S3) presigned-url that contains our transcription in JSON format. To access a txt file containing all the generated transcripts from Amazon Transcribe: [aws-generated-transcriptions folder](https://github.com/QTM350/ACCENTing-AWS_Transcribe-Accuracy-Code/tree/main/aws-generated-transcripts). This txt file contains all fifteen transcribed text URLs. These links includes the origin country accent in combination with assigned difficulty rating within the URL. Check out our blog for a code snippet on how to generate transcripts using AWS Transcribe!

###### *All URLs in the .txt file contains transcripts formatted as .json files*

---
#### To see data pertaining to our calculated Levenshtein Distance: [Data for Levenshtein distance.csv](https://github.com/QTM350/ACCENTing-AWS_Transcribe-Accuracy-Code/blob/main/Data%20for%20Levenshtein%20distance.csv). This CSV file includes three columns:
##### 1. `Accent`: *The origin country used in ttsreader.com.*

##### 2. `Difficulty`: *The corresponding text data outlined earlier in the README.*

##### 3. `Lev Dist`: *The calculated Levenshtein distance for the corresponding accent and difficulty rating.*

---

#### To see the confidence scores for each word in every accent transcribed by Amazon Transcribe: [Data_for_word_length_and_confidence.csv](Data_for_word_length_and_confidence.csv). This CSV file contains the same 'Accent' and 'Difficulty' columns from the Levenshtein file along with the following new columns:

##### 1. `confidence`: *Amazon Transcribe generated confidence score for specified word.*

##### 2. `content`: *Corresponding word from the text data.*

##### 3. `wrdLength`: *Length of 'content' word.*
---

#### To access the collab notebooks containg our code: [notebook-code folder](notebook-code/). This folder contains two Jupyter Notebooks containg all the code from using Amazon Transcribe to generate transcriptions of the audio files to the code used for our analysis and data visualizations. These notebooks also provide commentary for the code and data used.

### Notebook 1: Generating Transcripts From Audio Files Using AWS Transcribe

This notebook provides a thorough process and code for converting the fifteen audio files from ttsreader.com and obtaining a transcript for each one using Amazon Transcribe.
This notebook also details the three Amazon S3 buckets used for this project:
- actual-transcripts-for-comprison, a bucket for the actual transcript files of each excerpt,
- audio-files-to-be-transcribed, a bucket to hold the audio files we want to transcribe, and
- aws-generated-transcripts, a bucket to receive and store the output from Transcribe.

Below is a tutorial covering the preferred permission setting in AWS to properly allow Amazon Transcribe and Amazon S3 to function cooperatively.

[AWS Permissions Video Walkthrough](https://player.vimeo.com/video/479619829)

### Notebook 2: Cleaning, Wrangling, and Visualizing Outputs from AWS Transcribe: The following graph illustrates the distribution of confidence scores.

This notebook contains code on importing S3 transcript data, outling the data structure of the .json files (as pictured below), data analysis for calculating the Levenshtein distance, and code for creating visualizations of the word confidence scores by word lengths.

![ds](pics/datastruc.jpg)

###### *Both Jupyter Notebooks are formatted as .ipynb files*

---

#### To access the blog for our project: [Qtm350_Final_Blog.ipyng](https://github.com/QTM350/ACCENTing-AWS_Transcribe-Accuracy-Code/blob/main/QTM350_Final_Blog.ipynb). This blog covers an overview of Amazon Transcribe, the objectives/motivations behind the project, the project architecture, as well as the process of the data analysis from nb2-Data-Analysis.ipynb. 

###### Below is an example table taken from the blog outlining the major variations in the percentage of people who speak English in the selected countries for our project.

<p align="center">

| Country | % of Population who speak English |
| ----------- | ----------- |
| United States | 95.48% |
| United Kingdom | 97.74% |
| China | 0.9% |
| Spain | 22% |
| India | 12.18% |

</p>

---



# Project Architecture 

![PA](arch.png)

## AWS Cloud Computing Services used:
All AWS cloud computing services used in this project have been listed below along with a link to the official developer guide.

- [Amazon Transcribe]( https://docs.aws.amazon.com/transcribe/latest/dg/what-is-transcribe.html)

- [Amazon SageMaker]( https://docs.aws.amazon.com/sagemaker/latest/dg/whatis.html)

- [Amazon Simple Storage Service](https://docs.aws.amazon.com/AmazonS3/latest/dev/Welcome.html)

###### To download the architecture diagram: [arch.png](arch.png)

---

# Improvements & Further Analysis
For further analysis, comparisons can be made between Amazon Transcribe and other speech-to-text services including Dragon Professional, Otter, Speechmatic, etc… Readers may even use this data to do comparisons against other cloud service transcription services like Google Cloud’s Speech-to-Text or Microsoft Azure Speech to Text. These findings can help determine which services are worth the price since all of these examples are paid services.  

This project will also be helpful in comparing the quality of current closed captioning not just for shows on Netflix but for videos on YouTube and other video streaming webpages. This project has the potential to improve the quality of transcription algorithms and ultimately benefit deaf or hard of hearing individuals by highlighing the need for accurately transcribed content.

The automatic speech recognition (ASR) service limitations in this project can stem from ttsreader.com varying levels of accent thickness for certain countries. For example, the Spanish accent was much thicker than the Hindi accent, which may have been why the Spanish accent had the least accuracy and least confidence. In addition, the amount of punctuations in the scripts, such as commas and question marks, may have influenced the tone and cadence at which the scripts were read.

---

## Sources

### Websites:

AWS. "Amazon Transcribe." [link](https://aws.amazon.com/transcribe/?nc=sn&loc=0)

Besner, Linda. "When Is a Caption Close Enough?" [link](https://www.theatlantic.com/health/archive/2019/08/youtube-captions/595831/)

Diana. "Transcript: A Pep Talk From Kid President." [link]( http://complicatedmelody.com/content/transcript-pep-talk-kid-president)

Everson, Howard T., Tobias, Sigmund. "The ability to estimate knowledge and performance in college: A megacognitive analysis." [link](https://link.springer.com/article/10.1023/A:1003040130125)

List from Wikipedia. "List of countries by English-speaking population." [link](https://en.wikipedia.org/wiki/List_of_countries_by_English-speaking_population)

Radecic, Dario. "Calculating String Similarity in Python." [link](https://towardsdatascience.com/calculating-string-similarity-in-python-276e18a7d33a)

Speech-to-text. [link](https://ttsreader.com/)

Urban, Tim. "Inside the mind of a master procrastinator." [link](https://www.ted.com/talks/tim_urban_inside_the_mind_of_a_master_procrastinator/transcript#t-25363)


