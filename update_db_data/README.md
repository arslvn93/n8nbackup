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
    "Google Gemini Chat Model": {
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
    }
  },
  "createdAt": "2025-04-29T18:41:27.327Z",
  "id": "ibY5uEkPp2q9UCxi",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "update_db_data",
  "nodes": [
    {
      "parameters": {
        "promptType": "define",
        "text": "=id: {{ $json.id }}\nCrea una tarea con prieridad media que sea crear un mcp de notion",
        "hasOutputParser": true,
        "options": {
          "systemMessage": "Eres un agente encargado de construir un cuerpo JSON válido para crear un nuevo registro en una base de datos de Notion utilizando su API. Recibirás como entrada el ID de una base de datos de Notion y una descripción en lenguaje natural de lo que se desea registrar.\n\nTu tarea es completamente agnóstica a la estructura de la base de datos: debes procesar cualquier base de datos sin asumir campos específicos.\n\nPasos a seguir:\n\n1. Consulta el esquema de la base de datos con el endpoint `GET /v1/databases/{database_id}` para obtener dinámicamente:\n   - Los nombres exactos de todas las propiedades.\n   - El tipo de cada propiedad (por ejemplo: `title`, `rich_text`, `select`, `multi_select`, `number`, `checkbox`, `date`, `status`, `people`, `files`, etc.).\n   - Las opciones válidas para `select` y `multi_select` si existen.\n   - Qué propiedades tienen un tipo definido y por tanto deben considerarse requeridas.\n\n2. A partir de la descripción del usuario:\n   - Identifica a qué propiedad corresponde cada valor mencionado.\n   - Asigna valores únicamente si pueden inferirse con claridad.\n   - Si una propiedad es requerida por el esquema y no puede inferirse desde el mensaje, ignórala para evitar errores, a menos que sea del tipo `title`, que debe incluirse obligatoriamente.\n\n3. Al construir el objeto JSON final:\n   - Incluye solo las propiedades que tienen valores inferidos.\n   - Nunca incluyas una propiedad vacía ni con un valor incorrecto según su tipo.\n   - Usa las estructuras correctas para cada tipo, por ejemplo:\n     - `title`: debe ser un array con un objeto `text.content`.\n     - `select` y `multi_select`: deben incluir solo valores válidos predefinidos en el esquema.\n     - `date`: debe estar en formato ISO 8601 (`YYYY-MM-DD`).\n     - `checkbox`: debe ser booleano.\n     - `number`: debe ser numérico.\n   - Respeta estrictamente el formato de la API de Notion y no agregues propiedades que no estén definidas en el esquema.\n\nTu respuesta final debe ser exclusivamente un objeto JSON que represente el cuerpo de la solicitud para `POST /v1/pages`, siguiendo todas las reglas anteriores. No incluyas explicaciones ni comentarios, solo el JSON.\n"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.9,
      "position": [
        220,
        0
      ],
      "id": "ff8c4ee4-947f-4778-8d69-519cd29c29ba",
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
      "id": "a3e9d33c-7ddc-475a-a510-80fc3d65b605",
      "name": "When Executed by Another Workflow"
    },
    {
      "parameters": {
        "modelName": "models/gemini-2.5-flash-preview-04-17",
        "options": {
          "temperature": 0.4
        }
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        120,
        200
      ],
      "id": "7fa5d1f8-efcf-4479-a810-83934e446a0d",
      "name": "Google Gemini Chat Model",
      "credentials": {
        "googlePalmApi": {
          "id": "vAGPZIKKEemfw5Kl",
          "name": "Google Gemini(PaLM) Api account"
        }
      }
    },
    {
      "parameters": {
        "sseEndpoint": "https://n8n.salesgenius.co/mcp/notiondb/sse",
        "authentication": "bearerAuth",
        "include": "selected",
        "includeTools": [
          "get_db_structure"
        ]
      },
      "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
      "typeVersion": 1,
      "position": [
        360,
        260
      ],
      "id": "955ce564-dcc1-4de6-8689-d1d0f8227195",
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
        "method": "POST",
        "url": "https://api.notion.com/v1/pages",
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
      "id": "cd251a63-4e50-42c5-bd57-438c7f5b2c4b",
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
      "id": "c77cb2e8-936a-4d84-b542-c496b1030a5d",
      "name": "Auto-fixing Output Parser"
    },
    {
      "parameters": {
        "schemaType": "manual",
        "inputSchema": "{\n  \"type\": \"object\",\n  \"required\": [\"parent\", \"properties\"],\n  \"properties\": {\n    \"parent\": {\n      \"type\": \"object\",\n      \"required\": [\"database_id\"],\n      \"properties\": {\n        \"database_id\": {\n          \"type\": \"string\"\n        }\n      },\n      \"additionalProperties\": false\n    },\n    \"properties\": {\n      \"type\": \"object\",\n      \"minProperties\": 1,\n      \"additionalProperties\": {\n        \"type\": \"object\",\n        \"oneOf\": [\n          {\n            \"required\": [\"title\"],\n            \"properties\": {\n              \"title\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"text\"],\n                  \"properties\": {\n                    \"text\": {\n                      \"type\": \"object\",\n                      \"required\": [\"content\"],\n                      \"properties\": {\n                        \"content\": { \"type\": \"string\" }\n                      }\n                    }\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"rich_text\"],\n            \"properties\": {\n              \"rich_text\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"text\"],\n                  \"properties\": {\n                    \"text\": {\n                      \"type\": \"object\",\n                      \"required\": [\"content\"],\n                      \"properties\": {\n                        \"content\": { \"type\": \"string\" }\n                      }\n                    }\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"select\"],\n            \"properties\": {\n              \"select\": {\n                \"type\": \"object\",\n                \"required\": [\"name\"],\n                \"properties\": {\n                  \"name\": { \"type\": \"string\" }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"multi_select\"],\n            \"properties\": {\n              \"multi_select\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"name\"],\n                  \"properties\": {\n                    \"name\": { \"type\": \"string\" }\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"number\"],\n            \"properties\": {\n              \"number\": { \"type\": \"number\" }\n            }\n          },\n          {\n            \"required\": [\"checkbox\"],\n            \"properties\": {\n              \"checkbox\": { \"type\": \"boolean\" }\n            }\n          },\n          {\n            \"required\": [\"date\"],\n            \"properties\": {\n              \"date\": {\n                \"type\": \"object\",\n                \"required\": [\"start\"],\n                \"properties\": {\n                  \"start\": {\n                    \"type\": \"string\",\n                    \"format\": \"date\"\n                  },\n                  \"end\": {\n                    \"type\": \"string\",\n                    \"format\": \"date\"\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"status\"],\n            \"properties\": {\n              \"status\": {\n                \"type\": \"object\",\n                \"required\": [\"name\"],\n                \"properties\": {\n                  \"name\": { \"type\": \"string\" }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"people\"],\n            \"properties\": {\n              \"people\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\",\n                  \"required\": [\"id\"],\n                  \"properties\": {\n                    \"id\": { \"type\": \"string\" }\n                  }\n                }\n              }\n            }\n          },\n          {\n            \"required\": [\"files\"],\n            \"properties\": {\n              \"files\": {\n                \"type\": \"array\",\n                \"items\": {\n                  \"type\": \"object\"\n                }\n              }\n            }\n          }\n        ]\n      }\n    }\n  },\n  \"additionalProperties\": false\n}\n"
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserStructured",
      "typeVersion": 1.2,
      "position": [
        640,
        440
      ],
      "id": "be6e93ac-6ddd-48d5-8ab5-7140c27579b4",
      "name": "Structured Output Parser"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-29T18:41:27.337Z",
      "updatedAt": "2025-04-29T18:41:27.337Z",
      "role": "workflow:owner",
      "workflowId": "ibY5uEkPp2q9UCxi",
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
  "updatedAt": "2025-04-29T18:41:27.327Z",
  "versionId": "f45e8d51-744f-4996-8eca-47927f6093b6"
}