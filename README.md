# Denver Health Leader Navigator

**Version:** Demo v1.0  
**Client:** Denver Health & Hospital Authority (DHHA)  
**Purpose:** AI-powered web tool that helps Denver Health leaders navigate employee relations using official Denver Health guidance only.

---

## What This Tool Does

Denver Health Leader Navigator allows leaders to:

1. Ask natural-language questions about leadership, coaching, feedback, engagement, pay conversations, and administrative leave
2. Receive answers grounded **only** in Denver Health documents
3. See responses that reference Denver Health frameworks and terminology
4. Be explicitly directed to their HRBP when guidance is not available or escalation is required

This tool **does not replace HR** and **does not invent policy**.

---

## Core Rules (Non-Negotiable)

- Uses **Denver Health documents only**
- Never provides generic HR advice
- Never invents policies or procedures
- Explicitly directs leaders to their HRBP when information is missing
- Uses Denver Health terminology:
  - Leader
  - Team Member / Employee
  - HRBP
  - DHHA

---

## Technology Stack

| Layer | Technology |
|-----|------------|
| Frontend | HTML + React (CDN) |
| Backend | Vercel Serverless Functions (Node ≥18) |
| AI Model | Google Gemini (`gemini-1.5-flash`) |
| Knowledge Base | JavaScript file with searchable document chunks |
| Hosting | Vercel (Free Tier) |

---

## Project Structure

denver-health-navigator/
├── api/
│ └── chat.js # Backend API (search + Gemini)
├── data/
│ └── knowledge-base.js # Denver Health document chunks
├── public/
│ └── index.html # Frontend chat UI
├── package.json # Project metadata
├── vercel.json # Deployment configuration
└── README.md # This file


---

## Knowledge Base

The knowledge base consists of extracted content from official Denver Health documents, chunked and indexed for search.

Documents included:
1. Leader Resource Guide
2. Denver Health Coaching Model (4 Cs)
3. Administrative Leave Tip Sheet
4. Leadership Norms and Definitions
5. What is Feedback
6. What is LEAD

Each chunk includes:
- Source document
- Section title
- Content type (overview, policy, procedure, script, etc.)
- Searchable tags
- Exact text from the document (no paraphrasing)

---

## Backend API

### Endpoint
POST /api/chat


### Request Body
```json
{
  "messages": [
    { "role": "user", "content": "How do I give feedback to an employee?" }
  ]
}
Response Body
{
  "content": [
    { "text": "AI-generated response grounded in Denver Health content" }
  ]
}``


### Behavior Guarantees

-   If **no relevant Denver Health content** is found, the API returns:
    
    > "I don't have specific Denver Health guidance on this topic. Please consult your HRBP for assistance."
    
-   The Gemini API is **not called** when no relevant context exists.
    
-   Errors are handled gracefully and safely.
    

----------

## Environment Variables

One environment variable is required.

### Required

`GOOGLE_API_KEY` 

This must be set in the **Vercel Dashboard**:

1.  Go to your Vercel project
    
2.  Settings → Environment Variables
    
3.  Add:
    
    -   Name: `GOOGLE_API_KEY`
        
    -   Value: your Google Gemini API key
        
    -   Environment: Production (and Preview if needed)
        

----------

## Deployment Instructions (Vercel)

### 1. Prepare Repository

Ensure the project folder structure matches exactly as shown above.

### 2. Deploy

You may deploy via:

-   Vercel Dashboard (Import Git repository), or
    
-   Vercel CLI (`vercel`)
    

No build step is required.

### 3. Verify Deployment

After deployment:

-   Visit the root URL → loads the chat UI
    
-   Test `/api/chat` via the UI
    
-   Ask a known question (e.g., Coaching, Feedback)
    
-   Ask an unknown question → confirm HRBP fallback message appears
    

----------

## Demo Scope & Limitations

This demo **does not include**:

-   ABP disciplinary process
    
-   PIP procedures
    
-   Termination guidance
    
-   Documentation templates
    
-   Legal interpretation
    
-   Decision rules for when to involve HR
    

For all such topics, the system will direct leaders to their HRBP.

----------

## Intended Audience

-   Denver Health Leaders
    
-   Supervisors and Managers (referred to as Leaders)
    
-   Employee Relations partners (for demo and validation)
    

----------

## Ownership & Disclaimer

This tool is a **decision-support assistant**, not a policy authority.

Final decisions, investigations, and employee relations actions remain the responsibility of:

-   Leaders
    
-   HR Business Partners
    
-   Denver Health leadership
    

----------

## Demo Version Notice

**Demo v1.0**

Built for demonstration and stakeholder review.  
Not approved for production use without Denver Health validation and governance review.
