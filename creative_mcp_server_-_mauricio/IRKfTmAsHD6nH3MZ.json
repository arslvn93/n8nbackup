{
  "active": true,
  "connections": {
    "Lead In Agent": {
      "ai_tool": [
        [
          {
            "node": "MCP Server Trigger",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "Headline Agent": {
      "ai_tool": [
        [
          {
            "node": "MCP Server Trigger",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "body_copy_agent": {
      "ai_tool": [
        [
          {
            "node": "MCP Server Trigger",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-04-23T14:23:26.817Z",
  "id": "IRKfTmAsHD6nH3MZ",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "Creative MCP Server - Mauricio",
  "nodes": [
    {
      "parameters": {
        "authentication": "bearerAuth",
        "path": "CretiveText"
      },
      "type": "@n8n/n8n-nodes-langchain.mcpTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "07e91a18-5eb9-47f6-9669-2a389eb010b4",
      "name": "MCP Server Trigger",
      "webhookId": "9a1ec011-1a44-4dd9-816c-508c3e407242",
      "credentials": {
        "httpBearerAuth": {
          "id": "W8jPE6HrmWmbxBe2",
          "name": "MCPTEST"
        }
      }
    },
    {
      "parameters": {
        "name": "lead_in_agent",
        "description": "The lead_in_agent generates five unique, high-converting opening lines (lead-ins) for each of three Facebook ad body copies for a real estate property. Each set of lead-ins is tailored to a specific buyer group, using property details, buyer profiles, and the desired emotion to create compelling hooks that grab attention and drive readers to engage with the ad.\n\nInput Data\n\n\n\n\n\nProperty Essentials:\nDescribes the core elements that define the property’s value and appeal. Includes the type of property (e.g., townhouse, condo), the price or price range (only if the user wants it shown in the ad), the city and region (e.g., Innisfil, Ontario), the most standout feature (e.g., a freehold townhouse priced like a condo), and the primary emotion to evoke in potential buyers (e.g., excitement).\n\n\n\nTarget Audience:\nDefines the ideal buyer groups for the property. Includes descriptions of the main buyer group (e.g., young couples starting a family), a second buyer group (e.g., families who love beach proximity), and a third buyer group (e.g., remote-working professionals). These details help tailor the lead-ins to each group’s needs and desires.\n\n\n\nBody Copies:\nProvides three existing Facebook ad body copies, each written for one of the buyer groups. Each body copy includes property details and targets a specific buyer group, serving as the context for the lead-ins to flow seamlessly into.\n\n\n\nDesired Emotion:\nSpecifies the emotion the user wants potential buyers to feel when seeing the ad (e.g., excitement, curiosity). This guides the tone and style of the lead-ins to align with the ad’s emotional impact.",
        "workflowId": {
          "__rl": true,
          "mode": "id",
          "value": "yqsoJDFEuVDF2hc9"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {},
          "matchingColumns": [],
          "schema": [
            {
              "id": "Property Essentials",
              "displayName": "Property Essentials",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            },
            {
              "id": "Target Audience",
              "displayName": "Target Audience",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            },
            {
              "id": "Body Copies",
              "displayName": "Body Copies",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            },
            {
              "id": "Desired Emotion",
              "displayName": "Desired Emotion",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        }
      },
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow",
      "typeVersion": 2.1,
      "position": [
        160,
        220
      ],
      "id": "8dcce17e-859f-435d-a0ef-f269f7ea13c4",
      "name": "Lead In Agent"
    },
    {
      "parameters": {
        "name": "headline_agent",
        "description": "=The headline_agent generates 10 scroll-stopping Facebook ad headlines designed to achieve 6%+ click-through rates (CTR). Each headline is tailored to the property’s features, buyer profiles, and desired emotion, using proven copywriting techniques to capture attention and drive clicks. The headlines complement existing lead-ins and body copies, ensuring a cohesive ad campaign.",
        "workflowId": {
          "__rl": true,
          "value": "6k7968ycKuG0PjlP",
          "mode": "list",
          "cachedResultName": "My Sub-Workflow 1"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {},
          "matchingColumns": [],
          "schema": [
            {
              "id": "Property Essentials",
              "displayName": "Property Essentials",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            },
            {
              "id": "Target Audience",
              "displayName": "Target Audience",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            },
            {
              "id": "Lead-ins",
              "displayName": "Lead-ins",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            },
            {
              "id": "Body Copies",
              "displayName": "Body Copies",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            },
            {
              "id": "Desired Emotion",
              "displayName": "Desired Emotion",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": true
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        }
      },
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow",
      "typeVersion": 2.1,
      "position": [
        300,
        220
      ],
      "id": "29c2e302-6b01-4c7f-9001-6feb09e784f5",
      "name": "Headline Agent"
    },
    {
      "parameters": {
        "description": "Call this tool to generate a persuasive ad copy (150–250 words) for a real estate Facebook ad, tailored to a specific buyer profile. The input should be a natural language prompt describing the buyer profile, key property features, desired emotion, campaign goal, and 1–2 example ads to guide the tone.",
        "workflowId": {
          "__rl": true,
          "value": "wFvupa1fErzdnlwU",
          "mode": "list",
          "cachedResultName": "🛠 Tool: Body Copy Agent – Facebook Ad Writer (Real Estate)"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {},
          "matchingColumns": [],
          "schema": [],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        }
      },
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow",
      "typeVersion": 2.2,
      "position": [
        20,
        200
      ],
      "id": "ad33aeac-aea1-4eb8-97c1-548f58752554",
      "name": "body_copy_agent"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-23T14:23:26.823Z",
      "updatedAt": "2025-04-23T14:23:26.823Z",
      "role": "workflow:owner",
      "workflowId": "IRKfTmAsHD6nH3MZ",
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
              "updatedAt": "2025-02-14T18:38:15.546Z",
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
  "updatedAt": "2025-04-23T14:34:25.000Z",
  "versionId": "a6e1bc2a-cedd-4a8d-bb49-6408cc1815f3"
}