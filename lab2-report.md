# Lab Report 2

## Part 1
This is the code for my `ChatServer` implementation:

```java
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    ArrayList<String> messageList = new ArrayList<String>();

    public String handleRequest(URI url) {
        if (url.getPath().contains("/add-message")) {
            // splits query into "s=<message>" and "user=<username>"
            String[] parameters = url.getQuery().split("&");
            // splits first section into "s" and "message"
            String[] message = parameters[0].split("=");
            // splits second section into "user" and "username"
            String[] user = parameters[1].split("=");
            // adds it to list
            messageList.add(user[1] + ": " + message[1]);
            
            // creates return String
            String returnValue = "";
            for (int i = 0; i < messageList.size(); i++) {
                returnValue = returnValue + messageList.get(i) + "\n";
            }

            return returnValue;
        } else if (url.getPath().equals("/")) {
            return "Hello! Add some messages!";
        }
        return "Please follow this format: /add-message?s=<message>&user=<username>";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
    }
}
```

**Screenshot #1**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/81135d89-12b8-41d3-9c4a-120da783ec72)

For this screenshot, the `handleRequest` method in the `Handler` class was called. The argument to this method call was the URL I typed in, or `http://localhost:3000/add-message?s=Hello%20There&user=sarah`, which was stored in the `url` field. 

`url` was then split into a String array `parameters`, which took the query of the URL (`s=Hello%20There&user=sarah`) and split it around the `&` character. This would mean that `parameters[0]` would equal `s=Hello%20There` and `parameters[1]` would equal `user=sarah`. `parameters[0]` was then split into the String array `message` around the `=` character, meaning that `message[0]` would equal `s` and `message[1]` would equal the actual message, or in this case, `Hello%20There`. Similarly, `parameters[1]` was split into the String array `user` around the `=` character, meaning `user[0]` would equal `user` and `user[1]` would equal the actual username, or in this case, `sarah`.
