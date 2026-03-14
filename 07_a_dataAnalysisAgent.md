Use Case 1: Data Analysis Agent (DATA_AGENT.md) Problem: Query BigQuery, interpret results, generate insights.

[User Query] → [LLM Reasoning] → [BigQuery API] → [Result Interpretation] → [Report Generation]

Google Cloud Services: Vertex AI + BigQuery.

Interview Angle: “This shows how agents combine reasoning with tool use to automate analytics.”

# Data Analysis Agent (DATA_AGENT.md)

## Problem Statement
Students and professionals often need to query large datasets, interpret results, and generate insights quickly.  
An **Agentic AI Data Agent** automates this process by combining reasoning with tool use—querying BigQuery, analyzing results, and producing summaries or reports.

## Architecture Diagram (Flow)
[ User Query ]
↓
[ LLM Reasoning (Vertex AI) ]
↓
[ BigQuery API Call ]
↓
[ Result Interpretation ]
↓
[ Report Generation ]
↓
[ Reflection & Feedback Loop ]

## Workflow Explanation
1. **Perception**: The agent receives a user query (e.g., “Show average sales by region”).  
2. **Reasoning**: Vertex AI LLM interprets the query and plans the steps.  
3. **Action**: The agent calls the BigQuery API to execute SQL queries.  
4. **Interpretation**: Results are analyzed and converted into human‑readable insights.  
5. **Reflection**: If results are incomplete or errors occur, the agent retries or adjusts the query.  
6. **Output**: A concise report or visualization is generated for the user.

## Minimal Python Example

```python
from google.cloud import bigquery
from vertexai.preview.language_models import ChatModel

# Initialize BigQuery client
bq_client = bigquery.Client()

# Example query
query = """
SELECT region, AVG(sales) as avg_sales
FROM `project.dataset.sales_data`
GROUP BY region
LIMIT 10
"""

# Run query
query_job = bq_client.query(query)
results = query_job.result()

# Collect results
output = []
for row in results:
    output.append(f"Region: {row.region}, Avg Sales: {row.avg_sales}")

# Initialize Vertex AI Chat Model
chat_model = ChatModel.from_pretrained("chat-bison")
chat = chat_model.start_chat()

# Use LLM to interpret results
response = chat.send_message(
    "Summarize these sales results:\n" + "\n".join(output)
)

print("Agentic AI Report:")
print(response.text)
