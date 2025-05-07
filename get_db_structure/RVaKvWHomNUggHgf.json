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
    "Edit Fields": {
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
  "createdAt": "2025-04-25T17:53:23.007Z",
  "id": "RVaKvWHomNUggHgf",
  "meta": null,
  "name": "get_db_structure",
  "nodes": [
    {
      "parameters": {
        "url": "=https://api.notion.com/v1/databases/{{ $json.id }}",
        "authentication": "predefinedCredentialType",
        "nodeCredentialType": "notionApi",
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        200,
        -220
      ],
      "id": "081f48ea-a185-4419-ab3d-050ea12ac638",
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
        420,
        -220
      ],
      "id": "caecd37b-0a35-4a95-bb1a-b5e2db32e24f",
      "name": "Edit Fields"
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
        0,
        -220
      ],
      "id": "c3663e61-8c9a-42cb-aa07-7913165abcc2",
      "name": "When Executed by Another Workflow"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-25T17:53:23.076Z",
      "updatedAt": "2025-04-25T17:53:23.076Z",
      "role": "workflow:owner",
      "workflowId": "RVaKvWHomNUggHgf",
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
  "updatedAt": "2025-04-29T13:28:07.000Z",
  "versionId": "b946cea7-fbd3-4a83-aa36-e22bf9fcdccd"
}