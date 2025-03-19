
## 🎓 Context
During this milestone, we were asked to:

- Implement **Spring Data JPA**, removing all our DAO implementations
- Implement our own pagination / filtering system (**PageSearch** implementing **Pageable**)
	- Handling **offset**, **limit**, **sorting** and **search**
	- **Auto-fetch eager entities** in a single request
	- Handle **lazy entities** with **@EntityGraph**
	- Create a custom **Page** response to avoid issuing a count request during pagination
- Create a general **SearchSpecification** class to generate specifications from the user's search input
	- Handling several **operators** (eq, neq, gt, lt, null, like, in, etc.)
	- Handling **nested attributes**
	- Handling research on **Enums**
- Create a **@PageSearchDefault** annotation to automatically inflate the **PageSearch** parameter in the controllers

## 🤔 Difficulties
I haven't encountered notable difficulties, though handling research on enums and creating the @PageSearchDefault was challenging.