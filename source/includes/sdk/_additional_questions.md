# 9. Please answer some additional questions to customize your experience

One of the richest features of Occasion is that it enables merchants to add additional questions to each product they sell,
selecting from a wide range of:

### Categories

* Informational
* Price Changing
  * Add fixed value to price (`add`)
  * Add percentage to price (`multiply`)
  * Discount fixed value from price (`subtract`)
  * Discount percentage from price (`divide`)
  * Determine price based on permutation of multiple inputs (`permute`)
* View Components
* Special Fields

### Form Control Types

* Text input
* Text area
* Checkbox
* Drop down
* Radio buttons (known as Option List)
* Number input (known as Spin Button)
* Separator
* Text Output
* Waiver

The first two sections of this chapter will show how `Order.construct` assists in creating this section of the order form,
as well as some SDK helpers to provide your customer with instant price updates any time a `priceCalculating` question changes.

Each section thereafter will be dedicated to showing you how to display a specific form control type, for every possible category that
form control type can be (informational, price changing, view component, special). By learning how to display each form control type,
you will be able to successfully build the additional
questions section of the order widget.

## Create blank answer inputs for all the questions

```javascript
window.order.answers().target().map(function(answer) {
  console.log(answer.attributes()); // =>
  // {
  //   id: 'bg35ajhe',
  //   value: null
  // }
    
  console.log(answer.question().attributes()); // =>
  // {
  //   id: 'k127s2y',
  //   required: false,
  //   title: 'The first optional question',
  //   formControl: 'drop_down',
  //   priceCalculating: false,
  //   operation: null
  // }
  
  console.log(answer.question().options()); // =>
  // @see Drop Downs and Option Lists
});
```

`Order.construct` called in Chapter 4 initializes the order with blank `answers()` for each question in `window.product.questions()`.
You can iterate over every one of `order.answers()` and use each of their `question()`'s properties to display the answer input for the question on the order widget.

We've listed these properties in the example using `attributes()`.

The configuration of these properties will affect how you display each input and how you respond when the input changes.

### `answer.question().formControl`

The `formControl` attribute of each question will determine the type of input needed to be displayed in order to answer it.
Possible values are:

* `text_input`
* `text_area`
* `checkbox`
* `drop_down`
* `option_list`
* `spin_button`
* `separator`
* `text_output`
* `waiver`
* `attendee`

Individual sections of this chapter will show you how to map these values to HTML form inputs.

### `answer.question().title`

The `title` of each question should be used as a `<label></label>` for each answer input.

Depending on the form control, the question may have additional attributes that are useful or necessary when displaying a label and input. We'll cover these in each of the individual form control sections.

### `answer.question().required`

Answers with `question().required` equal to true must have a `value` or an `option()` specified.
Make sure to set the `required` attribute of the HTML input to this value for easier validation.

### `answer.question().position`

The order that questions should be displayed in is indicated by their `position`, from `1` to `n`.

### `answer.question().priceCalculating`

If `priceCalculating` equals `true`, you should add a callback so that any time the input changes, the price of the order displayed to the customer updates. The next section
will cover this functionality.

### `answer.question().operation`

Additionally, if the question is `priceCalculating`, it will also have an `operation` equal to one of the following:
`add`, `subtract`, `multiply`, `divide`, and `permute`. The value of `operation` will affect the attributes associated with a question and
how the customer will understand the question.

### `answer.question().options()`

If a question has `formControl` equal to `drop_down` or `option_list`, it will also have `options().target()` loaded with options
for the customer to choose from.

See the section on Drop Downs and Option Lists for more details.

### `answer.option()` or `answer.value`

In general, you will bind `answer.value` to the value of the input displayed for each question.
Drop downs and option lists will set `answer.option()` equal to one of their options.

## Calculating and updating the order's price

```javascript
window.afterPriceCalculatingItemChange = function() {
  // called after the answer on `window.order` has already
  // been updated to reflect the new option or value specified
  // in the DOM
  
  window.order.calculatePrice()
  .then(function(order) {
    // @todo Implement Chapter 12
  });
};
```

