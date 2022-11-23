### Task:
Design a database schema for a **hiring tool with skills assessments**. 
It should satisfy the following user stories:

 - Each workspace has multiple job openings (Frontend Developer,
   Support Agent, Accountant,
 - Each job opening has multiple tests (multiple choice test, video introduction, homework assignment)
 - Each test has multiple versions (which are created when questions are added/edited/removed to save the exact test each candidate took)
 - Each test version has multiple questions with different types (single choice, free text, code input, video recording)
 - Each question can have multiple options (for choice questions)
 - Each candidate can take multiple tests in any number of job openings from any workspace (a candidate can apply to multiple positions in any company)
 
 - Each test the candidate takes has:
	 -  Timestamps when the test was started and when it was submitted
	 - Answers to each question (including selected options)
	 - Percentage score calculated based on the answers
	 - Any number of fraud events for each answer (these can be copy-pasting the question text, leaving the browser window, etc.)

### Features to support:
 - Find suspicious candidates for each job opening. A suspicious candidate meets at least one of these conditions:
	 - Their IP address is the same as at least one other candidate who applied to the job opening
	 - Their email address is similar (see below) as at least one other candidate in the job opening
	 - They have at least one fraud event for one of their answers
	 - They submitted the test in less than 3 minutes (difference between the start and submit timestamps)


 - Retrieve all candidates in a workspace (they have applied to at least one job opening in the workspace) with filtering and pagination
	 - Candidates can be filtered by:
	 - The job opening they applied to (identified by its ID)
" The minimum/maximum score they received in a specific test (e.g. show me candidates who had
at least 80% in test 53279)
	 - Pagination should be cursor-based (e.g. to get the next size, we specify the ID of the last record from the previous page and the page size)
Two email addresses are similar if they are equal after sanitisation:
	 - Lowercase the whole address
	 - Remove + suffixes (haris+hire@example.com -> haris@example.com)
	 - Remove dots from the user part (haris.botic@example.com -> harisbotic@example.com)

### Requirements:
1. Implement the schema in a PostgreSQL database.
2. Fill the database with a large number of records (e.g. 10 workspaces, 100 job openings with 2 tests each, 1000000 candidates)
3. Write SQL queries for the two features and try to optimise them as much as possible. If not possible, suggest other ways to implement these features efficiently. Both queries should always run under 1 second.