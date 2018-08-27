**[Source](./docs/1-Intro.html)**

# This is a service for Automated UI Data-Driven-Tests for QA.


The syntax is of a YAML file (inspired by [Ansible](https://ansible.com)).


Each file is a list/an array of tasks (see, test/default.yml).

Every task must contain a "name" if it's not an "include" of another YAML file.

Moreover, it has to have an operation - the test itself.

NOTE: The names are arbitrary, but mandatory!


## The basic operations are:

- url      : Go to the given url
- click    : Click an element that has a given CSS selector
- script   : Run custom script
- set      : Set an element's value using a CSS selector
- get      : Get an element's value using a CSS selector
- alert    : Accept alert
- frame    : Switch to frame with given ID
- sleep    : Sleep for a given number of seconds


## The complex operations are:

- include  : Include another script/YAML instead of this step
- vars     : Set a list of named constants
- register : Register a dynamic variable from an element's value using its CSS selector
- if       : Run the task under condition
- tags     : A list of tags of the task

## Many Assertion types

## Special variable

- ${UUID}
- ${DATE}
- ${DATE_ISO}
- ${TIME}