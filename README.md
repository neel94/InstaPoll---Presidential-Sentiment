# InstaPoll : Presidential Sentiment


## Project Pipeline


I wrote a hacky python script to get tweets mentioning different presidential candidates. To make our spark streaming job easier in the later stage, we added an additional field 'candidate_name' in each of these tweets. 

We wanted to figure out the location, namely the state from which the tweets are coming from. Even though, twitter api contains a field named 'geocode', this is an optional field - for most of the tweets, this field contains a null value. So, instead we decided to use another field - 'user'/'location'. This is a text field that users can fill up any way they like. This may not be accurate all the time. We create a dictionary look up table to match the text contains in this field to state name and added another filed 'state' in the tweet messages.

We then piped these tweets using a socket to spark streaming job.

The spark streaming jobs use a 60 seconds window to calculate the number of mentions each of the presidential candidates have, the sentiment of these mentions, how many positive tweets each of the candidates are receiving, as well as where the tweets are coming from. The output looked like this:

![Pipeline](figures/output.png)


