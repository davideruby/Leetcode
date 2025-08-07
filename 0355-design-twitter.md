## [355. Design Twitter](https://leetcode.com/problems/design-twitter/)

${\textsf{\color{yellow}Medium}}$

Design a simplified version of Twitter where users can post tweets, follow/unfollow another user, and is able to see the 10 most recent tweets in the user's news feed.

Implement the Twitter class:

- Twitter() Initializes your twitter object.
- void postTweet(int userId, int tweetId) Composes a new tweet with ID tweetId by the user userId. Each call to this function will be made with a unique tweetId.
- List<Integer> getNewsFeed(int userId) Retrieves the 10 most recent tweet IDs in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user themself. Tweets must be ordered from most recent to least recent.
- void follow(int followerId, int followeeId) The user with ID followerId started following the user with ID followeeId.
- void unfollow(int followerId, int followeeId) The user with ID followerId started unfollowing the user with ID followeeId.

## Solution
```python
import heapq

class Twitter:

    def __init__(self):
        self.time = 0
        self.followees = {}
        self.tweets = {}


    def postTweet(self, userId: int, tweetId: int) -> None:
        if userId not in self.tweets:
            self.tweets[userId] = []

        self.tweets[userId].append([self.time, tweetId])
        self.time += 1


    def getNewsFeed(self, userId: int) -> List[int]:
        heap = []
        self.__selfFollow(userId)

        for followee in self.followees[userId]:
            if followee in self.tweets:
                index = len(self.tweets[followee]) - 1
                time, tweet = self.tweets[followee][index]
                heap.append([-time, tweet, followee, index])

        heapq.heapify(heap)
        news_feed = []
        while heap and len(news_feed) < 10:
            time, tweet, followee, index = heapq.heappop(heap)
            news_feed.append(tweet)

            if index > 0:
                time, tweet = self.tweets[followee][index - 1]
                heapq.heappush(heap, [-time, tweet, followee, index - 1])
        
        return news_feed
        

    def follow(self, followerId: int, followeeId: int) -> None:
        if followerId not in self.followees:
            self.followees[followerId] = set()

        self.followees[followerId].add(followeeId)


    def unfollow(self, followerId: int, followeeId: int) -> None:
        if followerId not in self.followees:
            return
        if followeeId not in self.followees[followerId]:
            return

        self.followees[followerId].remove(followeeId)
        

    def __selfFollow(self, userId):
        if userId not in self.followees:
            self.followees[userId] = set()
        self.followees[userId].add(userId)
```

## Notes
It should be hard in my opinion.

Store for each user his tweets in a hashset and his followees in an array. Then, to get the news feed of a user, first initialize a heap with the last tweet of each of his followee, taking the time of the tweet as the key of the heap. Then, iterate as follows:

- pop from the heap to get the last tweet
- given the followee whose tweet has just been popped, push into the heap his previous tweet.
