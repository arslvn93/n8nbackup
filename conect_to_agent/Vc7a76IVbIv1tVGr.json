{
  "active": false,
  "connections": {
    "When Executed by Another Workflow": {
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
  "createdAt": "2025-04-23T19:20:39.742Z",
  "id": "Vc7a76IVbIv1tVGr",
  "meta": null,
  "name": "conect to agent",
  "nodes": [
    {
      "parameters": {
        "workflowInputs": {
          "values": [
            {
              "name": "task"
            },
            {
              "name": "data.text"
            }
          ]
        }
      },
      "id": "c055762a-8fe7-4141-a639-df2372f30060",
      "typeVersion": 1.1,
      "name": "When Executed by Another Workflow",
      "type": "n8n-nodes-base.executeWorkflowTrigger",
      "position": [
        260,
        340
      ]
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://n8n.salesgenius.co/webhook/AgenteGemini",
        "sendBody": true,
        "bodyParameters": {
          "parameters": [
            {
              "name": "task",
              "value": "={{ $json.task }}"
            },
            {
              "name": "data.text",
              "value": "={{ $json['data.text'] }}"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        480,
        340
      ],
      "id": "80d35e42-0689-4992-a9f0-edff27da2e2c",
      "name": "HTTP Request"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-23T19:20:39.750Z",
      "updatedAt": "2025-04-23T19:20:39.750Z",
      "role": "workflow:owner",
      "workflowId": "Vc7a76IVbIv1tVGr",
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
  "updatedAt": "2025-04-23T20:57:19.000Z",
  "versionId": "d212061b-83ac-44d0-9f13-a21c77cd75fe"
}