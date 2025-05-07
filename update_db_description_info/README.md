{
  "active": false,
  "connections": {
    "When Executed by Another Workflow": {
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
    "HTTP Request1": {
      "main": [
        [
          {
            "node": "Edit Fields",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent": {
      "main": [
        [
          {
            "node": "Code",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Code": {
      "main": [
        [
          {
            "node": "HTTP Request1",
            "type": "main",
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
    }
  },
  "createdAt": "2025-04-28T18:31:13.200Z",
  "id": "O6SPqC4lsVgdfyH6",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "update_db_description_info",
  "nodes": [
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "4d699f35-b6fb-4654-8de7-7154b5226c1e",
              "name": "properties",
              "value": "={{ $json.properties }}",
              "type": "object"
            },
            {
              "id": "1ba93b76-e5fe-49bc-9510-9e0d19bb7caf",
              "name": "name",
              "value": "={{ $json.title[0].text.content }}",
              "type": "string"
            },
            {
              "id": "5ea6ee98-65bd-4dfc-a84f-b397140374c8",
              "name": "description",
              "value": "={{ $json.description[0].plain_text }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        520,
        20
      ],
      "id": "1b7e6ff9-2dc9-4dcc-a368-05af53e6dc07",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "workflowInputs": {
          "values": [
            {
              "name": "id"
            },
            {
              "name": "description"
            }
          ]
        }
      },
      "type": "n8n-nodes-base.executeWorkflowTrigger",
      "typeVersion": 1.1,
      "position": [
        -40,
        20
      ],
      "id": "2cbf3a41-9ed9-4211-91af-405d27f6baa6",
      "name": "When Executed by Another Workflow"
    },
    {
      "parameters": {
        "method": "PATCH",
        "url": "=https://api.notion.com/v1/databases/{{ $('When Executed by Another Workflow').item.json.id }}",
        "authentication": "predefinedCredentialType",
        "nodeCredentialType": "notionApi",
        "sendBody": true,
        "specifyBody": "json",
        "jsonBody": "={{ { \"description\": $json.description } }}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        320,
        20
      ],
      "id": "9bbdd4ba-a8a5-401b-94bf-88db004ca8ba",
      "name": "HTTP Request1",
      "credentials": {
        "notionApi": {
          "id": "3EhNxVoPGBbOY9vC",
          "name": "Notion account"
        }
      }
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.description }}",
        "hasOutputParser": true,
        "options": {
          "systemMessage": "You are a content generator for Notion database descriptions. Your goal is to build a JSON structure compatible with the \"rich_text\" format used in Notion databases.\n\n**Instructions:**\n\n1. The output must be an array of objects, where each object represents a section of the content.\n2. Each object must have this structure:\n```json\n{\n  \"type\": \"text\",\n  \"text\": {\n    \"content\": \"Text here\"\n  }\n}\n```\n3. The content must be formatted for improved readability, using:\n   - Titles in uppercase or surrounded by symbols to simulate hierarchies (e.g., `TÍTULO PRINCIPAL`).\n   - Subtitles preceded by symbols (`➤ Subtitle`).\n   - Simulated code blocks using triple backticks (```).  \n   - Line breaks (`\\n\\n`) to separate sections.\n4. The content should be designed to explain concepts clearly and in an organized way.\n\n**Example of expected output:**\n```json\n[\n  {\n    \"type\": \"text\",\n    \"text\": {\n      \"content\": \"MAIN TITLE\\n\\nThis is the introductory paragraph.\"\n    }\n  },\n  {\n    \"type\": \"text\",\n    \"text\": {\n      \"content\": \"➤ Subtitle\\n\\nDetailed description of this section.\"\n    }\n  },\n  {\n    \"type\": \"text\",\n    \"text\": {\n      \"content\": \"```\\nExample code here\\n```\"\n    }\n  }\n]\n```\n\n**Additional Notes:**\n- Never use structures or types not supported by Notion's rich_text format in databases (such as `\"heading_1\"` or `\"code\"` blocks outside of text content).\n- Make sure all the content is clear, organized, and easy to read.\n\n**Do not use emojis**"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.9,
      "position": [
        180,
        -240
      ],
      "id": "72f86b6a-01bb-4821-9b3a-70a29b4cd714",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "jsCode": "// Tomar el primer item del array (ya que solo esperamos un item)\nconst item = items[0];\nlet jsonString = (item.json && item.json.output) || item.output || '';\njsonString = jsonString.replace(/```json\\n?|\\n?```/g, '').trim();\njsonString = jsonString.replace(/[\\u{1F000}-\\u{1FFFF}\\u{2000}-\\u{2FFF}]/gu, match => {\n  let hex = '';\n  for (let i = 0; i < match.length; i++) {\n    hex += '\\\\u' + match.charCodeAt(i).toString(16).padStart(4, '0');\n  }\n  return hex;\n});\ntry {\n  const jsonObject = JSON.parse(jsonString);\n  const decodedBlocks = jsonObject.map(block => {\n    let content = block.text.content;\n    content = content.replace(/\\\\u([\\dA-F]{4})/gi, (match, hex) => {\n      return String.fromCharCode(parseInt(hex, 16));\n    });\n    return {\n      type: block.type,\n      text: {\n        content: content\n      }\n    };\n  });\n  // Devolver un solo objeto JSON, no un array\n  return {\n    description: decodedBlocks\n  };\n} catch (error) {\n  return {\n    description: [],\n    error: error.message,\n    rawString: jsonString\n  };\n}"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        620,
        -240
      ],
      "id": "38595dba-c543-415d-965b-f33ad576ddee",
      "name": "Code"
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "mode": "list",
          "value": "gpt-4o-mini"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.2,
      "position": [
        160,
        60
      ],
      "id": "7a4f1550-ecbe-4a50-aef2-64ecc92ce80c",
      "name": "OpenAI Chat Model",
      "credentials": {
        "openAiApi": {
          "id": "OLHtLOP5C47dG8d5",
          "name": "OpenAi account"
        }
      }
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-28T18:31:13.206Z",
      "updatedAt": "2025-04-28T18:31:13.206Z",
      "role": "workflow:owner",
      "workflowId": "O6SPqC4lsVgdfyH6",
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
  "triggerCount": 0,
  "updatedAt": "2025-04-30T16:58:53.000Z",
  "versionId": "3a90adc7-166e-4c61-9235-072465976bb7"
}