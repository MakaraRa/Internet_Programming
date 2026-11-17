# Week 05 – Explain It

### 1. Refreshing `/events/2`

During development, the Vite development server answers the browser request and serves the Vue application. In production, the web server must be configured to redirect unknown routes to `index.html` so Vue Router can handle the URL.

### 2. Route guard and event creation

Yes, a student could still try to create an event by sending a direct HTTP request to the backend API instead of using the website. The backend must check the user's role and reject requests from users who are not organisers. A frontend route guard alone is not enough to protect the data.

### 3. Using `watch` with `immediate: true`

Using only `onMounted` loads the event when the component is first created, but it does not automatically load another event when the route ID changes. Vue Router may reuse the same component when navigating between event details. Using `watch` with `immediate: true` handles both the initial load and later ID changes.

### 4. Using `storeToRefs(store)`

`storeToRefs(store)` keeps the extracted state and getters reactive. If we use `const { events } = store`, we lose the reactivity connection when destructuring the state. Therefore, `storeToRefs` allows the component to update automatically when the store changes.

### 5. POST booking followed by PATCH event

If the POST request succeeds but the PATCH request fails, the booking is saved while the event's booked seat count remains unchanged. This causes inconsistent data because the booking exists but the event does not reflect the reserved seats. The server can prevent this by using a database transaction so both operations succeed together or are rolled back together.