[**[Tree](https://github.com/freaker2k7/ui-data-driven-tests)**]


# Basic Usage


You should run each operation in an individual test. 

You can do combinations of operations in a single task, if it makes sense for you.

NOTE: Be careful to NOT use an operation more than once in a task!


## "url" - Go to the given url


### Example:

```yaml
- name: usually-the-first-task
  url: "http://example.com
```


## "click" - Click an element that has a given CSS selector


### Example 1:

```yaml
- name: some-task
  click: "#wrap > h2:last-child" # Or any CSS selector
```

NOTE: If the element doesn't exist, the whole test will fail!


### Example 2:

```yaml
- name: some-other-task
  click: h1
```



## "script" - Run custom script


### Example 1:

```yaml
- name: some-task
  script: "alert(22);"
```


### Example 2:


This is test/sub/disable-alerts.yml which can be included (see, test/docs/3-Advanced.md)
to disable some of the alerts for the test if needed.

```yaml
- name: some-task
  script: "window.alert = window.confirm = window.prompt = window.onbeforeunload = function(str) { return true; };"
```


## "set" - Set an element's value using a CSS selector


### Example 1:

```yaml
- name: some-set-task
  set: "input[type=\"email\"]"
  value: "abc@example.com" # Required !!!
```


### Example 2:

```yaml
- name: some-other-set-task
  set: "#username"
  value: "John Doe" # Required !!!
```


## "get" - Get an element's value using a CSS selector


### Example 1:

```yaml
- name: some-get-task
  get: "input[type=\"email\"]"
  expect: "to.be.visible" # Required !!!
```


### Example 2:

```yaml
- name: some-other-get-task
  get: "#username"
  expect: "to.have.count" # Required !!!
  value: 1 # (optional)
```


### Example 3:

```yaml
- name: some-other-get-task
  get: "#username"
  expect: "text" # Required !!!
  value: "John Doe" # (optional)
```


## "alert" - Accept alert


### Example:

```yaml
- name: some-alert-task
  alert: true
```


## "frame" - Switch to frame with given ID


### Example:

```yaml
- name: some-frame-task
  frame: "frame-id" # You can set an ID if such doesn't exist, with "script"
```


## "sleep" - Sleep for a given number of seconds


### Example:

```yaml
- name: some-sleep-task
  sleep: 3 # This will sleep for 3 seconds. 
```


## "notify" - A webhook url (POST)


### Example 1:

```yaml
- name: some-task-87
  get: "#username"
  expect: "text"
  value: "John Doe"
  notify: "http://example.com" # This will send the result status of this step
```
**NOTE: This notification will be send even if the previous tasks fail.**


### Example 2:

```yaml
- name: some-notift-task
  notify: "http://example.com" # This will send the overall status (at this point)
```


[**[Source](https://github.com/freaker2k7/ui-data-driven-tests/blob/master/2-Basic.md)**]
