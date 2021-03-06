[**[Tree](https://github.com/freaker2k7/ui-data-driven-tests)**]


# Special variable

These are magic variable (that you can't override) so you can insert functional values.


## ${UUID} - Generated a random UUID

### Example 1:

```yaml
- name: some-task-${UUID} # This will generate a fresh uuid
  ⋮

- name: some-task-${UUID} # And this one will generate a new uuid
  ⋮
```


### Example 2:

```yaml
- name: set-name
  vars:
    name: ${UUID} # In this case, both of the following tests will have the same name

- name: some-task-${name}
  ⋮

- name: some-task-${name}
  ⋮
```


### Example 3:

```yaml
- name: cache-buster
  url: "http://example.com/?_=${UUID}" # This will bypass the cache by force
```


## ${DATE} - Generate a new date string

### Example:

```yaml
- name: some-task-${UUID}:${DATE} # This will generate a fresh uuid and date
  ⋮
```


## ${DATE_ISO} - Generate a new ISO date string

### Example:

```yaml
- name: some-task
  set: "input[type=\"date\"]"
  value: ${DATE_ISO}
```


## ${TIME} - Generate a new unix timestamp in milliseconds

### Example:

```yaml
- name: some-task
  if:
    cond: ${TIME}
    op: "<"
    value: 2000000000
```


[**[Source](https://github.com/freaker2k7/ui-data-driven-tests/blob/master/5-Extras.md)**]