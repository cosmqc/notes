A design method intended to be a linear approach to software development.
Follows a "Measure twice, cut once" principle, and relies on clients not changing their requirements after initial planning.

![[Pasted image 20240605170633.png]]
### Stages
#### Requirements
- Gather all requirements upfront and understand them
	- Write the product design document
	- Includes costs, assumptions, dependencies, success metrics, and timelines
#### Design
- Design the *technical solution* to the problem set out by the requirements
- First a high-level logical design that describes purpose and scope of the project
- Next a low-level physical design using tools like UML, class diagrams
#### Implementation
- Actually write the designed code, and write unit tests to ensure code doesn't have any bugs / does what it was written to do
#### Verification / testing
- Go through the design docs, personas, and user scenarios to create acceptance test cases
- Acceptance testing
#### Deployment / maintenance
- As defects are found and new change requests come in, teams will be assigned to release new versions of the product

### Advantages
- Each contributor knows exactly what needs to be done
- Contributors can then plan their time effectively for the whole project
- Focus is put on comprehensive planning in the requirements/design stage
	- Developers can catch design errors early in development
	- Cost and time spent can be accurately estimated
- Developers who join the project in-progress can get caught up thanks to the design document.

### Disadvantages
- Projects can take longer to deliver compared to more iteration based strategies
- Clients aren't involved in design and implementation stages
- Clients don't often know exactly what they want at the start, leading to a bunch of changes and new features in the maintenance stage when they're a lot harder to accomodate.
- Deadline creep - one stage gets pushed back, they all get pushed back

