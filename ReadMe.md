# Introduction

Hola! My name is Noah Alexander and this is my project dedicated to understanding my progress in speaking Spanish through NLP and data analytics. Below is a description of the project, how the repository is structured, and what I learned throughout it!

## Driving Question

How did my speaking abilities change between Day 1 and Day 112 as seen in the data? How did improvement show / falter over time? 


# Insights Shown and What I Learned (Extended Description)

*Note: If you want a quick overview, read the infographic in the Visualizations folder. This is a more extended discussion of the project.*

One thing is clear- I can speak much faster at the end of the project than I could at the beginning. In fact, the last video more than doubled the Words per Minute (WPM) measure of a video early on in the project (the slowest recorded). Also, a recent development is that much less of my speech consists of "filler" words (sounds transcribed that I make while thinking or between words) in the last two weeks. These two trends together show that not only am I saying more words, but more of those words count. What happened is what one may expect, that with more time practicing the spoken language (and studying), that I would need less time to think about what I'm saying and say things quicker. In general, today I feel much more comfortable talking than I did 4 months ago.

Now to analyze vocabulary richness. For one, the videos usually covered things I did on a daily basis and did not deal with complex topics (although some were reflections about documentaries or complex ideas). For that reason, vocabulary isn't expected to grow as much without some kind of impulse, such as holidays, life events, or other novel things that happened throughout the time period. Entropy, TTR, and Unique_Words (and features engineered with the latter) seek to measure and understand the type of vocabulary growth. The problem that I ran into was that the length of the video greatly influenced the vocabulary distribution (as discovered in the correlation matrix). 

With this, I had to come up with some creative solutions to explore the trends while controlling for time. I decided to make a categorical variable to split the videos into 3 groups based on their ranking of length. Then I made the scatterplot with the same x and y values, but with the observations colored based on their group. With this, you could clearly see how video length influenced vocabulary richness, and a seemingly conflicting trend became even more evident- Unique_WPM increased over the course of the project, but TTR decreased and Entropy was somewhat constant. TTR aims to show the relation between the number of unique words with total words said, which is slightly different from Entropy- an even distribution of word usage. Thus, Entropy being constant does not conflict TTR or Unique_WPM trends, but rather shows that my random distribution of words is constant (albeit with some variation). 

This is where the most valuable lesson of this project came in- when understanding KPI (or calculated feature) trends, we must understand what is driving the change. TTR is the measure of Unique Words / Total Words, meaning:

Total Words increases -> TTR decreases
Unique Words increases -> TTR increases

As TTR increases, it indicates more unique words *in relation to the total amount of words*. However, our principal and most clear trend in the data is that WPM has steadily increased over the course of the project. Thus, Total Words is increasing and drives a TTR decrease. What we are seeing is the WPM growth outpaced Unique_WPM growth and thus we show a decrease in TTR. Unique_WPM growth simply could not keep up with WPM growth. I suspect that WPM will soon hit a ceiling and if Unique_WPM continues its growth, TTR will make a rebound and eventually improve from what it was at the beginning of the project. 

This taught me how important it is to understand how KPIs are calculated and understanding how their trends are being contributed to by the different variables that factor into how the KPI is calculated.

## Concrete Statistics of Week 1 vs Week 16 Comparisons:

WPM went from 77.8 to 114.8 (a 47.5% increase)  
Filler_Perc went from 10% to 5.2% (a 48.5% decrease)  
Unique_WPM increased when controlling for time, but it is not easily quantifiable  

## Limitations, Future Work, and Mistakes

Of course, there are limitations with the project. For one, the automated transcriptions are only about 95% accurate from what I have seen due to my accent. I’m sure this number changes with accent performance and could be an interesting way to look at growth in this area over time as well. Also, speaking is heavily dependent on me, a variable human being. There were some days where I was exhausted (like after we had to stay until 2 AM at a work party for my spouse and were still the first to leave), some days where I didn’t have much social energy, or just didn’t have anything new to talk about. Looking back, I wish I would have thought through how to take a self measurement of these different things with questions like: rate your energy level, did you have things to talk about, etc. Also, I had no clue that video length would so strongly influence my vocabulary trend measurements and add variation. If I could do this experiment over again, I would control the video length more and structure how I arrive at that better. However, I did doubt in the beginning that it would be hard for me to reach much more than 5 minutes daily. I have exceeded my own expectations in many ways!

