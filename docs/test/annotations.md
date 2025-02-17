---
title: Annotations
redirect_to: https://developer.adobe.com/commerce/testing/functional-testing-framework/test/annotations/
status: migrated
---

# Annotations


Annotations are essentially comments in the code. In PHP, they all are marked by a preceding `@` symbol.

Within [tests], annotations are contained within their own node.

## Principles

The following conventions apply to annotations in the Magento Functional Testing Framework (MFTF):

- All annotations are within an `<annotations>` element.
- Each element within corresponds to a supported annotation type.
- There is no distinction made in XML between Codeception annotations and Allure annotations.
- Each annotation contains only one value.
If multiple annotation values are supported and required each value requires a separate annotation.
- Tests must contain all of the following annotations: stories, title, description, severity.

Recommended use cases of the annotation types:

- [stories] - report grouping, a set of tests that verify a story.
- [title] - description of the test purpose.
- [group] - general functionality grouping.
- [description] - description of how the test achieves the purpose defined in the title.
- [skip] - a label for the test to be skipped during generation (for example, an incomplete test blocked by an issue)

## Example

```xml
<annotations>
    <stories value="Category Creation"/>
    <title value="Create a Category via Admin"/>
    <description value="Test logs into admin backend and creates a category."/>
    <severity value="CRITICAL"/>
    <group value="category"/>
</annotations>
```

## Reference

### description

The `<description>` element is an implementation of a [`@Description`] Allure tag; Metadata for report.

Attribute|Type|Use
---|---|--
`value`|string|required

#### Example

```xml
<description value="Add Catalog via Admin"/>
```

### features

The `<features>` element is an implementation of a [`@Features`] Allure tag.

`<features>` sets a string that will be displayed as a feature within the Allure report. Tests under the same feature are grouped together in the report.

Attribute|Type|Use
---|---|--
`value`|string|required

#### Example

```xml
<features value="Catalog"/>
<features value="Add/Edit"/>
```

### group

The `<group>` element is an implementation of a [`@group`] Codeception tag.

`<group>` specifies a string to identify and collect tests together.
Any test can be a part of multiple groups.
The purpose of grouping is to create a set of test for a functionality or purpose, such as all cart tests or all slow tests and run them together locally.

<div class="bs-callout bs-callout-warning" markdown="1">
Group values cannot collide with [suite][] names.
</div>

<div class="bs-callout bs-callout-tip" markdown="1">
Add `<skip>` to the test to skip it during test run.
</div>

Attribute|Type|Use|Definition
---|---|---|---
`value`|string|required|A value that is used to group tests. It should be lower case.

#### Example

```xml
<group value="category"/>
```

### return

The `<return>` element is an implementation of a [`@return`] Codeception tag.
It specifies what is returned from a test execution.

Attribute|Type|Use
---|---|--
`value`|string|required

#### Example

```xml
<return value="void"/>
```

### severity

The `<severity>` element is an implementation of the [`@Severity`] Allure annotation, which is used to prioritise tests by severity.

Attribute|Type|Use|Acceptable values
---|---|---|---
`value`|string|required|`MINOR`, `AVERAGE`, `MAJOR`, `CRITICAL`, `BLOCKER`

#### Example

```xml
<severity value="CRITICAL"/>
```

#### Usage guidelines

Severity Level|Usage
---|---
`BLOCKER`|If this test fails, the customer is completely blocked from purchasing a product.
`CRITICAL`|This is a serious problem impacting conversion, or affecting the operation of the store.
`MAJOR`|Store conversion rate is reduced owing to this issue. For example, something is broken or missing that impacts checkout frequency or cart volume.
`AVERAGE`|A fault on the storefront that can negatively impact conversion rate (like UI errors or omissions), or problems with Magento admin functionality.
`MINOR`|An application or configuration fault that has no impact on conversion rate.

### skip

Use the `<skip>` element to skip a test.
It contains one or more child elements `<issueId>` to specify one or more issues that cause the test skipping.

#### issueId

This element under `<skip>` is required at least once and contains references to issues that cause the test to be skipped.

Attribute|Type|Use
---|---|--
`value`|string|required

#### Example

```xml
<skip>
    <issueId value="#117"/>
    <issueId value="MC-345"/>
</skip>
```

### stories

The `<stories>` element is an implementation of a [`@Stories`] Allure tag.
It has the same functionality as [features], within the Story report group.

Attribute|Type|Use
---|---|--
`value`|string|required

#### Example

```xml
<stories value="Add Catalog"/>
<stories value="Edit Catalog"/>
```

### testCaseId

The `<testCaseId>` element is an implementation of a [`@TestCaseId`] Allure tag.
It specifies a ZephyrId for a test.

This tag is prefixed to a title of the test annotation to make the test title unique in Allure.

If the linkage is set up correctly in the Allure config, the test will have a hyperlink to the Zephyr test case in the report.

Learn more about [setup instructions in Allure].

Attribute|Type|Use
---|---|--
`value`|string|required

#### Example

```xml
<testCaseId value="#"/>
```

### title

The `<title>` element is an implementation of [`@Title`] Allure tag; Metadata for report.

Attribute|Type|Use
---|---|--
`value`|string|required

#### Example

```xml
<title value="Add Catalog"/>
```

### useCaseId

The `<useCaseId>` element is an implementation of a `@UseCaseId` custom tag. It specifies the use case ID for a test and is ignored by Allure configuration at the moment, as Allure implementation is not complete.

Attribute|Type|Use
---|---|--
`value`|string|required

#### Example

```xml
<useCaseId value="USECASE-1"/>
```

<!-- Link definitions -->

[`@Description`]: https://github.com/allure-framework/allure-phpunit#extended-test-class-or-test-method-description
[`@Features`]: https://github.com/allure-framework/allure-phpunit#map-test-classes-and-test-methods-to-features-and-stories
[`@group`]: https://codeception.com/docs/07-AdvancedUsage#Groups
[`@return`]: https://codeception.com/docs/07-AdvancedUsage#Examples
[`@Severity`]: https://github.com/allure-framework/allure-phpunit#set-test-severity
[`@Stories`]: https://github.com/allure-framework/allure-phpunit#map-test-classes-and-test-methods-to-features-and-stories
[`@TestCaseId`]: https://github.com/allure-framework/allure1/wiki/Test-Case-ID
[`@Title`]: https://github.com/allure-framework/allure-phpunit#human-readable-test-class-or-test-method-title
[description]: #description
[features]: #features
[group]: #group
[setup instructions in Allure]: https://github.com/allure-framework/allure1/wiki/Test-Case-ID
[severity]: #severity
[stories]: #stories
[suite]: ../suite.md
[tests]: ../test.md
[title]: #title
[skip]: #skip
