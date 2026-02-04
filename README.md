# Restaurant Microservices System

This project consists of two specialized microservices designed to handle a restaurant's workflow, from menu management to customer order processing.

1.  **Menu Service**: A catalog service for managing food items, descriptions, and pricing.
2.  **Order Service**: A service for placing orders, calculating totals, and tracking status, integrated with the Menu Service via REST and RabbitMQ.

## How to Run

### Prerequisites
- **Docker & Docker Compose**: To run the databases and message brokers.

### 1. Clone the Repositories
Open your terminal and run the following commands:

```bash
docker-compose up -d
```

Create a New Menu Item
```Bash
curl --request POST \
  --url http://localhost:8080/menu-items \
  --header 'content-type: application/json' \
  --data '{
  "name": "Pizza",
  "description": "Delicious cheese pizza",
  "price": 9.99
}'
```
Get Item by ID
```Bash
curl --request GET \
  --url http://localhost:8080/menu-items/6982985a44a5c30a2d459e49
```

List Items (Pagination)
```Bash
curl --request GET \
  --url 'http://localhost:8080/menu-items?offset=0&limit=1'
```
Delete an Item
```Bash
curl --request DELETE \
  --url http://localhost:8080/menu-items/6981c361c160b5638f4711b9
```
Order Service (Default Port: 8081)
Place a New Order
```Bash
curl --request POST \
  --url http://localhost:8081/orders \
  --header 'content-type: application/json' \
  --data '{
  "customer": {
    "fullName": "John Doe",
    "address": "123 Main St",
    "email": "john@example.com"
  },
  "orderItems": [
    {
      "productId": "6982985a44a5c30a2d459e49",
      "quantity": 2
    }
  ]
}'
```
Get Order Details
```Bash
curl --request GET \
  --url http://localhost:8081/orders/69829c63c657e410835ce832
```
List All Orders
```Bash
curl --request GET \
  --url 'http://localhost:8081/orders?limit=2&offset=0'
```
Update Order Status (PATCH)
```Bash
curl --request PATCH \
  --url http://localhost:8081/orders/69829c63c657e410835ce832/status \
  --header 'content-type: application/json' \
  --data '{
  "status": "READY"
}'
```