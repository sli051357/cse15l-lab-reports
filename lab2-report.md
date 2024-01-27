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

`url` was then split into a String array `parameters`, which took the query of the URL (`s=Hello%20There&user=sarah`) and split it around the `&` character. This would mean that `parameters[0]` would equal `s=Hello%20There` and `parameters[1]` would equal `user=sarah`. `parameters[0]` was then split into the String array `message` around the `=` character, meaning that `message[0]` would equal `s` and `message[1]` would equal the actual message, or in this case, `Hello%20There`. Similarly, `parameters[1]` was split into the String array `user` around the `=` character, meaning `user[0]` would equal `user` and `user[1]` would equal the actual username, or in this case, `sarah`. The formatted string then gets added to the ArrayList `messageList` and all the strings in the ArrayList are compiled into `returnValue` and then returned to the screen, which is the text that shows up on the page.

The most relevant value that got changed was the `messageList` ArrayList, because it stores the entire message history. It added the new message from the URL, which it then returns to the screen so the user can see it.

**Screenshot #2**

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/ac0fba6f-e29c-4e3f-aa1a-da058b90b161)

Similar to the previous screenshot, the `handleRequest` method in the `Handler` class was called. The argument to this method call was the URL I typed in, or `http://localhost:3000/add-message?s=goodbye&user=bob`, which was stored in the `url` field.

Like the previous method call, `url` was split into the String array `parameters`, where `parameters[0]` was equal to `s=goodbye`and `parameters[1]` was equal to `user=bob`. These were then further split into the String array `message`, where `message[0]` was equal to `s` and `message[1]` was equal to `goodbye`, and the String array `user`, where `user[0]` was equal to `user` and `user[1]` was equal to `bob`. These were then combined into a formatted string that was added to `messageList`, and all the strings in the ArrayList were then returned to the screen.

Once again, the most relevant value that got changed was the `messageList` ArrayList. What's important here is that the value that was first added (`sarah: Hello There`) from the previous method call was still in the ArrayList, and the new message was added. This way, by iterating through the ArrayList to create the String that gets returned, the previous messages are saved.

## Part 2

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/16ccacf9-0113-4a4d-b372-2dbbb0d1339d)

The absolute path to the private SSH key is `c/Users/sarah/.ssh/id_rsa`

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/0e934d49-7afd-49f1-b68d-fdf4594fc12d)

The absolute path to the public SSH key is `/home/linux/ieng6/oce/9f/sal075/.ssh/authorized_keys`

![image](https://github.com/sli051357/cse15l-lab-reports/assets/100035287/2d4a57cf-d46f-4106-a651-869ce8247df5)

This shows me logging into my `ieng6` account without being asked for a password.

## Part 3
One of the things I didn't know previously was that it was possible to split up a URL by its different parts and use those to create new messages or return statements. I thought it was really interesting how you could break down the query of a URL and split it so that you could analyze each part and create new things such as messages with them, especially because I've never really paid that much attention to how queries and oter parts in URL's can be used. It was also interesting how you could have different queries do different things, and although it seems obvious in retrospect, these differences in URLs is probably how many webpages function. For example, you could use it to have different reactions if somebody is logged in or not.
