# CAP Theorem

## Introduction

The CAP theorem explains how distributed databases behave when there is a network problem. A distributed database uses multiple servers to store and share information. If the connection between servers breaks, they may not have the same updated data.

## CAP Properties

- **Consistency:** A request receives the latest completed update or an error.
- **Availability:** Every request to a working server receives a successful response.
- **Partition Tolerance:** The system continues operating even when servers cannot communicate.

## Example

Imagine a movie booking application with two servers. Only one seat is available. If the connection breaks after one server sells the seat, the other server may not know about the booking.

- **CP (Consistency + Partition Tolerance):** The second server may reject new bookings to avoid selling the same seat twice.
- **AP (Availability + Partition Tolerance):** The second server keeps accepting requests but may temporarily use outdated seat information.

## Conclusion

The CAP theorem helps developers choose between consistency and availability during network failures. The best choice depends on the application.

## References

- [IBM - What Is the CAP Theorem?](https://www.ibm.com/think/topics/cap-theorem)
- [AWS - CAP Theorem](https://docs.aws.amazon.com/whitepapers/latest/availability-and-beyond-improving-resilience/cap-theorem.html)
