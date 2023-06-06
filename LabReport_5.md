**Student**

**What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?**

* I'm using a Windows 11 laptop and I'm trying to run my code through a bash terminal in Visual Studio Code, where I've written my other files as well.

**Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.**

* In my script, after running the tests, I try to catch the number of successes through this line of code: `passed_tests=$(echo "$output" | grep 'OK' | tr -dc '0-9')`. Unfortunately, when I run the script, the number of passed tests turns up blank. Screenshots provided below:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/screenshotreport1.png)
*Note, in this screenshot it is mentioned that ChatGPT was used to assist in writing some of the script. For the log of that conversation, see the bottom of the submission.*

**Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.**

* I'm running this command, which induces the failing input: $  bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected
* The command will run my script, which clones the linked repository onto my computer and runs jUnit tests on it. I do not have any previous commands to give. My working directory is: /c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main
* Below, I provide screenhots of my directory structure and my script:

```CPATH='/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/./:/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/lib/junit-4.13.2.jar:/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/lib/hamcrest-core-1.3.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

cd student-submission

file="ListExamples.java"

if [ -f "$file" ]
then 
echo "$file exists"
else 
echo "$file could not be found. Please check your submission for any missing files and resubmit."
exit
fi

cp *.java ../grading-area
cd ../grading-area


javac -cp $CPATH *.java


output=$(java -cp $CPATH org.junit.runner.JUnitCore TestListExamples)

#When writing line 35, I asked ChatGPT for some tips on how to isolate a character from the terminal. The discussion can be found in the file "chat.txt"

passed_tests=$(echo "$output" | grep 'OK' | tr -dc '0-9')


echo "Grade: $passed_tests / 4"
```

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/directory_structure.png)

**TA, Response:**

* Hmm, have you tried to see what is stored in $output in different cases? Check this, and think about why your results are blank.

**Console After Following Advice:**

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/outputafteradvice.png)

* It becomes evident after adding `echo $output` to the script that the jUnit output is not always in the format of OK(n) where n is the number of tests passed. Because of this, if a test fails, `passed_tests=$(echo "$output" | grep 'OK' | tr -dc '0-9')` will not catch the number of successes, which is why `passed_tests` is empty.

**All Information About Setup:**

Directory Setup:
![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/directory_structure.png)

Code Before Fix:

```CPATH='/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/./:/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/lib/junit-4.13.2.jar:/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/lib/hamcrest-core-1.3.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

cd student-submission

file="ListExamples.java"

if [ -f "$file" ]
then 
echo "$file exists"
else 
echo "$file could not be found. Please check your submission for any missing files and resubmit."
exit
fi

cp *.java ../grading-area
cd ../grading-area


javac -cp $CPATH *.java


output=$(java -cp $CPATH org.junit.runner.JUnitCore TestListExamples)

#When writing line 35, I asked ChatGPT for some tips on how to isolate a character from the terminal. The discussion can be found in the file "chat.txt"

passed_tests=$(echo "$output" | grep 'OK' | tr -dc '0-9')


echo "Grade: $passed_tests / 4"
```

Server.java Before Fix:
```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url) throws IOException;
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}
```

TestListExamples.java Before Fix:
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }
}
```

GradeServer.java Before Fix:

```
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.URI;
import java.net.URISyntaxException;
import java.util.Arrays;
import java.util.stream.Stream;

class ExecHelpers {

  /**
    Takes an input stream, reads the full stream, and returns the result as a
    string.

    In Java 9 and later, new String(out.readAllBytes()) would be a better
    option, but using Java 8 for compatibility with ieng6.
  */
  static String streamToString(InputStream out) throws IOException {
    String result = "";
    while(true) {
      int c = out.read();
      if(c == -1) { break; }
      result += (char)c;
    }
    return result;
  }

  /**
    Takes a command, represented as an array of strings as it would by typed at
    the command line, runs it, and returns its combined stdout and stderr as a
    string.
  */
  static String exec(String[] cmd) throws IOException {
    Process p = new ProcessBuilder()
                    .command(Arrays.asList(cmd))
                    .redirectErrorStream(true)
                    .start();
    InputStream outputOfBash = p.getInputStream();
    return String.format("%s\n", streamToString(outputOfBash));
  }

}

class Handler implements URLHandler {
    public String handleRequest(URI url) throws IOException {
       if (url.getPath().equals("/grade")) {
           String[] parameters = url.getQuery().split("=");
           if (parameters[0].equals("repo")) {
               String[] cmd = {"bash", "grade.sh", parameters[1]};
               String result = ExecHelpers.exec(cmd);
               return result;
           }
           else {
               return "Couldn't find query parameter repo";
           }
       }
       else {
           return "Don't know how to handle that path!";
       }
    }
}

class GradeServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

class ExecExamples {
  public static void main(String[] args) throws IOException {
    String[] cmd1 = {"ls", "lib"};
    System.out.println(ExecHelpers.exec(cmd1));

    String[] cmd2 = {"pwd"};
    System.out.println(ExecHelpers.exec(cmd2));

    String[] cmd3 = {"touch", "a-new-file.txt"};
    System.out.println(ExecHelpers.exec(cmd3));
  }
}
```

Cloned Repository Before Fix:

```

import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }


}
```

script.sh After Fix:

```CPATH='/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/./:/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/lib/junit-4.13.2.jar:/c/Users/padil/Desktop/list-examples-grader-2/list-examples-grader-main/lib/hamcrest-core-1.3.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

cd student-submission

file="ListExamples.java"

if [ -f "$file" ]
then 
echo "$file exists"
else 
echo "$file could not be found. Please check your submission for any missing files and resubmit."
exit
fi

cp *.java ../grading-area
cd ../grading-area


javac -cp $CPATH *.java


output=$(java -cp $CPATH org.junit.runner.JUnitCore TestListExamples)

#When writing line 35, I asked ChatGPT for some tips on how to isolate a character from the terminal. The discussion can be found in the file "chat.txt"

passed_tests=$(echo "$output" | grep 'OK' | tr -dc '0-9')
failed_tests=$(echo "$output" | grep 'Failures:' | cut -d ':' -f 2 | tr -dc '0-9')

# Check for passed tests
if [ -n "$passed_tests" ]; then
    echo "Grade: $passed_tests / 4"
else
    if [ -n "$failed_tests" ]; then
        echo "Failed tests: $failed_tests. Please check your code."
    else
        echo "No output from the tests. Please check your code."
    fi
fi


```

In order to fix the bug, we must take into account that JUnit outputs to the console are not always the same. We look to the format for tests failed, and we see that it takes the form `Tests run: 1, Failures: 1`. We simple create a new `$failed_tests` variable to catch the result given this output and add an if-statement structure where, if `$passed_tests` is empty and `$failed_tests` isn't, we return the number of tests failed.

Commands Ran to Trigger the Bug:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/screenshotreport1.png)



**Reflection:**

* A cool thing I've learned in lab recently has to be using VIM. I never knew you could edit code from the terminal!



**ChatGPT:**

When writing the script, I used ChatGPT to ask a couple of questions. The conversation is posted below:

Me: What are bash commands I can use to isolate a specific character outputted to the terminal?

ChatGPT: Isolating a specific character outputted to the terminal can be achieved using a variety of Bash commands and utilities. The commands used may differ based on your exact requirements. Below are a few examples.

1. **grep:** This is a very powerful command used for pattern searching and filtering. Here's an example usage:
   ```bash
   echo "Hello, World!" | grep -o 'H'
   ```
   This will output only 'H', the character you specified.

2. **cut:** This command is used to cut out sections from each line of input - usually fields or columns. To isolate a specific character at a specific position you can use it as follows:
   ```bash
   echo "Hello, World!" | cut -c1
   ```
   This will output 'H', the character at the first position.

3. **awk:** `awk` is another powerful utility for text processing. To isolate a specific character, you can use something like:
   ```bash
   echo "Hello, World!" | awk '{print substr($0,1,1)}'
   ```
   This will print 'H', the character at the first position.

4. **sed:** This is a stream editor for filtering and transforming text. Here's how you can use it:
   ```bash
   echo "Hello, World!" | sed 's/\(.\).*/\1/'
   ```
   This will output 'H', the first character.

Remember that indexing in most Unix utilities is 1-based, not 0-based. This means that the first character is at position 1, not 0.

These commands print the first character of a line. If you need a character at a different position, just replace the position number in the command.

Me: What about tr?

ChatGPT: The `tr` command in Unix/Linux is used for translating or deleting characters. It can be used to convert a character into another, squeeze repeating characters, or delete characters, but it doesn't have the capability to isolate and print specific characters like `cut`, `grep`, `awk`, or `sed`.

However, you can use `tr` for tasks like these:

1. Convert all lowercase letters to uppercase:

    ```bash
    echo "Hello, World!" | tr 'a-z' 'A-Z'
    ```

2. Delete specific characters:

    ```bash
    echo "Hello, World!" | tr -d ','
    ```

3. Replace all occurrences of a character:

    ```bash
    echo "Hello, World!" | tr 'o' 'a'
    ```

So, while `tr` is extremely useful in a lot of scenarios, isolating a specific character isn't one of its functionalities.
