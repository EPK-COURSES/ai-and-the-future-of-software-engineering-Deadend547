# Risks, Ethics, and Limitations of AI


## 1. Secuirty Vulnerability and Code Quality
A big risk of using LLMs for writing and reviewing code is the introduction of subtle but very critical  
security flaws.

### 1.1 Baseline
Studies across multiple papers show that AI agents write vulnerable code in 40% of cases in  
secuirty relevant tasks(Negri-Ribalta et al., 2024; TechRxiv, 2026).
### 1.2 Language Specific Vulnerabilities
Language Standards dictate risk profiles. Low level lanuguages like assembly, C, and C++ suffer a  
lot from AI generated code due to issues such as memory safety. This is because Agents lack the  
awareness that humans have to catch these errors(Negri-Ribalta et al., 2024; Shukla et al., 2025).  
In analyses of many different repositories,  Python code had around a 15% higher vulnerability density  
than Javascript or Typescript(Schreiber & Tippe, 2025). These usually revolved around insecure  
default configs and injection flaws(Nelson, 2025).
### 1.3 AI Feedback Loops
In most cases Developers never take AI code "as is". Usually they use follow up prompts to improve  
the code. However experiments show a ~40% increase in critical vulnerabilities after just 5 prompts  
without human intervention(Shukla et al., 2025). It is important to note that this is below the average  
number of prompts for large applications where these vulnerabilities are most  impactful. Studies show  
that prompts to "optimize" the code, frequently cause AI agents to sacrifice code security for this gained  
efficiency.
### 1.4 Cross-File Errors
AI tools and agents are often restricted to single file contexts, this causes these agents to miss critical  
context. Thus around 7% of security vulnerabilities happen in config files, like dockerfiles, YAML and  
build scripts.
### 1.5 Context Loss
As mentioned previously developers rarely take AI code "as is" and often iterate upon it. The way  
these AI tools actually work is when you prompt something, the entire conversation history is sent to  
be proccessed. After many prompts, this can cause the context window to be polluted with so many  
tokens that the AI starts to spit out code and make changes that it wasn't asked to make. The solution  
developers usually use to circumvent this is to copy paste the code into a new context window,  
however this comes with its own side effects. Developers may have given the AI some very critical  
instructions for it to follow in the previous context window which they forget to prompt again and thus  
the AI is now performing behavior that the developer doesn't expect it to.


## 2. Hallucinations and Maintenance

### 2.1 Dependency Hallucinations
AI tools frequently reference outdated or even entirely non-existent software libraries and APIs that at  
best lead to build/compilation issues and at worst references to unvetted libraries that open up the  
software to a whole world of security risks. Outdated packages can also lead to maintenance nightmares  
later down the line due to undefined behaviors in these depracated packages(M. S. Patel et al.). 
### 2.2 Code Bloat and (lack of) modularity
Analyses of AI tools show that they lack holistic context, that meaning that they can't understand  
the software as a whole. This leads these tools to generating bloated code that lacks long term  
modularity(TechRxiv, 2026). This phenomenon creates "black box" systems where developers struggle  
to implement later updates.
### 2.3 Comprehension Debt
This is a new type of technical debt that has come about due to the rapid adoption of AI tools  
(M. S. Patel et al.). This term refers to code that works in production but cannot be verified or modified  
by human developers because often they skipped the work of actually writing it, in some cases a specific  
piece of code may have never even been seen by a human before(M. S. Patel et al.). 