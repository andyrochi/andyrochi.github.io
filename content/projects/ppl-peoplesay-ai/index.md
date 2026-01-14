---
title: "People Say AI: Natural Language Querying for Qualitative Research Data"
date: 2025-05-01
updated: 2025-05-01
draft: false
tags: ["ai", "nlp", "qualitative-research", "streamlit", "llm"]
technologies: ["Python", "Streamlit", "Gemini API", "SQLite", "SQL", "Pandas"]
weight: 1
summary: "A collaborative AI-powered tool developed with the [Public Policy Lab](https://www.publicpolicylab.org/) to analyze qualitative data about older adults' experiences. Features natural language querying, automated SQL generation, and thematic summarization with source citations."
---

{{< button href="https://ppl-peoplesay-ai.streamlit.app" target="_blank" >}}
Live Demo
{{< /button >}}

{{< button href="https://github.com/andyrochi/ppl-peoplesay-ai" target="_blank" >}}
{{< icon "github" >}} Github Link
{{< /button >}}

**People Say AI: Leveraging AI for Qualitative Research Analysis**

People Say AI is a collaborative project with the [**Public Policy Lab**](https://www.publicpolicylab.org/) that explores the potential of artificial intelligence to democratize access to qualitative research data. Built to query [**The People Say**](https://thepeoplesay.org/) database—a comprehensive collection of older adults' experiences in the United States funded by The SCAN Foundation—the application demonstrates how large language models can enhance rather than replace human research capabilities.

## Project Overview

Qualitative research often involves navigating vast amounts of unstructured text, a process that can be time-consuming and difficult to scale. This project investigates how we can leverage AI to help researchers explore complex qualitative datasets more efficiently while preserving the depth and context that makes this research valuable. 

The application provides an intuitive interface where users can ask questions in plain English, which are then translated into data-driven insights. By bridging the gap between natural language and structured data, People Say AI makes valuable community perspectives more accessible to researchers, policymakers, and advocates. As noted by [The People Say](https://thepeoplesay.org/), the platform features older adults talking about their lives and the policy issues that affect them, including housing, healthcare, and financial security.

## Key Capabilities

### **Natural Language to SQL Querying**
Traditional data retrieval often requires specialized knowledge of SQL or database schemas. People Say AI simplifies this by using prompt engineering to convert natural language questions into precise SQL queries. This allows users to focus on their research questions rather than the technicalities of data retrieval. The system remains transparent by displaying the generated SQL, allowing for verification and trust.

### **AI-Powered Analysis & Summarization**
Once relevant data excerpts are retrieved, the application leverages **Gemini 1.5** models to synthesize the findings. Users can choose from different analytical frameworks—such as **Thematic Analysis**, **Narrative Analysis**, or **Comparative Analysis**—to guide how the model interprets the data. This flexibility ensures that the insights generated align with specific research methodologies.

### **Integrity through Source Citation**
A critical challenge in using AI for research is ensuring accuracy and preventing hallucinations. People Say AI addresses this by implementing an automatic citation system. Every summary generated includes direct references and quotes from the specific database excerpts used, ensuring full traceability from the AI's answer back to the original human experience.

## Technical Implementation

The application is built with a modular architecture focused on transparency and research integrity:

*   **Frontend**: Developed using **Streamlit** to provide a responsive, researcher-focused interface for real-time data exploration.
*   **Orchestration**: A core logic engine manages the pipeline, coordinating between LLM inference (**Gemini API**), SQLite database operations, and result formatting.
*   **Prompt Engineering**: Carefully crafted prompts ensure that the AI generates valid SQL and produces summaries that maintain the nuance of the original qualitative data.

## My Role & Contributions

As the primary developer on this project, I worked closely with the **Public Policy Lab** to translate research needs into a functional AI application. My contributions included:

*   **System Architecture**: Designing and building the full-stack application, from the SQLite database schema to the Streamlit frontend.
*   **AI Methodology**: Developing and testing prompt strategies that ensure high-fidelity data retrieval and context-aware summarization.
*   **Research Integrity**: Implementing the source citation system to ensure that every AI-generated insight is grounded in the original dataset.
*   **User Experience**: Designing a workflow that makes complex AI processes transparent and approachable for non-technical researchers.

## Conclusion

This collaboration highlights the potential for AI to serve as a powerful "co-pilot" for researchers. By making complex qualitative datasets more searchable and summarizable, People Say AI helps translate community voices into evidence-based policy insights. It stands as a model for how large language models can be deployed responsibly in research contexts—augmenting human insight while maintaining strict standards for transparency and attribution.
