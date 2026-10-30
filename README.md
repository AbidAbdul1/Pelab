# Pelab

# SET-1: Prompt Engineering and LCEL Chain Using Gemini API

1. Baseline vs. Enhanced Prompts

Aim

To compare a basic prompt and an enhanced prompt for generating a one-paragraph biography of Ada Lovelace and evaluate their relevance, completeness, and writing style.

A. Baseline Prompt

Prompt:

Write a one-paragraph bio of Ada Lovelace.

Output:

Ada Lovelace was an English mathematician and writer who is widely regarded as the world's first computer programmer. She was born in 1815 and was the daughter of the poet Lord Byron. She worked with Charles Babbage on his proposed Analytical Engine and wrote notes explaining how it could perform calculations. Her ideas about computing were far ahead of her time, and she is remembered for her important contributions to the development of computer science.

B. Enhanced Prompt

Prompt:

Act as a professional historian and science writer. Write a
single paragraph about Ada Lovelace in approximately 100 words.

Include the following details:
1. Her birth and background.
2. Her collaboration with Charles Babbage.
3. Her contributions to computing.
4. Why she is considered the first computer programmer.

Use clear, formal, and informative language suitable for
college students. Ensure the paragraph is historically
accurate, logically organized, and free from unnecessary
details.

Output:

Ada Lovelace (1815–1852) was an English mathematician whose work laid important foundations for modern computing. The daughter of poet Lord Byron, she developed a strong interest in mathematics and science. She collaborated with Charles Babbage, who designed the proposed Analytical Engine, a mechanical general-purpose computing machine. In 1843, Lovelace published extensive notes on the machine, including an algorithm intended to calculate Bernoulli numbers. This work is widely regarded as one of the earliest computer programs. She also recognized that computers could potentially manipulate symbols beyond numbers, demonstrating remarkable insight into the future possibilities of computing.

C. Comparison of Both Outputs

Evaluation Criteria| Baseline Prompt| Enhanced Prompt
Relevance| Provides relevant information about Ada Lovelace.| Focuses on the specific aspects requested.
Completeness| Includes basic facts and contributions.| Covers her background, collaboration, algorithm, and broader vision.
Writing Style| Simple and general.| Formal, structured, and informative.
Specificity| Provides limited details.| Includes specific historical details and the year 1843.
Format| One paragraph.| One paragraph with approximately 100 words.

Result

The enhanced prompt produces a more detailed, organized, and informative biography because it specifies the role, content, length, and writing style. The baseline prompt provides a reasonable answer but offers less control over the output.

Conclusion

Enhanced prompting improves the relevance, completeness, and consistency of AI-generated responses by providing clear and specific instructions.

---

2. Building a Simple LCEL Chain Using Gemini API

Aim

To create a simple LangChain Expression Language (LCEL) chain using the Gemini API that accepts a fixed instruction, sends it to a Large Language Model (LLM), and prints the generated summary.

Requirements

- Python 3
- LangChain
- LangChain Google GenAI integration
- Google Gemini API key
- Internet connection

Step 1: Install Required Libraries

Run the following command in your terminal:

pip install -U langchain langchain-google-genai

Step 2: Get Your Gemini API Key

1. Open "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in with your Google account.
3. Create an API key.
4. Copy the API key.

Step 3: Python Program

Create a Python file named "simple_lcel.py".

import os
from getpass import getpass

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# Enter Gemini API key
os.environ["GOOGLE_API_KEY"] = getpass("Enter Gemini API Key: ")

# Initialize Gemini model
llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    temperature=0
)

# Create prompt template
prompt = ChatPromptTemplate.from_template(
    "Summarize the following text in two sentences:\n{text}"
)

# Build LCEL chain
chain = prompt | llm | StrOutputParser()

# Input text
text = """
Artificial Intelligence is a branch of computer science that
enables machines to perform tasks requiring human intelligence.
It is used in healthcare, education, transportation, and many
other fields to improve efficiency and solve problems.
"""

# Execute the chain
result = chain.invoke({"text": text})

# Display the output
print("\nSummary:")
print(result)

Step 4: Execute the Program

Run the following command in the terminal:

python simple_lcel.py

Enter your Gemini API key when prompted.

Step 5: Expected Output

Enter Gemini API Key:

Summary:
Artificial Intelligence enables machines to perform tasks
that typically require human intelligence. It is used in
healthcare, education, transportation, and other fields to
improve efficiency and solve problems.

Note: The actual output may differ slightly depending on Gemini's response. The output above is illustrative.

Step 6: Explanation of the Code

Component| Purpose
"ChatGoogleGenerativeAI"| Connects LangChain to Google's Gemini API.
"ChatPromptTemplate"| Creates a prompt template for the input text.
"StrOutputParser"| Converts the model response into a string.
"prompt | llm | StrOutputParser()"| Connects all components into an LCEL chain.
"chain.invoke()"| Sends the input through the chain and obtains the result.
"print(result)"| Displays the generated summary.

Working Flow

Input Text
    |
    v
Prompt Template
    |
    v
Gemini API
    |
    v
Output Parser
    |
    v
Final Summary

Result

A simple LCEL chain was created using the Gemini API. The program accepts input text, sends the formatted prompt to Gemini, and prints the generated summary.

Conclusion

LangChain Expression Language simplifies LLM application development by connecting prompts, language models, and output parsers using the pipe ("|") operator. This program uses Google's Gemini API rather than OpenAI.

References

