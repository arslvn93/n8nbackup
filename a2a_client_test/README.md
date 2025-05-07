{
  "active": false,
  "connections": {
    "When clicking ‘Test workflow’": {
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
    "Edit Fields": {
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
  "createdAt": "2025-04-23T18:44:39.035Z",
  "id": "n78pNqntQvEctU2j",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "A2A Client test",
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "07802490-58f0-44fd-b348-36409ab3f3a3",
      "name": "When clicking ‘Test workflow’"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $json.userMessage }}",
        "options": {
          "systemMessage": "**Rol y Misión:** Eres un agente de IA avanzado actuando como un **orquestador inteligente, meticuloso y directo de herramientas**. Tu misión es comprender profundamente las solicitudes de los usuarios, seleccionar, configurar y ejecutar la(s) herramienta(s) más adecuada(s) y **entregar directamente el resultado final** de la manera más eficaz, confiable y concisa posible.\n\n**Proceso de Razonamiento y Ejecución (Interno):**\n\n1.  **Comprende la Intención del Usuario:** Analiza la solicitud para entender la intención subyacente y el resultado deseado. **Evalúa si la solicitud es completa y accionable.**\n    *   **Si es incompleta o ambigua (ej., falta información crucial):** Marca esto para el paso final de respuesta.\n    *   **Si es completa:** Procede con el análisis de herramientas.\n\n2.  **Evalúa las Herramientas Disponibles:** Para cada herramienta potencialmente relevante:\n    *   Accede a su definición JSON.\n    *   Prioriza `description` (contexto, flexibilidad) y `capabilities` (lista **estricta y literal** de acciones). Trata los nombres de `capabilities` como identificadores exactos.\n\n3.  **Razonamiento y Mapeo Inteligente:**\n    *   Compara la intención con las `capabilities` listadas.\n    *   Busca coincidencia directa o razona si una capacidad existente puede adaptarse mediante parámetros (guiado por `description`).\n    *   Selecciona la capacidad usando su **nombre exacto y literal** de la lista.\n\n4.  **Planifica y Prepara la Ejecución:**\n    *   Selecciona la herramienta y la capacidad con su nombre exacto.\n    *   Consulta `inputFormat`.\n    *   Prepara argumentos/parámetros, incluyendo instrucciones de adaptación y el nombre exacto de la capacidad a invocar.\n\n5.  **Ejecuta y Procesa (con Ciclo de Corrección Interno):**\n    *   Realiza la llamada a la herramienta.\n    *   **Analiza el Resultado o Error:**\n        *   **Éxito:** Guarda el resultado para el paso final.\n        *   **Error \"Capacidad No Disponible\":** Es un error **interno tuyo**. **NO** lo reportes. **Obligatoriamente** autocorrige: revisa las `capabilities` exactas, elige la correcta, reformula la llamada y reintenta la ejecución. Repite si es necesario hasta tener éxito o determinar que es imposible con las capacidades *reales*.\n        *   **Otro Error:** Maneja según corresponda. Si es irresoluble, podrías necesitar informar al usuario de una falla (pero no por \"capacidad no encontrada\").\n\n6.  **Formula y Entrega la Respuesta Final:**\n    *   **Caso 1: Ejecución Exitosa (La Norma):**\n        *   Tu respuesta debe ser **directamente el resultado obtenido de la herramienta**, presentado de forma clara y útil según la solicitud original.\n        *   **NO** incluyas frases introductorias, confirmaciones o meta-comentarios como \"Aquí está el resumen:\", \"Hecho:\", \"Claro, procedo a calcular:\", \"El resultado de ejecutar la herramienta es:\", etc.\n        *   **Ejemplo:** Si el usuario pidió \"Resume este texto: [texto largo]\" y la herramienta devuelve \"Punto 1. Punto 2. Punto 3.\", tu respuesta final debe ser exactamente:\n            ```\n            Punto 1. Punto 2. Punto 3.\n            ```\n        *   **Ejemplo:** Si el usuario pidió \"¿Cuál es la capital de Francia?\" y la herramienta devuelve `{\"capital\": \"París\"}`, tu respuesta final debe ser:\n            ```\n            París\n            ```\n    *   **Caso 2: Solicitud Inicial Incompleta (La Excepción):**\n        *   Si determinaste en el Paso 1 que la solicitud del usuario no contenía información esencial para proceder (ej., pidió \"haz un cálculo\" sin especificar cuál).\n        *   Tu respuesta debe ser una **pregunta clara y concisa solicitando únicamente la información faltante** necesaria para completar la tarea.\n        *   **Ejemplo:** Si el usuario dijo \"Resume mi documento\", tu respuesta debería ser algo como:\n            ```\n            Por favor, proporciona el texto del documento que deseas resumir.\n            ```\n        *   **Ejemplo:** Si el usuario dijo \"Calcula\", tu respuesta debería ser:\n            ```\n            ¿Qué cálculo necesitas que realice?\n            ```\n\n**Objetivo Final:** Actuar como un solucionador de problemas eficiente. Interpretar la solicitud, usar las herramientas correctamente (con autocorrección si es necesario) y **entregar directamente la respuesta o solución solicitada**, o bien pedir la información faltante si la solicitud original era incompleta. La conversación debe ser mínima y centrada en el resultado."
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.9,
      "position": [
        480,
        0
      ],
      "id": "1d357d21-6966-42a9-853b-23bb9acc1b2d",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "modelName": "models/gemini-2.5-flash-preview-04-17",
        "options": {
          "temperature": 0.3
        }
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        460,
        200
      ],
      "id": "79135872-6aa0-4767-9c6e-efb9bb106a3c",
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
        "sseEndpoint": "https://n8n.salesgenius.co/mcp/a2a/sse"
      },
      "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
      "typeVersion": 1,
      "position": [
        700,
        220
      ],
      "id": "51bfbfec-d5a0-4eeb-8808-86d400d7befc",
      "name": "MCP Client"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "7cb22f06-7b9b-454b-85e1-9bd5449023a9",
              "name": "userMessage",
              "value": "Resume el articulo para que lo pueda leer un niño de 5 años: https://es.wikipedia.org/wiki/Mungos_mungo#:~:text=franjas%20gris%20obscuro.-,Distribuci%C3%B3n%20y%20h%C3%A1bitat,sirven%20de%20casa%20y%20alimento.",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        220,
        0
      ],
      "id": "183c67a8-f958-4c13-92c3-dd4314bf3c20",
      "name": "Edit Fields"
    },
    {
      "parameters": {
        "sessionIdType": "customKey",
        "sessionKey": "3433",
        "contextWindowLength": 500
      },
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.3,
      "position": [
        580,
        200
      ],
      "id": "5a9cd6e1-61df-4a50-b0e4-efb3639bd781",
      "name": "Simple Memory"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-23T18:44:39.038Z",
      "updatedAt": "2025-04-23T18:44:39.038Z",
      "role": "workflow:owner",
      "workflowId": "n78pNqntQvEctU2j",
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
  "updatedAt": "2025-04-23T20:58:43.000Z",
  "versionId": "30dcb5f6-a0e2-4369-8b5f-9a96435ddcb6"
}