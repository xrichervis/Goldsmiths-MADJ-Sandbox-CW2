import twitter,json,csv

#Insert your own Twitter developper account keys and tokens

CONSUMER_KEY = ''
CONSUMER_SECRET = ''
OAUTH_TOKEN = ''
OAUTH_TOKEN_SECRET = ''

auth = twitter.oauth.OAuth(OAUTH_TOKEN, OAUTH_TOKEN_SECRET,
                           CONSUMER_KEY, CONSUMER_SECRET)

twitter_api = twitter.Twitter(auth=auth)

#Tweets are collected in a CSV file, in this case, a file called General_Election_Tweets(1).csv

csvfile = open('General_Election_Tweets(1).csv', 'w')
csvwriter = csv.writer(csvfile, delimiter='|')

# When importing csv later, make sure to delimit them with "|"

def getVal(val):
    clean = ""
    if val:
        val = val.replace('|', ' ')
        val = val.replace('\n', ' ')
        val = val.replace('\r', ' ')
        clean = val.encode('utf-8')
    return clean

# Tweets collected will include one of these three hashtags

q = "#GE19,#GE2019,#GeneralElection2019"

twitter_stream = twitter.TwitterStream(auth=twitter_api.auth)

stream = twitter_stream.statuses.filter(track=q)

for tweet in stream:
    try:
        if tweet['truncated']:
            tweet_text = tweet['extended_tweet']['full_text']
        else:
            tweet_text = tweet['text']

#Data being collected includes: 

        csvwriter.writerow([
            getVal(tweet['created_at']),
            getVal(tweet['user']['screen_name']),
            getVal(tweet_text),
            getVal(tweet['user']['location']),
            tweet['user']['followers_count'],
            tweet['user']['verified'],
            tweet['retweet_count'],
            tweet['favorite_count'],
            getVal (tweet ['lang']),
            ])
            
            # Allows for code to keep continuously running even if it struggles to collect a live streamed tweet
        print tweet['user']['screen_name'].encode('utf-8'), tweet['text'].encode('utf-8')
    except Exception, err:
        print err
        pass
