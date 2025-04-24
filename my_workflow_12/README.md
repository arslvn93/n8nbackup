{
  "active": true,
  "connections": {
    "Resumen": {
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
  "createdAt": "2025-04-23T18:43:58.464Z",
  "id": "16gZYcgsBb1mNI32",
  "meta": null,
  "name": "My workflow 12",
  "nodes": [
    {
      "parameters": {
        "path": "a2a"
      },
      "type": "@n8n/n8n-nodes-langchain.mcpTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "e290226b-1c4d-4859-a8a1-a27e2842318a",
      "name": "MCP Server Trigger",
      "webhookId": "f0900fb4-8372-4267-b150-b5f1fdabbd58"
    },
    {
      "parameters": {
        "description": "\"description\": \"Este agente resume textos largos para diferentes tipos de consumidor final. La respuesta dependera de como se le indique que haga su trabajo al consultarlo.\",\n\"capabilities\": [\n \"resume texto\", \"resume url content\"\n  ],\n",
        "workflowId": {
          "__rl": true,
          "value": "Vc7a76IVbIv1tVGr",
          "mode": "list",
          "cachedResultName": "My Sub-Workflow 1"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {
            "task": "={{ $fromAI('task', `La capacidad que se queire utiliar, debe ser unicamente una capacidad de la lista definida en la descripcion. Cualquier capacidad no definida sera descartada.`, 'string') }}",
            "data.text": "={{ $fromAI('data_text', `La consulta que se hara al agente para que realice la tarea definida, esta consulta puede contener informacion como detalles necesarios que mejoren la respuesta.`, 'string') }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "task",
              "displayName": "task",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string",
              "removed": false
            },
            {
              "id": "data.text",
              "displayName": "data.text",
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
        300,
        220
      ],
      "id": "1ac9f30a-b376-4de0-aa43-bf3dc47105b9",
      "name": "Resumen"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-23T18:43:58.469Z",
      "updatedAt": "2025-04-23T18:43:58.469Z",
      "role": "workflow:owner",
      "workflowId": "16gZYcgsBb1mNI32",
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
  "updatedAt": "2025-04-23T20:57:13.000Z",
  "versionId": "6bcebd26-a09d-43ff-a601-af0843982bd5"
}