# System Design Notes

Step one understand the problem
System design questions are intentionally vague. This is because it is the
interviewees job to ask questions about what the expectation and features of the
system are.  The following steps should help answer

4 Design Fundamentals

1) Underlying Design Fundamentals
Client Server Model
Network protocols
etc

2) Key Characteristics of system
availability
throughput
consistency
etc

3) Components of a system - components that provide your key characteristics 
Load balancer
proxy
cache
leader election
etc

4) Actual Tech that exists, these are implementations of the component that you
   can use
Zoo Keeper
AWS S3
etcd
redis

## Functional Requirements

These are the features you are actually going to be designing the system around.
You want to list out all the features you can think of and then ask the
interviewer which features they want you to explore.

## Non-Functional Requirements

These are not features but they are requirements of a systems operational
capabilities and constraints, these include
Performance and scalability
Portability and compatibility
Reliability, maintainability and availability.

## Client Server Model

Foundation of how computers communicate with each other.

Client - A client is a machine or process that requests data or a service from a
server.  When a client communicates with a server over HTTP it sends it's IP to
the server so that it knows where to send the requests back to.

Server - 

DNS Query - Website urls need to be resolved as an ip address.  To do this the
client first looks up the website url at a DNS.  The DNS provides the client
with the ip address of the server after it has done the lookup.  The DNS ips are
defined in your computer.

Ports - 


## Load Balancers


## Persistent Storage

an SSD or HDD that a database uses to store data to.  This is long term storage
and will keep our data even if the computer crashes.


Databases

ACID compliant
Atomicity - a transaction happens all or nothing
Consistency - consistency of constraints, ie. if you make a foreign key between
tables you know that they will both contain that key and any constraints on it,
ie. not null
Isolation - all transactions will occur in order, so you cannot have dirty reads
where you read data in a transaction that is partially complete.  Even though
transaction may appear to happen at the same time they happen one by one
Durability - all committed queries are guaranteed to be saved.


## Cache Notes

Caching Eviction policy

Least Frequently Used - start evicting if data isn't hit as much.  This can lead
to stale data that was viral at a time but now no longer used to stay in the
cache longer than it needs to.

Least Recently Used - evict older data


## Design requirements

we are
1) moving data
   - this can be done within one computer itself or from one computer to another computer across the world

2) storing data
   - where do we store data and why, do we store it in disk which is slower, but is cheaper and persistent, or do we use ram for faster access but it is volatile and we will lose it if the system goes down?  Or do we use a combination???
   - do we store data in the db or in a blob/object storage

3) transform data
   - ie we have a large number of logs and we want to transform / aggregate the data into a % of successful and % of failed requests
   - this is typically done in the application code



Availability - % of time the service is available for users to get a response from your application.

99.999% availability means you have 5min / year of downtime
99% availability gives you 3.65