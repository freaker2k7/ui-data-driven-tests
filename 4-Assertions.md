**[Source](./docs/4-Assertions.html)**

# Assertion Types

The assertions are what the "expect" field in the "get" operation is expecting.

## The full list of supported assertions


### Assertions without expected "value".

- .be.true
- .be.false
- .to.exist
- .to.be.null
- .to.be.undefined
- .to.be.empty
- .to.be.arguments
- .to.be.function
- .to.be.visible
- .to.be.hidden
- .to.be.checked
- .to.be.selected
- .to.be.enabled
- .to.be.disabled
- .to.be.empty
- .to.to.exist


### Assertions with **mandatory** expected "value".

- .to.be.instanceOf(expected)
- .to.equal(expected)
- .to.eql(expected)               // deep equality
- .to.deep.equal(expected)        // same as .eql
- .to.be.a('string')
- .to.be.text(expected)
- .to.include(expected)
- .be.ok(expected)
- .to.be.gt(numentic_expected)    // aka: .above .greaterThan
- .to.be.gte(numentic_expected)   // aka: .at.least
- .to.be.lt(numentic_expected)    // aka: .below
- .to.respondTo(string_expected)
- .to.have.members(numentic_expected_list)
- .to.have.keys(string_expected_list)
- .to.have.key(string_expected)
- .to.have.lengthOf(numentic_expected)
- .to.contain(string_expected)
- .to.have(expected_selector)
- .attr('foo')
- .prop('disabled')
- .data(expected_date_string)
- .class(string_expected)
- .id(string_expected)
- .html(string_expected_html)
- .text(string_expected)
- .value(string_expected)
- .css(string_expected_css_property)

<!-- # TODO: Implement expected value!!! -->
<!-- - .css(string_expected_css_property, string_expected_css_property_value) -->

NOTE: All the assertions with values should look like the following:

```yaml
- name: some-task
  get: ${some_selector}
  expect: ".to.have.key"
  value: foo
```

### Making an assertion negative

- .not                            // aka: .not.text('foo')
- .to.not                         // aka: .to.no.equal or .to.not.be.gt(8)


### Assertion chain order (downwards)

- .to
- .be
- .been
- .is
- .that
- .and
- .have
- .with
- .at
- .of
- .same
