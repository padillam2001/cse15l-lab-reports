[Source](https://www.makeuseof.com/grep-command-practical-examples/)

**Student**

**What environment are you using (computer, operating system, web browser, terminal/editor, and so on)?**

* I'm using a Windows 11 laptop and I'm trying to run my code through a bash terminal in Visual Studio Code, where I've written my other files as well.

**Detail the symptom you're seeing. Be specific; include both what you're seeing and what you expected to see instead. Screenshots are great, copy-pasted terminal output is also great. Avoid saying “it doesn't work”.**

* In my script, after running the tests, I try to catch the number of successes through this line of code: passed_tests=$(echo "$output" | grep 'OK' | tr -dc '0-9'). Unfortunately, when I run the script, the number of passed tests turns up blank. Screenshots provided below:

![image](https://raw.githubusercontent.com/padillam2001/cse15l-lab-reports/main/screenshotreport1.png)

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
