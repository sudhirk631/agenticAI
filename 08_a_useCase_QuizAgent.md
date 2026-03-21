# Use Case Description
The use is to build an agent which administers interactive learning quiz with an agentic AI workflow. The agent assesses a user's knowledge on a specific topic 
and it uses a persistent session state and long-term memory to create a personalized experience. The agent maintains a history of the user's answers, which lets 
it dynamically adjust the difficulty and content of subsequent questions. 
# Architecture

![Architecture Diagram](images/quizAgent_architecture_diagram.png)

## The architecture shows the following data flow:
1. A user performs an action, such as starting a quiz or submitting an answer, within the quiz application that is hosted on Cloud Run.
2. The application forwards the user's input to the AI agent.
3. The AI agent uses the Gemini model on Vertex AI to interpret the user's input. Based on the user's request, the agent calls the appropriate tools to perform the requested quiz action.
   For example, the agent selects a tool to start a quiz session, evaluate an answer, or generate the next question.
4. The agent sends the response to the quiz application.
5. The quiz application forwards the response to the user.

## To maintain the quiz's state and personalize the experience, the agent performs the following background tasks:
1. The agent appends the latest quiz progress and score to the history of the saved session that's stored in Vertex AI Agent Engine Sessions.
2. The agent transforms quiz data into memories and stores them in Memory Bank for long-term recall. The agent uses the historical data that's stored in memory to generate context-aware responses in future sessions.

## Technical stack
1. Cloud Run: A serverless compute platform that lets you run containers directly on top of Google's scalable infrastructure.
2. Agent Development Kit (ADK): A set of tools and libraries to develop, test, and deploy AI agents.
3. Vertex AI: An ML platform that lets you train and deploy ML models and AI applications, and customize LLMs for use in AI-powered applications.
4. Vertex AI Agent Engine Sessions: A persistent storage service that saves and retrieves the history of interactions between a user and agents.
5. Memory Bank: A persistent storage service that generates, refines, manages, and retrieves long-term memories based on a user's conversations with an agent.
