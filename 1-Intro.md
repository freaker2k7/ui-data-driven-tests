[**[Tree](https://github.com/freaker2k7/ui-data-driven-tests)**]


# This is a service for Automated UI Data-Driven-Tests for QA.


The syntax is of a YAML file (inspired by [Ansible](https://ansible.com)).


Each file is a list/an array of tasks (see, test/default.yml).

Every task must contain a "name" if it's not an "include" of another YAML file.

Moreover, it has to have an operation - the test itself.

NOTE: The names are arbitrary, but mandatory!


## The basic operations are:

- **url**          : Go to the given url
- **click**        : Click an element that has a given CSS selector
- **script**       : Run custom script
- **set**          : Set an element's value using a CSS selector
- **get**          : Get an element's value using a CSS selector
- **drag**         : Drag an element and Drop it on the given (selector or coordinate) value
- **alert**        : Accept alert
- **frame**        : Switch to frame with given ID
- **sleep**        : Sleep for a given number of seconds
- **notify**       : A webhook url (POST)


## The complex operations are:

- **useragent**    : Set the User-Agent for the test
- **resize**       : Set the window's width and height
- **file**         : Set a file for a file-selection input field using a CSS selector
- **include**      : Include another script/YAML instead of this step
- **vars**         : Set a list of named constants
- **register**     : Register a dynamic variable from an element's value using its CSS selector
- **if**           : Run the task under condition
- **tags**         : A list of tags of the task
- **format**       : The output format for the webhook [JSON / XML / Form / JUnit / E-Mail]
- **xpath**        : A flag for using XPath instead of CSS selectors (default is "false")

## Many Assertion types

## Special variable

- **${UUID}**      : Generated a random UUID
- **${DATE}**      : Generate a new date string
- **${DATE_ISO}**  : Generate a new ISO date string
- **${TIME}**      : Generate a new unix timestamp in milliseconds


[**[Source](https://github.com/freaker2k7/ui-data-driven-tests/blob/master/1-Intro.md)**]
