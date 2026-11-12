# ACID Properties in Databases

## Introduction

ACID stands for Atomicity, Consistency, Isolation and Durability. These four properties help a database handle important operations safely. They are especially useful when several changes must work together, such as transferring money between bank accounts.

## ACID Properties

- **Atomicity:** Either all steps of an operation are completed or none of them are saved.
- **Consistency:** The database follows its rules and keeps the data valid.
- **Isolation:** Transactions happening at the same time are controlled so they do not cause incorrect results.
- **Durability:** Once a transaction is committed, its changes stay saved even if the system crashes.

## Example

Imagine transferring ₹500 from Account A to Account B. The money must be deducted from A and added to B. If the second step fails, the first step should also be cancelled. This is an example of atomicity. The database must also follow rules such as preventing a negative balance.

## Conclusion

ACID properties make databases more reliable. They help protect data when operations fail, multiple users work at once or a system unexpectedly shuts down.

## References

- [IBM - ACID Properties of Transactions](https://www.ibm.com/docs/en/cics-tx/11.1.0?topic=processing-acid-properties-transactions)
- [MongoDB - What Is ACID Compliance?](https://www.mongodb.com/resources/products/capabilities/acid-compliance)
- [PostgreSQL - Glossary](https://www.postgresql.org/docs/current/glossary.html)