In terms of future work, one thing that I am really interested in doing is finding similar content from native speakers and making “benchmark” ranges to strive for, to understand the distance between me and a native speaker. I also think it would be interesting to analyze in a similar way videos from other speakers to understand what amount of variation within observations is normal and what influences the variance in different observations. Also, I think that the metrics designed from the transcripts can become more interesting with higher level NLP analytics, and someone with more skills in these areas (and the knowledge and tools to apply them to Spanish) could come up with some interesting insights as well.

Thank you for your time in reading about my project, if you have any questions feel free to [reach out to me on LinkedIn](https://www.linkedin.com/in/noah-alexander-153266222/)!


# What does the data represent?

For 112 consecutive days (except 3 where I lost my voice), I recorded myself speaking Spanish to a camera between 5-15 minutes. During this time, I averaged almost 5 hours of Spanish studying (through comprehensible input, speaking, and reading) every day. The timeline for this project is significant, because based on the learning method I am using ([described here](https://www.dreamingspanish.com/method)), from the beginning of the project to the end I go from “conversation is tiresome” to “conversationally fluent”, which is what happened with me! I am by no means fluent, but I can make friends and live life in Spanish with some occasional confusion. During this timeline I transitioned from being semi-dependent on materials made for students to only watching media intended for native speakers.

*Note: The raw text is private, only data for Videos 1 and 112 are available so that one can see how the ETL pipeline works. The finished dataset is saved in /Data/clean_data.csv*

The process for calculating the variables is as follows:
Record the video and upload to YouTube
Copy and Paste auto generated transcript into a text file
Transform the transcript into a frequency dictionary with (word, frequency) key-value pairs
Calculate measurements from the dictionaries for each video.

Each observation is a video, and below is a definition of all the variables:

1. Video_Number- An index representing the chronological order of recorded videos, ranging from 1 (earliest) to 112 (most recent), used as a proxy for progression over time.  
2. Date_Recorded- The calendar date that the video was recorded.  
3. Hours_CI_Students- The number of hours spent learning through watching Comprehensible Input for Learned (content not made for native speakers).  
4. Hours_Reading- The number of hours spent learning through reading.  
5. Hours_Talking- The number of hours spent learning through speaking with Natives.  
6. Hours_Native_Media- The number of hours spent learning through watching native media as a form of Comprehensible Input.  
7. Time_Recorded- The time of day that a video was recorded. Note: if the video is between 12 AM and 3 AM, it was recorded on the next calendar day, but counted as the video for the date listed in Date_Recorded. Sometimes I didn’t have time to record until late at night (the Spanish are a late night culture).  
8. Length_Minutes- The length in minutes of the video which was recorded.  
9. Total_Words- The total number of words which were transcribed.  
10. Unique_Words- The number of unique words which were transcribed.  
11. Avg_Word_Freq- The average number of times a word was used in the video. Calculated by Total_Words / Unique_Words (inverse of TTR).  
12. Med_Word_Freq- The median number of times a word was used in the video  
13. Entropy- Calculation of the entropy based on the word frequency. Used to measure variance. Look at the "Feature_Creation.ipynb" file to understand more.  
14. TTR- The Lexical Diversity (Type-Token Ratio, or TTR) of the video. Used to measure variance. Calculated by Unique_Words / Total_Words (inverse of Avg_Word_Freq).  


# Structure of the Repo

The Data folder has all the data. Raw_Transcripts are the text files and Processed_Transcripts are json files that store the data dictionary. The “clean_data.csv” is the joined and cleaned dataset, with “transcript_features.csv” and “video_features.csv” representing the calculated features and the hand collected features, respectively.

The Code folder has all the jupyter notebooks with the code I used for the project. Below is what each represents:

Transcript_Cleaner.ipynb- Code that transformed the text files into data dictionaries and saved them as json files.  
Feature_Creation.ipynb- Code that loads json files and makes calculations, resulting in “transcript_features.csv”.  
Data_Cleaning.ipynb- Code that joins “transcript_features.csv” and “video_features.csv” and cleans the data to prepare for analysis. Results in “clean_data.csv”.  
Analysis.ipynb- Code that analyzes and visualizes the data.  
Analysis_Weekly.ipynb- Code that groups data into 7 day groups (weeks) and does some calculations. Nothing novel is found.


The Visualizations folder has an infographic I made to share this project and its findings and images of the data visualizations I used in that infographic (generated at the end of “Analysis.ipynb”).
