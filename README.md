# AI-agent
to make own ai agent
pip install crewai langchain-openai
export OPENAI_API_KEY="your-api-key-here"
import os
from crewai import Agent, Task, Crew, Process
from langchain_openai import ChatOpenAI

# 1. Initialize the LLM (Default: GPT-4o)
llm = ChatOpenAI(model="gpt-4o", temperature=0.7)

# 2. Define the Agent and its persona
research_agent = Agent(
    role="Senior Research Analyst",
    goal="Uncover groundbreaking insights and analyze complex data trends",
    backstory="""You are a world-class researcher. You excel at taking broad, 
    complex topics and distilling them into highly accurate, structured actionable insights.""",
    verbose=True,
    llm=llm,
    allow_delegation=False
)

# 3. Define the specific task to execute
research_task = Task(
    description="Analyze the top 3 emerging trends in artificial intelligence for 2026.",
    expected_output="A bulleted report highlighting the trend name, impact, and a real-world example.",
    agent=research_agent
)

# 4. Assemble the Crew and kick off the autonomous loop
crew = Crew(
    agents=[research_agent],
    tasks=[research_task],
    process=Process.sequential
)

print("### AGENT STARTING WORK ###")
result = crew.kickoff()
print("\n### FINAL AGENT OUTPUT ###")
print(result)
python agent.py
