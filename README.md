# Chat With Your Data: 10-Q Financial Analysis Chatbot

A retrieval-augmented generation (RAG) chatbot built on Microsoft Foundry and Azure AI Search that answers plain-language questions about a company's 10-Q quarterly financial filing, with cited references. Built as Project 1 of the Udacity Azure Generative AI Engineer Nanodegree.

## Overview

The chatbot lets an analyst ask questions about a dense 10-Q filing and get grounded, cited answers covering financial performance, business operations, risk factors, and management discussion.

**Data source:** The Walt Disney Company Form 10-Q for the quarter ended June 27, 2026, from the SEC's EDGAR database:
https://www.sec.gov/Archives/edgar/data/1744489/000174448926000057/dis-20260627.htm

## Azure Services Used

| Service | Role |
| --- | --- |
| Resource Group | Container for all project resources |
| Azure Blob Storage | Stores the 10-Q document (HTML) |
| Azure AI Search | Indexes the document with vector search and semantic ranking |
| Azure OpenAI in Foundry: GPT-4.1-mini | Generates answers from retrieved content |
| Azure OpenAI in Foundry: text-embedding-ada-002 | Creates embeddings for vector search |
| Foundry Agent Service + Foundry IQ | Hosts the chatbot agent and connects it to the search index as a knowledge base |

## How It Works

1. The 10-Q is uploaded to Blob Storage.
2. The Azure AI Search import wizard chunks the document and creates embeddings with text-embedding-ada-002.
3. A Foundry IQ knowledge base connects the search index to the `SEC-Chatbot` agent.
4. When a user asks a question, relevant sections are retrieved from the index.
5. GPT-4.1-mini generates a concise answer grounded in the retrieved sections and cites its references.

## Implementation Note

Azure OpenAI "On Your Data," the original approach for this project, supports only GPT-4o models and is scheduled to retire on October 14, 2026. GPT-4o quota was unavailable on my subscription, so I implemented RAG with Foundry Agent Service and a Foundry IQ knowledge base backed by Azure AI Search, which is Microsoft's recommended replacement.

## Repository Contents

```
├── README.md
├── system-message.md                 # Agent instructions (system message)
├── prompts.md                        # 5 tested prompts
└── Evidence/
    ├── 01-system-configuration.png   # Model and parameter configuration
    ├── 02-system-message.png         # System message configuration
    ├── 03-chat-application.png       # Working chat application
    ├── 04a-prompt-1.png              # Prompts and responses with references
    ├── 04b-prompt-2.png
    ├── 04c-prompt-3.png
    ├── 04d-prompt-4.png
    ├── 04e-prompt-5.png
    ├── 05-prompt-response.png        # Single prompt response
    ├── 06-indexing-complete.png      # AI Search indexer run: Success
    ├── 07-ai-search-service.png      # AI Search service overview
    └── 08-model-deployments.png      # GPT-4.1-mini and ada-002 deployments
```

## Prompt Categories

The prompts in `prompts.md` were tested against the filing and cover:

- Financial performance
- Business operations
- Risk factors
- Management discussion and analysis

## Author

Samira Ray
