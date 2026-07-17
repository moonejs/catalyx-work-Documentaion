
- **Controller** = the waiter. Takes the customer's order (the HTTP request), doesn't cook anything itself, just passes it to the kitchen and brings back the food.
- **Service** = the kitchen/chef. Does the actual work — talks to the database, hashes passwords, generates tokens.
- **Module** = a section of the restaurant (e.g. "the bar", "the kitchen") — groups related waiters and chefs together, and tells the rest of the restaurant "here's what I offer, here's what I need from other sections."
- **DTO** = the order slip format. Defines exactly what a valid order looks like, so the kitchen never gets garbage input.
- **Guard** = the bouncer at the door. Checks ID (the token) before letting a request even reach the waiter.
- **Strategy** = the ID-checking method the bouncer uses (checking a driver's license vs a passport — you have two: access token vs refresh token).

That's genuinely the whole mental model. Everything else is detail on top of this.