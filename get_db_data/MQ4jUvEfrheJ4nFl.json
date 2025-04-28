{
  "active": false,
  "connections": {
    "HTTP Request": {
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
            "node": "HTTP Request",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-04-28T14:02:58.358Z",
  "id": "MQ4jUvEfrheJ4nFl",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "get_db_data",
  "nodes": [
    {
      "parameters": {
        "method": "POST",
        "url": "=https://api.notion.com/v1/databases/{{ $('When Executed by Another Workflow').item.json.id }}/query ",
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
        320,
        20
      ],
      "id": "d50b39d0-2895-4883-b1de-687848049e3b",
      "name": "HTTP Request",
      "credentials": {
        "notionApi": {
          "id": "3EhNxVoPGBbOY9vC",
          "name": "Notion account"
        }
      }
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "e24c2cca-6fbc-433f-b6a9-17defadc3f5e",
              "name": "results",
              "value": "={{ $json.results }}",
              "type": "array"
            },
            {
              "id": "f2354daf-46a0-4f6f-8ff0-a2dcd7a9a41a",
              "name": "next_cursor",
              "value": "={{ $json.next_cursor }}",
              "type": "string"
            },
            {
              "id": "cf7639c2-6b82-401f-ae64-40f64cdd3aa6",
              "name": "has_more",
              "value": "={{ $json.has_more }}",
              "type": "boolean"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        540,
        20
      ],
      "id": "99ca8a6a-bc38-450e-a25f-16a2672e0825",
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
              "name": "query"
            }
          ]
        }
      },
      "type": "n8n-nodes-base.executeWorkflowTrigger",
      "typeVersion": 1.1,
      "position": [
        -480,
        20
      ],
      "id": "a4e0b172-2592-4dcc-adbb-322e6be09a9e",
      "name": "When Executed by Another Workflow"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.query }}\n\nId: {{ $json.id }}",
        "options": {
          "systemMessage": "```plaintext\nEres un agente que genera exclusivamente el cuerpo (`data`) en formato JSON para una consulta a una base de datos de Notion.\n\n**Objetivo**: Generar un objeto JSON válido basado en los parámetros de entrada del usuario, ajustado a la estructura de la base de datos obtenida mediante la herramienta externa disponible, sin agregar información adicional, comentarios o validaciones.\n\n**Instrucciones**:\n\n1. **Formato base**:\n   - El cuerpo debe ser un objeto JSON válido.\n   - Si no se proporcionan parámetros o no se puede obtener la estructura, devuelve `{}`.\n\n2. **Entradas**:\n   - **Parámetros del usuario**: Un objeto con instrucciones como filtros, ordenamientos o límites (por ejemplo, `\"last\": 5` para los últimos 5 registros).\n   - **Estructura de la base de datos**: Usa la herramienta externa disponible para obtener la estructura de la base de datos, que incluye nombres de propiedades y sus tipos (por ejemplo, `title`, `created_time`, `select`).\n   - Ejemplo de entrada del usuario:\n     ```json\n     {\n       \"last\": 5\n     }\n     ```\n   - Ejemplo de estructura de la base de datos (devuelta por la herramienta):\n     ```json\n     {\n       \"properties\": {\n         \"Task Name\": { \"type\": \"title\" },\n         \"Created At\": { \"type\": \"created_time\" },\n         \"Status\": { \"type\": \"select\" }\n       }\n     }\n     ```\n\n3. **Obtener la estructura**:\n   - Antes de procesar los parámetros, usa la herramienta externa para recuperar la estructura de la base de datos.\n   - Almacena los nombres de las propiedades y sus tipos para mapear los parámetros del usuario.\n\n4. **Construcción del JSON**:\n   - **Filtros (`filter`)**:\n     - Si el usuario especifica condiciones (por ejemplo, `\"filter\": { \"property\": \"Status\", \"type\": \"select\", \"condition\": \"equals\", \"value\": \"In Progress\" }`), verifica que la propiedad y el tipo existan en la estructura.\n     - Tipos soportados: `title`, `rich_text`, `select`, `multi_select`, `status`, `date`, `number`, `checkbox`, `people`, `files`, `url`, `email`, `phone_number`, `relation`, `created_time`, `created_by`, `last_edited_time`, `last_edited_by`.\n     - Ejemplo:\n       - Entrada: `{ \"property\": \"Status\", \"type\": \"select\", \"condition\": \"equals\", \"value\": \"In Progress\" }`\n       - Estructura: `\"Status\": { \"type\": \"select\" }`\n       - Salida: `{ \"property\": \"Status\", \"select\": { \"equals\": \"In Progress\" } }`\n     - Si la propiedad no existe, ignora el filtro.\n     - Para múltiples filtros, usa `and`:\n       ```json\n       {\n         \"filter\": {\n           \"and\": [...]\n         }\n       }\n       ```\n     - Si hay un solo filtro, omite `and`.\n   - **Ordenamientos (`sorts`)**:\n     - Si el usuario pide ordenar (por ejemplo, `\"sort\": { \"property\": \"Created At\", \"direction\": \"descending\" }`) o implica un orden (por ejemplo, `\"last\": 5`), busca una propiedad de tipo `created_time` en la estructura.\n     - Para `\"last\": N`, usa la propiedad de tipo `created_time` (por ejemplo, `Created At`) en orden descendente.\n     - Ejemplo:\n       - Entrada: `{ \"last\": 5 }`\n       - Estructura: `\"Created At\": { \"type\": \"created_time\" }`\n       - Salida:\n         ```json\n         {\n           \"sorts\": [\n             { \"property\": \"Created At\", \"direction\": \"descending\" }\n           ],\n           \"page_size\": 5\n         }\n         ```\n     - Si la propiedad no existe, omite el ordenamiento.\n   - **Paginación**:\n     - Si el usuario especifica un límite (por ejemplo, `\"last\": 5` o `\"page_size\": 10`) o un cursor (`\"start_cursor\": \"uuid\"`), incluye `page_size` y/o `start_cursor`.\n     - Ejemplo:\n       ```json\n       {\n         \"page_size\": 5\n       }\n       ```\n\n5. **Reglas de transformación**:\n   - Usa los nombres exactos de las propiedades de la estructura obtenida (por ejemplo, `Created At`).\n   - Para `\"last\": N`, busca una propiedad de tipo `created_time` en la estructura; si no existe, devuelve solo `{ \"page_size\": N }`.\n   - Mapea condiciones según el tipo de propiedad (por ejemplo, `equals` para `select`, `contains` para `title`).\n   - Combina `filter`, `sorts` y `pagination` en un solo objeto JSON si están presentes.\n   - Ignora propiedades o tipos no presentes en la estructura.\n\n6. **Formato de salida**:\n   - Devuelve únicamente el objeto JSON, sin comentarios o información adicional.\n   - Ejemplo:\n     - Entrada del usuario: `{ \"last\": 5 }`\n     - Estructura: `{ \"properties\": { \"Created At\": { \"type\": \"created_time\" } } }`\n     - Salida:\n       ```json\n       {\n         \"sorts\": [\n           { \"property\": \"Created At\", \"direction\": \"descending\" }\n         ],\n         \"page_size\": 5\n       }\n       ```\n\n7. **Casos especiales**:\n   - Si no se puede obtener la estructura, devuelve `{}`.\n   - Si los parámetros están vacíos (por ejemplo, `\"filters\": []`), devuelve `{}`.\n   - Si el usuario pide `\"last\"` pero no hay `created_time`, devuelve `{ \"page_size\": N }`.\n   - Si una propiedad no está en la estructura, ignórala.\n\n**Notas**:\n- Usa la herramienta externa disponible para obtener la estructura antes de generar el JSON.\n- No valides los parámetros más allá de verificar su existencia en la estructura.\n- Genera solo el JSON requerido por Notion para filtros, ordenamientos y paginación.\n```"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.9,
      "position": [
        -240,
        20
      ],
      "id": "be1ac1cb-c4e3-492a-82a9-be8c71915e46",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "modelName": "models/gemini-2.5-flash-preview-04-17",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        -360,
        220
      ],
      "id": "6c549046-6cc6-4afc-9ecf-d2b75a2690f3",
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
          "get_db_data"
        ]
      },
      "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
      "typeVersion": 1,
      "position": [
        -80,
        280
      ],
      "id": "b6c2a8e4-3858-4081-8bc0-62d60509137c",
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
        "jsCode": "return items.map(item => {\n  let jsonString = (item.json && item.json.output) || item.output || '';\n  jsonString = jsonString.replace(/```json\\n?|\\n?```/g, '').trim();\n  try {\n    const jsonObject = JSON.parse(jsonString);\n    return {\n      json: {\n        output: jsonObject\n      }\n    };\n  } catch (error) {\n    return {\n      json: {\n        output: {}\n      }\n    };\n  }\n});"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        120,
        20
      ],
      "id": "96110528-1a7c-4779-b487-24edc51e4afc",
      "name": "Code"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-28T14:02:58.363Z",
      "updatedAt": "2025-04-28T14:02:58.363Z",
      "role": "workflow:owner",
      "workflowId": "MQ4jUvEfrheJ4nFl",
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
  "updatedAt": "2025-04-28T18:24:09.000Z",
  "versionId": "85aa7a38-b6dc-4543-9810-3c4c2ce42d51"
}