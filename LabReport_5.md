[Source](https://www.makeuseof.com/grep-command-practical-examples/)

Ways to use grep

Use 1 - Finding the exact occurrences of a string:
This can be done using the -w option with grep.

Example 1:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image1.png)


What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?

* I'm using a Windows 11 laptop and I'm trying to run my code through a bash terminal in Visual Studio Code, where I've written my other files as well.

Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.

* In my script, after running the tests, I try to catch the number of successes through this line of code: passed_tests=$(echo "$output" | grep 'OK' | tr -dc '0-9'). Unfortunately,
* when I run the script, the number of passed tests turns up blank. Screenshots provided below:

Detail the failure-inducing input and context. That might mean any or all of the command you're running, a test case, command-line arguments, working directory, even the last few commands you ran. Do your best to provide as much context as you can.

