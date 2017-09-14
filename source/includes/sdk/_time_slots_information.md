# 8. What time slot(s) do you want to book?

## Displaying pages of bookable time slots

```javascript
window.product.timeSlots().where({ status: 'bookable' }).perPage(10).all()
  .then(function(timeSlotsPage) {
    
    // do something with mapped version of time slots page
    timeSlotsPage.map(function(timeSlot) {
      console.log(timeSlot.attributes()) // =>
      // {
      //   duration: 7200, // seconds
      //   spotsAvailable: 5,
      //   startsAt: '2015-10-24T11:00:44.539-05:00'
      // }
    });
    
    if(timeSlotsPage.hasNextPage()) {
      timeSlotsPage.nextPage()
      .then(function(nextTimeSlotsPage) {
        // do something with next page of 10 time slots
      });
    }
  })
```

The standard product in Occasion enables a customer to select a single time slot to book an order for. To allow a customer to book one, you should show them lists of time slots to choose from.

Product time slots are loaded in pages, and you can specify the page size when you load the first page using `product.timeSlots().first(n)`. Every page thereafter can be loaded using `nextPage()`.

## Products choose how to display individual time slots

```javascript
timeSlotsPage.map(function(timeSlot) {
  // Always display startsAt
  console.log(timeSlot.startsAt);
  
  // Only display spotsAvailable if product.showOccurrenceAvailability
  if(window.product.showOccurrenceAvailability) {
    console.log(timeSlot.spotsAvailable);
  }
  
  // Only display duration if product.showTimeSlotDuration
  if(window.product.showTimeSlotDuration) {
    console.log(timeSlot.duration);
  }
});
```

Each product has a specific way of displaying individual time slots, based on two properties: `showOccurrenceAvailability` and `showTimeSlotDuration`.
The example demonstrates how these two properties affect output.

> Note that `timeSlot.duration` is in seconds, and should be converted to a more meaningful time metric for the customer before display.

## Managing selected time slots

```javascript
// Add selected time slot
window.order.timeSlots().target().push(selectedTimeSlot);

// Remove selected time slot
window.order.timeSlots().target().delete(selectedTimeSlot);

// Clear selected time slots
window.order.timeSlots().target().clear();
```

`order.timeSlots()` is a collection relationship, but for now, orders require that only a single time slot be selected. *Future releases will allow the ability to select multiple timeSlots.*

The example shows some basic ways to manipulate selected time slots.

## Sessions

Coming soon...