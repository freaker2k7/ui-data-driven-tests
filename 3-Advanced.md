[**[Tree](https://github.com/freaker2k7/ui-data-driven-tests)**]


# Advanced Usage


On top of the "Basic" operations there are some features, 

giving the test the ability to become dynamic.


## "include" - Include another script/YAML instead of this step


NOTE: As mentioned, "include" tasks are the only ones that don't need a name,
because they will be overridden with the tasks of the given file.


### Example 1:

```yaml
- include: "test/sub/disable-alerts.yml"
```


## "vars" - Set a list of named constants


### Example 1:

```yaml
- name: some-task
  vars:
    foo: bar
    tar: baz
    val: 1

- name: "some-${foo}-task"
  get: "#${baz} h1"
  expect: "to.have.count"
  value: ${val}
```

### Example 2:

```yaml
- include: "test/sub/facebook.yml"
  vars:
    username: fooBarBaz
    password: 1qaz2wsx
```

### Example 3:

Variables can also be overridden.


```yaml
- name: some-task-87
  vars:
    foo: 12

- name: some-task-88
  get: "#rows li:nth-child(${foo})" # This will be translated into '#rows li:nth-child(12)'
  expect: "to.be.hidden"

- name: some-task-89
  vars:
    foo: 22

- name: some-task-90
  get: "#rows li:nth-child(${foo})" # And this will be correctly translated into '#rows li:nth-child(22)'
  expect: "to.be.visible"
```


## "register" - Register a dynamic variable from an element's value using its CSS selector


This is similar to "vars" except that it's being populated during the run from the DOM.


### Example:

This following code is taken from "test/sub/paypal.yml".
It's getting the value of the element with an id "payment_type_paypal"
and it "registers" it to the variable called "paypal_subscription".

I do it to determine later on the type of paypal page - Checkout vs Subscription.

NOTE: The registered variable can also override other registered variables.


```yaml
- name: paypal-check-type
  get: "#payment_type_paypal"
  register: paypal_subscription
```


## "if" - Run the task under condition

This is a (safe) simple if statement.

It has 4 fields:
- cond     : The condition value
- op       : The operand
- value    : The expected value
- dynamic  : Which part is dynamic [cond|value|both]

For now there are the following operands (you're welcome to contact me, see test/LICENSE.md):

- 'lt' or '<'
- 'gt' or '>'
- 'lte' or '<='
- 'gte' or '>='
- 'eq' - String comparison
- '==='
- 'ne' - String comparison
- '!=='
- !! (default, if not given)


### Example 1:

As we continue the previous example (register)...
We would like to click on the element with an id "payment_type_paypal"
if there is value in the **dynamic** variable "paypal_subscription" (!!paypal_subscription).


```yaml
- name: paypal-choose-account
  click: "#payment_type_paypal"
  if:
    - cond: paypal_subscription
      dynamic: cond
```


### Example 2:

Somewhere later, we would want to click on an element with an id "btnNext" and sleep for 2 seconds
if the **dynamic** (condition) variable fully equals (===) null (or in other words - empty).

```yaml
- name: paypal-account-login-continue
  click: "#btnNext"
  sleep: 2
  if:
    - cond: paypal_subscription
      op: "==="
      value: null
      dynamic: cond
```


### Example 3:

We can include the same script/YAML many times with different variable 
and have small if's navigating the tasks' flow.

```yaml
- include: 'test/sub/some-test.tml'
  vars:
    user_id: 1

- include: 'test/sub/some-test.tml'
  vars:
    user_id: 2

- include: 'test/sub/some-test.tml'
  vars:
    user_id: 22
```

Now inside 'test/sub/some-test.tml' you can have simple conditions like

```yaml
- name: some-task-15
  click: "#some-button"
  if:
    - cond: ${user_id}
      op: ">"
      value: 5
```

... or ...

```yaml
- name: some-task-51
  click: "#some-other-button"
  if:
    - cond: ${user_id}
      op: "==="
      value: 2
```


## tags - A list of tags of the task


This is used for scheduled runs.
I'm adding nowadays an ability to add tags and schedules ("cron" and "rate") for PRO users.

It'll work this way - you'll simply be able to add tags to each task/step.



### Example:

```yaml
- name: some-task-87
  ⋮
  tags:
    - nightly

- name: some-task-88
  ⋮
  tags:
    - nightly

- name: some-task-89
  ⋮
  tags:
    - nightly
    - daily
```


## format - The output format for the webhook [JSON / XML / Form / JUnit]


This is a complementary option for the "notify" parameter.
It can take one of the 4 values:

- json (Default)
- xml
- junit
- form

**NOTE: "form" is used when the receipient can accept only application/x-www-form-urlencoded and multipart/form-data.**
**NOTE: "format" should be used per notify, otherwise, it does nothing.**


### Example:

```yaml
- name: some-task-87
  ⋮
  notify: "http://example.com"
  format: junit # This will send http://example.com
```


## xpath - A flag for using XPath instead of CSS selectors


This is a complementary option for the "get", "set" and "click" parameters.
It can take be true or false.


### Example:

```yaml
- name: some-task-87
  click: "//*[@id='btnNext']"
  xpath: true
```


[**[Source](https://github.com/freaker2k7/ui-data-driven-tests/blob/master/3-Advanced.md)**]
