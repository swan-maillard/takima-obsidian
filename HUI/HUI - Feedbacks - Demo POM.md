
# ⚙  Features
- List of feedbacks
- Create feedback
- Import feedbacks
- Validate feedbacks

---

# 🗣  KU feedbacks

### List of feedbacks
- The "validation alert" is not intuitive => We should rather use a button at the same level as "Create" and "Import" with the number of feedbacks in parenthesis
- Improve responsivity
	- ![[Pasted image 20250527173314.png]]

### Creation
- Have a page instead of modal for users which don't have the validation roles
	- Maybe have a page instead of modal all the time ?
- The "information" alert should be divided in two
	- Warning: Be polite, etc 
		- => Just above the input
		- => Again when we validate the creation "are you sure that the comment is constructive / polite / etc."
	- Advice: What you should ask yourself, etc.
		- => Write it instead of "Message" label
- Divide the "message" input to two inputs (positive and negative feedback)
	- ![[Pasted image 20250527172519.png]]
	- In validation, display the two separate fields
- Add front validation for creation form (selects)

### Validation
- When refusing a feedback that was modified, don't keep the modification
- Concurrency issues => How to avoid that ?
	-  When navigating to navigation, "assign" X feedbacks to the validator, and lock them for other validators?

### Roles
- Creation
	- LEAD, COMMERCIALS, STAFF

### Other needs
- Enable managers to see the feedbacks they wrote
- During validation step, a feedback can be transformed into highlight
- During EO, at the Synthesis step, being able to visualize the feedbacks of the consultant
- Auto-validating feedbacks