Every time the answer to a `priceCalculating` question changes, you must update the price displayed on the order widget
so the customer can see real-time how their choices affect the order's price.

After change event has been processed and the answer itself has been changed on `window.order`, you can call `window.order.calculatePrice()`, which will automatically
update `window.order` to have various pricing attributes useful to the customer.

The implementation of this method is completed in Chapter 12, we're showing it here so you can hook up this callback
as you follow along with building views for the different form control types.

## Text Inputs and Text Areas

```javascript
window.order.answers().target().map(function(answer) {
  console.log(answer.question().attributes()); // =>
  // {
  //   id: 'k127s2y',
  //   required: true,
  //   title: 'What is your favorite color?',
  //   formControl: 'text_input'
  // }
  //
  // *or*
  //
  // {
  //   id: '6gdt3aw',
  //   required: true,
  //   title: 'What is your favorite color? Elaborate.',
  //   formControl: 'text_area'
  // }
});
```

Text inputs and text areas are the simplest form control types.

A `text_input` corresponds to an `<input type='text'></input>`.

A `text_area` corresponds to a `<textarea></textarea>`.

```javascript
// Assign new value on input change
window.onInputChanged = function(e) {
  answer.value = e.target.value;
};
```

The second example in this section shows a basic version of an onChange callback for any answer input without `options()`. Any time the input changes,
read the value of the input and assign it to `answer.value`.

> This is the way answers are completed for every form control type except
those with `options()` (drop downs and option lists). This guide assumes you will use this snippet when answering
such form controls.

## Checkboxes

```javascript
window.order.answers().target().map(function(answer) {
  console.log(answer.question().attributes()); // =>
  // {
  //   id: 'mjyw4t5',
  //   must_be_checked: false,
  //   title: 'Would you like to enable this free feature?',
  //   formControl: 'checkbox',
  //   priceCalculating: false
  // }
  //
  // *or*
  //
  // {
  //   id: 'mjyw4t5',
  //   must_be_checked: false,
  //   title: 'Would you like to add this specific item?',
  //   formControl: 'checkbox',
  //   priceCalculating: true,
  //   operation: 'add',
  //   price: '5.0'
  // }
  //
  // *or*
  //
  // {
  //   id: 'mjyw4t5',
  //   must_be_checked: false,
  //   title: 'Would you like to a fixed discount based on this?',
  //   formControl: 'checkbox',
  //   priceCalculating: true,
  //   operation: 'subtract',
  //   price: '5.0'
  // }
  //
  // *or*
  //
  // {
  //   id: 'mjyw4t5',
  //   must_be_checked: false,
  //   title: 'Want a premium upgrade?',
  //   formControl: 'checkbox',
  //   priceCalculating: true,
  //   operation: 'multiply',
  //   percentage: '25.0'
  // }
  //
  // *or*
  //
  // {
  //   id: 'mjyw4t5',
  //   must_be_checked: false,
  //   title: 'Are you a student?',
  //   formControl: 'checkbox',
  //   priceCalculating: true,
  //   operation: 'divide',
  //   percentage: '10.0'
  // }
  //
  // *or*
  //
  // {
  //   id: 'mjyw4t5',
  //   must_be_checked: false,
  //   title: 'Combine this with other package deals',
  //   formControl: 'checkbox',
  //   priceCalculating: true,
  //   operation: 'permute',
  //   price: null
  // }
});
```

Checkboxes can collect information or change the price of the order. The example shows the types of checkbox questions
you can expect to see on a product.

If the checkbox is checked, set `answer.value` equal to `true`. Otherwise, set it equal to `false`.

First, note that all of them use `must_be_checked` rather `required` to indicate if they must be checked.
This goes along with HTML5, which allows all inputs except `[type=checkbox]` to use the `required` attribute to validate
presence of a value. Use `answer.value` to validate on your own that any checkbox that `must_be_checked` is in fact so.

The first object in the example is an informational checkbox question, `priceCalculating` is false.

The rest of them are price changing questions, and each of them has a price `operation` as well as an extra property regarding
its impact on price.

