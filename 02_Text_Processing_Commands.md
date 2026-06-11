# <u> Linux Text Processing: Essential Commands & Options </u>


## <u> What is Text Processing in Linux? <u/>

Text processing is the practice of using commands to search, edit, filter, slice, and reorganize text files (like configuration files, spreadsheets, or server logs) directly from the command line, without ever opening a heavy graphical program like Microsoft Word or Excel.


## <u> Why is it Useful? <u/>

  - Unmatched Speed : You can scan or edit a massive 10GB file in seconds, whereas normal text editors would freeze or crash.

  - Automation : You can write a single line of code to clean up hundreds of files automatically.

  - Command Chaining (Piping) : You can easily send the output of one command into another (using the | pipe symbol) to perform complex tasks in one go.


## <u> Our Practice File : employees.txt </u>

To keep things simple, imagine we are working with this text file:

    Alice,Engineer,30
    Bob,Manager,45
    Charlie,Designer,25
    david,Engineer,28


## <u> The 7 Essential Commands & Their Options </u>


### 01. grep (The Searcher)

  - What it does : Searches for a specific word or pattern in a file and prints the matching lines.

Key Options :

  - -i (Ignore Case): Searches without caring about uppercase or lowercase.

        Example: grep -i "david" employees.txt (matches "david" or "David")

  - -v (Invert Match): Shows lines that do NOT match.

        Example: grep -v "Engineer" employees.txt (shows everyone except engineers)

  - -n (Line Numbers): Prints the line number next to the match.

        Example: grep -n "Manager" employees.txt (prints 2:Bob,Manager,45)
<u> ----------------------------------------------------------------------------------------------------------------------------------------------- </u>
### 02. awk (The Column Plucker)

  - What it does: Scans files line-by-line, breaks each line into columns, and lets you extract or analyze them.

Key Options:

  - -F (Field Separator): Tells awk what character splits your columns (comma, space, tab, etc.).

        Example: awk -F"," '{print $1}' employees.txt (uses , to grab the 1st column: Names)

  - NR (Number of Record): Filters and displays text based on specific line/row numbers.

        Example: awk 'NR==3' employees.txt (prints only the 3rd line of the file: Charlie)
<u> ----------------------------------------------------------------------------------------------------------------------------------------------- </u>
### 03. sed (The Stream Editor)

  - What it does: Finds a specific piece of text and automatically replaces it with something else.

Key Options:

  - g (Global Replace): Replaces every match on a line instead of just the first one.

        Example: sed 's/e/X/g' employees.txt (replaces every letter "e" with "X")

  - -i (In-Place Edit): Saves the changes directly to the file permanently.

        Example: sed -i 's/Manager/Director/' employees.txt (permanently updates "Manager" to "Director" inside the file)
<u> ----------------------------------------------------------------------------------------------------------------------------------------------- </u>
### 04. sort (The Organizer)

  - What it does: Sorts lines of text alphabetically or numerically.

Key Options:

  - -r (Reverse): Sorts in reverse order (Z to A, or largest to smallest).

        Example: sort -r employees.txt

  - -n (Numerical Sort): Sorts by actual math value instead of alphabet (so 10 comes after 2, instead of before it).

        Example: sort -n numbers.txt

  - -u (Unique): Sorts the file and automatically deletes any duplicate lines.

        Example: sort -u employees.txt
<u> ----------------------------------------------------------------------------------------------------------------------------------------------- </u>
### 05. cut (The Slicer)

  - What it does: Quickly cuts out a specific section (characters or columns) from each line. It is like a lighter, simpler version of awk.

Key Options:

  - -d (Delimiter) & -f (Field): Used together to extract columns.

        Example: cut -d"," -f1 employees.txt (splits by comma, grabs the 1st column)

  - -c (Character Cut): Cuts specific character positions instead of whole words.

        Example: cut -c 1-5 employees.txt (grabs only the first 5 characters of every line)
<u> ----------------------------------------------------------------------------------------------------------------------------------------------- </u>
### 06. head (The Top Previewer)

  - What it does: Shows the very beginning (the "head") of a file. (Defaults to the first 10 lines).

Key Options:

  - -n (Number of lines): Customizes how many lines you want to see from the top.

        Example: head -n 2 employees.txt (shows the first 2 lines)

  - -c (Bytes/Characters): Shows just the first few characters/bytes instead of full lines.

        Example: head -c 5 employees.txt (shows just Alice)
<u> ----------------------------------------------------------------------------------------------------------------------------------------------- </u>
### 7. tail (The Bottom Previewer)

  - What it does: Shows the very end (the "tail") of a file. (Defaults to the last 10 lines).

Key Options:

  - -n (Number of lines): Customizes how many lines you want to see from the bottom.

        Example: tail -n 1 employees.txt (shows just the very last line)

  - -f (Follow): Keeps the file open on your screen and displays new lines in real-time as they are added (essential for watching live logs!).

        Example: tail -f server.log
