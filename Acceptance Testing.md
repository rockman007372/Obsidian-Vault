>[!definition]
> _Acceptance testing_ (aka _User Acceptance Testing (UAT)_: test the system to ensure it meets the user requirements.

Acceptance tests **give an assurance to the customer that the system does what it is intended to do.** Acceptance test cases are often defined at the beginning of the project, usually based on the use case specification. Successful completion of UAT is often a prerequisite to the project sign-off.

## Acceptance vs Sytem Testing

Acceptance testing comes **after** [[System Testing]]. 

Similarity: involves testing the whole system.

Differences:

| System Testing                                    | Acceptance Testing                                      |
| ------------------------------------------------- | ------------------------------------------------------- |
| Done against the system specification             | Done against the requirements specification             |
| Done by testers of the project team               | Done by a team that represents the customer             |
| Done on the development environment or a test bed | Done on the deployment side or a close simulation of it |
| Both positive and negative test cases             | More focus on the positive test cases                   | 

> [!note]
> Differences between System specifications and Requirement specifications:
> - System includes how system will fail and recover, while requirement is limited to how it behaves in normal working condition
> - Sytem shows how the problem is solved while requirement only shows the problem
> - Sytem may contain aditional APIs not available to end-users while requirement only has the final system API


While acceptance testing comes **after** [[System Testing]], passing system tests does **not** necessarily mean passing acceptance testing. Examples:
- The system might work on the testbed environments but might not work the same way in the deployment environment.
- The system might conform to the system specification but could fail to solve the problem it was supposed to solve for the user (flaw in system design)

