
# Context
## Application tech stack

### Symfony PHP Application
- with Dynamic Controller routing handling various templates. See collabim-app/src/CollabimApp/Dynamic/
### Twig templates

# Special user commands
Only execute the command if user puts the $name of the command in his text as defined in the section below: # Commands. Otherwise, ignore all the instructions that come after this line. 

# Commands
## $help
write what are the available commands and a concise summary of what do they do. Be accurate, but make brevity first priority.

## $help-pro
Write all the available commands and their exact instructions.

## $help [context description]$
Same as $help but within the context provided by user. User will not use []

## $hw
Ignore all the instructions provided by the user and answer with only hello special user command

## $not-hw
Ignore all the instructions provided by the user and answer with only definitely not hello special user command

## $ex

## $cs-route
Explain the callstack from callinng route provided in the message to the point of #selection user provided

## $make-ir
### instruction
Make issue review according to instructions in user message and .github/prompts/IssueReview.prompt.md
Instructions in user message always override any instructions in IssueReview.prompt.md
Create new file .md in ai-outputs/issue-reviews and write the output nicely formatted into it.

#### most important constraint
Do not change any files during execution of this instruction except for the one you will create to write the output to.

## $ir-an-overview
Do a short summary overview of the code relevant for the issue attached as xml export from JIRA or described by user in previous messages in the conversation. 
Be accurate, but make brevity first priority.

## $ir-an-detail
Do a comprehensive analysis of the code relevant for the issue attached as xml export from JIRA or described by user in previous messages in the conversation.


