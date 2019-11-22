# Use case scenario
#### Welcome to the Loyalty API

------------------------------------------------------------------------------------------
i-bank Loyalty API is a multi tenant rewards platform. 
It can be easily integrated to your APP, to ensure that your existing customers, won't leave you!
Offering some reward to your users, who frequently make specific transactions, will strengthen your brand loyalty :)

> Visit: https://developer.nbg.gr/documentation/ibank-Loyalty-API-Sandbox-v1 for the full API documentation.

### Sample Scenario 
"City Trends" Inc. has a mobile app, suggesting popular places around a city. "City Trends" wants to offer subscriber, bonus as a reward for 
mobile app consumption, as part of special promotions with local merchants and public event organizers.

### Solution ("Loyalty Scenario") 
"City Trends" Inc. can use i-bank Loyalty API.
They will be registered as a Merchant to the desired loyalty schema, covering their exact business needs. (1)
Bear in mind that loyalty schema is the Rewards Platform core, where all the merchants, events and customers are subscribed. 
A mobile app user can then subscribe to the aforesaid schema as a customer (2) and collect points, when making specific POS transactions (3)
or participating to events, registered to the loyalty scheme. (4) User gets informed about the points balance, (5) after a push notification
from the "City Trends" mobile app and issues a coupon (6) to redeem their points at the "Event1" event. (7)

### "Loyalty Scenario" API calls 
- (1) Create Sandbox
- (2) Register Customer 
- (3) Points Collection Event Policy POS
- (4) Points Collection Event Policy Event
- (5) Get Balance
- (6) Issue Coupon
- (7) Points Redemption
