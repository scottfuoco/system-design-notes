# Reddit Api

Design the Reddit API knowing the following information

- User | userId: string, ... // More stuff but not needed 
- Subreddit | subredditId: string, ... // More stuff but not needed 

Features of reddit and subreddits

Clarification on the topic
Ability to create subreddits
Ability to create posts within subreddits
Subreddits contain moderators
Like posts
Comment on posts
share
report posts
controversial, best, relevant comments
**uploading images** always ask

Focus on:
writing posts
writing comments
up/down votes

Don't need to focus on
sharing
moderating
reporting

Focus on the narrow but core functionality/features of
creating posts in a subredit, commenting on those posts, and upvote/downvoting

Define a few more entities
Posts
Comments
etc

Define an API with methods to interact with these entities, such as create,
read, update, and delete posts.  Make sure to include the signature for each
method, so the input and outputs of each.

ACL Access control list in order to delete posts, so that users cannot delete
other users posts.

----
Primary entities

--Post Table Schema--
postId: string unique;
subredditId: string;
creatorId: string;
title: string;
content: string;
voteCount: int;
commentsCount: int;

createdAt: date;
updatedAt: date;

-- Post Table API
Create
    inputs
    subredditId, userId, title, content

    output - returns the entity that was just created
    Post

Get
    inputs
    userId
    postId

Update:
    inputs
    postId, userId, title, content

    output
    Post

Delete:
    inputs
    userId, postId

    output
    Post

List
    inputs
    userId, subreddit, pageSize, pageToken

    output
    Post[], nextPageToken, prevPageToken

--Comment Table Schema--
postId: string;
commentId: string;
commenterId: string;
parentId: string;
content: string;
votesCount: int;
isDeleted: boolean;
createdAt: string;
updatedAt: string;

Create
    input
    userId, content, postId, parentId?

    output
    comment

Get - usually you want to get a list of comments, but for completeness
    input
    userId, commentId

Edit
    input
    userId, commentId, content

    output
    comment

Delete
    input
    userId, commentId

    output
    comment

List
    input
    userId, subredditId, 


Notes on replies
tell the ui that we are dealing with a comment thread.

Options
Store all the replies directly on the comment

Store a parentId this way you can get a list of all comments that are parents
because their id would be null, and then if the user clicked expand you would
query for all children with that comments id as a parent

Create a subcomment table

Awards API

BuyAward
    input
    userId, paymentToken, quantity

GiveAward
    input
    userId, targetId




Supporting the development of microservices, by providing a way for different services to communicate with each other
