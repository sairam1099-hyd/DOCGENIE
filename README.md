DOCGENIE
DocGenie — A hallucination-free n8n RAG AI Agent workflow that answimers questions strictly from your uploaded documents with exact quotes and human-escalation guardrails
DOCGENIE — AI DOCUMENT ASSISTANT (N8N WORKFLOW)
<img width="670" height="472" alt="image" src="https://github.com/user-attachments/assets/7ec9a56f-ac90-4d88-bdfc-753893d93187" />


WHAT IS DOCGENIE?
-----------------
DocGenie is an AI chatbot built using n8n that reads any uploaded document (like a company policy manual, PDF guide, or study notes) and answers questions using ONLY the information inside that file.

Normally, AI chatbots can guess or make up wrong answers when they do not know something. DocGenie is built to solve that problem: if the answer is in your document, it quotes or summarizes it accurately; if the answer is not in your document, it honestly says so and hands the user over to a human agent.


HOW IT WORKS (FLOWCHART)
<img width="396" height="535" alt="image" src="https://github.com/user-attachments/assets/1cbdb4e2-b592-409f-99d0-57320965cf1b" />


[Upload File] ─> [Break into Chunks & Save in Vector Database]
                                      ▲
[User Question] ─> [DocGenie AI] <─> [Search_the_Docs Tool]
                        │
        ┌───────────────┼───────────────┐
        ▼               ▼               ▼
   (Greeting)    (Answer Found)    (Not Found)
        ▼               ▼               ▼
  Polite Reply   Quote / Summary   Human Handoff


WHY THIS PROJECT STANDS OUT (KEY ENGINEERING HIGHLIGHTS)
--------------------------------------------------------
1. Prevents AI Hallucinations (Strict Grounding):
   The AI is locked to your uploaded file. It is forbidden from inventing rules, dates, prices, or policies.

2. Smart Intent Handling:
   - Simple Greetings ("Hi", "Hello"): Replies politely without wasting database searches.
   - Specific Questions ("What is the return window?"): Finds the exact sentence in the file and quotes it directly.
   - Broad Questions ("What is the refund policy?"): Pulls multiple relevant points and gives a clean summary.
   - Unknown Questions: Triggers a safe fallback message to pass the user to a human agent.

3. Strict Tool Parameter Control:
   Configured the AI Agent to pass strictly formatted inputs ({"input": "..."}) to the Search_the_Docs tool and limited it to one search per question for speed and reliability.

4. Clean User-Friendly Output:
   Eliminated raw backend JSON metadata (like "pageContent" and brackets) from the final response so users only see clean, readable plain text.


WHAT IS IN THIS REPOSITORY?
---------------------------
- DocGenie.json : The complete n8n workflow file containing the Chat Trigger, AI Agent, Vector Store retriever tool, and custom guardrail system prompt.


HOW TO TEST IT IN N8N (4 SIMPLE STEPS)
--------------------------------------
1. Download the DocGenie.json file from this repository.
2. Open n8n, create a new workflow, click the "..." menu (top-right), and select "Import from File...".
3. Connect your preferred AI Chat Model (OpenAI, Gemini, Groq, etc.) and Embeddings/Vector Store nodes.
4. Upload any PDF or text file into the document loader, open the n8n Chat window, and start asking questions!
