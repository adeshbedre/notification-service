# Notification-service
A generic notification system that consumes a message and sends it to across the appropriate channel.

## Instructions to run the program
1. run mvn spring-boot:run to start the application
2. In Postman run POST http://localhost:8080/api/v1/notification
   With requestbody for email
   
         {
          "channel": "email",
         "notificationMessage": {
            "from": "adeshbedre@gmail.com",
            "to": "someotherguy@gmail.com",
            "subject": "Billing process failing",
            "body": "Billing process is failing with outofmemory exception."
         }
       }
  
  
  or for slack
  
  
      {
         "channel": "slack",
         "notificationMessage": {
            "from": "adeshbedre@gmail.com",
            "to": "someotherguy@gmail.com",
            "subject": "Billing process failing",
            "body": "Billing process is failing with outofmemory exception."
         }
      }
  
## Working
The notification system pushes the message to ThreadPoolTaskExecutor's blocking queue and will be picked up asynchronously by another thead which will consume the message and send it to the appropriate channel. Please note that both channels are mocked right now. Adding new channels would require implementing Channel class and adding the new channel to channelTypeEnum and ChannelFactory.