Operation | Property | Description
--------- | -------- | -----------
**`add`** | **`price`** | The checkbox will add a fixed value `price` to the order total if checked.
**`subtract`** | **`price`** | The checkbox will *subtract* a fixed value `price` from the order total if checked.
**`multiply`** | **`percentage`** | The checkbox will add a `percentage` markup to the order total if checked.
**`divide`** | **`percentage`** | The checkbox will *subtract* a `percentage` discount from the order total if checked.
**`permute`** | N/A | The specific value of this checkbox combined with the specific value of other questions will determine the price change, based on what is set by the merchant. As such, these will not have a `price` or `percentage` attribute. *This calculation is done for you in the SDK, so think of these as price changing questions with no price or percentage needed for display.*

> Remember to bind the change event for `priceCalculating` checkbox inputs to update the order price using `afterPriceCalculatingItemChange`.
See section 2 of this chapter. 

Merchants usually do not put the `price` or `percentage` that applies to any individual question in its `title`, so you should use `operation` and
these attributes to modify the label of the question accordingly.

For example, if the question had `operation == 'divide'`, an appropriate modification might be: `<label>[TITLE] ([PERCENTAGE]% off)</label>`

## Drop Downs and Option Lists

```javascript
window.order.answers().target().map(function(answer) {
  console.log(answer.question().attributes()); // =>
  // {
  //   id: 'j1ng3s4',
  //   required: true,
  //   title: 'Which of these items is your favorite?',
  //   formControl: 'drop_down',
  //   priceCalculating: false,
  //   operation: null
  // }
  //
  // *or*
  //
  // {
  //   id: 'bsg36hy',
  //   required: true,
  //   title: 'Pick one of the following items',
  //   formControl: 'option_list',
  //   priceCalculating: true,
  //   operation: 'add'
  // }
  //
  // *or*
  //
  // {
  //   id: 'j1ng3s4',
  //   required: true,
  //   title: 'Pick one of the following items',
  //   formControl: 'drop_down',
  //   priceCalculating: true,
  //   operation: 'permute'
  // }
  
  console.log(answer.question().options().target().toArray()); // =>
  // [
  //   {
  //     id: 'j47ash',
  //     title: 'The first option.',
  //     position: 0,
  //     default: false,
  //     price: null
  //   }, {
  //     id: 'bt5a9yt',
  //     title: 'The second option.',
  //     position: 1,
  //     default: true,
  //     price: null
  //   }
  // ]
  //
  // *or*
  //
  // [
  //   {
  //     id: 'j47ash',
  //     title: 'The first option.',
  //     position: 0,
  //     default: false,
  //     price: '5.0'
  //   }, {
  //     id: 'bt5a9yt',
  //     title: 'The second option.',
  //     position: 1,
  //     default: true,
  //     price: '20.0'
  //   }
  // ]
});
```

Drop downs and option lists are the two types of questions that have `options()`. 

A drop down corresponds to a `<select></select>` tag with an `<option></option>` for each option in `question().options()`.

An option list corresponds to a group of `<input type='radio'></input>`s for each option in `question().options()`.

For each option:

* `title` is the label that would displayed for any option.
* `position` determines the order the `options()` are displayed in
* `default` *may* be true for *one* of the `options()` - that option should be selected by default.

If the question is `priceCalculating`, then the drop down or option list will perform one of two operations:

Operation | Property | Description
--------- | -------- | -----------
**`add`** | **`price`** | Each option will add a fixed value `option.price` to the order total if checked.
**`permute`** | N/A | The specific value of each option combined with the specific value of other questions will determine the price change, based on what is set by the merchant. As such, no options will have a `price` attribute.

Merchants usually do not put the `price` that applies to any individual option in its `title`, so you should add this to each option's label so
customers know the price of each option.

```javascript
// Directly assign answer.option
answer.assignOption(answer.question().options().target().first());
```

```javascript
// Find option by ID then assign answer.option
let selectedOptionId = 'yt5mfkg';

let selectedOption = answer.questions.options()
                     .target().detect(function(o) {
                       return o.id == selectedOptionId;
                     });

answer.assignOption(selectedOption);
```

<br/>
The second and third examples in this section show:

Once an option has been selected, you can set the `answer.option()` to the selected option using `assignOption(option)`.

