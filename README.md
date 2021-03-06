
# Custom Channel Integration Server (Example)

This is a sample project to help you get started with integrating the [chatiico.com](https://chatiico.com) platform with any third-party messaging service provider, as a "custom channel" within chatiico.com.

This example implements an SMS provider called [ClickSend.com](https://clicksend.com). The code can be used as a general reference.

## API Routes

| Method | Path | Type | Description |
| ---- | ------ | --- | ------------------ |
| POST| /message | Outbound | Receive messages from chatiico.com and pass them to ClickSend using API |
| POST| /clicksend/push_message | Inbound | Receive messages from ClickSend and pass them to chatiico.com via the custom channel webhook |

>**Port**: 3030.

Follow the steps [here](http://docs.respond.com.co/) to get the custom channel API token.

## Setup

Run the following commands:

- `npm install`
- `npm start`

## How it works?

### Outbound Messages
```mermaid
sequenceDiagram
    participant chatiico.com
    participant Custom Integration Server
    participant ClickSend.com
    chatiico.com ->> Custom Integration Server: Send outbound message. Route: /message
    Custom Integration Server->> ClickSend.com: Calls SMS send API with the outbound message
    ClickSend.com ->> Custom Integration Server: Send response: 200 OK or 4xx
    Custom Integration Server ->> chatiico.com: Send response: 200 OK or 4xx (with error message)
    
```
### Inbound Messages
```mermaid
sequenceDiagram
    participant chatiico.com
    participant Custom Integration Server
    participant ClickSend.com
    
    ClickSend.com ->> Custom Integration Server: Receive inbound message. Route: /clicksend/push_message
    Custom Integration Server ->> chatiico.com: Calls custom channel webhook with the inbound message
    
    chatiico.com ->> Custom Integration Server: Send response: 200 OK or 4xx
    Custom Integration Server ->> ClickSend.com: Send response: 200 OK or 4xx
```
[See the visual diagram on Whimsical](https://whimsical.com/diagram-4eQ4FGca7go5gZ7vMEJfwU)

## References

- [ClickSend.com API Docs](https://developers.clicksend.com/docs/rest/v3/#view-inbound-sms)
- [respond.com.co: Custom Channel](http://docs.respond.com.co/?docs=canal-personalizado%ef%bf%bc)




