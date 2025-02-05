# Lecture 5 - Writing Computer Programmes

- Speaker: Dr. Abhishek Dutta - Senior Research Software Engineer - Visual Geometry Group, Department of Engineering Science

Programming is a continuous process that includes *DETECTING THE PROBLEM*, *PRODUCING A MENTAL MODEL OF COMPUTATION*, *TRANSLATING AND REPRESENTING THE MENTAL MODEL INTO THE CODE* and *ITERATIVELY REFINING THE STRUCTURE*. Through this process, what is the most important in code writing is *MAKING THE CODE WORK AND GIVING THE CORRECT OUTPUT*.

However, for most of the time, programming is a team work, which means your code needs to be read by others. In that case, *MAKING THE CODE READABLE* is as important as making it work. In detail, good code allows others to faithfully reproduce the mental model of computation and by contrast, bad code makes others unable to reproduce the model.

## Naming Identifies

> ```java
> static inline int count_leading_zeros(unsigned long x)
> {
>     if (sizeof(x) == 4)
>         return BITS_PER_LONG - fls(x);
>     else
>         return BITS_PER_LONG - fls64(x);
> }
> ```
>
> - `count_leading_zeros`: function name
> - `x`: variable name
> - `BITS_PER_LONG`: numerical constant name

Identifier names can also be seen as a **post-it-note** attached to different parts of a program code.

How to choose an identifier name?

- **Use common knowledge and analogies** to reduce the need for extensive documentation

> `walkdir()`: relies on the concepts of walking and directories (or folders) containing multiple items.
>
> `split_dataset()`: relies on the concept of splitting a collection of things into two or more groups.

- If multiple choices exist between different identifier names, choose the one that can be explained to a 5-year-old.
- A **well chosen identifier name** helps you avoid the need to comment your code.

How do you know which concepts are widely understood?

- Engaging with code and documentation written by others helps you break free from the constraints of
  - *The here*: the era in which you were born
  - *The now*: your field or expertise (e.g. engineering)
- Exposure to ideas in **other disciplines** or **your sub-discipline** (i.e., remote in space) also helps you escape the captivity of personal viewpoints and allows you to survey a wider horizon of ideas.
  - For an engineer, other discipline means Humanities, Biology, Anthropology, Art, etc.
  - For an engineer with expertise in AI, your sub-discipline means operating system, database software, communication tools, etc.
- Engaging with historical software (i.e., remote in time) and documentation also brings clarity about concepts that have stood the test of time.

To choose a good identifier name, you need to break free from the "tyranny of the here and the now" by surveying ideas, code, and documentation that are:

- **remote in time** (e.g., historical releases)
- **remote in space** (i.e., beyond your field of expertise)

Some tips from *Linux Kernel* developers include:

- Use proper descriptive names that are **short** and **to the point**.
    > Prefer `cout_active_users()` over `cntusr()`
    > `i`: for loop counter
    > `tmp`: for a variable that holds a temporary value
- *Functions should be short and sweet, and do just one thing.*
  - They should fit on one or two screenfuls of text, and do one thing and do that well.
  - The number of local variables should not exceed 5 to 10.

Some tips from developers at *Google*:

- Spend time considering names—it's worth it.
  - Don't default to the first name that comes to mind.
  - If you're feeling stuck, consider running a new name by a teammate. (Nowadays, you can also ask an AI agent for help!)
- Describe behavior: Encourage **naming based on what functions do** rather than when they are called.
  - Prefer `button.listen('click', addItemToCart)` over `button.listen('click', handleClick)`
- Balance clarity and conciseness—use abbreviations with care.
  - Ask yourself, "Will my readers immediately understand this label? **Will someone five years from now understand it?**"
- Software changes, and names should change with it.

## Version Control

- An atomic commit in a version control system is a commit that contains a single, self-contained change or a logical unit of work.
  - e,g, a bug fix, feature addition, a new test case, etc.
- Version control history serves as a form of free documentation.
  - The evolution of the codebase becomes easier to understand.
- For example, if you are trying to understand a specific feature of a piece of software, you can locate the version control commit that introduces this feature:
  - The commit message would describe the changes.
  - Diffrent view would show the changes that were required for this feature
- Many open-source projects have a policy of accepting only atomic changes with detailed commit messages.
- Atomic commits improve the intelligibility of your software code by encouraging authors to think in terms of logical units of change.

## Tests

- Test code allows you to ensure that your code adheres to the input/output requirements of users.
- Test code can also serve as **a form of documentation**.
  - Tests define the **expected behavior** of a module.
  - Tests also document various **usage** of a module.
  - Tests show what types of inputs are acceptable and what forms of output can be generated.
- It is more useful to **keep a module and its test code together** so that the test code serves as an example of how a module should be used and its expected behaviour.

## Documentation

- The need for extensive code documentation can be reduced by using:
  - Intelligible identifier names based on common knowledge
  - Atomic commits in version control system
  - Tests that showcase the usage and expected behaviour
- Code documentation becomes essential when the above methods are insufficient to describe the purpose of a code block.

Some tips from *Heras* developers:

- A function docstring may include the following items:
  - A one-line description of the function.
  - Paragraphs of more detailed information.
  - An examples section. (*Optional*)
  - An args section for the function arguments.
  - Returns section for the return values.
  - A raises section for possible errors. (*Optional*)

Even a well-thought-out identifier name can sometimes lead to confusion. Documentation can help further clarify the purpose of an identifier.

If a source file is large, the concept of "**Table of Contents**" can be used to organise the content into sections.

Explain what your code does in comments:

- Readers are generally interested in two types of information:
  - **What the code does**: This should be described in comments.
  - **How the code works**: The code itself should convey this information.
- Never try to explain **HOW** your code works in a comment: it's better to write the code so that its **functionality** is obvious. It's a waste of time to explain poorly written code. Generally, comments should describe **WHAT** your code does, not **HOW**.

## Summary

The intelligibility of code can be improved by:

- Choosing identifier names wisely.
- Using **atomic commits** in version control.
- Relying on tests as a form of documentation for **usage and expected behaviour** of a module.
- Documenting only **what** is being done by the code and letting the code describe how it is being done.

If a code is easy to understand, more people will be able to fix, extend and reuse it.

Maintainability also depends on factors such as external dependencies, software architecture, etc.

**Others** can fix, extend, and reuse your code if it is easy to understand.

After a few months or years, you will become the **others** and will need help to understand your own code.

Making things easier to understand often brings **greater clarity** to your own thoughts.

If you are not satisfied with an identifier name or code structure, it is useful to **cross-examine** the code-generating agent and find more convincing solutions.
