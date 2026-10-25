# Input/Output Redirection Examples

Redirection allows you to change where a command gets its input from or where it sends its output.

## `Cmd < fichier`
---
**Description:** Redirects the **standard input**  of a command (`Cmd`) to come from a `fichier` (file), instead of the keyboard.

* **Example:** Count the number of lines in `my_text.txt` by providing it as input to `wc -l`.
    ```bash
    echo "Line 1" > my_text.txt
    echo "Line 2" >> my_text.txt
    wc -l < my_text.txt
    # Output: 2
    ```

## `Cmd > fichier`
---
**Description:** Redirects the **standard output** of a command (`Cmd`) to `fichier`. If `fichier` exists, it will be **overwritten**. If it doesn't exist, it will be created.

* **Example:** Save the list of files in the current directory to `file_list.txt`.
    ```bash
    ls > file_list.txt
    # The content of 'file_list.txt' will now be the output of 'ls'.
    ```

## `Cmd >> fichier`
---
**Description:** Redirects the **standard output**  of a command (`Cmd`) to `fichier`. If `fichier` exists, the output will be **appended** to its current content. If it doesn't exist, it will be created.

* **Example:** Add the current date and time to the end of `log.txt`.
```bash
    echo "First entry" > log.txt # Create initial log file
    date >> log.txt
    # The content of 'log.txt' will now include "First entry" followed by the date.
```


# `|` (Pipe)

The pipe operator `|` is a fundamental concept in the Linux shell. It takes the **standard output** of the command on its left and feeds it directly as the **standard input** to the command on its right. 

* **Example:** List all files in the current directory, and then filter that list to only show lines containing the word "report".
    ```bash
    ls -l | grep "report"
    ```
    * **Explanation:**
        1.  `ls -l` lists the contents of the current directory in a long format.
        2.  The `|` takes that entire `ls -l` output.
        3.  `grep "report"` receives that output as its input and filters it, displaying only the lines that contain the string "report".

# `wc` (Word Count)

The `wc` command (short for "word count") is used to count the number of lines, words, and characters (bytes) in files. If no file is specified, it reads from standard input.

* **Example:** Count the lines, words, and characters in a file named `sample.txt`.
    ```bash
    echo "Hello world" > sample.txt
    echo "This is a test." >> sample.txt
    wc sample.txt
    # Output will show counts for lines, words, and characters, followed by the filename.
    # e.g., 2  7 28 sample.txt
    ```

---

# `wc` Command Options

| Option | Description (English)                                          | Example Command        |
| ------ | -------------------------------------------------------------- | ---------------------- |
| `-l`   | Gives the number of lines of the specified file(s).            | ```wc -l sample.txt``` |
| `-w`   | Gives the number of words of the specified file(s).            | ```wc -w sample.txt``` |
| `-c`   | Gives the number of bytes/characters of the specified file(s). | ```wc -c sample.txt``` |

# `grep` (Global Regular Expression Print)

The `grep` command is a powerful utility used to **search for specific patterns (strings or regular expressions)** within text files or standard input. It prints lines that contain a match for the specified pattern.

* **Example (Basic `grep`):** Find all lines containing the word "error" in `syslog.log`.
    ```bash
    # Create a dummy log file
    echo "INFO: System started\nERROR: Disk full \n WARNING: Low memory" > syslog.log
    grep "error" syslog.log
    # Output: ERROR: Disk full
    ```

---

# `grep` Command Options

| Option | Description                                               | Example Command                    |
| ------ | --------------------------------------------------------- | ---------------------------------- |
| `-v`   | Returns lines that do NOT contain the following text      | ```grep -v "error" syslog.log```   |
| `-c`   | Counts the number of lines containing the text            | ```grep -c "INFO" syslog.log```    |
| `-n`   | returns the lines containing  the text in an ordered list | ```grep -n "WARNING" syslog.log``` |

# Regular Expressions with `grep`

