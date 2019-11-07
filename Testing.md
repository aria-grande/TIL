# FIT - Fault Injection Testing
FIT is a software testing method that breaking the system and occurs errors on purpose to ensure that it can withstand and recover from the error conditions.

## Goal
- To ensure it can withstand and recover from error conditions
- To uncover any potential faults that may have been introduced in production

## How to test
### Compile time injection
- Simulates faults by modifying the source code

### Run time injection
- Use a software trigger to initiate injecting a fault to software while it's running
(e.g. interrupt software at specific lines of code)

## Ref
- [What is FIT](https://searchsoftwarequality.techtarget.com/definition/fault-injection-testing)
- [FIT by Netflix](https://medium.com/netflix-techblog/fit-failure-injection-testing-35d8e2a9bb2)
