{
  "active": true,
  "connections": {
    "Webhook": {
      "main": [
        [
          {
            "node": "Notion",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-05-02T19:58:01.494Z",
  "id": "K4ZskyYXyIyUQTja",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "Open House Site - Form Submissions",
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "openhouse",
        "options": {}
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2,
      "position": [
        -400,
        0
      ],
      "id": "fb1b561d-b43a-4d1d-b886-ac716d6bd5e0",
      "name": "Webhook",
      "webhookId": "c8f3eec5-92fd-4cb4-a3cd-4606d36acd93"
    },
    {
      "parameters": {
        "resource": "databasePage",
        "databaseId": {
          "__rl": true,
          "value": "1ed1d08c-4f5a-80d5-95fa-c072acd33579",
          "mode": "list",
          "cachedResultName": "Open House Leads",
          "cachedResultUrl": "https://www.notion.so/1ed1d08c4f5a80d595fac072acd33579"
        },
        "title": "={{ $json.body.fullName }}",
        "propertiesUi": {
          "propertyValues": [
            {
              "key": "Email|email",
              "emailValue": "={{ $json.body.email }}"
            },
            {
              "key": "Phone|phone_number",
              "phoneValue": "={{ $json.body.phone }}"
            },
            {
              "key": "Question 1|rich_text",
              "textContent": "={{ $json.body.questions[0].answer }}"
            },
            {}
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.notion",
      "typeVersion": 2.2,
      "position": [
        -180,
        0
      ],
      "id": "e97208d3-e4fa-4414-b63d-5f7206da5907",
      "name": "Notion",
      "credentials": {
        "notionApi": {
          "id": "3EhNxVoPGBbOY9vC",
          "name": "Notion account"
        }
      }
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-05-02T19:58:01.503Z",
      "updatedAt": "2025-05-02T19:58:01.503Z",
      "role": "workflow:owner",
      "workflowId": "K4ZskyYXyIyUQTja",
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
  "triggerCount": 1,
  "updatedAt": "2025-05-08T16:11:50.000Z",
  "versionId": "a472de9f-40d7-46d1-b79d-4792ff3f05a0"
}