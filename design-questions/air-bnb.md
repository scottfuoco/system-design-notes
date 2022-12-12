# Air&BnB

air bnb like many consumer service products there are two sides to it.  For air
bnb we have a renter facing side and a host facing side.  Are we focusing on
designing both or just one of these?

Host features
CRUD for listings

Renter features
browse
booking
but not managing

multiple users can browse the same property at the same date range, but once one
of them books the property then it is no longer available for any other user.
When a user clicks book now we can lock the property for 15minutes while they
add their credit card.

Do we want to look at features such as contacting hosts, authentication, and
payments?

For browsing do we want to have the ability to filter by location, price, date
range?  are there any properties we can search / filter?

For location can we store the geo data as lat+long? yes!

systems characteristics
how many users
how many listings
what kind of latency constraints do we have
and availability?

50M users (only concerned with the US region)
1M listings
we care about latency and want the system to always be available

Because hosts and renters are both going to be interacting with listings, where
the host will be creating, updating and deleting them.  Where as renters will be
viewing and creating bookings on them.  Then we should probably have them both
use the same storage solution.

when using geo location data at a large scale we might want to have an auxiliary
storage for fast lookups on that.  For this example we can use a quad tree to
store the geo location data, even though that might be over engineering for this
particular example because it only has 1million lists.  Something like google
maps would require a quad tree because they would have potentially +100 million
locations.


