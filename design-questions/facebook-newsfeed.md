# Facebook News Feed

load and view a news feed
refresh news feed
posting/update status
liking

feed creation and refreshing

ask if we care about posts and how they are stored, ie. images, video and text.
for this instance we don't care about how posts are implemented.

Do I need to implement the ranking algorithm based on relevance etc, 
should we worry about ads?

How many users?
1B users per day
10 million posts per day

How many news feed loads are there?
5 Billion News Feeds per day

How many friends can we assume users have?
500 friends on average, but there are some with a lot of users, which need to be
handled differently

Because we have a global audience is it ok if friends in different regions have
receive updates at different times?
friends near you can have a 1s delay and friends far away can have up to 1minute
delay.

posts have to persistence, we want good availability but doesn't need to be
highly available.

-----------

Core user actions
Create Post and GetFeed

with this kind of scale we need to have some heavy load balancing in front of
the servers.

When creating a post we don't need any kind of caching or sticky sessions, just
add data to the db.

Load balancing with round robin for the create post

For get feed we want a different kind of load balancing

Shard your database based on userId so that all paginated data for each user
exists on the same shard, so your pagination token works

When a user creates a post it should update the users next feed update, so next
pagination or refresh.

In order to achieve real time updating of the feed shards we want to create a
pubsub system that connects the two.  So as new posts are created we push
updates to the feed shards.  The topics for the pubsub system will match the
same userId hashing that the load balancer has so that when a user creates a new
post it pushes the update into the correct shard.


idempotent, you can re-run the same operation 