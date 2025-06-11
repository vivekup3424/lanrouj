A fixed window counter rate limiter is a type of rate limiting algorithm used to manage and throttle the incoming requests or events to a system. The key idea behind this approach is to maintain a fixed-size time window and count the number of requests that occur within that window.

Here's how it works:

1. Define a fixed time window size (e.g., 1 minute, 1 second, etc.).
2. Maintain a counter that tracks the number of requests made within the current time window.
3. When a new request arrives, check if the current counter value is less than the configured request limit.
   - If the counter is less than the limit, increment the counter and allow the request.
   - If the counter is equal to or greater than the limit, reject the request.
4. When the time window expires, reset the counter to zero and start a new time window.

Here's a simple Python implementation of a fixed window counter rate limiter:

```python
from datetime import datetime, timedelta

class FixedWindowRateLimiter:
    def __init__(self, window_size, max_requests):
        self.window_size = window_size
        self.max_requests = max_requests
        self.request_counts = {}

    def is_allowed(self, key):
        now = datetime.now()
        window_start = now - timedelta(seconds=self.window_size)

        if key not in self.request_counts:
            self.request_counts[key] = []

        # Remove expired requests from the list
        self.request_counts[key] = [req for req in self.request_counts[key] if req >= window_start]

        # Check if the current request is allowed
        if len(self.request_counts[key]) < self.max_requests:
            self.request_counts[key].append(now)
            return True
        else:
            return False
```

In this implementation, the `FixedWindowRateLimiter` class takes two parameters:
- `window_size`: The duration of the fixed time window in seconds
- `max_requests`: The maximum number of requests allowed within the time window

The `is_allowed` method checks if a new request should be allowed for a given `key` (e.g., a user ID, an API key, etc.):

1. It first calculates the start of the current time window by subtracting the `window_size` from the current time.
2. It then retrieves the list of request timestamps for the given `key`. If the list doesn't exist, it creates a new one.
3. It removes any expired requests (i.e., requests that occurred before the current time window) from the list.
4. Finally, it checks if the length of the remaining request list is less than the `max_requests` limit. If so, it adds the current timestamp to the list and returns `True`, indicating that the request is allowed. Otherwise, it returns `False`, rejecting the request.

This implementation allows you to easily integrate the fixed window counter rate limiter into your application to control the rate of incoming requests.

The sliding window counter rate limiter is another type of rate limiting algorithm that aims to provide more precise control over the rate of incoming requests or events. Unlike the fixed window counter approach, the sliding window counter keeps track of requests over a continuously sliding time window.

Here's how it works:

1. Define a time window size (e.g., 1 minute) and a maximum number of requests allowed within that window.
2. Maintain a circular buffer (e.g., a list or deque) to store the timestamps of the last `N` requests, where `N` is the maximum allowed requests.
3. When a new request arrives:
   - Check the oldest timestamp in the buffer. If the time elapsed since that timestamp is greater than the time window size, remove it from the buffer.
   - If the buffer size is less than the maximum allowed requests, add the current timestamp to the buffer and allow the request.
   - If the buffer size is equal to the maximum allowed requests, reject the request.

Here's a Python implementation of a sliding window counter rate limiter:

```python
from collections import deque
from datetime import datetime, timedelta

class SlidingWindowRateLimiter:
    def __init__(self, window_size, max_requests):
        self.window_size = window_size
        self.max_requests = max_requests
        self.request_timestamps = deque()

    def is_allowed(self, key):
        now = datetime.now()
        window_start = now - timedelta(seconds=self.window_size)

        # Remove expired requests from the deque
        while self.request_timestamps and self.request_timestamps[0] < window_start:
            self.request_timestamps.popleft()

        # Check if the current request is allowed
        if len(self.request_timestamps) < self.max_requests:
            self.request_timestamps.append(now)
            return True
        else:
            return False
```

In this implementation, we use a deque (double-ended queue) to store the timestamps of the last `N` requests, where `N` is the `max_requests` limit.

The `is_allowed` method first calculates the start of the current time window by subtracting the `window_size` from the current time. It then removes any expired requests (i.e., requests that occurred before the current time window) from the deque.

Finally, it checks if the length of the remaining request timestamps is less than the `max_requests` limit. If so, it adds the current timestamp to the deque and returns `True`, indicating that the request is allowed. Otherwise, it returns `False`, rejecting the request.

The key advantages of the sliding window counter approach are:

1. **More Precise Rate Limiting**: By continuously sliding the time window, the sliding window counter can more accurately track the rate of incoming requests and provide finer-grained control over the rate limit.
2. **Better Handling of Bursts**: The sliding window approach is more resilient to sudden bursts of requests, as it only considers the most recent `N` requests rather than all requests within a fixed time window.
3. **Easier to Implement**: The sliding window counter is generally simpler to implement than more complex rate limiting algorithms, such as the token bucket or leaky bucket approaches.

Overall, the sliding window counter rate limiter is a versatile and efficient algorithm for managing the rate of incoming requests or events in your system.5



## Token Bucket Algorithm
```c++
#include <iostream>
#include <chrono>
```
