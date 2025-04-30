{
  "active": false,
  "connections": {
    "HTTP Request": {
      "main": [
        []
      ]
    },
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
  "createdAt": "2025-04-30T12:23:30.329Z",
  "id": "HVUF21XJwErOq8WK",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "get_db_data_by_id",
  "nodes": [
    {
      "parameters": {
        "url": "=https://api.notion.com/v1/pages/{{ $('When Executed by Another Workflow').item.json.id }}",
        "authentication": "predefinedCredentialType",
        "nodeCredentialType": "notionApi",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        -240,
        20
      ],
      "id": "b9cecff6-b921-41ed-abe3-fd8b65690fc2",
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
        "workflowInputs": {
          "values": [
            {
              "name": "id"
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
      "id": "3e88b07e-3b95-4042-8ee5-ac24443d7767",
      "name": "When Executed by Another Workflow"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-30T12:23:30.334Z",
      "updatedAt": "2025-04-30T12:23:30.334Z",
      "role": "workflow:owner",
      "workflowId": "HVUF21XJwErOq8WK",
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
  "updatedAt": "2025-04-30T13:28:37.000Z",
  "versionId": "0185a7e4-ce1b-45ab-81de-b5a84d33f6c0"
}