Regular expressions are sequences of characters that define a search pattern. They are extremely powerful for defining complex search criteria. `grep` is built to use them.

| Expression | Description                                                             | Example Command                                                                                                                                                                          |
| ---------- | ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `^`        | Matches the beginning of a line.                                        | ```grep "^ERROR" syslog.log # Matches lines that START with "ERROR".```                                                                                                                  |
| `.`        | Matches any single character                                            | ```echo "cat\ncut\ncot" grep "c.t" # Matches "cat", "cut", "cot".```                                                                                                                     |
| `$`        | Matches the end of a line.                                              | ```grep "full$" syslog.log # Matches lines that END with "full".```                                                                                                                      |
| `x*`       | Matches zero or more repetitions of the character `x` that precedes it. | ```echo "color\ncolour"  grep "colou*r" # Matches both "color" (0 'u's) and "colour" (1 'u').```                                                                                         |
| `[...]`    | Matches any single character within the specified set or range.         | ```echo "grey\ngray"grep "gr[ae]y" # Matches "grey" or "gray".```                                                                                                                        |
| `[^...]`   | Matches any single character NOT within the specified set or range.     | ```echo "test1\ntestA"   grep "test[^0-9]" # Matches "testA" (any non-digit after "test")```                                                                                             |

# `find` Command Options

The `find` command uses a logical structure where you specify a **starting path**, followed by **criteria (options/tests)**, and then **actions** to perform on the found items.

| Option                  | Description                                                                                                                                                                            | Example Command                                                                                                                        |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `-name NOM`             | Recherche sur le nom du fichier (`NOM`). Supports wildcards (`*`, `?`, `[]`).                                                                                                          | ```find /home/user -name "*.log" # Finds all files ending with .log in /home/user and its subdirectories.```                           |
| `-type TYPE`            | Recherche sur le type de fichier. `TYPE` peut être: <br> `d` (répertoire), <br> `f` (fichier normal),                                                                                  | ```find . -type d -name "config*" # Finds all directories starting with "config" in the current path.```                               |
| `-mtime N`              | Recherche par date de dernière modification du fichier.                                                                                                                                | ```find . -mtime -1 -type f\n# Finds regular files modified in the last 24 hours.```                                                   |
| `-exec COMMANDE {} \\;` | Exécute `COMMANDE` pour chaque fichier trouvé. L'expression `{}` est remplacée par le chemin du fichier actuel. Le point-virgule `;` termine la commande et doit être échappé (`\\;`). | ```find . -name "*.tmp" -exec rm {} \\; # Finds and deletes all files ending with .tmp in the current directory and subdirectories.``` |
| `-delete`               | Supprime les fichiers trouvés. (Plus simple et plus sûr que `-exec rm {} \\;` si c'est la seule action.)                                                                               | ```find /old_temp -name "*.bak" -delete # Finds and deletes all files ending with .bak in /old_temp.```                                |

# `cut`

The `cut` command is used to **extract sections (columns) from each line of files or standard input**. It's very useful for parsing data where fields are separated by delimiters or by fixed character positions.

* **Example (Basic `cut` - using default tab delimiter):**
    Let's create a dummy file with some tab-separated data:
```bash
    echo -e "ID\tName\tCity" > data.tsv
    echo -e "1\tAlice\tNew York" >> data.tsv
    echo -e "2\tBob\tLondon" >> data.tsv
    cut -f 2 data.tsv
    # Output:
    # Name
    # Alice
    # Bobcut Command Options
```


| Option                          | Description                                                              | Example Command                                                                                                                                                                                              |
| ------------------------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `-d DELIM`, `--delimiter=DELIM` | Use `DELIM` as the field delimiter character instead of the default tab. | ```echo "Name,Age,City" > people.csv echo "Alice,30,New York" >> people.csv         echo "Bob,24,London" >> people.csv     <br>cut -d ',' -f 1,3 people.csv  # Output:Name,City Alice,New York Bob,London``` |
