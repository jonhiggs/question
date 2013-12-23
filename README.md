# question

Ask and validate a question within a shell script. It will set correct exit
codes and/or return the entered value.

## Requirements
It should run on any Unix OS. If you have
[cecho](http://github.com:jonhiggs/cecho.git) then you'll get some colour.

## Usage
`question [OPTIONS] <question>`

## Options

| Switch     | Value        |                                                 |
| ---------- | ------------ | ------------------------------------------------|
| --type=    | yes_no       | Either 'yes' or 'no'.                           |
|            | environment  | Either 'testing', 'staging' or 'production'.    |
|            | instance-id  | An AWS instance-id like i-aaaaaaaa.             |
|            | integer      | A number.                                       |
|            | multiword    | A string of words.                              |
|            | singleword   | A single word.                                  |
| --quiet    |              | Do not echo the answer.                         |
| --verbose  |              | Echo the answer.                                |

## Examples

Set a variable with the answer of a question:

        TYPES=$(question --type=multiword "What type of animals do you farm")

Set a variable with a value:

        ANIMALS=$(question --type=integer "How many animals")

You can enter a block using the return value of a question.

        if question "Do you have any camels"; then
            echo "I wonder if you can drink a camels milk..."
        fi

Or you can get the actual value that was set with the verbose switch:

        FARMER=$(question --verbose "Are you a farmer")