- "Google AI Studio — Gemini API Key" (https://aistudio.google.com/apikey)
- "LangChain Google GenAI Integration Documentation" (https://reference.langchain.com/python/langchain-google-genai/langchain_google_genai)
- "LangChain Documentation" (https://python.langchain.com/docs/introduction/)

---

Technology Stack: Python | LangChain | LCEL | Google Gemini API




# SET-2: Iterative Prompt Refinement and LCEL Chain Using Gemini API

1. Iterative Refinement on a Simple Task

Aim

To summarize the plot of Shakespeare's play Romeo and Juliet through three rounds of prompt refinement and observe how adding length, style, and content constraints improves the generated output.

Introduction

Prompt refinement is the process of improving an instruction given to an AI model to obtain more accurate, relevant, and well-structured responses. In this experiment, three prompts are designed with increasing levels of detail and evaluated using the Gemini API.

Iteration 1: Minimal Instruction

Prompt:

Summarize the plot of Romeo and Juliet.

Output:

Romeo and Juliet is a tragedy by William Shakespeare about two young lovers from rival families in Verona. They fall in love and secretly marry, but a series of misunderstandings and tragic events leads to their deaths, finally bringing peace between their families.

Observation:

The prompt produces a general summary of the play. However, it does not specify the length, writing style, or important plot details that must be included.

Iteration 2: Addition of Length and Style Constraints

Prompt:

Summarize the plot of William Shakespeare's play Romeo and Juliet
in exactly two sentences. Use simple, clear English suitable for
college students. Maintain a formal and informative writing style.

Output:

In Verona, Romeo Montague and Juliet Capulet fall in love despite their families' bitter rivalry and secretly marry with the help of Friar Laurence. After a series of violent events and a failed plan to reunite them, both lovers die tragically, and their deaths finally end the conflict between their families.

Observation:

The second prompt provides better control over the response. The output follows the two-sentence requirement and uses clear, formal language.

Iteration 3: Specification of Key Content Elements

Prompt:

Act as a literature teacher and summarize William Shakespeare's
tragedy Romeo and Juliet in exactly two sentences.

Include the following key elements:
1. Setting: Verona, Italy.
2. Main characters: Romeo Montague and Juliet Capulet.
3. Central conflict: Their families are bitter enemies.
4. Major events: Their secret marriage and the tragic misunderstanding
   involving Friar Laurence's plan.
5. Theme: Love, family hatred, fate, and the consequences of violence.

Use simple, formal English suitable for college students.
Ensure the summary is accurate, coherent, and limited to exactly
two sentences.

Output:

Set in Verona, Italy, William Shakespeare's tragedy Romeo and Juliet follows Romeo Montague and Juliet Capulet, who fall deeply in love and secretly marry despite the bitter hatred between their families. When violence, a failed plan by Friar Laurence, and a tragic misunderstanding separate them, both lovers die, ultimately ending the family feud and highlighting the destructive consequences of hatred and the power of love.

Observation:

The third prompt produces a more focused and informative summary. It explicitly includes the setting, main characters, central conflict, major events, and themes while maintaining the required length and style.

Comparison of the Three Iterations

Criteria| Iteration 1| Iteration 2| Iteration 3
Prompt Type| Minimal instruction| Length and style constraints| Detailed content requirements
Length Control| Not specified| Exactly two sentences| Exactly two sentences
Writing Style| General| Simple and formal| Simple and formal
Setting| Not explicitly required| Not explicitly required| Verona, Italy
Main Characters| Mentioned generally| Clearly identified| Clearly identified
Major Events| Briefly summarized| More focused| Explicitly specified
Themes| Not explicitly required| Implied| Explicitly included
Overall Quality| Basic| Improved| Most comprehensive

Result

The experiment demonstrates that the quality and structure of AI-generated summaries can be improved through iterative prompt refinement. The first prompt produces a general summary, the second introduces length and style constraints, and the third specifies the important plot elements and themes.

Conclusion

Iterative prompt refinement helps generate more relevant, complete, and consistent responses. Adding clear instructions, length constraints, style requirements, and key content elements improves the usefulness of the final output.

---

2. Building a Simple LCEL Chain Using Gemini API

Aim

To create a minimal LangChain Expression Language (LCEL) script that accepts a fixed instruction, passes it to a Gemini language model, and prints the generated result.

Requirements

- Python 3
- LangChain
- LangChain Google GenAI integration
- Google Gemini API key
- Internet connection

Step 1: Install Required Libraries

Run the following command in your terminal:

pip install -U langchain langchain-google-genai

Step 2: Get Your Gemini API Key

1. Open "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in with your Google account.
3. Create an API key.
4. Copy the API key.

Step 3: Python Program

Create a Python file named "simple_lcel.py".

import os
from getpass import getpass

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# Enter Gemini API key
os.environ["GOOGLE_API_KEY"] = getpass("Enter Gemini API Key: ")

# Initialize Gemini model
llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    temperature=0
)

# Create prompt template
prompt = ChatPromptTemplate.from_template(
    "Summarize the following text in two sentences:\n{text}"
)

# Build LCEL chain
chain = prompt | llm | StrOutputParser()

# Input text
text = """
Artificial Intelligence is a branch of computer science that
enables machines to perform tasks requiring human intelligence.
It is used in healthcare, education, transportation, and many
other fields to improve efficiency and solve problems.
"""

# Execute the chain
result = chain.invoke({"text": text})

# Display the output
print("\nSummary:")
print(result)

Step 4: Execute the Program

Run the following command:

python simple_lcel.py

Enter your Gemini API key when prompted.

Step 5: Expected Output

Enter Gemini API Key:

Summary:
Artificial Intelligence enables machines to perform tasks
that typically require human intelligence. It is used in
healthcare, education, transportation, and other fields to
improve efficiency and solve problems.

Note: The output shown above is illustrative. The actual response may differ slightly depending on the model.

Step 6: Explanation of the Code

Component| Description
"ChatGoogleGenerativeAI"| Connects LangChain to Google's Gemini API.
"ChatPromptTemplate"| Creates a structured prompt with an input variable.
"StrOutputParser"| Converts the model response into a plain string.
"prompt | llm | StrOutputParser()"| Connects the components into an LCEL chain.
"chain.invoke()"| Sends the input through the chain and obtains the result.
"print(result)"| Displays the generated summary.

Working Flow

Input Text
    |
    v
Prompt Template
    |
    v
Gemini API
    |
    v
Output Parser
    |
    v
Final Summary

Result

A simple LCEL chain was implemented using the Gemini API. It accepts input text, formats the prompt, sends it to the language model, and prints the generated summary.

Conclusion

LCEL simplifies the development of LLM applications by connecting prompt templates, language models, and output parsers using the pipe ("|") operator. The implementation uses Google's Gemini API to generate the requested summary.

---

References

- "Google AI Studio — Gemini API Key" (https://aistudio.google.com/apikey)
- "LangChain Google GenAI Integration Documentation" (https://reference.langchain.com/python/langchain-google-genai/langchain_google_genai)
- "LangChain Documentation" (https://python.langchain.com/docs/introduction/)

---

Technology Stack: Python | LangChain | LCEL | Google Gemini API



# SET-3: Diagnosing Prompt Failures & Edge Cases and Building a Simple LCEL Chain Using Gemini API

1. Diagnosing Prompt Failures & Edge Cases

Aim

To identify common prompt failures such as ambiguity, missing context, and contradictory instructions, analyze their effects on AI-generated responses, and improve the prompts by adding clear instructions and examples using Google Gemini.

Introduction

Prompt failures occur when an AI model receives unclear, incomplete, or contradictory instructions. These problems can lead to irrelevant, incorrect, or poorly formatted responses.

In this experiment, a vague prompt is created, its failure is analyzed, and an improved prompt is designed to generate a better response.

A. Creating a Vague Prompt

Prompt:

Explain Java.

Output:

Java is a programming language used to develop applications. It is object-oriented and platform-independent. Java is commonly used in web development, mobile applications, and enterprise software.

Observation

The response provides basic information about Java, but the prompt is too general. It does not specify the expected length, target audience, important concepts, or writing format.

B. Identifying the Prompt Failure

Failure Type| Description| Example
Ambiguity| The instruction is not specific.| Explain Java.
Missing Context| The prompt does not provide enough information.| Explain Java without specifying the audience.
Format Error| The expected output format is not mentioned.| No instruction about paragraphs or bullet points.
Lack of Specificity| Important topics are not identified.| No mention of OOP concepts or features.

C. Improving the Prompt

Enhanced Prompt:

Act as an experienced Java programming instructor.

Explain Java programming in simple English for beginners
and college students.

Include the following topics:

1. Definition of Java.
2. Important features of Java.
3. Object-Oriented Programming concepts.
4. Platform independence.
5. Real-world applications of Java.

Use clear headings and bullet points.
Provide simple examples wherever necessary.
Keep the explanation informative and easy to understand.

Output:

Introduction to Java

Java is a high-level, object-oriented programming language developed by James Gosling and his team at Sun Microsystems. It is widely used to develop web applications, mobile applications, desktop software, and enterprise systems.

Important Features of Java

1. Platform Independent: Java programs run on different operating systems using the Java Virtual Machine (JVM).
2. Object-Oriented: Java supports classes, objects, inheritance, polymorphism, abstraction, and encapsulation.
3. Simple: Java has a syntax that is relatively easy to learn for beginners.
4. Secure: Java provides security features such as bytecode verification and runtime checks.
5. Multithreading: Java supports executing multiple tasks simultaneously.

Object-Oriented Programming Concepts

- Encapsulation: Wrapping data and methods into a single unit.
- Inheritance: Acquiring properties and methods from another class.
- Polymorphism: Performing different operations using the same interface.
- Abstraction: Hiding implementation details and showing essential features.

Platform Independence

Java source code is compiled into bytecode. This bytecode can run on any system with a compatible Java Virtual Machine (JVM).

Applications of Java

- Web applications.
- Android applications.
- Banking software.
- Enterprise applications.
- Desktop applications.

D. Comparison of Both Prompts

Evaluation Criteria| Vague Prompt| Enhanced Prompt
Clarity| Low| High
Specificity| General| Detailed
Context| Missing| Clearly provided
Output Format| Not specified| Headings and bullet points
Completeness| Basic information| Covers important concepts
Usefulness| Limited| More useful for beginners

Result

The vague prompt generated a general explanation of Java without covering specific concepts. The enhanced prompt generated a structured and informative response by providing clear instructions, context, and formatting requirements.

Conclusion

Prompt refinement helps identify and correct common prompt failures. Adding clear instructions, relevant context, examples, and output format requirements improves the quality, accuracy, and usefulness of AI-generated responses.

---

2. Building a Simple LCEL Chain Using Gemini API

Aim

To create a minimal LangChain Expression Language (LCEL) script that accepts a fixed instruction, passes it to a Gemini language model, and prints the generated result.

Requirements

- Python 3
- LangChain
- LangChain Google GenAI integration
- Google Gemini API key
- Internet connection

Step 1: Install Required Libraries

Run the following command in the terminal:

pip install -U langchain langchain-google-genai

Step 2: Get Your Gemini API Key

1. Open "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in with your Google account.
3. Create an API key.
4. Copy the API key.

Step 3: Python Program

Create a Python file named "simple_lcel.py".

import os
from getpass import getpass

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# Enter Gemini API key
os.environ["GOOGLE_API_KEY"] = getpass("Enter Gemini API Key: ")

# Initialize Gemini model
llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    temperature=0
)

# Create prompt template
prompt = ChatPromptTemplate.from_template(
    "Summarize the following text in two sentences:\n{text}"
)

# Build LCEL chain
chain = prompt | llm | StrOutputParser()

# Input text
text = """
Artificial Intelligence is a branch of computer science that
enables machines to perform tasks requiring human intelligence.
It is used in healthcare, education, transportation, and many
other fields to improve efficiency and solve problems.
"""

# Execute the chain
result = chain.invoke({"text": text})

# Display the output
print("\nSummary:")
print(result)

Step 4: Execute the Program

Run the following command:

python simple_lcel.py

Enter your Gemini API key when prompted.

Step 5: Expected Output

Enter Gemini API Key:

Summary:
Artificial Intelligence enables machines to perform tasks
that typically require human intelligence. It is used in
healthcare, education, transportation, and other fields to
improve efficiency and solve problems.

Note: The actual output may differ slightly depending on Gemini's response. The output shown above is illustrative.

Step 6: Explanation of the Code

Component| Description
"ChatGoogleGenerativeAI"| Connects LangChain to Google's Gemini API.
"ChatPromptTemplate"| Creates a structured prompt with an input variable.
"StrOutputParser"| Converts the model response into a plain string.
"prompt | llm | StrOutputParser()"| Connects all components into an LCEL chain.
"chain.invoke()"| Sends the input through the chain and obtains the result.
"print(result)"| Displays the generated summary.

Working Flow

Input Text
    |
    v
Prompt Template
    |
    v
Gemini API
    |
    v
Output Parser
    |
    v
Final Summary

Result

A simple LCEL chain was created using the Gemini API. The program accepts input text, formats the prompt, sends it to Gemini, and prints the generated summary.

Conclusion

LangChain Expression Language simplifies LLM application development by connecting prompt templates, language models, and output parsers using the pipe ("|") operator. This implementation uses Google's Gemini API to generate the requested summary.

---

References

- "Google AI Studio – Gemini API Key" (https://aistudio.google.com/apikey)
- "LangChain Google GenAI Integration Documentation" (https://reference.langchain.com/python/langchain-google-genai/langchain_google_genai)
- "LangChain Documentation" (https://python.langchain.com/docs/introduction/)

---

Technology Stack: Python | LangChain | LCEL | Google Gemini API





# SET-4: Few-Shot vs. Zero-Shot Prompting and LCEL Chain Using Gemini API

1. Few-Shot vs. Zero-Shot Comparison

Aim

To design and execute zero-shot and few-shot prompts using a text classification task (sentiment analysis), compare their outputs, and evaluate their accuracy, consistency, and adherence to examples using Google Gemini.

Introduction

Prompting is a technique used to guide an AI model to perform a specific task.

There are two important prompting techniques:

1. Zero-Shot Prompting: The model performs a task without receiving any examples.
2. Few-Shot Prompting: The model receives a few input-output examples before performing the actual task.

In this experiment, both techniques are used to classify customer reviews into Positive, Negative, or Neutral sentiment.

A. Zero-Shot Prompting

Prompt:

Classify the sentiment of the following customer review
as Positive, Negative, or Neutral.

Review: "The product quality is excellent and delivery
was very fast."

Return only the sentiment label.

Output:

Positive

Observation:

The model successfully identifies the sentiment without receiving any examples. It understands the instruction and classifies the customer review as Positive.

B. Few-Shot Prompting

Prompt:

You are a sentiment analysis assistant.

Classify customer reviews into Positive, Negative, or Neutral.

Follow these examples:

Example 1:
Review: "The product is amazing and works perfectly."
Sentiment: Positive

Example 2:
Review: "The product is damaged and delivery was late."
Sentiment: Negative

Example 3:
Review: "The product arrived yesterday."
Sentiment: Neutral

Now classify the following review:

Review: "The product quality is excellent and delivery
was very fast."

Return only the sentiment label.

Output:

Positive

Observation:

The model uses the given examples to understand the expected classification pattern. It produces the correct sentiment label while following the demonstrated format.

C. Testing with Multiple Reviews

Both prompting techniques can be tested using the following reviews.

Customer Review| Expected Sentiment
The product is excellent and very useful.| Positive
The service was terrible and disappointing.| Negative
The package arrived this morning.| Neutral
I am very happy with the purchase.| Positive
The product stopped working after one day.| Negative

D. Comparison of Zero-Shot and Few-Shot Prompting

Evaluation Criteria| Zero-Shot Prompting| Few-Shot Prompting
Examples| No examples provided| 2–3 examples provided
Instructions| Direct task instruction| Task instruction with examples
Accuracy| Depends on model understanding| Can improve with relevant examples
Consistency| May vary in output format| Better format consistency when examples are clear
Complexity| Simple| Requires additional examples
Best Use| General classification tasks| Tasks requiring specific patterns or formats

Result

Both zero-shot and few-shot prompting successfully classify the customer review as Positive. Zero-shot prompting performs the task using only instructions, whereas few-shot prompting uses example input-output pairs to guide the model.

Conclusion

Zero-shot prompting is useful for simple tasks that require no examples. Few-shot prompting is useful when a model needs to follow a particular classification pattern or output format. The choice depends on task complexity and the required consistency.

---

2. Building a Simple LCEL Chain Using Gemini API

Aim

To create a minimal LangChain Expression Language (LCEL) script that accepts a fixed instruction, passes it to a Gemini language model, and prints the generated result.

Requirements

- Python 3
- LangChain
- LangChain Google GenAI integration
- Google Gemini API key
- Internet connection

Step 1: Install Required Libraries

Run the following command in your terminal:

pip install -U langchain langchain-google-genai

Step 2: Get Your Gemini API Key

1. Open "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in with your Google account.
3. Create an API key.
4. Copy the API key.

Step 3: Python Program

Create a Python file named "simple_lcel.py".

import os
from getpass import getpass

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

# Enter Gemini API key
os.environ["GOOGLE_API_KEY"] = getpass("Enter Gemini API Key: ")

# Initialize Gemini model
llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    temperature=0
)

# Create prompt template
prompt = ChatPromptTemplate.from_template(
    "Summarize the following text in two sentences:\n{text}"
)

# Build LCEL chain
chain = prompt | llm | StrOutputParser()

# Input text
text = """
Artificial Intelligence is a branch of computer science that
enables machines to perform tasks requiring human intelligence.
It is used in healthcare, education, transportation, and many
other fields to improve efficiency and solve problems.
"""

# Execute the chain
result = chain.invoke({"text": text})

# Display the output
print("\nSummary:")
print(result)

Step 4: Execute the Program

Run the following command:

python simple_lcel.py

Enter your Gemini API key when prompted.

Step 5: Expected Output

Enter Gemini API Key:

Summary:
Artificial Intelligence enables machines to perform tasks
that typically require human intelligence. It is used in
healthcare, education, transportation, and other fields to
improve efficiency and solve problems.

Note: The actual output may differ slightly depending on Gemini's response. The output shown above is illustrative.

Step 6: Explanation of the Code

Component| Description
"ChatGoogleGenerativeAI"| Connects LangChain to Google's Gemini API.
"ChatPromptTemplate"| Creates a structured prompt with an input variable.
"StrOutputParser"| Converts the model response into a plain string.
"prompt | llm | StrOutputParser()"| Connects all components into an LCEL chain.
"chain.invoke()"| Sends the input through the chain and obtains the result.
"print(result)"| Displays the generated summary.

Working Flow

Input Text
    |
    v
Prompt Template
    |
    v
Gemini API
    |
    v
Output Parser
    |
    v
Final Summary

Result

A simple LCEL chain was created using the Gemini API. The program accepts input text, formats the prompt, sends it to Gemini, and prints the generated summary.

Conclusion

LangChain Expression Language simplifies LLM application development by connecting prompt templates, language models, and output parsers using the pipe ("|") operator. This implementation uses Google's Gemini API to generate the requested summary.

---

References

- "Google AI Studio – Gemini API Key" (https://aistudio.google.com/apikey)
- "LangChain Google GenAI Integration Documentation" (https://reference.langchain.com/python/langchain-google-genai/langchain_google_genai)
- "LangChain Documentation" (https://python.langchain.com/docs/introduction/)

---

Technology Stack: Python | LangChain | LCEL | Google Gemini API




# SET-5: Generative AI Lab Practicals

Technology Used: Python, Google Gemini API

This set contains two practical experiments based on prompt engineering and LangChain Expression Language (LCEL), implemented using Google's Gemini API.

---

Experiment 1: Role-Based and Negative Prompting

1. Aim

To implement role-based prompting and negative prompting using the Google Gemini API and evaluate how each technique influences the model's response.

2. Introduction

Prompt engineering is the process of designing effective instructions to obtain relevant and useful responses from an AI model.

Role-Based Prompting

Role-based prompting assigns a specific role or personality to an AI model.

Examples:

- You are a teacher.
- You are a software engineer.
- You are a financial advisor.
- You are a healthcare technology expert.

It helps the model generate responses according to the assigned role, tone, and perspective.

Negative Prompting

Negative prompting provides instructions about what the AI model should avoid generating.

Examples:

- Do not mention brand names.
- Do not use complicated technical terms.
- Do not include advertisements.
- Do not provide unrelated information.

It helps control unwanted content in the generated response.

3. Requirements

- Python 3.x
- Google Gemini API
- Google Gen AI Python SDK
- VS Code / Google Colab

4. Installation

Install the required library:

pip install google-genai

5. Generate Gemini API Key

1. Visit "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in using your Google account.
3. Click on Create API Key.
4. Copy the generated API key.
5. Keep your API key private.

6. Python Implementation

Create a file named "role_prompting.py".

from google import genai

# Initialize Gemini API
client = genai.Client(api_key="YOUR_GEMINI_API_KEY")

# Input question
question = """
Explain three benefits of Artificial Intelligence in healthcare.
"""

# --------------------------------
# 1. Role-Based Prompting
# --------------------------------

role_prompt = """
You are an experienced healthcare technology advisor.

Explain the benefits of Artificial Intelligence in healthcare
in a professional and simple manner.

Provide three important benefits.
"""

response1 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=role_prompt + question
)

print("\n===== ROLE-BASED PROMPTING =====")
print(response1.text)


# --------------------------------
# 2. Role-Based + Negative Prompting
# --------------------------------

negative_prompt = """
You are an experienced healthcare technology advisor.

Explain the benefits of Artificial Intelligence in healthcare
in a professional and simple manner.

Provide three important benefits.

Negative Instructions:
- Do not mention any brand names.
- Do not use complicated technical terms.
- Do not include advertisements.
- Do not provide unrelated information.
"""

response2 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=negative_prompt + question
)

print("\n===== NEGATIVE PROMPTING =====")
print(response2.text)

Note: Replace "YOUR_GEMINI_API_KEY" with your actual Gemini API key. Never upload your API key to GitHub.

7. Code Explanation

Component| Description
"from google import genai"| Imports the Google Gen AI library.
"genai.Client()"| Establishes a connection with Gemini API.
"question"| Contains the input question.
"role_prompt"| Defines the role assigned to the AI model.
"negative_prompt"| Defines instructions to avoid unwanted content.
"generate_content()"| Sends the prompt to Gemini and generates a response.
"response.text"| Extracts the generated text.
"print()"| Displays the generated response.

8. Expected Output

Output 1: Role-Based Prompting

===== ROLE-BASED PROMPTING =====

1. Early Disease Detection:
AI helps identify diseases at an early stage.

2. Improved Diagnosis:
AI assists doctors in analyzing medical data.

3. Better Patient Care:
AI helps healthcare professionals provide
personalized treatment.

Output 2: Negative Prompting

===== NEGATIVE PROMPTING =====

1. Early Disease Detection:
AI helps detect diseases earlier.

2. Accurate Diagnosis:
AI assists doctors in identifying health problems.

3. Patient Care:
AI helps improve treatment planning and monitoring.

Note: Actual responses may vary depending on the Gemini model.

9. Observation

Prompting Technique| Observation
Role-Based Prompting| Influences the tone, style, and perspective of the response.
Negative Prompting| Helps suppress unwanted content.
Combined Prompting| Provides better control over the generated response.

10. Result

Role-based and negative prompting were successfully implemented using the Google Gemini API. The experiment demonstrated how assigning a specific role and providing negative instructions influence the AI-generated response.

---

Experiment 2: Building a Simple LCEL Chain

1. Aim

To create a simple LCEL (LangChain Expression Language) chain that accepts a fixed instruction, passes it to a Large Language Model using the Google Gemini API, and prints the generated result.

2. Introduction

LCEL stands for LangChain Expression Language.

It is a framework feature used to connect different components of an AI application into a single processing pipeline.

A chain is a sequence of operations connected together to perform a particular task.

In this experiment, we create a simple text summarization chain using Gemini.

Working Process

1. Accept an input instruction.
2. Create a prompt using a prompt template.
3. Send the prompt to the Gemini model.
4. Process the generated response.
5. Display the final output.

3. Requirements

- Python 3.x
- Google Gemini API
- LangChain
- langchain-google-genai
- VS Code / Google Colab

4. Installation

Install the required libraries:

pip install langchain langchain-google-genai

5. Configure Gemini API Key

1. Visit "Google AI Studio" (https://aistudio.google.com/apikey).
2. Generate an API key.
3. Copy the API key.
4. Use it in the Python program.

6. Python Implementation

Create a file named "simple_lcel.py".

import os

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import PromptTemplate
from langchain_core.output_parsers import StrOutputParser

# Step 1: Configure Gemini API Key
os.environ["GOOGLE_API_KEY"] = "YOUR_GEMINI_API_KEY"

# Step 2: Initialize Gemini Model
llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    temperature=0.3
)

# Step 3: Create Prompt Template
prompt = PromptTemplate.from_template(
    "Summarize the following text in simple words:\n{text}"
)

# Step 4: Create Output Parser
parser = StrOutputParser()

# Step 5: Build LCEL Chain
chain = prompt | llm | parser

# Step 6: Provide Input Text
text = """
Artificial Intelligence is a technology that enables
machines to perform tasks that normally require human
intelligence. It is used in healthcare, education,
transportation, banking and many other industries.
AI helps automate tasks, analyze information and
improve decision-making.
"""

# Step 7: Execute the Chain
result = chain.invoke({"text": text})

# Step 8: Print the Result
print("\n===== GEMINI LCEL OUTPUT =====")
print(result)

Note: Replace "YOUR_GEMINI_API_KEY" with your actual Gemini API key. Do not commit API keys to GitHub.

7. Code Explanation

Step 1: Import Required Libraries

import os

from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.prompts import PromptTemplate
from langchain_core.output_parsers import StrOutputParser

- "os": Used to access environment variables.
- "ChatGoogleGenerativeAI": Connects LangChain to Google Gemini.
- "PromptTemplate": Creates reusable prompts with placeholders.
- "StrOutputParser": Converts the model response into a plain text string.

Step 2: Configure Gemini API

os.environ["GOOGLE_API_KEY"] = "YOUR_GEMINI_API_KEY"

This stores the Gemini API key in an environment variable so that LangChain can access the Gemini service.

Step 3: Initialize Gemini Model

llm = ChatGoogleGenerativeAI(
    model="gemini-2.5-flash",
    temperature=0.3
)

- "model": Specifies the Gemini model.
- "temperature": Controls the randomness of the generated response. A lower value generally produces more consistent output.

Step 4: Create Prompt Template

prompt = PromptTemplate.from_template(
    "Summarize the following text in simple words:\n{text}"
)

This creates a reusable prompt.

Here, "{text}" is a placeholder that will be replaced with the actual input text.

Step 5: Create Output Parser

parser = StrOutputParser()

This converts the AI-generated response into a normal string.

Step 6: Build LCEL Chain

chain = prompt | llm | parser

This is the most important line in the experiment.

The pipe operator ("|") connects three components:

1. Prompt Template: Creates the instruction.
2. Gemini LLM: Processes the instruction and generates a response.
3. Output Parser: Converts the response into plain text.

LCEL Workflow:

Input Text
    |
    v
Prompt Template
    |
    v
Google Gemini LLM
    |
    v
Output Parser
    |
    v
Final Generated Summary

Step 7: Execute the Chain

result = chain.invoke({"text": text})

The "invoke()" method executes the complete chain by passing the input text through all connected components.

Step 8: Display the Result

print(result)

This displays the generated summary in the terminal.

8. Expected Output

===== GEMINI LCEL OUTPUT =====

Artificial Intelligence (AI) allows machines
to perform tasks that usually require human
intelligence.

It is used in various fields such as healthcare,
education, banking and transportation.

AI helps automate work, analyze data and
make better decisions.

Note: Actual responses may vary depending on the Gemini model.

9. Observation

Component| Function
PromptTemplate| Creates the input instruction.
Gemini LLM| Generates the response.
StrOutputParser| Converts the response into plain text.
LCEL Chain| Connects all components into one pipeline.
invoke()| Executes the complete chain.

10. Result

A simple LCEL chain was successfully implemented using LangChain and the Google Gemini API. The chain accepted a fixed instruction, processed the input text through the Gemini model, converted the response into plain text, and displayed the final summary.

---

Viva Questions and Answers

1. What is Prompt Engineering?

Prompt engineering is the process of designing effective instructions to obtain accurate and useful responses from an AI model.

2. What is Role-Based Prompting?

Role-based prompting assigns a specific role or personality to an AI model to influence its response.

3. What is Negative Prompting?

Negative prompting provides instructions to the AI model about what it should avoid generating.

4. What is Gemini API?

Gemini API is Google's application programming interface that allows developers to integrate Gemini AI models into their applications.

5. What is LCEL?

LCEL stands for LangChain Expression Language. It is used to connect different AI components into a processing chain.

6. What is the purpose of the pipe operator ("|")?

The pipe operator connects multiple components in an LCEL chain and passes the output of one component to the next.

7. What is PromptTemplate?

PromptTemplate is used to create reusable prompts with placeholders for input values.

8. What is StrOutputParser?

StrOutputParser converts the model's response into a plain text string.

9. What is an LLM?

LLM stands for Large Language Model. It is an AI model trained on large amounts of text data to understand and generate human-like language.

10. What is Temperature?

Temperature controls the randomness of generated responses. Lower values generally produce more predictable responses.

11. What is the purpose of invoke()?

The "invoke()" method executes an LCEL chain by passing input data through all connected components.

12. Which AI model is used in these experiments?

Google Gemini 2.5 Flash is used as the AI model in both experiments.

---

Conclusion

In Set-5, two practical experiments were successfully implemented using the Google Gemini API.

1. Role-Based and Negative Prompting: Demonstrated how role instructions and negative instructions influence AI-generated responses.
2. Building a Simple LCEL Chain: Demonstrated how to connect a prompt template, Gemini LLM, and output parser into a single processing pipeline.

Both experiments provide a basic understanding of prompt engineering, LLM integration, and building AI applications using Python.

---

References

- "Google Gemini API Documentation" (https://ai.google.dev/gemini-api/docs)
- "Google AI Studio" (https://aistudio.google.com/)
- "Google Gen AI Python SDK" (https://github.com/googleapis/python-genai)
- "LangChain Documentation" (https://python.langchain.com/docs/)
- "LangChain Google GenAI Integration" (https://python.langchain.com/docs/integrations/chat/google_generative_ai/)




# SET-6: Generative AI Lab Practicals

Technology Used: Python, Google Gemini API

This set contains two practical experiments based on prompt engineering, iterative refinement, and Retrieval-Augmented Generation (RAG).

---

Experiment 1: Constraint Specification and Iterative Refinement

1. Aim

To improve the quality of AI-generated responses by applying explicit constraints and performing iterative prompt refinement using the Google Gemini API.

2. Introduction

Prompt refinement is the process of improving an initial prompt to obtain better responses from an AI model.

Sometimes, a basic prompt may generate responses that are too lengthy, poorly structured, or missing important information.

To overcome these problems, we use constraint specification and iterative refinement.

Constraint Specification

Constraint specification means providing clear instructions and limitations to the AI model.

Examples:

- Specify the required word count.
- Request bullet-point formatting.
- Use simple language.
- Include only important information.
- Avoid unnecessary explanations.

Iterative Refinement

Iterative refinement means improving a prompt step by step based on the problems identified in the previous response.

In this experiment, we perform two refinement cycles:

1. Initial Prompt: Generate a basic response.
2. First Refinement: Add word-count and formatting constraints.
3. Second Refinement: Add further instructions to improve clarity and relevance.

3. Requirements

- Python 3.x
- Google Gemini API
- Google Gen AI Python SDK
- VS Code / Google Colab

4. Installation

Install the required library:

pip install google-genai

5. Generate Gemini API Key

1. Visit "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in using your Google account.
3. Generate an API key.
4. Copy the API key.
5. Keep your API key private.

6. Python Implementation

Create a file named "iterative_refinement.py".

from google import genai

# Initialize Gemini API
client = genai.Client(api_key="YOUR_GEMINI_API_KEY")

# Input topic
topic = """
Explain the importance of Artificial Intelligence
in modern healthcare.
"""

# --------------------------------
# Initial Prompt
# --------------------------------

prompt1 = f"""
{topic}

Explain the topic.
"""

response1 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=prompt1
)

print("\n===== INITIAL RESPONSE =====")
print(response1.text)


# --------------------------------
# First Refinement Cycle
# --------------------------------

prompt2 = f"""
{topic}

Instructions:
1. Explain in approximately 100 words.
2. Use simple English.
3. Present the answer in bullet points.
4. Include the most important benefits.
"""

response2 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=prompt2
)

print("\n===== FIRST REFINEMENT =====")
print(response2.text)


# --------------------------------
# Second Refinement Cycle
# --------------------------------

prompt3 = f"""
{topic}

Instructions:
1. Write approximately 100 words.
2. Use simple and clear English.
3. Provide exactly five bullet points.
4. Give each bullet point a short heading.
5. Avoid repeated information.
6. Include practical healthcare applications.
7. Do not include an introduction or conclusion.
"""

response3 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=prompt3
)

print("\n===== SECOND REFINEMENT =====")
print(response3.text)

Note: Replace "YOUR_GEMINI_API_KEY" with your actual API key.

7. Code Explanation

Step 1: Import the Library

from google import genai

Imports the Google Gen AI library to communicate with the Gemini API.

Step 2: Initialize Gemini

client = genai.Client(api_key="YOUR_GEMINI_API_KEY")

Creates a Gemini API client using the generated API key.

Step 3: Define the Topic

topic = """
Explain the importance of Artificial Intelligence
in modern healthcare.
"""

This is the input topic given to the AI model.

Step 4: Initial Prompt

prompt1 = f"""
{topic}
Explain the topic.
"""

A basic instruction is provided without specifying length or format.

The generated response may contain unnecessary details or inconsistent formatting.

Step 5: First Refinement

prompt2 = f"""
{topic}

Instructions:
1. Explain in approximately 100 words.
2. Use simple English.
3. Present the answer in bullet points.
4. Include the most important benefits.
"""

Additional constraints are added to improve the response.

The model is instructed to use simple language, approximately 100 words, and bullet points.

Step 6: Second Refinement

prompt3 = f"""
{topic}

Instructions:
1. Write approximately 100 words.
2. Use simple and clear English.
3. Provide exactly five bullet points.
4. Give each bullet point a short heading.
5. Avoid repeated information.
6. Include practical healthcare applications.
7. Do not include an introduction or conclusion.
"""

More specific instructions are added to improve consistency, relevance, and structure.

Step 7: Generate Responses

response = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=prompt
)

The Gemini model processes each prompt and generates a response.

Step 8: Display the Responses

print(response.text)

Displays the generated response in the terminal.

8. Expected Output

Output 1: Initial Response

===== INITIAL RESPONSE =====

Artificial Intelligence plays an important role
in modern healthcare.

It helps doctors diagnose diseases, analyze
medical reports, monitor patients, and improve
treatment planning.

AI also helps hospitals manage their resources
and automate routine activities.

Output 2: First Refinement

===== FIRST REFINEMENT =====

- Early Diagnosis: AI helps identify diseases
  at an early stage.

- Medical Analysis: AI assists doctors in
  analyzing medical reports.

- Patient Monitoring: AI helps monitor
  patients continuously.

- Treatment Planning: AI supports personalized
  treatment decisions.

- Hospital Management: AI helps improve
  healthcare operations.

Output 3: Second Refinement

===== SECOND REFINEMENT =====

- Early Diagnosis: Helps detect diseases early.

- Medical Analysis: Assists doctors in
  analyzing medical reports.

- Patient Monitoring: Tracks patient health
  conditions.

- Personalized Treatment: Supports better
  treatment planning.

- Hospital Management: Improves hospital
  operations and resource management.

Note: These are illustrative outputs. Actual Gemini responses may vary.

9. Observation

Refinement Stage| Observation
Initial Prompt| Response may be lengthy and less structured.
First Refinement| Word count and bullet-point formatting improve.
Second Refinement| Response becomes more specific, organized, and relevant.

Improvements After Two Refinement Cycles

1. Improved response structure.
2. Better control over response length.
3. Clear and simple language.
4. Reduced unnecessary information.
5. More relevant and consistent output.

10. Result

Constraint specification and iterative refinement were successfully implemented using the Google Gemini API. Two refinement cycles improved the structure, clarity, and relevance of the generated responses.

---

Experiment 2: Basic Data Indexing for RAG

1. Aim

To implement basic data indexing for Retrieval-Augmented Generation (RAG) by loading documents, splitting them into uniform chunks, generating embeddings using the Google Gemini API, and storing them in an in-memory vector store.

2. Introduction

RAG stands for Retrieval-Augmented Generation.

It is a technique that combines information retrieval with AI-generated responses.

Instead of depending only on the knowledge learned during model training, a RAG system retrieves relevant information from external documents and uses that information to answer questions.

Important Concepts

1. Document Loading

Document loading means collecting and reading the source documents that contain useful information.

2. Text Chunking

Text chunking means dividing large documents into smaller sections called chunks.

For example, a document containing 1,000 tokens can be divided into five chunks of approximately 200 tokens each.

Chunking makes document processing and information retrieval easier.

3. Embeddings

Embeddings are numerical representations of text.

They convert text into vectors that capture semantic meaning.

Gemini provides an embedding model that can generate these vector representations.

4. Vector Store

A vector store is used to store embeddings along with their original text.

It helps retrieve relevant information based on similarity.

In this experiment, we use a simple in-memory vector store implemented using Python.

3. Requirements

- Python 3.x
- Google Gemini API
- Google Gen AI Python SDK
- NumPy
- VS Code / Google Colab

4. Installation

Install the required libraries:

pip install google-genai numpy

5. Generate Gemini API Key

1. Visit "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in using your Google account.
3. Generate an API key.
4. Copy the API key.
5. Keep your API key private.

6. Python Implementation

Create a file named "rag_indexing.py".

from google import genai
import numpy as np
import re

# --------------------------------
# Step 1: Initialize Gemini API
# --------------------------------

client = genai.Client(
    api_key="YOUR_GEMINI_API_KEY"
)

# --------------------------------
# Step 2: Create Sample Documents
# --------------------------------

documents = [
    """
    Artificial Intelligence is a technology that
    enables machines to perform tasks that normally
    require human intelligence. AI is widely used in
    healthcare, education, banking, and transportation.
    """,

    """
    Machine Learning is a branch of Artificial
    Intelligence that allows computers to learn
    from data and improve their performance.
    It includes supervised, unsupervised, and
    reinforcement learning.
    """,

    """
    Deep Learning is a subset of Machine Learning.
    It uses artificial neural networks to process
    complex data such as images, audio, and text.
    Deep Learning is widely used in computer vision
    and natural language processing.
    """
]

# --------------------------------
# Step 3: Split Documents into
# Approximately 200-token Chunks
# --------------------------------

def split_into_chunks(text, max_tokens=200):

    sentences = re.split(r'(?<=[.!?])\s+', text.strip())

    chunks = []
    current_chunk = ""

    for sentence in sentences:

        candidate = (current_chunk + " " + sentence).strip()

        token_count = client.models.count_tokens(
            model="gemini-2.5-flash",
            contents=candidate
        ).total_tokens

        if token_count <= max_tokens:
            current_chunk = candidate

        else:
            if current_chunk:
                chunks.append(current_chunk)

            current_chunk = sentence

    if current_chunk:
        chunks.append(current_chunk)

    return chunks


# --------------------------------
# Step 4: Generate Chunks
# --------------------------------

all_chunks = []

for doc_id, document in enumerate(documents):

    chunks = split_into_chunks(document)

    for chunk in chunks:

        all_chunks.append({
            "document_id": doc_id,
            "text": chunk
        })


print("\n===== DOCUMENT CHUNKS =====")

for index, chunk in enumerate(all_chunks):

    print(f"\nChunk {index + 1}:")
    print(chunk["text"])


# --------------------------------
# Step 5: Generate Gemini Embeddings
# --------------------------------

vector_store = []

for chunk in all_chunks:

    embedding_response = client.models.embed_content(
        model="gemini-embedding-001",
        contents=chunk["text"]
    )

    embedding = embedding_response.embeddings[0].values

    vector_store.append({
        "document_id": chunk["document_id"],
        "text": chunk["text"],
        "embedding": np.array(embedding, dtype=np.float32)
    })


# --------------------------------
# Step 6: Inspect Vector Store
# --------------------------------

print("\n===== VECTOR STORE DETAILS =====")

print("Total Documents:", len(documents))
print("Total Chunks:", len(all_chunks))
print("Total Embeddings:", len(vector_store))

for index, item in enumerate(vector_store):

    print(f"\nEmbedding {index + 1}")
    print("Document ID:", item["document_id"])
    print("Vector Dimensions:", len(item["embedding"]))
    print("Text:", item["text"])


# --------------------------------
# Step 7: Check Consistency
# --------------------------------

dimensions = [
    len(item["embedding"])
    for item in vector_store
]

if len(set(dimensions)) == 1:

    print("\nAll embeddings have consistent dimensions.")

else:

    print("\nEmbedding dimension mismatch detected!")


# --------------------------------
# Step 8: Similarity Search
# --------------------------------

query = "How does AI help computers learn from data?"

query_response = client.models.embed_content(
    model="gemini-embedding-001",
    contents=query
)

query_embedding = np.array(
    query_response.embeddings[0].values,
    dtype=np.float32
)


def cosine_similarity(vector1, vector2):

    return np.dot(vector1, vector2) / (
        np.linalg.norm(vector1) *
        np.linalg.norm(vector2)
    )


scores = []

for item in vector_store:

    score = cosine_similarity(
        query_embedding,
        item["embedding"]
    )

    scores.append((score, item["text"]))


# Sort results by similarity
scores.sort(key=lambda x: x[0], reverse=True)

print("\n===== MOST RELEVANT CHUNKS =====")

for score, text in scores[:3]:

    print("\nSimilarity Score:", round(float(score), 4))
    print("Retrieved Text:", text)

Note: Replace "YOUR_GEMINI_API_KEY" with your actual Gemini API key.

7. Code Explanation

Step 1: Import Required Libraries

from google import genai
import numpy as np
import re

- "google.genai": Connects Python with the Gemini API.
- "numpy": Handles numerical vectors and similarity calculations.
- "re": Helps split documents into sentences.

Step 2: Initialize Gemini API

client = genai.Client(
    api_key="YOUR_GEMINI_API_KEY"
)

Creates a connection with the Gemini API.

Step 3: Create Sample Documents

documents = [
    "Artificial Intelligence is a technology...",
    "Machine Learning is a branch of AI...",
    "Deep Learning is a subset of Machine Learning..."
]

Creates a small collection of sample documents.

These documents act as the knowledge source for the RAG indexing process.

Step 4: Split Documents into Chunks

def split_into_chunks(text, max_tokens=200):

This function divides a document into smaller sections.

The Gemini token-counting API checks the size of each candidate chunk so that chunks stay within approximately 200 tokens.

Chunking makes it easier to process and retrieve relevant information.

Step 5: Generate Embeddings

embedding_response = client.models.embed_content(
    model="gemini-embedding-001",
    contents=chunk["text"]
)

This sends each text chunk to the Gemini embedding model.

The model converts the text into a numerical vector representing its semantic meaning.

Step 6: Store Embeddings in Memory

vector_store.append({
    "document_id": chunk["document_id"],
    "text": chunk["text"],
    "embedding": np.array(embedding, dtype=np.float32)
})

Stores the following information:

- Document ID
- Original text chunk
- Numerical embedding vector

The vector store is maintained in Python memory using a list of dictionaries.

Step 7: Inspect the Vector Store

print("Total Chunks:", len(all_chunks))
print("Total Embeddings:", len(vector_store))

Displays the number of documents, chunks, and embeddings generated.

It also checks whether all embedding vectors have consistent dimensions.

Step 8: Generate Query Embedding

query_response = client.models.embed_content(
    model="gemini-embedding-001",
    contents=query
)

Converts the user's search query into an embedding vector using the same Gemini embedding model.

Step 9: Calculate Cosine Similarity

def cosine_similarity(vector1, vector2):

    return np.dot(vector1, vector2) / (
        np.linalg.norm(vector1) *
        np.linalg.norm(vector2)
    )

Cosine similarity measures how similar two vectors are.

A higher similarity score generally indicates that the two text embeddings are semantically closer.

Step 10: Retrieve Relevant Chunks

scores.sort(key=lambda x: x[0], reverse=True)

Sorts the chunks according to their similarity scores.

The most relevant chunks are displayed first.

8. RAG Indexing Workflow

       Sample Documents
              |
              v
       Document Loading
              |
              v
        Text Chunking
       (Approx. 200 Tokens)
              |
              v
      Gemini Embedding API
              |
              v
       Numerical Vectors
              |
              v
      In-Memory Vector Store
              |
              v
        Query Embedding
              |
              v
       Cosine Similarity
              |
              v
      Relevant Chunk Retrieval

9. Expected Output

===== DOCUMENT CHUNKS =====

Chunk 1:
Artificial Intelligence is a technology that
enables machines to perform tasks that normally
require human intelligence...

Chunk 2:
Machine Learning is a branch of Artificial
Intelligence that allows computers to learn
from data...

Chunk 3:
Deep Learning is a subset of Machine Learning...

===== VECTOR STORE DETAILS =====

Total Documents: 3
Total Chunks: 3
Total Embeddings: 3

Embedding 1
Document ID: 0
Vector Dimensions: 3072

Embedding 2
Document ID: 1
Vector Dimensions: 3072

Embedding 3
Document ID: 2
Vector Dimensions: 3072

All embeddings have consistent dimensions.

===== MOST RELEVANT CHUNKS =====

Similarity Score: 0.85
Retrieved Text: Machine Learning is a branch of
Artificial Intelligence that allows computers
to learn from data...

Note: Output values and similarity scores are illustrative. Actual results depend on the Gemini API response and the input documents. The embedding model used here normally returns 3072-dimensional vectors by default.

10. Observation

Component| Observation
Document Loading| Successfully loads a collection of sample documents.
Text Chunking| Divides documents into smaller sections.
Embedding Generation| Converts text chunks into numerical vectors using Gemini.
Vector Storage| Stores embeddings and original text in memory.
Consistency Check| Verifies that all embedding vectors have matching dimensions.
Similarity Search| Retrieves relevant chunks based on cosine similarity.

11. Result

Basic data indexing for RAG was successfully implemented using the Google Gemini embedding API. The documents were loaded, divided into approximately 200-token chunks, converted into numerical embeddings, and stored in an in-memory vector store. Embedding consistency was verified, and relevant chunks were retrieved using cosine similarity.

---

Viva Questions and Answers

1. What is Constraint Specification?

Constraint specification means providing clear instructions and limitations to an AI model to control its response.

2. What is Iterative Refinement?

Iterative refinement is the process of improving a prompt through multiple cycles to obtain better results.

3. What is the purpose of word-count constraints?

Word-count constraints help control the length of AI-generated responses.

4. What is RAG?

RAG stands for Retrieval-Augmented Generation. It combines information retrieval with AI-generated responses.

5. What is Document Chunking?

Document chunking is the process of dividing large documents into smaller sections for easier processing and retrieval.

6. What are Embeddings?

Embeddings are numerical representations of text that capture semantic meaning.

7. Which Gemini model is used for generating embeddings?

The "gemini-embedding-001" model is used to generate text embeddings.

8. What is a Vector Store?

A vector store stores numerical embe




 # SET-7: Generative AI Lab Practicals

Technology Used: Python, Google Gemini API

This set contains two practical experiments based on structured format prompting and basic data indexing for Retrieval-Augmented Generation (RAG).

---

Experiment 1: Structured Format Prompting

1. Aim

To implement structured format prompting using the Google Gemini API and generate information in specific formats such as bullet lists and Markdown tables.

2. Introduction

Structured format prompting is a prompt engineering technique in which we instruct an AI model to generate responses in a specific format.

Instead of generating ordinary paragraphs, the model is instructed to organize information using predefined structures.

Types of Structured Formats

1. Bullet Lists

Bullet lists organize information into separate points, making it easier to read and understand.

2. Markdown Tables

Markdown tables organize information into rows and columns.

They are useful for comparing information and presenting structured data.

Advantages

- Improves readability.
- Organizes information clearly.
- Makes responses easier to understand.
- Helps maintain consistent output formatting.
- Makes generated information easier to process.

3. Requirements

- Python 3.x
- Google Gemini API
- Google Gen AI Python SDK
- VS Code / Google Colab

4. Installation

Install the required library:

pip install google-genai

5. Generate Gemini API Key

1. Visit "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in using your Google account.
3. Generate an API key.
4. Copy the generated API key.
5. Keep your API key private.

6. Python Implementation

Create a file named "structured_prompting.py".

from google import genai

# Initialize Gemini API
client = genai.Client(
    api_key="YOUR_GEMINI_API_KEY"
)

# --------------------------------
# Experiment 1: Bullet List Format
# --------------------------------

bullet_prompt = """
List three benefits of daily exercise.

Instructions:
1. Present the answer as a bullet list.
2. Use simple English.
3. Explain each benefit in one sentence.
4. Do not write a paragraph.
"""

response1 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=bullet_prompt
)

print("\n===== BULLET LIST OUTPUT =====")
print(response1.text)


# --------------------------------
# Experiment 2: Markdown Table Format
# --------------------------------

table_prompt = """
List three benefits of daily exercise.

Instructions:
1. Present the answer as a Markdown table.
2. Use exactly two columns:
   Benefit and Description.
3. Include three rows of information.
4. Use simple English.
"""

response2 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=table_prompt
)

print("\n===== MARKDOWN TABLE OUTPUT =====")
print(response2.text)

Note: Replace "YOUR_GEMINI_API_KEY" with your actual Gemini API key. Never upload your API key to GitHub.

7. Code Explanation

Step 1: Import the Library

from google import genai

Imports the Google Gen AI library to communicate with the Gemini API.

Step 2: Initialize Gemini API

client = genai.Client(
    api_key="YOUR_GEMINI_API_KEY"
)

Creates a client connection using the Gemini API key.

Step 3: Create a Bullet List Prompt

bullet_prompt = """
List three benefits of daily exercise.

Instructions:
1. Present the answer as a bullet list.
2. Use simple English.
3. Explain each benefit in one sentence.
4. Do not write a paragraph.
"""

This prompt instructs Gemini to generate three benefits of daily exercise in bullet-point format.

Step 4: Generate the Bullet List Response

response1 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=bullet_prompt
)

Sends the bullet-list prompt to the Gemini model and generates a response.

Step 5: Create a Markdown Table Prompt

table_prompt = """
List three benefits of daily exercise.

Instructions:
1. Present the answer as a Markdown table.
2. Use exactly two columns:
   Benefit and Description.
3. Include three rows of information.
4. Use simple English.
"""

This prompt instructs Gemini to generate information in a Markdown table with two specified columns.

Step 6: Generate the Table Response

response2 = client.models.generate_content(
    model="gemini-2.5-flash",
    contents=table_prompt
)

Sends the table prompt to Gemini and generates a structured response.

Step 7: Display the Responses

print(response1.text)
print(response2.text)

Displays both generated responses in the terminal.

8. Expected Output

Output 1: Bullet List

===== BULLET LIST OUTPUT =====

- Improves Heart Health: Daily exercise
  strengthens the heart and improves blood circulation.

- Controls Body Weight: Exercise helps burn
  calories and maintain a healthy weight.

- Reduces Stress: Physical activity helps
  improve mood and reduce stress.

Output 2: Markdown Table

===== MARKDOWN TABLE OUTPUT =====

| Benefit | Description |
|---------|-------------|
| Heart Health | Improves heart function
and blood circulation. |
| Weight Control | Helps maintain a
healthy body weight. |
| Mental Health | Helps reduce stress
and improve mood. |

Note: These are sample outputs. Actual Gemini responses may vary.

9. Observation

Format| Observation
Bullet List| Organizes information into separate points.
Markdown Table| Organizes information into rows and columns.
Structured Prompting| Helps control the format and presentation of generated responses.

10. Result

Structured format prompting was successfully implemented using the Google Gemini API. The model generated information in both bullet-list and Markdown-table formats according to the given instructions.

---

Experiment 2: Basic Data Indexing for RAG

1. Aim

To implement basic data indexing for Retrieval-Augmented Generation (RAG) by loading a small collection of documents, splitting them into approximately 200-token chunks, generating embeddings using the Google Gemini API, and storing them in an in-memory vector store.

2. Introduction

RAG stands for Retrieval-Augmented Generation.

It is a technique that combines information retrieval with AI-generated responses.

A RAG system retrieves relevant information from external documents instead of depending only on the knowledge learned during model training.

Important Concepts

1. Document Loading

Document loading is the process of collecting and reading source documents containing useful information.

2. Text Chunking

Text chunking means dividing large documents into smaller sections called chunks.

For example, a document containing approximately 1,000 tokens can be divided into five chunks of approximately 200 tokens each.

3. Embeddings

Embeddings are numerical representations of text that capture semantic meaning.

The Gemini embedding model converts text into numerical vectors.

4. Vector Store

A vector store stores embeddings along with their corresponding text.

It allows the system to retrieve relevant information based on similarity.

In this experiment, we use a simple in-memory vector store implemented using Python.

3. Requirements

- Python 3.x
- Google Gemini API
- Google Gen AI Python SDK
- NumPy
- VS Code / Google Colab

4. Installation

Install the required libraries:

pip install google-genai numpy

5. Generate Gemini API Key

1. Visit "Google AI Studio" (https://aistudio.google.com/apikey).
2. Sign in using your Google account.
3. Generate an API key.
4. Copy the generated API key.
5. Keep your API key private.

6. Python Implementation

Create a file named "rag_indexing.py".

from google import genai
import numpy as np
import re

# --------------------------------
# Step 1: Initialize Gemini API
# --------------------------------

client = genai.Client(
    api_key="YOUR_GEMINI_API_KEY"
)

# --------------------------------
# Step 2: Create Sample Documents
# --------------------------------

documents = [
    """
    Artificial Intelligence is a technology that
    enables machines to perform tasks that normally
    require human intelligence. AI is widely used in
    healthcare, education, banking, and transportation.
    """,

    """
    Machine Learning is a branch of Artificial
    Intelligence that allows computers to learn
    from data and improve their performance.
    It includes supervised, unsupervised, and
    reinforcement learning.
    """,

    """
    Deep Learning is a subset of Machine Learning.
    It uses artificial neural networks to process
    complex data such as images, audio, and text.
    Deep Learning is widely used in computer vision
    and natural language processing.
    """
]

# --------------------------------
# Step 3: Split Documents into Chunks
# --------------------------------

def split_into_chunks(text, max_tokens=200):

    sentences = re.split(r'(?<=[.!?])\s+', text.strip())

    chunks = []
    current_chunk = ""

    for sentence in sentences:

        candidate = (current_chunk + " " + sentence).strip()

        token_count = client.models.count_tokens(
            model="gemini-2.5-flash",
            contents=candidate
        ).total_tokens

        if token_count <= max_tokens:
            current_chunk = candidate

        else:
            if current_chunk:
                chunks.append(current_chunk)

            current_chunk = sentence

    if current_chunk:
        chunks.append(current_chunk)

    return chunks


# --------------------------------
# Step 4: Generate Document Chunks
# --------------------------------

all_chunks = []

for doc_id, document in enumerate(documents):

    chunks = split_into_chunks(document)

    for chunk in chunks:

        all_chunks.append({
            "document_id": doc_id,
            "text": chunk
        })


print("\n===== DOCUMENT CHUNKS =====")

for index, chunk in enumerate(all_chunks):

    print(f"\nChunk {index + 1}:")
    print(chunk["text"])


# --------------------------------
# Step 5: Generate Gemini Embeddings
# --------------------------------

vector_store = []

for chunk in all_chunks:

    embedding_response = client.models.embed_content(
        model="gemini-embedding-001",
        contents=chunk["text"]
    )

    embedding = embedding_response.embeddings[0].values

    vector_store.append({
        "document_id": chunk["document_id"],
        "text": chunk["text"],
        "embedding": np.array(
            embedding,
            dtype=np.float32
        )
    })


# --------------------------------
# Step 6: Inspect Vector Store
# --------------------------------

print("\n===== VECTOR STORE DETAILS =====")

print("Total Documents:", len(documents))
print("Total Chunks:", len(all_chunks))
print("Total Embeddings:", len(vector_store))

for index, item in enumerate(vector_store):

    print(f"\nEmbedding {index + 1}")
    print("Document ID:", item["document_id"])
    print("Vector Dimensions:", len(item["embedding"]))
    print("Text:", item["text"])


# --------------------------------
# Step 7: Check Embedding Consistency
# --------------------------------

dimensions = [
    len(item["embedding"])
    for item in vector_store
]

if len(set(dimensions)) == 1:

    print("\nAll embeddings have consistent dimensions.")

else:

    print("\nEmbedding dimension mismatch detected!")


# --------------------------------
# Step 8: Similarity Search
# --------------------------------

query = "How does AI help computers learn from data?"

query_response = client.models.embed_content(
    model="gemini-embedding-001",
    contents=query
)

query_embedding = np.array(
    query_response.embeddings[0].values,
    dtype=np.float32
)


def cosine_similarity(vector1, vector2):

    denominator = (
        np.linalg.norm(vector1) *
        np.linalg.norm(vector2)
    )

    if denominator == 0:
        return 0.0

    return np.dot(vector1, vector2) / denominator


scores = []

for item in vector_store:

    score = cosine_similarity(
        query_embedding,
        item["embedding"]
    )

    scores.append((score, item["text"]))


# Sort by similarity score
scores.sort(
    key=lambda x: x[0],
    reverse=True
)

print("\n===== MOST RELEVANT CHUNKS =====")

for score, text in scores[:3]:

    print("\nSimilarity Score:", round(float(score), 4))
    print("Retrieved Text:", text)

Note: Replace "YOUR_GEMINI_API_KEY" with your actual Gemini API key. Do not upload your API key to GitHub.

7. Code Explanation

Step 1: Import Required Libraries

from google import genai
import numpy as np
import re

- "google.genai": Connects Python with Gemini API.
- "numpy": Handles numerical vectors and similarity calculations.
- "re": Helps split documents into sentences.

Step 2: Initialize Gemini API

client = genai.Client(
    api_key="YOUR_GEMINI_API_KEY"
)

Creates a connection with the Gemini API.

Step 3: Create Sample Documents

documents = [
    "Artificial Intelligence is a technology...",
    "Machine Learning is a branch of AI...",
    "Deep Learning is a subset of Machine Learning..."
]

Creates a small collection of sample documents.

These documents act as the knowledge source for the RAG indexing process.

Step 4: Split Documents into Chunks

def split_into_chunks(text, max_tokens=200):

This function divides documents into smaller sections.

The Gemini token-counting API checks the size of each candidate chunk so that chunks stay within approximately 200 tokens.

Step 5: Generate Embeddings

embedding_response = client.models.embed_content(
    model="gemini-embedding-001",
    contents=chunk["text"]
)

Sends each text chunk to the Gemini embedding model.

The model converts the text into a numerical vector representing its semantic meaning.

Step 6: Store Embeddings in Memory

vector_store.append({
    "document_id": chunk["document_id"],
    "text": chunk["text"],
    "embedding": np.array(embedding, dtype=np.float32)
})

Stores the following information:

- Document ID
- Original text chunk
- Numerical embedding vector

The vector store is maintained in Python memory using a list of dictionaries.

Step 7: Inspect the Vector Store

print("Total Chunks:", len(all_chunks))
print("Total Embeddings:", len(vector_store))

Displays the number of documents, chunks, and embeddings generated.

It also checks whether all embedding vectors have consistent dimensions.

Step 8: Generate Query Embedding

query_response = client.models.embed_content(
    model="gemini-embedding-001",
    contents=query
)

Converts the search query into an embedding vector using the same Gemini embedding model.

Step 9: Calculate Cosine Similarity

def cosine_similarity(vector1, vector2):

    return np.dot(vector1, vector2) / (
        np.linalg.norm(vector1) *
        np.linalg.norm(vector2)
    )

Cosine similarity measures the similarity between two vectors.

A higher similarity score generally indicates that two text embeddings are semantically closer.

Step 10: Retrieve Relevant Chunks

scores.sort(key=lambda x: x[0], reverse=True)

Sorts the chunks according to their similarity scores.

The most relevant chunks are displayed first.

8. RAG Indexing Workflow

       Sample Documents
              |
              v
       Document Loading
              |
              v
        Text Chunking
       (Approx. 200 Tokens)
              |
              v
      Gemini Embedding API
              |
              v
       Numerical Vectors
              |
              v
      In-Memory Vector Store
              |
              v
        Query Embedding
              |
              v
       Cosine Similarity
              |
              v
      Relevant Chunk Retrieval

9. Expected Output

===== DOCUMENT CHUNKS =====

Chunk 1:
Artificial Intelligence is a technology that
enables machines to perform tasks that normally
require human intelligence...

Chunk 2:
Machine Learning is a branch of Artificial
Intelligence that allows computers to learn
from data...

Chunk 3:
Deep Learning is a subset of Machine Learning...

===== VECTOR STORE DETAILS =====

Total Documents: 3
Total Chunks: 3
Total Embeddings: 3

Embedding 1
Document ID: 0
Vector Dimensions: 3072

Embedding 2
Document ID: 1
Vector Dimensions: 3072

Embedding 3
Document ID: 2
Vector Dimensions: 3072

All embeddings have consistent dimensions.

===== MOST RELEVANT CHUNKS =====

Similarity Score: 0.85
Retrieved Text: Machine Learning is a branch of
Artificial Intelligence that allows computers
to learn from data...

Note: Output values and similarity scores are illustrative. Actual results depend on Gemini API responses and the input documents. The default embedding dimension is 3072.

10. Observation

Component| Observation
Document Loading| Successfully loads a collection of sample documents.
Text Chunking| Divides documents into smaller sections.
Embedding Generation| Converts text chunks into numerical vectors using Gemini.
Vector Storage| Stores embeddings and original text in memory.
Consistency Check| Verifies that all embedding vectors have matching dimensions.
Similarity Search| Retrieves relevant chunks based on cosine similarity.

11. Result

Basic data indexing for RAG was successfully implemented using the Google Gemini embedding API. The documents were loaded, divided into approximately 200-token chunks, converted into numerical embeddings, and stored in an in-memory vector store. Embedding consistency was verified, and relevant chunks were retrieved using cosine similarity.

---

Viva Questions and Answers

1. What is Structured Format Prompting?

Structured format prompting is a technique that instructs an AI model to generate responses in a specific format, such as bullet lists or Markdown tables.

2. What is a Markdown Table?

A Markdown table is a structured format that organizes information into rows and columns.

3. What is the advantage of structured prompting?

It improves readability, consistency, organization, and presentation of AI-generated information.

4. What is RAG?

RAG stands for Retrieval-Augmented Generation. It combines information retrieval with AI-generated responses.

5. What is Document Chunking?

Document chunking is the process of dividing large documents into smaller sections for easier processing and retrieval.

6. What are Embeddings?

Embeddings are numerical representations of text that capture semantic meaning.

7. Which Gemini model is used for generating embeddings?

The "gemini-embedding-001" model is used to generate text embeddings.

8. What is a Vector Store?

A vector store stores numerical embeddings along with their corresponding text and supports similarity-based retrieval.

9. What is Cosine Similarity?

Cosine similarity measures the similarity between two vectors based on the angle between them.

10. Why is Chunking important in RAG?

Chunking divides large documents into manageable sections and helps retrieve relevant information efficiently.

11. What is an In-Memory Vector Store?

An in-memory vector store stores embeddings temporarily in computer memory rather than in a permanent database.

12. What is the difference between an embedding and a chunk?

A chunk is a small section of text, whereas an embedding is the numerical vector representation of that text.

---

Conclusion

In Set-7, two practical experiments were successfully implemented using the Google Gemini API.

1. Structured Format Prompting: Demonstrated how to generate information in bullet-list and Markdown-table formats using specific instructions.

2. Basic Data Indexing for RAG: Demonstrated document loading, text chunking, Gemini embedding generation, in-memory vector storage, consistency checking, and similarity-based retrieval.

These experiments provide a basic understanding of structured prompt engineering, text embeddings, and the indexing process used in Retrieval-Augmented Generation systems.

---

References

- "Google Gemini API Documentation" (https://ai.google.dev/gemini-api/docs)
- "Google AI Studio" (https://aistudio.google.com/)
- "Google Gen AI Python SDK" (https://github.com/googleapis/python-genai)
- "Gemini Embedd
 

# GENERATIVE AI LAB – SET 8

Experiment 1: JSON/YAML Generation and Validation Using Gemini API

Experiment 2: Basic Data Indexing for Retrieval-Augmented Generation (RAG)

---

Experiment 1: JSON/YAML Generation and Validation

1. Aim

To generate structured data in JSON and YAML formats using the Google Gemini API, validate the generated output using Python parsers, and refine prompts if the generated format contains errors.

2. Introduction

Structured data formats such as JSON and YAML are widely used for storing, transferring, and organizing information.

- JSON (JavaScript Object Notation): A lightweight data format commonly used in APIs and web applications.
- YAML (YAML Ain't Markup Language): A human-readable data serialization format commonly used in configuration files.

Generative AI models can generate JSON and YAML based on natural-language instructions. However, generated content may sometimes contain syntax errors or unwanted explanations.

In this experiment, Google Gemini generates information about three books in JSON and YAML formats. Python parsers are used to validate the generated output.

3. Requirements

- Python 3.9 or above
- Google Gemini API key
- Google GenAI Python SDK
- PyYAML library

4. Installation

Install the required packages:

pip install google-genai pyyaml

5. API Key Configuration

Obtain an API key from Google AI Studio:

https://aistudio.google.com/apikey

Set the API key as an environment variable.

Windows:

set GOOGLE_API_KEY=your_api_key

Linux/macOS:

export GOOGLE_API_KEY="your_api_key"

Do not upload your API key to GitHub.

6. Python Implementation

Create a Python file named:

"json_yaml_generation.py"

import os
import json
import yaml
from google import genai

# Initialize Gemini client
client = genai.Client(
    api_key=os.environ.get("GOOGLE_API_KEY")
)

MODEL = "gemini-2.5-flash"

# Dataset description
dataset_description = """
Create a dataset containing information about three books.

Each book must contain:
- title
- author
- publication_year

Use realistic sample book information.
"""

# Function to generate structured output
def generate_data(format_name, previous_error=None):

    prompt = f"""
    {dataset_description}

    Generate the dataset in valid {format_name} format.

    Requirements:
    1. Include exactly three books.
    2. Use the fields title, author, and publication_year.
    3. publication_year must be an integer.
    4. Return only the {format_name} data.
    5. Do not include explanations or Markdown code fences.
    """

    if previous_error:
        prompt += f"""

        Your previous output could not be parsed.
        Validation error: {previous_error}

        Correct the formatting and return valid {format_name} only.
        """

    response = client.models.generate_content(
        model=MODEL,
        contents=prompt
    )

    return response.text.strip()


# Validate JSON output
def validate_json(data):

    parsed_data = json.loads(data)

    if "books" not in parsed_data:
        raise ValueError("Missing books field")

    books = parsed_data["books"]

    if len(books) != 3:
        raise ValueError("Dataset must contain exactly three books")

    for book in books:
        if not all(
            field in book
            for field in ["title", "author", "publication_year"]
        ):
            raise ValueError("Missing required book fields")

        if not isinstance(book["publication_year"], int):
            raise ValueError("publication_year must be an integer")

    return parsed_data


# Validate YAML output
def validate_yaml(data):

    parsed_data = yaml.safe_load(data)

    if not isinstance(parsed_data, dict):
        raise ValueError("YAML must contain a dictionary")

    if "books" not in parsed_data:
        raise ValueError("Missing books field")

    books = parsed_data["books"]

    if not isinstance(books, list) or len(books) != 3:
        raise ValueError("Dataset must contain exactly three books")

    for book in books:
        if not all(
            field in book
            for field in ["title", "author", "publication_year"]
        ):
            raise ValueError("Missing required book fields")

        if not isinstance(book["publication_year"], int):
            raise ValueError("publication_year must be an integer")

    return parsed_data


# Generate and validate with iterative refinement
def generate_and_validate(format_name, validator):

    previous_error = None

    for attempt in range(1, 4):

        print(f"\nAttempt {attempt}: Generating {format_name}")

        generated_data = generate_data(
            format_name,
            previous_error
        )

        try:
            parsed_data = validator(generated_data)

            print(f"\nValid {format_name} output:")
            print(generated_data)

            print(f"\n{format_name} validation successful!")
            print("Number of books:", len(parsed_data["books"]))

            with open(
                f"books.{format_name.lower()}",
                "w",
                encoding="utf-8"
            ) as file:
                file.write(generated_data)

            return

        except (ValueError, TypeError, KeyError, yaml.YAMLError,
                json.JSONDecodeError) as error:

            previous_error = str(error)

            print("Validation failed:", previous_error)

    print(f"Unable to generate valid {format_name} after 3 attempts.")


# Main program
if __name__ == "__main__":

    generate_and_validate("JSON", validate_json)

    generate_and_validate("YAML", validate_yaml)

7. Explanation of the Code

1. Gemini Client: Connects the Python application to Google's Gemini API.
2. Dataset Description: Defines the required information about three books.
3. Generation Function: Sends instructions to Gemini to generate JSON or YAML.
4. JSON Validation: Uses "json.loads()" to check whether the generated JSON is syntactically valid.
5. YAML Validation: Uses "yaml.safe_load()" to parse the generated YAML safely.
6. Schema Validation: Checks whether all three books contain the required fields and correct data types.
7. Iterative Refinement: If validation fails, the error is sent back to Gemini so it can correct the output.
8. File Storage: Saves validated output into "books.json" and "books.yaml".

8. Sample Output

The following is an illustrative output. Actual generated book information may differ.

JSON Output:

{
  "books": [
    {
      "title": "The Alchemist",
      "author": "Paulo Coelho",
      "publication_year": 1988
    },
    {
      "title": "1984",
      "author": "George Orwell",
      "publication_year": 1949
    },
    {
      "title": "Wings of Fire",
      "author": "A. P. J. Abdul Kalam",
      "publication_year": 1999
    }
  ]
}

YAML Output:

books:
  - title: The Alchemist
    author: Paulo Coelho
    publication_year: 1988

  - title: "1984"
    author: George Orwell
    publication_year: 1949

  - title: Wings of Fire
    author: A. P. J. Abdul Kalam
    publication_year: 1999

Expected Terminal Output:

Attempt 1: Generating JSON

Valid JSON output:
...
JSON validation successful!
Number of books: 3

Attempt 1: Generating YAML

Valid YAML output:
...
YAML validation successful!
Number of books: 3

9. Observations

- Gemini can generate structured information using natural-language prompts.
- JSON and YAML are useful formats for storing generated information.
- Python parsers help identify syntax errors.
- Schema validation checks whether the output follows the required structure.
- Iterative refinement improves the reliability of generated structured data.

10. Result

Successfully generated structured datasets in JSON and YAML formats using the Google Gemini API. The generated outputs were validated using Python parsers and refined when necessary.

---

Experiment 2: Basic Data Indexing for RAG

1. Aim

To implement basic data indexing for Retrieval-Augmented Generation (RAG) by loading documents, splitting them into smaller chunks, generating embeddings using the Google Gemini API, and storing them in an in-memory vector store.

2. Introduction

Retrieval-Augmented Generation (RAG) is a technique that combines information retrieval with generative AI.

Instead of depending only on the model's internal knowledge, RAG retrieves relevant information from an external document collection before generating an answer.

The basic RAG workflow consists of:

1. Loading documents.
2. Splitting documents into smaller chunks.
3. Generating embeddings for each chunk.
4. Storing embeddings in a vector store.
5. Retrieving relevant chunks based on a user query.

An embedding is a numerical representation of text. Texts with similar meanings generally have similar embedding representations.

In this experiment, Gemini generates embeddings, and NumPy is used to calculate cosine similarity between document chunks.

3. Requirements

- Python 3.9 or above
- Google Gemini API key
- Google GenAI Python SDK
- NumPy

4. Installation

pip install google-genai numpy

5. API Key Configuration

Obtain an API key from:

https://aistudio.google.com/apikey

Set the environment variable:

Windows:

set GOOGLE_API_KEY=your_api_key

Linux/macOS:

export GOOGLE_API_KEY="your_api_key"

6. Python Implementation

Create a Python file named:

"rag_indexing.py"

import os
import numpy as np
from google import genai

# Initialize Gemini client
client = genai.Client(
    api_key=os.environ.get("GOOGLE_API_KEY")
)

GENERATION_MODEL = "gemini-2.5-flash"
EMBEDDING_MODEL = "gemini-embedding-001"

# Sample document collection
documents = [
    """
    Artificial Intelligence is a field of computer science
    that focuses on creating machines capable of performing
    tasks that normally require human intelligence.
    """,

    """
    Machine Learning is a subset of Artificial Intelligence.
    It enables computers to learn patterns from data and
    make predictions without being explicitly programmed.
    """,

    """
    Deep Learning is a subset of Machine Learning that uses
    neural networks with multiple layers to learn complex
    patterns from large datasets.
    """
]


# Split documents into chunks
def split_into_chunks(text, max_tokens=200):

    sentences = text.strip().split(".")
    chunks = []
    current_chunk = ""

    for sentence in sentences:

        sentence = sentence.strip()

        if not sentence:
            continue

        candidate = (
            current_chunk + " " + sentence
        ).strip()

        candidate = candidate + "."

        token_count = client.models.count_tokens(
            model=GENERATION_MODEL,
            contents=candidate
        ).total_tokens

        if token_count <= max_tokens:
            current_chunk = candidate

        else:
            if current_chunk:
                chunks.append(current_chunk)

            current_chunk = sentence + "."

    if current_chunk:
        chunks.append(current_chunk)

    return chunks


# Generate embeddings
def generate_embedding(text):

    response = client.models.embed_content(
        model=EMBEDDING_MODEL,
        contents=text
    )

    return np.array(
        response.embeddings[0].values,
        dtype=np.float32
    )


# Step 1: Load and split documents
all_chunks = []

for document in documents:

    chunks = split_into_chunks(
        document,
        max_tokens=200
    )

    all_chunks.extend(chunks)


print("Total documents:", len(documents))
print("Total chunks:", len(all_chunks))


# Step 2: Generate embeddings
vector_store = []

for index, chunk in enumerate(all_chunks):

    embedding = generate_embedding(chunk)

    vector_store.append({
        "id": index,
        "text": chunk,
        "embedding": embedding
    })


print("\nEmbeddings generated successfully!")

print(
    "Embedding dimensions:",
    len(vector_store[0]["embedding"])
)


# Step 3: Calculate cosine similarity
def cosine_similarity(vector1, vector2):

    denominator = (
        np.linalg.norm(vector1) *
        np.linalg.norm(vector2)
    )

    if denominator == 0:
        return 0.0

    return float(
        np.dot(vector1, vector2) / denominator
    )


# Step 4: Retrieve relevant chunks
def retrieve_documents(query, top_k=2):

    query_embedding = generate_embedding(query)

    results = []

    for item in vector_store:

        score = cosine_similarity(
            query_embedding,
            item["embedding"]
        )

        results.append({
            "text": item["text"],
            "score": score
        })

    results.sort(
        key=lambda item: item["score"],
        reverse=True
    )

    return results[:top_k]


# Example query
query = "What is machine learning?"

retrieved_results = retrieve_documents(query)

print("\nUser Query:", query)

print("\nRetrieved Documents:")

for result in retrieved_results:

    print("\nSimilarity Score:",
          round(result["score"], 4))

    print("Text:", result["text"])

7. Explanation of the Code

Step 1: Document Loading

Three sample documents related to Artificial Intelligence, Machine Learning, and Deep Learning are stored in a Python list.

Step 2: Text Chunking

The documents are divided into smaller chunks.

The Gemini token-counting API is used to estimate the number of tokens in each candidate chunk. The program attempts to keep each chunk within the specified 200-token limit.

Step 3: Embedding Generation

The Gemini embedding model "gemini-embedding-001" converts each text chunk into a numerical vector.

For example:

"Machine Learning is a subset of AI"

is converted into a numerical embedding representation.

Step 4: In-Memory Vector Store

Each chunk and its embedding are stored together in a Python list.

The vector store contains:

- Chunk ID
- Original text
- Numerical embedding

This storage is temporary and exists only while the Python program is running.

Step 5: Cosine Similarity

Cosine similarity measures the similarity between two vectors.

The formula is:

[
\text{Cosine Similarity}(A,B)

\frac{A \cdot B}{|A||B|}
]

A higher score generally indicates greater similarity between the query and the document chunk.

Step 6: Document Retrieval

The user's query is converted into an embedding. The program compares it with stored document embeddings and retrieves the top two most similar chunks.

8. Sample Output

The output below is illustrative. Embedding dimensions and similarity scores should be checked against the actual API response.

Total documents: 3
Total chunks: 3

Embeddings generated successfully!

Embedding dimensions: 3072

User Query: What is machine learning?

Retrieved Documents:

Similarity Score: 0.82
Text: Machine Learning is a subset of Artificial Intelligence...

Similarity Score: 0.71
Text: Deep Learning is a subset of Machine Learning...

9. Observations

- Documents can be divided into smaller chunks for indexing.
- Gemini embedding models convert text into numerical vectors.
- Embeddings help represent the semantic meaning of text.
- Cosine similarity helps identify relevant document chunks.
- An in-memory vector store provides a simple way to store and retrieve embeddings.
- The retrieval process can provide relevant context for a RAG application.

10. Result

Successfully implemented the basic data indexing process for RAG using the Google Gemini API. Documents were loaded, split into chunks, converted into embeddings, stored in memory, and retrieved based on semantic similarity.

Note: This experiment implements the indexing and retrieval foundation of RAG. It does not yet generate a final answer using retrieved context.

---

Viva Questions and Answers

Experiment 1: JSON/YAML Generation

1. What is JSON?

JSON is a lightweight data format used to store and exchange structured information.

2. What is YAML?

YAML is a human-readable data serialization format commonly used for configuration files.

3. What is the difference between JSON and YAML?

JSON uses braces, brackets, and commas, whereas YAML primarily uses indentation to represent structured data.

4. What is prompt engineering?

Prompt engineering is the process of designing effective instructions to guide an AI model toward the desired output.

5. Why do we validate generated JSON?

Validation ensures that the generated output follows valid JSON syntax and can be processed by applications.

6. What is "json.loads()"?

It converts a JSON-formatted string into a Python object.

7. What is "yaml.safe_load()"?

It parses YAML data into Python objects using a safer loading method.

8. What is iterative refinement?

It is the process of improving an AI response by providing additional instructions based on errors or missing requirements.

9. Why is schema validation required?

It checks whether the generated data contains the expected fields and data types.

10. Which Gemini model is used in this experiment?

Gemini 2.5 Flash.

Experiment 2: Basic Data Indexing for RAG

1. What is RAG?

RAG stands for Retrieval-Augmented Generation. It retrieves relevant external information to provide context for an AI-generated response.

2. What is an embedding?

An embedding is a numerical vector representation of text or other data.

3. Why do we split documents into chunks?

Chunking makes large documents easier to process, index, and retrieve.

4. What is a vector store?

A vector store stores numerical embeddings and associated information for similarity-based retrieval.

5. What is cosine similarity?

Cosine similarity measures the similarity between two vectors based on the angle between them.

6. Which embedding model is used?

Google Gemini's "gemini-embedding-001".

7. Why are embeddings useful in RAG?

They allow the system to retrieve semantically relevant information rather than relying only on exact keyword matching.

8. What is the purpose of NumPy?

NumPy is used for numerical operations, vector calculations, and cosine similarity.

9. What is the difference between indexing and retrieval?

Indexing prepares and stores document embeddings. Retrieval finds the most relevant stored chunks for a given query.

10. Is this a complete RAG system?

No. It implements the basic indexing and retrieval stages. A complete RAG system also passes the retrieved context to a generative model to produce an answer.

---

Overall Conclusion

In Set-8, two important Generative AI concepts were implemented using the Google Gemini API.

1. JSON/YAML Generation: Generated structured datasets using Gemini and validated them using Python parsers. Iterative refinement was used to correct invalid outputs.
2. Basic Data Indexing for RAG: Loaded documents, divided them into chunks, generated embeddings, stored them in an in-memory vector store, and retrieved relevant information using cosine similarity.

These experiments demonstrate how Generative AI can generate structured data and how embedding-based retrieval can be used to build the foundation of Retrieval-Augmented Generation systems.

---

References

1. Google Gemini API Documentation: https://ai.google.dev/gemini-api/docs
2. Google AI Studio: https://aistudio.google.com/
3. Python JSON Documentation: https://docs.python.org/3/library/json.html
4. PyYAML Documentation: https://pyyaml.org/wiki/PyYAMLDocumentation
5. NumPy Documentation: https://numpy.org/doc/
6. Retrieval-Augmented Generation: https://arxiv.org/abs/2005.11401


#
