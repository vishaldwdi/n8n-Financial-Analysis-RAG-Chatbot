# n8n-Financial-Analysis-RAG-Chatbot
This n8n workflow analyzes company quarterly earnings using OpenAI, Gemini AI, &amp; Pinecone. It extracts data from earnings report PDFs, answers financial questions, &amp; creates structured reports in Google Docs.

This n8n workflow creates a financial analysis tool that generates reports on a company's quarterly earnings using the capabilities of OpenAI GPT-4o-mini, Google's Gemini AI and Pinecone's vector search. By analyzing PDFs of any company's earnings reports from their Investor Relations page, this workflow can answer complex financial questions and automatically compile findings into a structured Google Doc.

**How it works:**

**Data loading and indexing**

*   Fetches links to PDF earnings document from a Google Sheet containing a list of file links.
*   Downloads the PDFs from Google Drive.
*   Parses the PDFs, splits the text into chunks, and generates embeddings using the Embeddings Google AI node (text-embedding-004 model).
*   Stores the embeddings and corresponding text chunks in a Pinecone vector database for semantic search.

**Report generation with AI agent**

*   Utilizes an AI Agent node with a specifically crafted system prompt. The agent orchestrates the entire process.
*   The agent uses a Vector Store Tool to access and retrieve information from the Pinecone database.

**Report delivery**

*   Saves the generated report as a Google Doc in a specified Google Drive location.

**Set up steps**

**Google Cloud Project & Vertex AI API:**

*   Create a Google Cloud project.
*   Enable the Vertex AI API for your project.

**Google AI API key:**

*   Obtain a Google AI API key from Google AI Studio.

**Pinecone account and API key:**

*   Create a free account on the Pinecone website.
*   Obtain your API key from your Pinecone dashboard.
*   Create an index named company-earnings in your Pinecone project.

**Google Drive - download and save financial documents:**

*   Go to a company you want to analyze and download their quarterly earnings PDFs
*   Save the PDFs in Google Drive
*   Create a Google Sheet that stores a list of file URLs pointing to the PDFs you downloaded and saved to Google Drive

**Configure credentials in your n8n environment for:**

*   Google Sheets OAuth2
*   Google Drive OAuth2
*   Google Docs OAuth2
*   Google Gemini(PaLM) Api (using your Google AI API key)
*   Pinecone API (using your Pinecone API key)

**Import and configure the workflow:**

*   Import this workflow into your n8n instance.
*   Update the List Of Files To Load (Google Sheets) node to point to your Google Sheet.
*   Update the Download File From Google Drive to point to the column where the file URLs are
*   Update the Save Report to Google Docs node to point to your Google Doc where you want the report saved.
