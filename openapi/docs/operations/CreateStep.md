This operation supports idempotency for safely retrying requests without accidentally performing the same operation twice. This is useful when an API call is disrupted in transit and you do not receive a response. For example, if a request to create a step does not respond due to a network connection error, you can retry the request with the same idempotency key to guarantee that no more than one step is created.

To perform an idempotent request, provide an additional IdempotencyKey header to the request options.
