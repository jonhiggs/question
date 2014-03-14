# question

Ask and validate a question within a shell script. It will set correct exit
codes and/or return the entered value.

## Requirements
It should run on any Unix OS. If you have
[cecho](http://github.com:jonhiggs/cecho.git) then you'll get some colour.

## Usage
`question [OPTIONS] <question>`

## Options


| Switch          | Value            |                                                     |
| --------------- | ---------------- | --------------------------------------------------- |
| --accepted-inputs= | regex          | Regular Expression describing acceptable inputs.
| --no-colour     |                  | Don't colour the string.
| --no-notify     |                  | Do not attempt to notify with terminal-notifier.
| --no-revalidate |                  | Exit with error if first answer is invalid.
| --quiet         |                  | Do not echo the answer.
| --title=        | string           | Title to send to terminal notifier.
| --type=         | ami              | An Amazon Machine Image ami-aaaaaaaa.
|                 | date             | A date (requires GNU date).
|                 | environment      | Either 'testing', 'staging' or 'production'.
|                 | existing_file    | A file that currently exists.
|                 | instance-id      | An AWS instance-id like i-aaaaaaaa.
|                 | integer          | A number.
|                 | list             | A comma delimited list.
|                 | multiword        | A string of words.
|                 | singleword       | A single word.
|                 | yes_no           | Either 'yes' or 'no'. (default)
| --verbose       |                  | Echo the answer.


## Examples

Set a variable with the answer of a question:

        TYPES=$(question --type=multiword "What type of animals do you farm")

Set a variable with a value:

        ANIMALS=$(question --type=integer "How many animals")

Set a variable with one of two options:

        GENDER=$(question --accepted-inputs="^(boy|girl)$" "Whats your gender")

You can enter a block using the return value of a question.

        if question "Do you have any camels"; then
            echo "I wonder if you can drink a camels milk..."
        fi

Or you can get the actual value that was set with the verbose switch:

        FARMER=$(question --verbose "Are you a farmer")

You can loop over a list of answers:

    RESULT=0
    for x in $(./question --type=list "What scores did you get"); do
        RESULT=$(( ${RESULT} + $x ))
    done
    echo ${RESULT}

