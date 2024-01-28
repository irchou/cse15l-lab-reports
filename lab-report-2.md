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
![Image](/images/ChatLog2.png) 

## Part 2

## Part 3
