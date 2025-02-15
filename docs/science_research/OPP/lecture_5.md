---
comments: true
---

# Lecture 5 - Writing Computer Programmes

- Speaker: Dr. Abhishek Dutta - Senior Research Software Engineer - Visual Geometry Group, Department of Engineering Science

Programming is an iterative process encompassing *problem identification*, *developing a mental model of computation*, *translating and representing this model in code*, and *refining the structure iteratively*. The primary goal in writing code is to ensure it *functions correctly and produces accurate results*.

However, programming is often a collaborative effort, meaning your code must be comprehensible to others. Therefore, *ensuring code readability* is as crucial as ensuring its functionality. Specifically, well-written code enables others to accurately reconstruct the mental model of computation, whereas poorly written code hinders this process.

## Naming Identifiers

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

Identifier names can be likened to **post-it notes** affixed to various sections of a program.

How should one select an appropriate identifier name?

- **Use common knowledge and analogies** to reduce the need for extensive documentation

> `walkdir()`: relies on the concepts of walking and directories (or folders) containing multiple items.
>
> `split_dataset()`: relies on the concept of splitting a collection of things into two or more groups.

- When multiple identifier names are viable, select the one that can be easily explained to a five-year-old.
- A **well-chosen identifier name** can eliminate the necessity for extensive code comments.

How can one determine which concepts are universally understood?

- Engaging with code and documentation authored by others enables one to transcend the limitations imposed by
  - *The here*: the temporal context of one's birth
  - *The now*: one's field of expertise (e.g., engineering)
- Exposure to concepts from **other disciplines** or **sub-disciplines** (i.e., spatially remote fields) facilitates the liberation from personal biases and broadens one's intellectual perspective.
  - For engineers, other disciplines encompass the humanities, biology, anthropology, art, and related fields.
  - For AI specialists, sub-disciplines include operating systems, database software, communication tools, and related areas.
- Engaging with historical software (i.e., temporally remote) and documentation provides clarity regarding concepts that have proven enduring.

Selecting an effective identifier name requires transcending the "tyranny of the here and now" by exploring ideas, code, and documentation that are:

- **remote in time** (e.g., historical releases)
- **remote in space** (i.e., beyond your field of expertise)

Some tips from *Linux Kernel* developers include:

- Employ concise and descriptive names that are **brief** and **precise**.
    > Prefer `cout_active_users()` over `cntusr()`
    > `i`: for loop counter
    > `tmp`: for a variable that holds a temporary value
- *Functions should be concise, focused, and perform a single task effectively.*
  - They should occupy no more than one or two screenfuls of text, performing a single task efficiently.
  - The number of local variables should not exceed 5 to 10.

Some tips from developers at *Google*:

- Dedicate time to selecting appropriate names—it is a worthwhile investment.
  - Avoid defaulting to the first name that occurs to you.
  - If uncertain, consult a teammate for feedback on potential names. (Alternatively, seek assistance from an AI agent.)
- Emphasise behaviour: Prioritise **naming functions based on their actions** rather than their invocation context.
  - Prefer `button.listen('click', addItemToCart)` over `button.listen('click', handleClick)`
- Strive for a balance between clarity and conciseness—exercise caution when using abbreviations.
  - Consider whether your readers will instantly comprehend the label and whether it will remain intelligible five years hence.
- As software evolves, so too should its nomenclature.

## Version Control

- An atomic commit within a version control system encapsulates a single, self-contained modification or a coherent unit of work.
  - Examples include bug fixes, feature implementations, new test cases, and similar modifications.
- The history of version control acts as an implicit form of documentation.
  - It facilitates a clearer understanding of the codebase's evolution.
- For instance, to comprehend a specific software feature, one can identify the version control commit that introduced it:
  - The commit message typically outlines the modifications.
  - A different view would display the changes necessary for implementing the feature.
- Numerous open-source projects enforce policies requiring atomic changes accompanied by detailed commit messages.
- Atomic commits enhance code clarity by prompting authors to conceptualise changes as logical units.

## Tests

- Test code ensures that your software complies with user-defined input/output specifications.
- Test code also functions as **a form of documentation**.
  - Tests specify the **expected behaviour** of a module.
  - Tests also document the various **applications** of a module.
  - Tests illustrate the acceptable input types and the potential output forms.
- It is advantageous to **maintain a module alongside its test code**, as the latter exemplifies the module's usage and expected behaviour.

## Documentation

- The necessity for comprehensive code documentation can be minimised through:
  - Intelligible identifier names based on common knowledge
  - Atomic commits within the version control system
  - Tests that showcase the usage and expected behaviour
- Code documentation becomes indispensable when the aforementioned methods fail to adequately describe a code block's purpose.

Some tips from *Heras* developers:

- A function's docstring may encompass the following elements:
  - A one-line description of the function.
  - Paragraphs of more detailed information.
  - An examples section. (*Optional*)
  - An args section for the function arguments.
  - Returns section for the return values.
  - A raises section for possible errors. (*Optional*)

Even meticulously chosen identifier names may occasionally cause confusion. Documentation serves to further elucidate their purpose.

For extensive source files, employing a "**Table of Contents**" can effectively organise the content into coherent sections.

Use comments to elucidate the functionality of your code:

- Readers typically seek two types of information:
  - **What the code accomplishes**: This should be articulated in comments.
  - **How the code operates**: The code itself should communicate this information.
- Avoid explaining **how** your code operates in comments; instead, write code whose **functionality** is self-evident. Explaining poorly written code is inefficient. Typically, comments should describe **what** your code achieves, not **how**.

## Summary

Code clarity can be enhanced through:

- Choosing identifier names wisely.
- Using **atomic commits** in version control.
- Relying on tests as a form of documentation for **usage and expected behaviour** of a module.
- Documenting solely **what** the code accomplishes, allowing the code itself to illustrate **how** it operates.

If code is comprehensible, it becomes more accessible for others to debug, extend, and repurpose.

Maintainability is also influenced by factors such as external dependencies, software architecture, and related considerations.

**Others** can debug, extend, and repurpose your code if it is comprehensible.

After several months or years, you may find yourself among the **others**, requiring assistance to comprehend your own code.

Enhancing comprehensibility often leads to **greater clarity** in one's own understanding.

If dissatisfied with an identifier name or code structure, it is beneficial to **critically evaluate** the code-generating agent and identify more effective solutions.
