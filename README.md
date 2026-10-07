# Chat With Your Data: 10-Q Financial Analysis Chatbot

A retrieval-augmented generation (RAG) chatbot built with Azure OpenAI Service that answers questions about a company's 10-Q quarterly financial filing. Built as Project 1 of the Udacity Azure Generative AI Engineer Nanodegree.

## Overview

The chatbot lets an analyst ask plain-language questions about a dense 10-Q filing and get grounded answers with references to the source document, covering financial performance, business operations, risk factors, and management discussion.

**Data source:** The Walt Disney Company Form 10-Q for the quarter ended June 27, 2026, from the SEC's EDGAR database:
https://www.sec.gov/Archives/edgar/data/1744489/000174448926000057/dis-20260627.htm

## Azure Services Used

| Service | Role |
| --- | --- |
| Resource Group | Container for all project resources |
| Azure Blob Storage | Stores the 10-Q document |
| Azure AI Search | Indexes the document, with vector search for semantic retrieval |
| Azure OpenAI Service: GPT-4 | Generates answers from retrieved content |
| Azure OpenAI Service: text-embedding-ada-002 | Creates embeddings for vector search |
| Azure AI Foundry portal | Model deployment, data connection, and testing |

## How It Works

1. The 10-Q is uploaded to Blob Storage.
2. Azure AI Search indexes the document and creates embeddings with text-embedding-ada-002.
3. When a user asks a question, relevant sections are retrieved from the index.
4. GPT-4 generates an answer grounded in the retrieved sections and cites its references.

## Repository Contents

```
├── README.md
├── prompts.md                      # 5+ tested prompts
└── screenshots/
    ├── 01-system-configuration.png # GPT model and parameter configuration
    ├── 02-system-message.png       # System message configuration
    ├── 03-chat-application.png     # Working chat application
    ├── 04-prompts-and-responses.png# Prompts with responses and references
    └── 05-prompt-response.png      # Single prompt response
```

## Prompt Categories

The prompts in `prompts.md` were tested against the filing and cover:

- Financial performance
- Business operations
- Risk factors
- Management discussion and analysis

## Author

Samira Ray
