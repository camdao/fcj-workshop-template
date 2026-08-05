---
title: "AWS FCAJ Agent Forge - Deepdive"
date: 2026-08-01
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---


# Learning Report: "AWS FCAJ Agent Forge - Deepdive (Day 1)"


### Event Purpose


The workshop was organized to help participants:


- Understand foundational concepts of **Agentic AI** and AI Agents.
- Learn how to build and deploy AI Agents for **production** environments using **Amazon Bedrock AgentCore**.
- Master the architecture, lifecycle, and components of an AI Agent system.
- Practice using tools, security processes, and techniques necessary for developing AI Agents.
- Explore real-world applications of AI Agents in process automation and solving business problems.


### Workshop Format


This is a **3-day workshop series**, designed with a progression from foundational knowledge to deploying AI Agents in production environments using Amazon Bedrock AgentCore.


- **Day 1 (08/01): AgentCore Foundations**  
  Learn the overall architecture of Amazon Bedrock AgentCore, including **Runtime**, **Gateway**, and **Identity**, along with foundational concepts for building AI Agents.


- **Day 2 (08/08): Memory, Evaluations, Observability & Optimization**  
  Explore how to manage **Memory**, evaluate AI Agent effectiveness (**Evaluations**), monitor systems (**Observability**), and optimize performance (**Optimization**).


- **Day 3 (08/15): DevOps, Policies & Production Best Practices**  
  Learn about **DevOps** processes for AI Agents, building **Policies**, applying security measures, and **best practices** for deploying AI Agents in production environments.


---


## Key Highlights


### 1. Overview of Agentic AI


#### What is Agentic AI?


**Agentic AI** refers to artificial intelligence systems capable of **autonomously executing towards a goal** rather than simply responding to individual user commands. After receiving a goal, Agentic AI can independently plan, select tools, execute necessary steps, and evaluate results to complete tasks.


Key characteristics of Agentic AI:


- **Planning**: Breaking down complex tasks into specific action steps.
- **Decision-making**: Choosing appropriate actions based on context and goals.
- **Tool usage**: Calling APIs, searching for information, accessing databases, or using external services.
- **Self-execution**: Performing multiple consecutive steps with minimal human intervention.
- **Evaluation and adjustment**: Checking results after each step and modifying plans when necessary.


**Example:** A user requests *"Deploy application to AWS"*. Instead of just providing step-by-step instructions, Agentic AI can autonomously build the application, create a Docker image, push the image to a container registry, deploy to the cloud service, check system status, and report final results.


#### Levels of Autonomy


The workshop categorizes AI agents across an autonomy spectrum:


1. **Deterministic agents**: Operate according to fixed rules.  
   *Example:* Automatically format source code or run CI workflows based on preset configurations.


2. **Reactive agents**: React to input without planning ahead.  
   *Example:* GitHub Copilot generates code when a programmer enters a request.


3. **Goal-oriented agents**: Plan to achieve objectives.  
   *Example:* AI receives a request to "Add payment functionality" then autonomously analyzes, writes code, creates APIs, and tests.


4. **Learning agents**: Learn from experience and improve.  
   *Example:* AI remembers previous deployment errors to select more effective solutions in future attempts.


5. **Multi-agent systems**: Multiple agents coordinate with each other.  
   *Example:* Coding Agent, Testing Agent, Security Agent, and DevOps Agent collaborate to complete a software project.
---
### 2. Amazon Bedrock AgentCore


#### Overview


**Amazon Bedrock AgentCore** is an AWS service that supports building, deploying, and operating AI Agents in production environments. The service provides fully managed infrastructure, allowing developers to focus on agent logic rather than managing servers or infrastructure.


Notable capabilities of AgentCore:


- **Serverless Runtime**: Provides execution environment without infrastructure management.
- **Auto-scaling**: Automatically scales resources up or down based on traffic.
- **Integrated security**: Supports authentication, authorization, and integration with AWS security services.
- **AI Agent lifecycle management**: Supports development, testing, deployment, and operation in production environments.


#### Benefits


- **Reduced operational costs** through serverless architecture and AWS-managed infrastructure.
- **Increased scalability** to handle varying request volumes over time.
- **Ensured security** with built-in authentication and authorization mechanisms.
- **Pay-per-use pricing**, only paying for actual resources or executions.
- **Shortened development time** through rapid deployment and testing processes.
---
### 3. Runtime Environment


#### Agent Execution Model


**Amazon Bedrock AgentCore Runtime** provides a fully managed execution environment (runtime) for running AI Agents in production environments.


