# spring-cloud-config-server

Order to up microservices is : 

1) Start cloud-config-server(Once this microservice is up then and then we can start other microservices because in this microservice we have mention common config properties)
2) Start order-service
3) Start payment-service
4) Start gateway-api-service
5) Start Hystrix service

Note:- You can see in console that in each and every console of microservices config from server at : http://localhost:9196 because there we have set common property.

Now go to http://localhost:8761

You will see status of all 4 microservices(It must up).

Now lets check API if its work or not:

1) go to postman and write url for order service: 

URL : http://localhost:8989/order/bookOrder
HTTP Method : POST

Request: {
          "order":{
            "id":103,
            "name":"Mobile",
            "qty":1,
            "price":8000

          },
          "payment":{}
        }
        
Response: {
              "order": {
                  "id": 26,
                  "name": "ear-phone",
                  "qty": 5,
                  "price": 4000
              },
              "amount": 4000,
              "transactionId": "9a021fa6-2061-4332-bdb7-b1358b3430c2",
              "message": "payment processing successful and order placed"
          }
          
For payment service: 

URL : http://localhost:8989/payment/26
HTTP Method : GET

Response: {
              "paymentId": 1,
              "transactionId": "d86cfeca-0b26-455e-a1a2-ac3e53707829",
              "orderId": 103,
              "paymentStatus": "SUCCESS",
              "amount":4000
          }
