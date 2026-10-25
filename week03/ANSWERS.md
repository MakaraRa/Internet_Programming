# Week 03 Answers

**1. In EventList, what goes wrong if you use the array index as `:key` and the list gets filtered while a card has local state (for example an open details panel)?**

If we use the array index as the key, Vue may reuse the wrong component when the list is filtered. For example, an open details panel might appear on a different event.

**2. Why is `visible` a computed and not a function called from the template? What is the difference when you type in the search box?**

`visible` is computed because it updates automatically when the search text or category changes. It also caches the result and only recalculates when its dependencies change, while a function called in the template may run again during each render.

**3. EventCard emits `book` instead of changing `event.booked`. Give two reasons.**

First, `EventCard` should not directly change the data it receives through props. Second, the parent component manages the booking data, so it can update the event and booking count in one place.

**4. You write `const { booked } = reactive(event); booked++`. The page does not change. Why?**

Destructuring `booked` creates a separate local variable, so it loses the reactive connection to `event.booked`. Changing `booked` does not update the original event property.

**5. Where does `myBookings` live, and why not in EventCard or EventList?**

`myBookings` lives in `App.vue` because it manages the bookings for the whole application. It should not live in `EventCard` or `EventList` because those components mainly display and filter events, while the parent needs to track the total bookings and save them in localStorage.