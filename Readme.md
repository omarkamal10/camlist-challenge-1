# Pet store Challenge 1

I implemented most of endpoints in the pet store swagger spec from scratch and added the two main end points required in the challenge to showcase my code structure and organization.

## Setup and running the project

1. Install node dependencies ➡ `npm install`
2. Run Docker Compose ➡ `docker-compose up`

That's all you need to run the project.

## Documentation

Postman collection in Documentation folder
Base URL ➡ http://localhost:9000/api

### When the project first starts there will be some seeded data:

1. 3 users with these credentials:
   - username: user1, password: 1234
   - username: user2, password: 1234
   - username: user3, password: 1234
2. A pet with category of Dog with id: 1
3. An auction created by user1 for other users to bid on the pet above. Note that the user that created the auction cannot bid in his own pet sale.
   - auctionId: 1
   - petId: 1

### I added three main endpoint for the challenge as per my understanding.

All of these endpoint require authentication so the user must login

1. User to bid on specific pet - POST ➡ http://localhost:9000/api/auction/:auctionId/bid
2. Pet owner to list all bids in general - GET ➡ http://localhost:9000/api/auction/bid/all ➡ Return all bids for all pets for that particular user
3. Pet owner to list all bids for specific pet - GET ➡ http://localhost:9000/api/auction/bid/pet/:petId ➡ Return all bids for that particular petId for that particular user

### Example scenario to test the challenge endpoints.

1. As user1 is the owner of the auction and the seller/owner of that pet so only he can see all the bids made on that pet or in his other pets as well.
2. Login with user2 and place a bid - POST ➡ http://localhost:9000/api/auction/1/bid with json body {"amount":50}
3. user2 cannot place another bid until another user places a bid.
4. Login with user3 and place a bid - POST ➡ http://localhost:9000/api/auction/1/bid with json body {"amount":60}. Note that if the amount is less than the highest bid, it will result in an error stating to place a higher bid.
5. Login with user1 to check the bids on that particular pet - GET ➡ http://localhost:9000/api/auction/bid/pet/1 ➡ will return array of bids made with each bidder value as the userId
   [
   {
   "amount": 101,
   "bidder": 2
   },
   {
   "amount": 103,
   "bidder": 3
   ]
6. You can test the other endpoint as per the postman collection with their input data.