If you only know the ID of the option the customer selected, you can find the option itself amongst `answer.question().options()`
using `detect(predicate)`, which takes in a function that iterates over every option and returns the first option
where the function returns true.

In this case, we check to see if the option's ID is equal to the `selectedOptionId`.

> Remember to bind the change event for `priceCalculating` drop down and option list inputs to update the order price using `afterPriceCalculatingItemChange`.
See section 2 of this chapter.

## Spin Buttons

```javascript
window.order.answers().target().map(function(answer) {
  console.log(answer.question().attributes()); // =>
  // {
  //   id: 'j1ng3s4',
  //   required: true,
  //   title: 'How many free items do you want?',
  //   formControl: 'spin_button',
  //   priceCalculating: false,
  //   operation: null,
  //   max: 10,
  //   exclude_zero: false
  // }
  //
  // *or*
  //
  // {
  //   id: 'bsg36hy',
  //   required: true,
  //   title: 'How many priced items do you want?',
  //   formControl: 'spin_button',
  //   priceCalculating: true,
  //   operation: 'add',
  //   max: 5,
  //   exclude_zero: false,
  //   price: '10.0'
  // }
  //
  // *or*
  //
  // {
  //   id: 'bsg36hy',
  //   required: true,
  //   title: 'Do you want more than one of this order?',
  //   formControl: 'spin_button',
  //   priceCalculating: true,
  //   operation: 'multiply',
  //   max: 5,
  //   exclude_zero: false
  // }
});
```

Spin buttons count incrementally up or down.

A spin button corresponds to an `<input type='number'></input>` tag.

Attributes specific to this form control type:

* `max` indicates the max value for the spin button, and can be set on the HTML as the `max` attribute too.
* `exclude_zero` indicates whether the spin button's HTML `min` attribute is `0` or `1`.

If the question is `priceCalculating`, then the spin button will perform one of two operations:

Operation | Property | Description
--------- | -------- | -----------
**`add`** | **`price`** | Each time the spin button is incremented, the fixed value `price` will be added to the order total.
**`multiply`** | N/A | The order total is multiplied by the value of the spin button.

Merchants usually do not put the `price` that applies to any individual increment of the spin button, so you should add this to the
label so customers know the price of each increment.

> Remember to bind the change event for `priceCalculating` spin button inputs to update the order price using `afterPriceCalculatingItemChange`.
See section 2 of this chapter.

## View Components

```javascript
window.order.answers().target().map(function(answer) {
  console.log(answer.question().attributes()); // =>
  // {
  //   id: 'j1ng3s4',
  //   title: '',
  //   formControl: 'separator',
  //   priceCalculating: false
  // }
  //
  // *or*
  //
  // {
  //   id: 'j1ng3s4',
  //   title: 'This is some text to display for the customer.',
  //   formControl: 'text_output',
  //   displayAsTitle: true,
  //   priceCalculating: false
  // }
});
```

Some questions in Occasion are not questions at all
<img src='https://assets-cdn.github.com/images/icons/emoji/unicode/1f61b.png?v5' width='25px' style='margin-bottom: -5px;' />

Instead, some are just helpful view components like separators and titles that make the widget more helpful and aesthetic.

There are two view component form control types right now: `separator`, and `text_output`.

`separator` corresponds to an `<hr/>` tag. That's about it.

`text_output` corresponds to a `<p></p>` tag with `title` as the content. However, if `question().displayAsTitle` is true,
switch to a `<h3></h3>` or similar.

## Special Fields

```javascript
window.order.answers().target().map(function(answer) {
  console.log(answer.question().attributes()); // =>
  // {
  //   id: 'j1ng3s4',
  //   title: 'Do you accept the terms and conditions?',
  //   formControl: 'waiver',
  //   priceCalculating: false,
  //   waiverText: 'By agreeing to these terms, you accept that ...'
  // }
});
```

### Waiver Fields

The first special field form control type is the Waiver Field, which is an upgraded checkbox that allows for an additional `waiverText`
attribute on top of the standard `title`. These fields will not have a `must_be_checked` attribute, **but waiver fields must always be checked for successful purchase.**

### Attendees Fields

Coming soon...