Key features:


- **Serverless Runtime**: Agents are launched on-demand, with no server management or provisioning required.
- **Firecracker MicroVM**: Each agent execution occurs in an isolated **Firecracker MicroVM**, enhancing security and ensuring consistent execution environment.
- **Auto-scaling**: Runtime automatically scales resources up or down based on request volume.
- **Session management**: Supports maintaining agent state throughout processing.


#### Memory Management


Runtime supports multiple memory management mechanisms to help AI Agents maintain context and perform multi-step tasks:


- **Session Memory**: Stores context within a session or conversation.
- **Long-term Memory**: Stores long-term information for reuse in future sessions.
- **Context Management**: Manages and optimizes the amount of context passed to language models.


#### Streaming Data Processing


AgentCore Runtime supports real-time responses to improve user experience:


- **Streaming Response**: Returns results incrementally as they're generated rather than waiting for complete processing.
- **Progress Updates**: Displays status or processing steps of the agent during execution.
- **Reduced perceived latency**: Users receive earlier responses for tasks with long processing times.
---
### 4. Identity & Security


#### Authentication & Authorization


Amazon Bedrock AgentCore provides authentication and authorization mechanisms to help AI Agents access resources securely.


- **JSON Web Token (JWT)**: Authenticates users or applications using tokens.
- **Amazon Cognito**: Manages identity and user authentication.
- **AWS IAM**: Controls AI Agent access to AWS resources following the **least privilege** principle.
- **Service-to-Service Authentication**: Secure authentication when AI Agents communicate with other services or APIs.


#### Tool Call Security


When AI Agents use external tools or APIs:


- Only granted access to necessary resources (**Least Privilege**).
- Each tool or API can have separate authorization policies applied.
- Activities are logged through **AWS CloudTrail** for auditing and monitoring.
- Data is encrypted during transmission using **HTTPS/TLS**.


#### Security Best Practices


For deploying AI Agents in production environments, AWS recommends:


- Deploy within **Amazon VPC** when network isolation is needed.
- Store API keys and sensitive information using **AWS Secrets Manager**.
- Apply **Least Privilege** principle for all IAM Roles and Policies.
- Monitor activities using **Amazon CloudWatch** and **AWS CloudTrail** for incident detection and audit support.
---
### 5. Gateway & Middleware


#### AgentCore Gateway


**Amazon Bedrock AgentCore Gateway** is an intermediary layer that helps AI Agents connect with external tools, APIs, and services securely and consistently.


Key functions:


- **Request routing**: Routes AI Agent requests to the correct API or service.
- **API management**: Supports connections with various service types and protocols.
- **Authentication and authorization**: Controls access before AI Agents call tools.
- **Monitoring**: Records and tracks requests between AI Agents and external systems.


#### Human-in-the-Loop (HITL)


For critical tasks, AI Agents can request human approval before proceeding.


Examples:


- Approving financial transactions.
- Confirming bulk email or notification sends.
- Reviewing content before publication.


#### Middleware


Middleware helps AI Agents communicate effectively with other systems.


Common functions:


- **Data transformation** between AI Agents and APIs.
- **Caching** to reduce API calls and improve performance.
- **Retry and Error Handling** when external services encounter temporary errors.
- **Logging and Monitoring** to support oversight and troubleshooting.


### 6. Hands-on Practice


#### 6.1. Getting Familiar with Kiro IDE


In the first part of the workshop, participants practiced installing and configuring the development environment with **Kiro**. They also learned about AI-assisted programming features and used **Steering** to guide how AI generates code according to project requirements.


Practice content included:


- Installing and setting up the Kiro environment.
- Exploring AI-assisted programming features.
- Setting up Steering to guide code generation.
- Practicing creation, editing, and code explanation with AI assistance.


---


#### 6.2. Building and Deploying AI Agent Practice


Participants practiced following workshop instructions to initialize and deploy an AI Agent using **Amazon Bedrock AgentCore CLI**, while learning the deployment process for Agents to execution environments.


Practice content included:


- Initializing AI Agent project using AgentCore CLI.
- Practicing deploying Agent to Amazon Bedrock AgentCore.
- Testing the Agent's request reception and processing.
- Observing Agent workflow after deployment.


---


#### 6.3. Returns & Refunds Agent Practice


The workshop guided participants in building an AI Agent to handle return and refund requests, illustrating the process of solving a business problem.


Practice content included:


