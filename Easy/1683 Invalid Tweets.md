# 1683. Invalid Tweets
https://leetcode-cn.com/problems/invalid-tweets/  

Table: Tweets

| Column Name    | Type    |
| ------ | ------ |
| tweet_id       | int     |
| content        | varchar |

tweet_id is the primary key for this table.  
This table contains all the tweets in a social media app.  

Write an SQL query to find the IDs of the invalid tweets. The tweet is invalid if the number of characters used in the content of the tweet is strictly greater than 15.  
Return the result table in any order.  
The query result format is in the following example.  

Example 1:  
Input: 
Tweets table:

| tweet_id | content                          |
| ------ | ------ |
| 1        | Vote for Biden                   |
| 2        | Let us make America great again! |

Output: 

| tweet_id |
| ------ |
| 2        |

Explanation: 
Tweet 1 has length = 14. It is a valid tweet.
Tweet 2 has length = 32. It is an invalid tweet.

## solution
Foucs on the difference of LENGTH() and CHAR_LENGTH()
1. CHAR_LENGTH()
- unit of measurement：char
- For digit, letter and Chinese character, they all count as one char.
2. LENGTH()
- unit of measurement: byte
- utf8(8-bit Unicode Transformation Format)：Three bytes for a Chinese character, one byte for adigit or a letter. 
- gbk：Two bytes for a Chinese character, one byte for adigit or a letter. 

``` sql
# Write your MySQL query statement below
SELECT tweet_id FROM Tweets WHERE CHAR_LENGTH(content) > 15;
```
