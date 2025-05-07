{
  "active": false,
  "connections": {
    "MCP Get Notion Tools": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "When chat message received": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "MCP Search Notion Database": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Simple Memory": {
      "ai_memory": [
        [
          {
            "node": "AI Agent",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-05-06T13:10:22.760Z",
  "id": "gSwy3pUcXBLyBeBv",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "Facebook Ad MCP",
  "nodes": [
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.9,
      "position": [
        260,
        0
      ],
      "id": "334bdf03-5330-42c5-b339-dc0882693d1a",
      "name": "AI Agent"
    },
    {
      "parameters": {},
      "type": "n8n-nodes-mcp.mcpClientTool",
      "typeVersion": 1,
      "position": [
        400,
        300
      ],
      "id": "ed85b4cf-af10-4345-81a7-1a773b00fbe2",
      "name": "MCP Get Notion Tools",
      "credentials": {
        "mcpClientApi": {
          "id": "WBPtkIhXDO8Yv1LK",
          "name": "Facebook Ad MCP"
        }
      }
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.chatTrigger",
      "typeVersion": 1.1,
      "position": [
        0,
        0
      ],
      "id": "dbb72ee1-067f-446d-b892-dc56bc18e2d2",
      "name": "When chat message received",
      "webhookId": "bf00ba32-fb2d-4094-a323-46dfe046c0f9"
    },
    {
      "parameters": {
        "operation": "executeTool",
        "toolName": "={{ $fromAI('tool', 'Set this with the specific tool name') }}",
        "toolParameters": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('Tool_Parameters', ``, 'json') }}"
      },
      "type": "n8n-nodes-mcp.mcpClientTool",
      "typeVersion": 1,
      "position": [
        580,
        300
      ],
      "id": "cc9f50b8-de1f-4513-a705-92a5f3521796",
      "name": "MCP Search Notion Database",
      "credentials": {
        "mcpClientApi": {
          "id": "ko0j3fThBkrVXmkm",
          "name": "Notion MCP"
        }
      }
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "value": "gpt-4.1-mini",
          "mode": "list",
          "cachedResultName": "gpt-4.1-mini"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.2,
      "position": [
        40,
        220
      ],
      "id": "6ac1df60-b50a-4750-8abd-e19d1713ad4b",
      "name": "OpenAI Chat Model",
      "credentials": {
        "openAiApi": {
          "id": "OLHtLOP5C47dG8d5",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "contextWindowLength": 10
      },
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.3,
      "position": [
        220,
        280
      ],
      "id": "8fd11e9b-eeed-42d1-a036-8a3c5ac01211",
      "name": "Simple Memory"
    },
    {
      "parameters": {
        "content": "## Prompt\nPlease query the Notion database \"Client Ad Campaigns\" (ID: 1a41d08c4f5a808b8944c0faa8922503) using the \"notion_query_database\" tool. Apply these filters:\n\nCampaign Type (multi_select) includes \"Listing Ad\" Status (status) equals \"Active\" Return all matching items with no limit. For each item, provide the complete, unabridged text for these properties:\n\nCampaign Name Body Copy 1 Body Copy 2 Headline 1 Headline 2 Headline 3 Notion page URL Do not truncate or summarize any text. Include all matching items fully.",
        "height": 300,
        "width": 440
      },
      "type": "n8n-nodes-base.stickyNote",
      "typeVersion": 1,
      "position": [
        -560,
        0
      ],
      "id": "6c25cef7-1071-4311-9cb1-f21d5b7e744b",
      "name": "Sticky Note"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-05-06T13:10:22.767Z",
      "updatedAt": "2025-05-06T13:10:22.767Z",
      "role": "workflow:owner",
      "workflowId": "gSwy3pUcXBLyBeBv",
      "projectId": "JPifOz0qwqZ4t1q3",
      "project": {
        "createdAt": "2025-01-22T02:43:20.320Z",
        "updatedAt": "2025-01-22T02:44:04.001Z",
        "id": "JPifOz0qwqZ4t1q3",
        "name": "Emma Pace <emma@salesgenius.co>",
        "type": "personal",
        "icon": null,
        "projectRelations": [
          {
            "createdAt": "2025-01-22T02:43:20.320Z",
            "updatedAt": "2025-01-22T02:43:20.320Z",
            "role": "project:personalOwner",
            "userId": "f8bb0fb6-1857-45fa-9ac1-27b6e6497323",
            "projectId": "JPifOz0qwqZ4t1q3",
            "user": {
              "createdAt": "2025-01-22T02:43:19.556Z",
              "updatedAt": "2025-05-02T12:52:46.487Z",
              "id": "f8bb0fb6-1857-45fa-9ac1-27b6e6497323",
              "email": "emma@salesgenius.co",
              "firstName": "Emma",
              "lastName": "Pace",
              "personalizationAnswers": {
                "version": "v4",
                "personalization_survey_submitted_at": "2025-01-22T02:45:22.428Z",
                "personalization_survey_n8n_version": "1.74.3",
                "companySize": "<20",
                "companyType": "digital-agency",
                "role": "business-owner",
                "reportedSource": "youtube"
              },
              "settings": {
                "userActivated": true,
                "easyAIWorkflowOnboarded": true,
                "firstSuccessfulWorkflowId": "TotyBJ1rIIIGlYrK",
                "userActivatedAt": 1737997390312,
                "npsSurvey": {
                  "responded": true,
                  "lastShownAt": 1739558292687
                }
              },
              "role": "global:owner",
              "disabled": false,
              "mfaEnabled": false,
              "isPending": false,
              "isOwner": true
            }
          }
        ]
      }
    }
  ],
  "staticData": null,
  "tags": [],
  "triggerCount": 1,
  "updatedAt": "2025-05-06T13:42:49.000Z",
  "versionId": "e75a92df-d90c-4a53-8cc5-72c08c2aa459"
}