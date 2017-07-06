# ! This is a development build, use at your own risk !

# Fraud Detection for twitter
The purpose of this program is to detect fraud on twitter. It does this by targeting a specific companies handle (for example @sprint). It then will read any twitter user that complains to @sprint and begins monitoring for people responding to that tweet that are offering help. If they are not an official supported account then they are marked as fraudulent.

## How it works
#### 1) Find tweets complaining
- Twitter API to read tweets @handle
- Nodejs sentiment to determine if tweet is a complaint
- If tweet is a complaint store using MongoDB

#### 2) Find replies
- Use Twitter API to search the handle of the people who tweeted @handle
- Match in_reply_to_status_id_str to complaining tweet
- Determine if helpful
  - Note: Currently this simply searches through a list of monitored common words. in the future TF-IDF could be used monitoring the official account.
- Verify replying users account
- Store relevant info in MongoDB

#### 3) Display results
- Standard HTML, CSS, and JavaScript front extended
- PassportJS local login method
- Users stored in Nodejs
- Stylized datatables plugin to show tweet info

## Requirements
- In high volume case 2 twitter app keys are used, one for tweet gathering and one for reply searching.
- Nodejs
- MongoDB

## Setup
##### 1) Setup config file like follows
- server/config/authorization.json

```javascript
{
  "url":"mongodb://localhost:27017/DBNAME",
  "port":3000,
  "debug":false,
  "keys":[
    {
      "CONSUMER_KEY":"",
      "CONSUMER_SECRET":"",
      "ACCESS_KEY":"",
      "ACCESS_SECRET":""
    },{
      "CONSUMER_KEY":"",
      "CONSUMER_SECRET":"",
      "ACCESS_KEY":"",
      "ACCESS_SECRET":""
    }
  ]
}
```
#### 2) Create MongoDB collections

```javascript
db.createCollection("tweets")
db.createCollection("constants")
db.createCollection("users")
```

#### 3) User collection in MongoDB

- Only required fields are uname and an md5 hashed password

```javascript
{uname:"criggs626",password:"ijhzgdfiuhasdoifjaosifgadsf",email:"example@whatever.com",name:"Caleb Riggs"}
```
#### 3) Constants collection in MongoDB
- required for tracking searched tweets and verified handles

```javascript
{name:"lastID","handle":"SEARCH TERM",value:"0"}
{name:"verifiedHandles",value:["handle",""]}
{name:"statistics",count:0,negativeCount:0,averageScore:0,averageNegativeScore:0,validRepliesFound:0,fraudulentRepliesFound:0}
```

## Running
- ### Foreground
To run in the foreground simply navigate to the server and 'node' the index file.
```
cd WORKING_PATH/fraud/server/
node index.js
```
- ### Background
For running in the background I recomend forever a node package. Once forever is installed follow same steps as above just 'forever start' instead of 'node'.
```
cd WORKING_PATH/fraud/server/
forever start index.js
```

## Stats
- #### 1,398 Lines of JavaScript
- #### 483 Lines of HTML
- #### 135 Lines of CSS
- #### 112 Lines of MD (This totally counts...)
- #### 2,116 Total Lines Written

## Other Stats
- #### ∞ Tacos Eaten
- #### 2 Cats pet
- #### 0 Coffees drank