- Building Returns & Refunds Agent following instructions.
- Learning the return request processing workflow.
- Testing conversation flow between users and AI Agent.
- Observing how the Agent uses tools to handle requests.


---


#### 6.4. Persistent Memory Practice


Participants practiced configuring **Persistent Memory** so AI Agents can store and reuse information across multiple sessions.


Practice content included:


- Configuring Persistent Memory for Agent.
- Storing and retrieving conversation information.
- Testing information retention between sessions.
- Observing memory's impact on Agent response quality.


---


#### 6.5. Connecting DynamoDB and Knowledge Base Practice


The workshop guided connecting AI Agents with data sources to enhance information retrieval and response capabilities.


Practice content included:


- Connecting Agent with Amazon DynamoDB.
- Integrating Knowledge Base.
- Practicing data retrieval for request processing.
- Testing Agent response capabilities based on connected data.


---


#### 6.6. Web Chat Interface Development Practice


Participants practiced deploying a Web Chat interface to interact with AI Agent following workshop instructions.


Practice content included:


- Deploying interface using Streamlit.
- Integrating Amazon Cognito for user authentication.
- Connecting interface with AI Agent.
- Testing interaction between users and AI Agent.


---


#### 6.7. Observing and Evaluating Agent Performance


The workshop introduced tools supporting monitoring and quality assessment of AI Agent operations on Amazon Bedrock AgentCore.


Practice content included:


- Observing Logs, Traces, and GenAI Dashboard.
- Tracking Agent request processing.
- Practicing AgentCore Evaluations for response quality assessment.
- Analyzing evaluation results to identify improvement areas.


---


#### 6.8. AgentCore Policies Setup Practice


In the final workshop section, participants practiced configuring **AgentCore Policies** to control AI Agent access to tools and data sources.


Practice content included:


- Setting up AgentCore Policies.
- Configuring Agent access permissions for tools.
- Testing Agent operations after applying policies.
- Learning the role of security policies in AI Agent deployment.




---
## Key Learnings


After attending the workshop, I gained extensive knowledge about Agentic AI and Amazon Bedrock AgentCore, including:


### Technical Knowledge


- Understanding the **Agentic AI** concept and its differences from traditional AI applications.
- Grasping AI Agent autonomy levels, from **Deterministic Agent** to **Multi-Agent System**.
- Understanding **Amazon Bedrock AgentCore** architecture, including Runtime, Gateway, and Identity.
- Learning how AI Agents plan, use tools, and execute multiple steps to complete goals.
- Understanding security mechanisms like JWT, Amazon Cognito, IAM, and the **Least Privilege** principle.


### Deployment Knowledge


- Understanding the process of building and deploying AI Agents in production environments.
- Learning how to integrate AI Agents with external APIs and tools.
- Understanding the role of Human-in-the-Loop in tasks requiring human approval.
- Gaining knowledge of Prompt Engineering techniques and workflow optimization for AI Agents.


### Practical Lessons


- Design AI Agents with small functions before building complex systems.
- Always prioritize security and authorization when AI Agents access resources.
- Monitor, evaluate, and optimize AI Agents based on real-world results.
- Build AI Agents for easy scalability and maintainability.


---


## Workshop Experience


Participating in **Day 1 of AWS FCAJ Agent Forge – Deep Dive** provided me with a comprehensive overview of building and operating AI Agents in enterprise environments.


Through speaker presentations and illustrative content, I gained better understanding of AI Agent workflows, from analyzing requests, planning, using tools, to completing objectives. The workshop also helped me approach the **Amazon Bedrock AgentCore** architecture and important components like Runtime, Gateway, and Identity.


Beyond theory, I learned about real-world applications of AI Agents in process automation, customer support, and software development. I also learned Prompt Engineering techniques, workflow optimization methods, as well as security principles and AI Agent deployment in production environments.


The workshop provided substantial practical knowledge, helping me better understand Agentic AI development trends and establishing a foundation to continue researching specialized content in upcoming workshop sessions.


### Event Photos
![Event Photo 1](images/photo_01.jpg)


---


> **Overall Assessment:** Day 1 of **AWS FCAJ Agent Forge – Deep Dive** provided a solid foundation in **Agentic AI** and **Amazon Bedrock AgentCore**, helping participants understand everything from basic concepts to architecture and AI Agent deployment in production environments. The workshop combined theory, illustrative examples, and hands-on practice, while emphasizing important factors such as security, scalability, lifecycle management, and tool integration. This is a valuable program for those looking to build AI Agent systems that meet enterprise environment requirements.