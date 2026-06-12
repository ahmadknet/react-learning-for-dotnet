A **prompt** is the instruction, question, or input that you give to an LLM.

### Simple Examples

**Prompt:**

> What is the capital of India?

**Response:**

> New Delhi.

---

**Prompt:**

> Write a C# program to reverse a string.

**Response:**

```csharp
string input = "Hello";
char[] arr = input.ToCharArray();
Array.Reverse(arr);
Console.WriteLine(new string(arr));
```

---

### Types of Prompts

#### 1. Question Prompt

```text
What is dependency injection in .NET?
```

#### 2. Instruction Prompt

```text
Explain microservices in simple terms.
```

#### 3. Role-Based Prompt

```text
Act as a Senior .NET Architect and explain CQRS.
```

#### 4. Few-Shot Prompt

Provide examples before asking the model to perform a task.

```text
English: Hello
French: Bonjour

English: Thank you
French:
```

#### 5. Chain-of-Thought Style Prompt

Ask for a step-by-step explanation.

```text
Explain how an HTTP request travels from browser to server step by step.
```

---

### Prompt Engineering

**Prompt Engineering** is the skill of writing better prompts to get better results from an LLM.

Example:

❌ Weak Prompt:

```text
Teach me Azure.
```

✅ Better Prompt:

```text
You are an Azure Solution Architect.

I am a Senior .NET Developer with 10+ years of experience.

Teach me Azure from beginner to architect level.
Focus on App Services, Functions, Storage Accounts, Service Bus, AKS, and Azure DevOps.
Provide practical examples and interview questions.
```

The second prompt gives:

* A role
* User background
* Scope
* Expected output

So the response is usually much better.

### Prompt Formula

A useful structure is:

```text
Role
+
Context
+
Task
+
Constraints
+
Output Format
```

Example:

```text
Role:
You are a Senior .NET Architect.

Context:
I have 10 years of .NET experience and want AI/Cloud roles.

Task:
Explain Azure Service Bus.

Constraints:
Use simple language and real-world examples.

Output:
1. Concept
2. Architecture
3. C# Example
4. Interview Questions
```

This often produces more focused and useful answers.

### In AI Terms

```text
Prompt  →  LLM  →  Response
```

The quality of the prompt heavily influences the quality of the response. That's why prompt engineering has become an important skill when working with LLMs such as GPT-4, GPT-5, Claude, and Gemini.
