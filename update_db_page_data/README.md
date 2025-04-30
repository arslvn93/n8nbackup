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
    "MCP Client": {
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
    "AI Agent": {
      "main": [
        [
          {
            "node": "HTTP Request",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Auto-fixing Output Parser": {
      "ai_outputParser": [
        [
          {
            "node": "AI Agent",
            "type": "ai_outputParser",
            "index": 0
          }
        ]
      ]
    },
    "Structured Output Parser": {
      "ai_outputParser": [
        [
          {
            "node": "Auto-fixing Output Parser",
            "type": "ai_outputParser",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request": {
      "main": [
        [],
        []
      ]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          },
          {
            "node": "Auto-fixing Output Parser",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-04-30T12:01:55.960Z",
  "id": "1oSNKAvsISWkUSlP",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "update_db_page_data",
  "nodes": [
    {
      "parameters": {
        "promptType": "define",
        "text": "=id: {{ $json.id }}\n{{ $json.description }}",
        "hasOutputParser": true,
        "options": {
          "systemMessage": "You are an agent responsible for building a valid JSON body to update an existing record in a Notion database using its API. You will receive as input the ID of a Notion page and a natural language description of the changes that should be applied.\n\nYour task is completely agnostic to the structure of the database: you must process any database without assuming specific fields.\n\n**Steps to follow:**\n\n1. Use the **tool to get the page from its ID** in order to retrieve:\n   - The schema of the associated database.\n   - The exact names of all properties and their current values.\n   - The type of each property (e.g.: `title`, `rich_text`, `select`, `multi_select`, `number`, `checkbox`, `date`, `status`, `people`, `files`, etc.).\n   - Valid options for `select` and `multi_select` if they exist.\n   - Which properties have a defined type and therefore must maintain valid values.\n\n2. From the user's description:\n   - Interpret what information should be **modified**, based on what is expressed in natural language.\n   - Determine which properties should **retain their current value**, either because they are not mentioned or because no change is requested.\n   - Assign new values only if they can be clearly inferred.\n   - If a property is mentioned but the new value cannot be determined with certainty, it should not be modified.\n\n3. When constructing the final JSON object:\n   - Include only the properties that should be updated with newly inferred values.\n   - Never include an empty property or one with an invalid value for its type.\n   - Use the correct structures for each type, for example:\n     - `title`: must be an array with a `text.content` object.\n     - `select` and `multi_select`: must include only predefined valid values from the schema.\n     - `date`: must be in ISO 8601 format (`YYYY-MM-DD`).\n     - `checkbox`: must be boolean.\n     - `number`: must be numeric.\n   - Strictly follow the format required by the Notion API and do not add any non-existent or unauthorized properties.\n\nYour final response must be exclusively a JSON object representing the body of the request for `PATCH /v1/pages/{page_id}`, following all of the above rules. Do **not** include explanations or comments—only the JSON."
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.9,
      "position": [
        220,
        0
      ],
      "id": "c54a5f7a-da88-4212-9380-62cdfc7b5bda",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "workflowInputs": {
          "values": [
            {
              "name": "id"
            },
            {
              "name": "data"
            }
          ]
        }
      },
      "type": "n8n-nodes-base.executeWorkflowTrigger",
      "typeVersion": 1.1,
      "position": [
        0,
        0
      ],
      "id": "82eeed00-baf6-4ebf-9480-084d7b106177",
      "name": "When Executed by Another Workflow"
    },
    {
      "parameters": {
        "sseEndpoint": "https://n8n.salesgenius.co/mcp/notiondb/sse",
        "authentication": "bearerAuth",
        "include": "selected",
        "includeTools": [
          "get_page_db_data_by_id"
        ]
      },
      "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
      "typeVersion": 1,
      "position": [
        360,
        260
      ],
      "id": "d0ae90a4-550e-4b07-915b-a450151d6125",
      "name": "MCP Client",
      "credentials": {
        "httpBearerAuth": {
          "id": "W8jPE6HrmWmbxBe2",
          "name": "MCPTEST"
        }
      }
    },
    {
      "parameters": {
        "method": "PATCH",
        "url": "=https://api.notion.com/v1/pages/{{ $('When Executed by Another Workflow').item.json.id }}",
        "authentication": "predefinedCredentialType",
        "nodeCredentialType": "notionApi",
        "sendBody": true,
        "specifyBody": "json",
        "jsonBody": "={{ $json.output }}",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        660,
        -220
      ],
      "id": "4b642129-d336-4f42-b9d2-4800f8aec63f",
      "name": "HTTP Request",
      "credentials": {
        "notionApi": {
          "id": "3EhNxVoPGBbOY9vC",
          "name": "Notion account"
        }
      },
      "onError": "continueRegularOutput"
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserAutofixing",
      "typeVersion": 1,
      "position": [
        460,
        180
      ],
      "id": "7618961b-55a6-4e31-8952-be1909e173da",
      "name": "Auto-fixing Output Parser"
    },
    {
      "parameters": {
        "schemaType": "manual",
        "inputSchema": "{\n  \"type\": \"object\",\n  \"required\": [\"properties\"],\n  \"properties\": {\n    \"properties\": {\n      \"type\": \"object\",\n      \"minProperties\": 1,\n      \"additionalProperties\": {\n        \"type\": \"object\",\n        \"oneOf\": [\n          {\n            \"required\": [\"title\"],\n            \"properties\": {\n              \"title\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"text\"],\n                  \"properties\": {\n                    \"text\": {\n                      \"type\": \"object\",\n                      \"required\": [\"content\"],\n                      \"properties\": {\n                        \"content\": { \"type\": \"string\" }\n                      }\n                    }\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"rich_text\"],\n            \"properties\": {\n              \"rich_text\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"text\"],\n                  \"properties\": {\n                    \"text\": {\n                      \"type\": \"object\",\n                      \"required\": [\"content\"],\n                      \"properties\": {\n                        \"content\": { \"type\": \"string\" }\n                      }\n                    }\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"number\"],\n            \"properties\": {\n              \"number\": { \"type\": \"number\" }\n            }\n          },\n          {\n            \"required\": [\"select\"],\n            \"properties\": {\n              \"select\": {\n                \"type\": \"object\",\n                \"required\": [\"name\"],\n                \"properties\": {\n                  \"name\": { \"type\": \"string\" }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"multi_select\"],\n            \"properties\": {\n              \"multi_select\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"name\"],\n                  \"properties\": {\n                    \"name\": { \"type\": \"string\" }\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"status\"],\n            \"properties\": {\n              \"status\": {\n                \"type\": \"object\",\n                \"required\": [\"name\"],\n                \"properties\": {\n                  \"name\": { \"type\": \"string\" }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"date\"],\n            \"properties\": {\n              \"date\": {\n                \"type\": \"object\",\n                \"required\": [\"start\"],\n                \"properties\": {\n                  \"start\": { \"type\": \"string\", \"format\": \"date-time\" },\n                  \"end\": { \"type\": \"string\", \"format\": \"date-time\" },\n                  \"time_zone\": { \"type\": \"string\" }\n                },\n                \"additionalProperties\": false\n              }\n            }\n          },\n          {\n            \"required\": [\"people\"],\n            \"properties\": {\n              \"people\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"object\", \"id\"],\n                  \"properties\": {\n                    \"object\": { \"type\": \"string\", \"enum\": [\"user\"] },\n                    \"id\": { \"type\": \"string\" }\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"files\"],\n            \"properties\": {\n              \"files\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"oneOf\": [\n                    {\n                      \"required\": [\"name\", \"external\"],\n                      \"properties\": {\n                        \"name\": { \"type\": \"string\" },\n                        \"external\": {\n                          \"type\": \"object\",\n                          \"required\": [\"url\"],\n                          \"properties\": {\n                            \"url\": { \"type\": \"string\", \"format\": \"uri\" }\n                          }\n                        }\n                      }\n                    },\n                    {\n                      \"required\": [\"name\", \"file\"],\n                      \"properties\": {\n                        \"name\": { \"type\": \"string\" },\n                        \"file\": {\n                          \"type\": \"object\",\n                          \"required\": [\"url\"],\n                          \"properties\": {\n                            \"url\": { \"type\": \"string\", \"format\": \"uri\" }\n                          }\n                        }\n                      }\n                    }\n                  ]\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"checkbox\"],\n            \"properties\": {\n              \"checkbox\": { \"type\": \"boolean\" }\n            }\n          },\n          {\n            \"required\": [\"url\"],\n            \"properties\": {\n              \"url\": { \"type\": \"string\", \"format\": \"uri\" }\n            }\n          },\n          {\n            \"required\": [\"email\"],\n            \"properties\": {\n              \"email\": { \"type\": \"string\", \"format\": \"email\" }\n            }\n          },\n          {\n            \"required\": [\"phone_number\"],\n            \"properties\": {\n              \"phone_number\": { \"type\": \"string\" }\n            }\n          },\n          {\n            \"required\": [\"relation\"],\n            \"properties\": {\n              \"relation\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"id\"],\n                  \"properties\": {\n                    \"id\": { \"type\": \"string\" }\n                  }\n                }\n              }\n            }\n          }\n        ]\n      }\n    }\n  },\n  \"additionalProperties\": false\n}\n"
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserStructured",
      "typeVersion": 1.2,
      "position": [
        640,
        440
      ],
      "id": "9139a7f5-bf40-43fd-abce-4b491c309dfe",
      "name": "Structured Output Parser"
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
        140,
        260
      ],
      "id": "8dd430c5-5876-4d83-b918-1c63f4b05b52",
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
      "createdAt": "2025-04-30T12:01:55.965Z",
      "updatedAt": "2025-04-30T12:01:55.965Z",
      "role": "workflow:owner",
      "workflowId": "1oSNKAvsISWkUSlP",
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
  "triggerCount": 0,
  "updatedAt": "2025-04-30T15:32:58.000Z",
  "versionId": "5782fe1b-a0e1-4c20-ae9f-9efbc2387a6c"
}