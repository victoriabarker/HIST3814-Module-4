# Module 4 Fail Log

## Exercise 1

Downloaded Gephi on my computer

Opened github and saved my texas correspondence csv to my desktop 

Opened Gephi and selected data laboratory 

Dowloaded my CSV file and changed the settings to comma & edges table

Clicked on Nodes

Then ‘transfer data to another column’, selected ID, pressed OK

Went to  layout 

Chose ForceAtlas 2 – ran it 

Pressed stop 

Went to the ‘statistics’ tab

Selected connected components

Selected ‘UnDirected’ 

Pressed ok

Closed the window that opened 

I then went to the ‘Filters’

Clicked ‘attributes’

Then ‘equal’
 
Clicked Component ID integer (nodes) 

Then clicked  ‘filter’

Went to the statistics tab

Clicked ‘run’ beside ‘page rank’

Selected ‘use edge weight’ 

Pressed ‘OK’

Selected ‘nodes’

Went to attributes

Selected ‘Page Rank’

Made the min size 1 and the max size 2

Pressed apply

Ran Force Atlas 2

Went to the preview page 

Selected show labels, proportional size, rescale weight and deselected curved edges.

Pressed refreshed

Save to desktop 
 
## Exercise 3

Opended DH Box 

Went to Rline

Created new project

Then downloaded the following 

install.packages("mallet")

library("mallet")

install.packages('RCurl')

library(RCurl)

then x <- getURL("https://raw.githubusercontent.com/shawngraham/exercise/gh-pages/CND.csv", .opts = list(ssl.verifypeer = FALSE))

then documents <- read.csv(text = x, col.names=c("Article_ID", "Newspaper Title", "Newspaper City", "Newspaper Province", "Newspaper Country", "Year", "Month", "Day", "Article Type", "Text", "Keywords"), colClasses=rep("character", 3), sep=",", quote="")

then counts <- table(documents$Newspaper.City)

then barplot(counts, main="Cities", xlab="Number of Articles")

then years <- table(documents$Year)

barplot(years, main="Publication Year", xlab="Year", ylab="Number of Articles")

Then I created a new file by clicking on the new file tab & selecting new text file

I copy pasted the list provided by Matt Jockers

Saved the document as en.txt

mallet.instances <- mallet.import(documents$Article_ID, documents$Text, "en.txt", token.regexp = "\\p{L}[\\p{L}\\p{P}]+\\p{L}")

Then I did mallet.instances <- mallet.import(documents$id, documents$text, "en.txt", token.regexp = "\\p{L}[\\p{L}\\p{P}]+\\p{L}")

-	(side note, I could not figure out how to this step on the command line however from what I can tell it worked alright with just this command in the Rstudio as I was not working with the equity files. 

I then did (#)set the number of desired topics
num.topics <- 20
topic.model <- MalletLDA(num.topics)

then topic.model$loadDocuments(mallet.instances)
Get the vocabulary, and some statistics about word frequencies.
These may be useful in further curating the stopword list.
vocabulary <- topic.model$getVocabulary()
word.freqs <- mallet.word.freqs(topic.model)
head(word.freqs)

then write.csv(word.freqs, "word-freqs.csv" )

Then (##) Optimize hyperparameters every 20 iterations,
(##) after 50 burn-in iterations.
topic.model$setAlphaOptimization(20, 50)
(##) Now train a model. Note that hyperparameter optimization is on, by default.
(##) We can specify the number of iterations. Here we'll use a large-ish round number.
(##) When you run the next line, a *lot* of information will scroll through your console.
(##) Just be patient and wait til it hits that 1000 iteration.
topic.model$train(1000)
(##) Run through a few iterations where we pick the best topic for each token,
(##) rather than sampling from the posterior distribution.
topic.model$maximize(10)
(##) Get the probability of topics in documents and the probability of words in topics.
(##) By default, these functions return raw word counts. Here we want probabilities,
(##) so we normalize, and add "smoothing" so that nothing has exactly 0 probability.
doc.topics <- mallet.doc.topics(topic.model, smoothed=T, normalized=T)
topic.words <- mallet.topic.words(topic.model, smoothed=T, normalized=T)

then mallet.top.words(topic.model, topic.words[7,])

then topic.docs <- t(doc.topics)
topic.docs <- topic.docs / rowSums(topic.docs)
write.csv(topic.docs, "topics-docs.csv" )
(#) that file enables you to see what topics are most present in what issues/documents

(##) Get a vector containing short names for the topics
topics.labels <- rep("", num.topics)
for (topic in 1:num.topics) topics.labels[topic] <- paste(mallet.top.words(topic.model, topic.words[topic,], num.top.words=5)$words, collapse=" ")
(#) have a look at keywords for each topic
topics.labels

write.csv(topics.labels, "topics-labels.csv")

then plot(hclust(dist(topic.words)), labels=topics.labels)

then plot(hclust(dist(topic.words)))

Then I uploaded the graph I created on Github 

## Exercise 4

Made an account with Overview 

Watched the tutorial video and read a bit of the blog

Uploaded the CND.csv file 

Observed the word cloud

Did a couple of random searches in the search bar and multisearch bar

Made a screensave of the wordcloud 

Uploaded that file into Github

## Exercise 6

Went to http://voyant-tools.org

And copy pasted this: https://raw.githubusercontent.com/shawngraham/exercise/gh-pages/CND.csv .

I got an error code – said it could not open

Then I did http://voyant-tools.org/?corpus=colonial-newspapers&stopList=stop.en.taporware.txt

That worked 

Could not find the wheel that was mentioned in the instructions 

Noticed a peer was in the same situation and had asked a question via annotation 

Decided to wait until she got a response 

## Exercise 7

Opened RAW 

Copy pasted the Texas data into RAW

Got the error code that was mentioned in the instructions

Opened google sheets

Pasted =IMPORTDATA("https://raw.githubusercontent.com/hist3907b-winter2015/module4-holes/master/texas.csv") into A1

Then while the mouse hovered over B1 I did shift+cmnd+downarrow

Followed by shit+cmnd+rightarrow

Then cmnd+c 

Then went to edit 

Then paste special 

Then paste values only 

Then I deleted the #REF in the A1 box 

Then I went to Add ons

Followed by Get Add ons and selected Blank Detector

I installed Blank Detector 

I then highlighted my data by doing command +a

Went back to add ons

Then selected blank detector 

Did set value , input ‘null’

Then I ran it 

I had to run it around 5 times in order for the entire thing to complete as I was continuing to receive the ‘run exceeded maximum time' error code. 

Then I copied (command a) all of the data

Pasted into Raw

Selected the ‘alluvial’ diagram

Input 1 & 2, then 1,2,3 &4 and 3&4 

I observed them for differences and saved the files on my hardrive

Uploaded them to github. 

## Exercise 8

Made an account with World Map Harvard.edu

Found a historical map of Liverpool on Google 

Uploaded that map on WorldMap Harvard.edu and put in the information I knew about the map 

I then went to rectify 

Found the same location on both of the maps and made a control point

I did this another 3 times, making four control points in total

Then selected ‘wrapped imagine’

Then went to export – none of the links worked, even the KML 



