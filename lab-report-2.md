# Lab Report 2

## Part 1
**Code for `ChatServer.java`**
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    String messagesHistory = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String[] message = parameters[0].split("=");
            String[] user = parameters[1].split("=");
            if(user[0].equals("user")) {
                messagesHistory = messagesHistory + user[1] + ": ";
            }
            if(message[0].equals("s")) {
                messagesHistory = messagesHistory + message[1] + "\n";
            }
            return messagesHistory;
        } else {
            return messagesHistory;
        }
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }
        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}
```

**Using `/add-message` examples**
![Image](/images/ChatLog1.png) 
The `handleRequest()` method in the code is called. The `handleRequest()` method takes in an URI as an argument, which it uses to get the `/add-message` query in the url. The `handleRequest()` method also uses the relevant `messagesHistory` String field. The `messagesHistory` field gets changed to store the newly added message from the url query. The `handleRequest()` method takes the query and appropriately formats the user and corresponding message before storing it `messagesHistory`.

![Image](/images/ChatLog2.png) 
The `handleRequest()` method in the code is called. The `handleRequest()` method takes in an URI as an argument, which it uses to get the `/add-message` query in the url. The `handleRequest()` method also uses the relevant `messagesHistory` String field. The `messagesHistory` field gets changed to store the newly added message from the url query. The `handleRequest()` method takes the query and appropriately formats the user and corresponding message before adding it to `messagesHistory`, so that both the previous and new messages are displayed.

## Part 2
**Path to private key**

![Image](/images/private key.png) 

**Path to public key**

![Image](/images/public key.png) 

**Logging into `ieng` account**

![Image](/images/ssh login.png) 

## Part 3
