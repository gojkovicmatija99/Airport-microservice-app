# Airport-microservice-app

Design and implement a system for selling airline tickets in microservice architecture.
Brief description of the system:
The system consists of 3 services. These services include the customer service that the user uses for
login to the system and receive a user token with which to further authorize each
addressing the system. Also a flight service that is responsible for management and administration
flights and a ticket service.
Functionalities:
- Service 1 (Customer Service):
  - Registration - Name, surname, email, code, passport number (at the end of registration
an email is sent to the user to verify the email address).
  - Login - the user forwards the email and password, if the login is successful he gets JWT
token in response.
  - Edit profile - when the user logs in to the system it has the ability to change
all its parameters. If you change your email address, you need to send it
verification message to new email.
  - Credit card - the user can add 1 or more credit cards to the system.
The credit card of the parameters has: Name and Surname of the owner, card number and
security number of 3 digits.
  - Ranks - Users are assigned a certain rank depending on the miles they are
and assigned when buying tickets. The ranks are Gold (> 10000 mi), Silver
(> 1000 mi), Bronze (<1000 mi).
  - Admin - In addition to the regular user, there is also an admin, his role is to add and
deleting flights. The admin of the parameters has only a username and a password.
Administrators are inserted into the system at initial startup and theirs
parameters can be predefined. (administrator accounts are hardcoded
into the system).

- Service 2 (Flight Service):
  - Flight list - The flight list is displayed to the user. Flight parameters are airplane,
starting destination, final destination, flight length, price. The user does not
show flights whose passenger capacity is full.
  - Flight Search - The user can search for flights based on all
parameters.
  - When showing flights, it is necessary to do pagination. So they don't load
all flights at once than piece by piece depending on query parameters.
  - Adding and deleting airplanes - The administrator can add and delete airplanes.
The aircraft of the parameters has the name and capacity of the passenger. However, it can be deleted
an aircraft only if it is not added to any flight.
- Add and delete flights - Administrator can add and delete flights,
however when deleting if at least one ticket has been sold then for
the given flight performs a refund (There is no literal refund because it is
payment only simulated, here the user should send a notification via
email, take away his miles and mark the flight and tickets as canceled). On occasion
refund information is promoted to service 1 and service 3 via
message broker.

- Service 3 (Ticket Service):
  - Ticket purchase - The user can buy tickets for existing ones through this service
flights. When making a purchase, the user chooses the credit card with which he wants to pay,
if he did not enter any card in the system before the purchase, then it will be required
at the end of the purchase to enter the card with which he wants to pay. If the capacity
aircraft for a given flight full, the user will be shown an error when purchasing. U
depending on the rank of the user, he gets a discount on the ticket price (gold-20%,
silver-10%, bronze-0%). After a successful purchase, they are updated for the user
miles. The information card contains user information, flight information and
Date of purchase.
  - Overview of purchased tickets - The user can see all the tickets he bought,
sorted by date of purchase.

Services must communicate via http. For each task which system must process if
need services must communicate with each other, one example would be for shopping
tickets, here service 3 must first communicate with service 2 to see if it is filled
capacity, then with service 1 to collect user data (card, discounts, etc.) and
eventually communicates again with service 2 at the end of the purchase to update it
the number of passengers for a given flight and then with service 1 to update the mileage and rank of the user.
Users must not contact the services directly, but there must be an API between them
a gateway that will deal with routing. In the exercises, we will cover Netflix libraries for
api gateway (Zuul) and service discovery (Eureku) and it is allowed to use them in the project.
You also need to create a client application (GUI) for the system. Client design and type
applications (desktop, web, android ...) can be done however anyone wants. Points for
client applications are assigned depending on the number of system functionalities they are on
available through it. 
