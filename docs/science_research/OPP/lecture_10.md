---
comments: true
---

# Lecture 10 - Ethics and Artificial Intelligence

Speaker: Dr. Mackenzie Graham

## Introduction

There is significant enthusiasm regarding the potential benefits of artificial intelligence (AI) and machine learning in fields such as healthcare, science, education, and finance.

How should we ethically evaluate the development and deployment of AI within these domains?

What ethical challenges might arise from the use of AI in these contexts?

## Medicine

### Current Situation

The primary objective of healthcare providers is to utilise medical knowledge, clinical expertise, and available interventions to safeguard and enhance patient health and well-being. However, medical knowledge remains incomplete, and the learning environment is often characterised by significant noise and variability.

Leveraging extensive repositories of medical data can facilitate the development of resources that enhance learning efficiency, thereby increasing the likelihood of positive patient outcomes.

### The Goals of AI in Medicine

- Effectiveness: The capacity to accurately diagnose, prevent, or treat illnesses, injuries, or diseases.
- Efficiency: The ability to achieve healthcare objectives more rapidly and with reduced resource utilisation.
- Equity: The capacity to address the health needs of diverse populations equitably within healthcare systems.

> **Case 1**
>
> In 2017, the Royal Free NHS Foundation Trust shared personal data of approximately 1.6 million patients with Google DeepMind without obtaining explicit consent. This data transfer was conducted for the clinical safety testing of *Streams*, an application designed to assist in the diagnosis and detection of acute kidney injury.
>
> What ethical issues does this case present, if any?

> **Case 2**
>
> An AI developer is attempting to create software using patient electronic health data. The datasets are sourced from hospitals in wealthier districts, as these datasets are more comprehensive.
>
> What ethical issues does this case present, if any?

### Challenge: Data Sourcing

Is the data used for AI research selected based on clinical necessity, or is it merely drawn from readily available sources?

Is the data generated from current clinical practices suitable for AI development?

Inequities in access can result in disparities in dataset representation: for example, 81% of genetic samples used in genome-wide association studies (GWAS) are of European ancestry, while only 3% are of African ancestry (Popejoy, 2016).

Social structures external to the healthcare system can exacerbate disparities in access to care. These disparities are often misinterpreted as reflecting biological differences, leading to biased treatment practices. Consequently, data derived from such practices may embed biases into AI algorithms.

Data generated through routine healthcare operations may not align with research requirements: critical factors influencing disease progression or treatment efficacy are often omitted from existing datasets. Additionally, data collection may lack the necessary frequency, granularity, or scope to identify meaningful relationships.

Uncoordinated practices in data collection and dissemination result in datasets that are poorly suited for training AI systems. For instance, common clinical practices may introduce confounding variables.

Health data is frequently collected without explicit participant consent: obtaining informed consent for the use of patient data in AI algorithm development may not always be feasible or deemed necessary. Furthermore, there may be disagreements regarding the appropriate uses of such data.

> **Case 3**
>
> An AI-driven clinical decision support system provides an incorrect treatment recommendation (one that a human clinician would not have made), which the clinician follows, leading to patient harm.
>
> What ethical issues does this case present, if any?

### Challenge: Clinical Deployment

Many machine learning algorithms are inherently opaque, failing to provide users with explanations for their decisions.

This opacity undermines a clinician's ability to assess the *epistemic authority* of the algorithm, raising concerns regarding physician accountability, patient autonomy, and trust.

Even when AI systems function as intended, their real-world clinical utility remains questionable. For instance, cost prediction is often used as a proxy for care prediction. The hype surrounding medical AI has created an environment where clinicians, administrators, and policymakers struggle to accurately assess the capabilities and limitations of current AI systems, as exemplified by the performance of IBM's Watson and Epic Sepsis (which exhibited a 67% false-negative rate).

### Summary

Funding and coordinated initiatives are essential to collect data with the standardisation, frequency, granularity, and attention to confounding factors required to develop accurate and equitable AI systems. (Data Sourcing)

Standards must be developed to better elucidate the maturity of AI systems and the level of evidence supporting specific claims of clinical utility. (Product Development)

Funding agencies, healthcare systems, clinicians, and AI developers must identify areas where current AI systems can significantly enhance the equity, effectiveness, or efficiency of healthcare delivery. (Clinical Deployment)

## Education

Large language models (LLMs), such as ChatGPT, are fundamentally transforming the ways in which we access and interact with information.

Surveys indicate that approximately 20% of students in the United States have utilised ChatGPT to complete academic assignments.

> **Case 4**
>
> Dr. X, a professor at a leading research university seeking tenure, employs ChatGPT to draft her research papers. She generates the ideas and provides the headings, while ChatGPT composes the text. This approach reduces her writing time from four weeks to four hours.
>
> What ethical issues does this case present, if any, does Dr. X's use of ChatGPT raise?

## Companionship

Several companies, such as Replika, provide AI chatbots designed to offer companionship.

Some users report that these chatbots assist them in managing emotional challenges, while others describe their interactions with the chatbots as akin to *friendship* or even *love*.

> **Case 5**
>
> John, a 75-year-old widower living alone with no children, downloads an AI chatbot named *Anna* for companionship. He regularly interacts with the chatbot. When a care worker suggests that he visit the community centre to socialise, John becomes agitated, stating, "Anna is real, and she's the only friend I need."
>
> What ethical issues does this case present, if any?
