{
  "active": true,
  "connections": {
    "Edit Fields1": {
      "main": [
        [
          {
            "node": "validate",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "If": {
      "main": [
        [
          {
            "node": "Validation fail",
            "type": "main",
            "index": 0
          }
        ],
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
    "AI Agent": {
      "main": [
        [
          {
            "node": "JSON RPC agent output",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "validate": {
      "main": [
        [
          {
            "node": "If",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP Request": {
      "main": [
        [
          {
            "node": "Edit Fields1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Agent Card Webhook": {
      "main": [
        [
          {
            "node": "Agent Card",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Agent Webhook": {
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
    "Call n8n Workflow Tool": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-04-23T14:13:13.874Z",
  "id": "W6aLSh3xtVGMubzM",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "Remote Agent Mauricio",
  "nodes": [
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict",
            "version": 2
          },
          "conditions": [
            {
              "id": "22e4a6f7-441d-4fa7-84b4-340a09fc5882",
              "leftValue": "={{ $json.success }}",
              "rightValue": "",
              "operator": {
                "type": "boolean",
                "operation": "exists",
                "singleValue": true
              }
            },
            {
              "id": "96379786-c4e3-475e-8330-cc55647e14e1",
              "leftValue": "={{ $json.success }}",
              "rightValue": "",
              "operator": {
                "type": "boolean",
                "operation": "false",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.2,
      "position": [
        520,
        420
      ],
      "id": "078fed6a-f2e1-4b0a-b769-3d0bcac34d4d",
      "name": "If"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "ebdff9f3-82c5-4e16-9187-1d5223401d16",
              "name": "task",
              "value": "={{ $('Agent Webhook').item.json.body.task }}",
              "type": "string"
            },
            {
              "id": "89a9686e-e9a9-49c3-b8a2-5c98c23126e4",
              "name": "data",
              "value": "={{ $('Agent Webhook').item.json.body.data }}",
              "type": "object"
            },
            {
              "id": "7726336a-3bc0-4f68-b0a4-b78016442818",
              "name": "capabilities",
              "value": "={{ $json.capabilities }}",
              "type": "array"
            },
            {
              "id": "be4b9b8a-c676-4eab-b8e2-7d68bdd20e50",
              "name": "inputFormat",
              "value": "={{ $json.inputFormat }}",
              "type": "array"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        200,
        420
      ],
      "id": "c394ec96-bd50-4da0-9b5f-5465e8e03138",
      "name": "Edit Fields1"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "=Task: {{ $json.task }}\n\nData: {{ $json.data.text }}",
        "options": {
          "systemMessage": "Eres un agente remoto que cumple con el protocolo Agent2Agent (A2A).\n\nTu tarea es procesar solicitudes de tipo \"resumen\". Recibirás un texto en el campo \"Data\". Debes generar un resumen breve y útil. En caso que de indique en Data características de como debe ser el resumen debes cumplirlas.\n\nTu respuesta debe estar siempre dentro del siguiente bloque, usando este formato exacto:\n\n<response>\nsuccess: true\nresult: [aquí va el resumen generado]\nmetadata: {\"modelo\": \"Gemini\", \"longitud_original\": X, \"longitud_resumen\": Y}\n</response>\n\nSi no puedes generar un resumen por algún motivo, responde con:\n\n<response>\nsuccess: false\nerror: [explicación legible del problema]\n</response>\n\nNo incluyas texto fuera de las etiquetas <response>. No expliques tu razonamiento.\n"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.8,
      "position": [
        780,
        320
      ],
      "id": "7ae13505-0d0d-4673-8260-b8c9c1bba592",
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
        780,
        500
      ],
      "id": "3de00940-5447-4836-a302-eceb4127279a",
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
        "assignments": {
          "assignments": [
            {
              "id": "60a8dba8-f3eb-42e9-8841-b0872dc715aa",
              "name": "agentId",
              "value": "a2a-agente-remoto-001",
              "type": "string"
            },
            {
              "id": "180529f2-af1d-4b3a-b28f-a96b5626657e",
              "name": "name",
              "value": "AgenteGemini",
              "type": "string"
            },
            {
              "id": "1283a361-0ab7-4615-9932-d225d841cf86",
              "name": "description",
              "value": "Este agente A2A usa Gemini y herramientas MCP para procesar tareas.",
              "type": "string"
            },
            {
              "id": "f498ff26-ca25-4d6b-acea-a076a5dd05d7",
              "name": "capabilities",
              "value": "[\"resume texto\", \"resume url content\"]",
              "type": "array"
            },
            {
              "id": "5f75f268-9796-4569-bb4c-7c7f1cb907a0",
              "name": "endpoint",
              "value": "=https://{{ $json.headers.host }}/webhook/AgenteGemini",
              "type": "string"
            },
            {
              "id": "bd4a7873-c309-4379-84a9-c9536a0c7913",
              "name": "inputFormat",
              "value": "[\"text\", \"json\"]",
              "type": "array"
            },
            {
              "id": "7a3c2499-b72d-4447-9557-97627e119cd0",
              "name": "outputFormat",
              "value": "[\"json\"]",
              "type": "array"
            },
            {
              "id": "dc38e705-3e48-4d0a-aa0b-5c2c33fce5e6",
              "name": "tools",
              "value": "[\"MCP Client Tool\"]",
              "type": "array"
            },
            {
              "id": "6c7b04e5-ebe2-428b-b2ae-745f8e06b156",
              "name": "authentication",
              "value": "{\"type\": \"none\"}",
              "type": "object"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        200,
        100
      ],
      "id": "d05cb46c-df40-4d19-a8d8-bca5f0feb321",
      "name": "Agent Card"
    },
    {
      "parameters": {
        "jsCode": "const item = items[0].json;\n\n// Definiciones desde la Agent Card (hardcoded o podrías cargarlas dinámicamente)\nconst supportedTasks = item.capabilities;\nconst supportedFormats = item.inputFormat;\n\nconst task = item.task;\nconst data = item.data;\n\n// 1. Validar task\nif (!supportedTasks.includes(task)) {\n\treturn [\n\t\t{\n\t\t\tjson: {\n\t\t\t\tsuccess: false,\n\t\t\t\terror: {\n\t\t\t\t\tmessage: `La tarea '${task}' no está soportada por este agente.`,\n\t\t\t\t\ttype: \"UnsupportedCapability\"\n\t\t\t\t}\n\t\t\t}\n\t\t}\n\t];\n}\n\n// 2. Determinar el formato de entrada\nlet format = \"unknown\";\nif (typeof data === \"string\" || typeof data?.text === \"string\") {\n\tformat = \"text\";\n} else if (typeof data === \"object\") {\n\tformat = \"json\";\n}\n\n// 3. Validar inputFormat\nif (!supportedFormats.includes(format)) {\n\treturn [\n\t\t{\n\t\t\tjson: {\n\t\t\t\tsuccess: false,\n\t\t\t\terror: {\n\t\t\t\t\tmessage: `El formato de entrada '${format}' no está soportado por este agente.`,\n\t\t\t\t\ttype: \"UnsupportedInputFormat\"\n\t\t\t\t}\n\t\t\t}\n\t\t}\n\t];\n}\n\n// ✅ Si pasa ambas validaciones, continuar\nreturn [ { json: item } ];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        360,
        420
      ],
      "id": "04ea0111-873d-453d-b8b3-cb46867832b6",
      "name": "validate"
    },
    {
      "parameters": {
        "url": "=https://n8n.salesgenius.co/webhook/.well-known/agent.json",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Accept",
              "value": "application/json"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        40,
        420
      ],
      "id": "c7ea8bdb-7d58-414e-a8bd-98f8958cb821",
      "name": "HTTP Request"
    },
    {
      "parameters": {
        "content": "## Agent card ",
        "height": 260,
        "width": 340
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        0,
        0
      ],
      "typeVersion": 1,
      "id": "65a52183-2a1b-4e2d-aebe-09dd064f94ae",
      "name": "Sticky Note"
    },
    {
      "parameters": {
        "content": "## Validation ",
        "height": 320,
        "width": 660
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        0,
        300
      ],
      "typeVersion": 1,
      "id": "201c6ba5-0b97-4050-b13d-fa87f3429c8a",
      "name": "Sticky Note1"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "3fc91318-8ad6-4497-84fc-10ff9d4d3ee5",
              "name": "success",
              "value": "={{ $json.success }}",
              "type": "boolean"
            },
            {
              "id": "9a38b65d-d376-4cbb-ac3d-48bdce650ed7",
              "name": "error",
              "value": "={{ $json.error }}",
              "type": "object"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        780,
        100
      ],
      "id": "878afb88-e1df-413e-89eb-5d15e6e4bc57",
      "name": "Validation fail"
    },
    {
      "parameters": {
        "jsCode": "const rawOutput = $json.output || \"\"; \n// Buscar contenido entre <response>...</response>\nconst match = rawOutput.match(/<response>([\\s\\S]*?)<\\/response>/);\n\nif (!match) {\n  return [{\n    json: {\n      jsonrpc: \"2.0\",\n      error: {\n        code: -32700,\n        message: \"No se encontró una sección <response> válida.\"\n      },\n      id: 1\n    }\n  }];\n}\n\nconst content = match[1].trim();\n\n// Caso: error explícito\nif (content.includes(\"success: false\")) {\n  const errorMessage = content.match(/error:\\s*(.*)/)?.[1]?.trim() ?? \"Error desconocido\";\n  return [{\n    json: {\n      jsonrpc: \"2.0\",\n      error: {\n        code: -32000,\n        message: errorMessage\n      },\n      id: 1\n    }\n  }];\n}\n\n// Caso: éxito\nconst resultMatch = content.match(/result:\\s*([\\s\\S]*?)(?=\\nmetadata:|$)/);\nconst metadataMatch = content.match(/metadata:\\s*(\\{[\\s\\S]*\\})/);\n\nconst result = resultMatch?.[1]?.trim() ?? \"\";\nlet metadata = {};\n\ntry {\n  metadata = metadataMatch ? JSON.parse(metadataMatch[1]) : {};\n} catch (err) {\n  metadata = {};\n}\n\nreturn [{\n  json: {\n    jsonrpc: \"2.0\",\n    result: {\n      summary: result,\n      metadata\n    },\n    id: 1\n  }\n}];"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1100,
        320
      ],
      "id": "48a9f79e-2cbb-49c3-b6c0-1efa79bd2a14",
      "name": "JSON RPC agent output"
    },
    {
      "parameters": {
        "path": "/.well-known/agent.json",
        "responseMode": "lastNode",
        "options": {}
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2,
      "position": [
        40,
        100
      ],
      "id": "d6b86b9b-76f6-4cc6-b424-7d2d529e2c2c",
      "name": "Agent Card Webhook",
      "webhookId": "3f26c1e6-85c9-4d4b-9274-32a93349b48d"
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "/AgenteGemini",
        "responseMode": "lastNode",
        "options": {}
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2,
      "position": [
        -200,
        420
      ],
      "id": "dd9f1a54-2f0e-4ec7-b040-08e9c77a506a",
      "name": "Agent Webhook",
      "webhookId": "3f26c1e6-85c9-4d4b-9274-32a93349b48d"
    },
    {
      "parameters": {
        "description": "Utiliza esta herramienta para extraer el contenido de una url. Obtendrás como respuesta el contenido de la URL en formato markdown.",
        "workflowId": {
          "__rl": true,
          "value": "4f2Y9JpebK0YYH0G",
          "mode": "list",
          "cachedResultName": "JinAI url to markdown"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {
            "Url": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('Url', `La URL de la que se quiere obtener el contenido.`, 'string') }}"
          },
          "matchingColumns": [
            "Url"
          ],
          "schema": [
            {
              "id": "Url",
              "displayName": "Url",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        }
      },
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow",
      "typeVersion": 2.2,
      "position": [
        940,
        540
      ],
      "id": "8aac5234-ebe3-410b-ac9f-a88648859597",
      "name": "Call n8n Workflow Tool"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-23T14:13:13.880Z",
      "updatedAt": "2025-04-23T14:13:13.880Z",
      "role": "workflow:owner",
      "workflowId": "W6aLSh3xtVGMubzM",
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
  "triggerCount": 2,
  "updatedAt": "2025-04-23T20:48:19.000Z",
  "versionId": "68c74cd7-7d48-47ed-b986-872697dc5a73"
}