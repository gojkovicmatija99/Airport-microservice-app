# Airport-microservice-app

Design and implement a system for selling airline tickets in microservice architecture.
Brief description of the system:
The system consists of 3 services. These services include the customer, ticket and flight services.
# User service:
  - Registration - name, surname, email, code, passport number (at the end of registration
an email is sent to the user to verify the email address).
  - Login - the user forwards the email and password, if the login is successful he gets JWT
token in response.
  - Edit profile - when the user logs in to the system it has the ability to change
all its parameters.
  - Credit card - the user can add 1 or more credit cards to the system.
  - Ranks - Users are assigned a certain rank depending on the miles they are
and assigned when buying tickets. The ranks are Gold (> 10000 mi), Silver
(> 1000 mi), Bronze (<1000 mi).
  - Admin - In addition to the regular user, there is also an admin, his role is to add and
deleting flights. The admin of the parameters has only a username and a password.
- [See service](https://github.com/gojkovicmatija99/airport-user-service)

# Flight service:
  - Flight list - The flight list is displayed to the user. Flight parameters are airplane,
starting destination, final destination, flight length, price. The user does not
show flights whose passenger capacity is full.
  - Flight Search - The user can search for flights based on all
parameters.
  - Adding and deleting airplanes - The administrator can add and delete airplanes.
The aircraft of the parameters has the name and capacity of the passenger. However, it can be deleted
an aircraft only if it is not added to any flight.
- Add and delete flights - Administrator can add and delete flights,
however when deleting if at least one ticket has been sold then for
the given flight performs a refund.
- [See service](https://github.com/gojkovicmatija99/airport-flight-service)

# Ticket service:
  - Ticket purchase - The user can buy tickets for existing ones through this service
flights. When making a purchase, the user chooses the credit card with which he wants to pay. If the capacity for a given flight full, the user will be shown an error when purchasing. Depending on the rank of the user, he gets a discount on the ticket price (gold-20%,
silver-10%, bronze-0%). After a successful purchase, they are updated for the user
miles. The information card contains user information, flight information and
date of purchase.
  - Overview of purchased tickets - The user can see all the tickets he bought,
sorted by date of purchase.
- [See service](https://github.com/gojkovicmatija99/airport-ticket-service)

# Other features:
- [Vue.js frontend](https://github.com/gojkovicmatija99/airport-frontend)
- [Zull API gateway](https://github.com/gojkovicmatija99/airport-zull)
- [Eureka discovery server](https://github.com/gojkovicmatija99/airport-eureka)

# Example:
<p align="center">
  <img width="400" height="500" src="https://github.com/gojkovicmatija99/Airport-microservice-app/blob/master/graphviz(1).png">
</p>

User selects a ticket to buy and after connecting to the ticket service the following actions occur:
1. The ticket service sends a request to the flight service with the flight id to get the ticket information
2. The ticket service sends a request to the user service with the user token to get the user information
3. The ticket service saves the ticket into it's database
4. The ticket service sends a message to the message broker to update user's miles
5. The ticket service sends a message to the message broker to update the number of passengers on the flight
6. When the service is available it updates user's miles
7. When the service is available it updates the number of passengers on a flight
