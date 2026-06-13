# <u> -------------------- Bash Shell Scripting -------------------- <u/>

1. What is Bash Scripting?A Bash Script is a plain text file containing a sequence of commands that the Bash (Bourne Again SHell) program executes. Instead of typing commands one by one into a terminal manually, you group them inside a script file to execute complex workflows automatically.Primary Uses:Automation: Automating repetitive system maintenance tasks, log rotation, and backups.DevOps Pipelines: Building CI/CD deployment logic, provisioning cloud servers, and creating environment configurations.System Utilities: Writing custom shortcuts and tooling for your local development environment.2. Bash SyntaxEvery standard Bash script must start with a specialized line called a Shebang (#!/bin/bash). This tells the operating system's kernel to interpret the file using the Bash engine located in the /bin directory.Structural Requirements:Must start with #!/bin/bash on line 1.Comments start with a hash # symbol (the system ignores these lines).Files are typically saved with a .sh extension.To run a script, you must grant it execution permissions using chmod +x filename.sh and execute it with ./filename.sh.Bash#!/bin/bash
# This is a comment explaining what the script does

echo "Initializing system check..."
3. Bash VariablesVariables act as temporary storage blocks for data. In Bash, you don't declare data types; you simply assign a value using an equals sign.Important Syntax Rules:No spaces are allowed before or after the equals (=) sign during assignment.Variable names are case-sensitive and traditionally uppercase in professional workflows.To read or reference the variable later, prefix its name with a dollar sign ($).Bash#!/bin/bash

# Assigning values (Notice there are NO spaces around '=')
PROJECT_NAME="E-Commerce-Backend"
BUILD_VERSION=42

# Referencing variables using '$'
echo "Deploying project: $PROJECT_NAME"
echo "Current Build Number: $BUILD_VERSION"
4. Bash Data TypesBash is fundamentally a weakly typed language. It treats almost everything as a plain string of characters by default. However, depending on the context or syntax wrappers you use, Bash handles three distinct data structures:Strings: Text fields wrapped in single or double quotes.Integers: Whole numbers evaluated using arithmetic wrappers like $(( ... )).Constants: Read-only variables whose values cannot be changed or unassigned after definition.Bash#!/bin/bash

# 1. String Data Type
ENVIRONMENT="Production"

# 2. Integer Data Type (Evaluated inside double parentheses)
$((TIMEOUT_LIMIT = 30 + 15))
echo "The connection timeout limit is: $TIMEOUT_LIMIT seconds."

# 3. Constant Data Type
readonly CORE_DATABASE="postgres_db"
# CORE_DATABASE="mysql_db" # Uncommenting this line will trigger an execution error
5. Bash OperatorsOperators evaluate expressions, perform math operations, or compare strings and numbers. Because Bash treats things as strings by default, it uses distinct alphabetic flags (like -eq or -gt) for numeric comparisons instead of standard symbols.Operator TypeFlag / SymbolMeaningContext UsageArithmetic+, -, *, /Add, Subtract, Multiply, DivideWrap in $(( ))Numeric Comparison-eqEqual toInside [ ] conditional evaluationNumeric Comparison-neNot equal toInside [ ] conditional evaluationNumeric Comparison-gtGreater thanInside [ ] conditional evaluationNumeric Comparison-ltLess thanInside [ ] conditional evaluationString Comparison==Strings are identicalInside [ ] conditional evaluationString Comparison!=Strings are differentInside [ ] conditional evaluationLogical Control&&Logical ANDCombines multiple conditionsLogical Control||Logical ORCombines multiple conditionsBash#!/bin/bash

# Arithmetic operation
AVAILABLE_SLOTS=$((10 - 3))

# Numeric Comparison using flags
if [ $AVAILABLE_SLOTS -gt 5 ]; then
    echo "Server load is stable. Available slots: $AVAILABLE_SLOTS"
fi
6. Bash If...Else (Conditionals)Conditional statements control the execution path of a script based on whether a specific rule evaluates to true or false.Key Syntax Rules:You must include spaces inside the opening and closing square brackets [ ]. Failing to add a space after [ or before ] will break the script.Every conditional block opens with if and closes with fi (if spelled backwards).Bash#!/bin/bash

DISK_USAGE=85

# Checking conditions
if [ $DISK_USAGE -gt 90 ]; then
    echo "CRITICAL: Disk usage is over 90%! Clearing temporary cache..."
elif [ $DISK_USAGE -gt 80 ]; then
    echo "WARNING: Disk usage is at $DISK_USAGE%. Monitor closely."
else
    echo "SUCCESS: Disk space utilization is completely normal."
fi
7. Bash LoopsLoops allow you to run a block of code multiple times. The two main loops are:For Loop: Iterates through a fixed, predefined list of items.While Loop: Runs continuously as long as a specified condition remains true.Bash#!/bin/bash

echo "=== Running For Loop ==="
# Iterating over a list of microservices
for service in auth-service gateway-service database-service; do
    echo "Starting component: $service"
done

echo "=== Running While Loop ==="
# Running a countdown until a threshold condition breaks
RETRY_COUNT=3
while [ $RETRY_COUNT -gt 0 ]; do
    echo "Connecting to remote server... Retries left: $RETRY_COUNT"
    RETRY_COUNT=$((RETRY_COUNT - 1))
done
8. Bash FunctionsFunctions are reusable code blocks. Once a function is defined, it can be called multiple times throughout the script, preventing code duplication.Passing Arguments:Functions do not take explicitly named parameters in their definitions. Instead, you pass arguments sequentially when calling the function, and access them inside using positional tokens like $1 (first argument), $2 (second argument), etc.Bash#!/bin/bash

# Defining a reusable logging function
log_event() {
    local LOG_LEVEL=$1
    local LOG_MSG=$2
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] [$LOG_LEVEL] : $LOG_MSG"
}

# Invoking the function with positional arguments
log_event "INFO" "Application started successfully."
log_event "ERROR" "Failed to connect to the external API gateway."
9. Bash ArraysAn array is a data structure that lets you bundle multiple values into a single variable name.Access Rules:Arrays are defined inside parentheses ( ), separated by spaces.Individual items are accessed using index positions starting at 0.The special symbol @ is used to reference or loop through every element in the array simultaneously.Bash#!/bin/bash

# Defining an array of target backup directories
TARGET_DIRECTORIES=("/var/log" "/etc/nginx" "/opt/app/data")

# Accessing an individual item using index 0
echo "Primary backup target: ${TARGET_DIRECTORIES[0]}"

# Iterating through all items inside the array using "${ARRAY_NAME[@]}"
echo "Beginning full backup cycle for:"
for dir in "${TARGET_DIRECTORIES[@]}"; do
    echo " -> Backing up: $dir"
