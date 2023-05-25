https://www.makeuseof.com/grep-command-practical-examples/
(Source)

Ways to use grep

Use 1 - Finding the exact occurrences of a string:
This can be done using the -w option with grep.

Example 1:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image1.png)

Output 1:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image2.png)

Example 2:

https://www.makeuseof.com/grep-command-practical-examples/
(Source)

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image3.png)
![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image4.png)

This can be useful if you do not want to include lines that only have partial matches.

Use 2 - to search for strings without regard for case sensitivity:

Examples:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image5.png)

Outputs:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image6.png)
![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image7.png)

This is useful in allowing you to search for key terms without needing to deal with all potential ways it can be capitalized.

Use 3 - Display line numbers along with rest of output with -n

https://www.makeuseof.com/grep-command-practical-examples/
(Source)

For this one, I asked ChatGPT to help me clarify what -n does:

ChatGPT Help:

Q: What does grep -n do?

A: The grep command is a powerful command-line tool used for searching text patterns within files. The -n option is an additional flag that tells grep to display the line numbers in the output along with the lines that match the specified pattern.
When you use grep -n followed by a pattern and a file or list of files, it searches for the given pattern and returns the matching lines with their corresponding line numbers.
For example, if you want to search for the pattern "apple" in a file called "fruits.txt" and display the line numbers, you would use the following command:
perl
Copy code
grep -n 'apple' fruits.txt
If the pattern "apple" is found in the file, the output will show the line number(s) along with the line(s) containing the pattern. If the pattern is not found, there will be no output.
Keep in mind that the grep command is case-sensitive by default. To perform a case-insensitive search, you can use the -i flag along with the -n flag:
perl
Copy code
grep -n -i 'apple' fruits.txt


Examples:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image8.png)

Outputs:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image9.png)
![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image10.png)

This is useful if you want to go to the lines after running grep to read what you found.


Use 4 - Find list of all files in directory of a particular extension with “.[extension]”

https://www.makeuseof.com/grep-command-practical-examples/
(Source)

Example 1:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image11.png)

Example 2:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/image12.png)

This can be useful if you want to get an idea of how much of a particular file type you have. You can use this output to, by counting each of the lines, find out precisely how many you have.
