###Best Practices for Scientific Computing
https://arxiv.org/abs/1210.0530


- Write programs for people, not computers.
  - A program should not require its readers to hold more than a handful of facts in memory at once
  - Names should be consistent, distinctive and meaningful
  - Code style and formatting should be consistent
  - All aspects of software development should be broken down into tasks roughly an hour long
- Automate repetitive tasks.
  - Rely on the computer to repeat tasks
  - Save recent commands in a file for re-use
  - Use a build tool to automate scientific workflows
- Use the computer to record history.
  - Software tools should be  used to track computational work automatically
- Make incremental changes.
  - Work in small steps with frequent feedback and course correction
- Use version control.
  - Use a version control system
  - Everything that has been created manually should be put in version control
- Don’t repeat yourself (or others).
  - Every piece of data must have a single authoritative representation in the system
  - Code should be modularized rather than copied and pasted
  - Re-use code instead of rewriting it
- Plan for mistakes.
  - Add assertions to programs to check their operation
  - Use an off-the-shelf unit testing library
  - Use all available oracles when testing programs
  - Turn bugs into test cases
  - Use a symbolic debugger
- Optimize software only after it works correctly.
  - Use a profiler to identify bottlenecks
  - Write code in the highest-level language possible
- Document design and purpose, not mechanics.
  - Document interfaces and reasons, not implementations
  - Refactor code instead of explaining how it works
  - Embed the documentation for a piece of software in that software
- Collaborate.
  - Use pre-merge code reviews
  - Use pair programming when bringing someone new up to speed and when tackling particularly tricky problems

More
- Maintain and update older code.


###Good Enough Practices in Scientific Computing
https://arxiv.org/abs/1609.00037

- Data Management
  - Save the raw data.
  - Create the data you wish to see in the world.
  - Create analysis-friendly data.
  - Record all the steps used to process data.
  - Anticipate the need to use multiple tables.
  - Submit data to a reputable DOI-issuing repository so that others can access and cite it.
- Software
  - Place a brief explanatory comment at the start of every program.
  - Decompose programs into functions.
  - Be ruthless about eliminating duplication.
  - Always search for well-maintained software libraries that do what you need.
  - Test libraries before relying on them.
  - Give functions and variables meaningful names.
  - Make dependencies and requirements explicit.
  - Do not comment and uncomment sections of code to control a program's behavior.
  - Provide a simple example or test data set.
  - Submit code to a reputable DOI-issuing repository.
- Collaboration
  - Create an overview of your project.
  - Create a shared public "to-do" list.
  - Make the license explicit.
  - Make the project citable.
- Project Organization
  - Put each project in its own directory, which is named after the project.
  - Put text documents associated with the project in the doc directory.
  - Put raw data and metadata in a data directory, and files generated during cleanup and analysis in a results directory.
  - Put project source code in the src directory.
  - Put external scripts, or compiled programs in the bin directory.
  - Name all files to reflect their content or function.
- Keeping Track of Changes
  - Back up (almost) everything created by a human being as soon as it is created.
  - Keep changes small.
  - Share changes frequently.
  - Create, maintain, and use a checklist for saving and sharing changes to the project.
  - Store each project in a folder that is mirrored off the researcher's working machine.
  - Add a file called CHANGELOG.txt to the project's docs subfolder.
  - Copy the entire project whenever a significant change has been made.
- Manuscripts
  - Write manuscripts using online tools with rich formatting, change tracking, and reference management.
  - Include a PUBLICATIONS file in the project's doc directory.
  - Write the manuscript in a plain text format that permits version control.
  - Include tools needed to compile manuscripts in the project folder.