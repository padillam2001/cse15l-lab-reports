Code: 
import java.io.IOException;
import java.net.URI;


class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String str = "";


    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(str);
        } else if (url.getPath().contains("/add-message")) {
            String nw = url.getQuery().split("=")[1];
            str = str + "\n" + nw;
            return String.format(str);
        } else {
            return "404 Not Found!";
        }
    }
}


class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }


        int port = Integer.parseInt(args[0]);


        Server.start(port, new Handler());
    }
}

![image](https://github.com/padillam2001/cse15l-lab-reports/blob/main/scsh1.png)
![image](https://github.com/padillam2001/cse15l-lab-reports/blob/main/scsh2.png)

--------------------------------------------------------------------------------

getPath(), equals(), contains(), getQuery(), split(), and format() are called

Arguments:
* getPath() does not take any arguments and is called on the URL object
* getQuery() does not take any arguments and is called on the URL object
* split() takes “=” as its argument and is called on the output of getQuery()
* format() does not take any arguments and is called on the string containing all the input strings
* contains() takes “/add-message” as its argument and is called on the output of getPath()

The value of the str field is changed when the /add-message path is used

Part 2:

Part 3:

I learned how to fork a repository from Github and how to use Github desktop to modify a repository. I imagine these things are pretty invaluable when working on a project, let alone with a team.
