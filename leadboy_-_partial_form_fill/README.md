{
  "active": true,
  "connections": {
    "Webhook": {
      "main": [
        [
          {
            "node": "answers",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "answers": {
      "main": [
        [
          {
            "node": "Notion",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Enrich Realtor Data": {
      "main": [
        [
          {
            "node": "Wait",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Wait": {
      "main": [
        [
          {
            "node": "Notion1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Notion1": {
      "main": [
        [
          {
            "node": "Notion2",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Notion": {
      "main": [
        [
          {
            "node": "Enrich Realtor Data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-04-23T13:42:48.420Z",
  "id": "DRI2pTTOhCO3Rqnp",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "LEADBOY - Partial Form Fill",
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "leadboy",
        "options": {
          "allowedOrigins": "*",
          "noResponseBody": false,
          "rawBody": false,
          "responseData": ""
        }
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2,
      "position": [
        -1580,
        -80
      ],
      "id": "ce513943-2c45-49d1-95d9-bb865dac3139",
      "name": "Webhook",
      "webhookId": "a784d83c-117b-42b0-a634-ff76ac7b5f21"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "4c4e6a4d-8ef2-41c8-b48e-d9742b5728e3",
              "name": "Full Name",
              "value": "={{ $json.body['Full Name:'] }}",
              "type": "string"
            },
            {
              "id": "21a82209-5199-45b0-a281-c26dbfa52696",
              "name": "Brokerage Name",
              "value": "={{  $json.body['Brokerage:'] }}",
              "type": "string"
            },
            {
              "id": "671cfbd4-f642-4b03-885d-908199c0e6b4",
              "name": "Email Address",
              "value": "={{  $json.body['Email Address:'] }}",
              "type": "string"
            },
            {
              "id": "3fa7bda9-0ba9-4cc1-b3d9-d65afea6a3bb",
              "name": "Primary Market Location",
              "value": "={{ $json.body['Primary Market Location:'] }}",
              "type": "string"
            },
            {
              "id": "4684d804-b7ae-4634-a138-0b73df417154",
              "name": "Phone Number",
              "value": "={{ $json.body[\"Phone Number:\"] }}",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        -1360,
        -80
      ],
      "id": "d3bbee96-74ef-417d-a1df-9d10b899f797",
      "name": "answers"
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://n8n.salesgenius.co/webhook/createRealtor",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Authorization",
              "value": "Bearer TU_TOKEN_AQUI"
            }
          ]
        },
        "sendBody": true,
        "bodyParameters": {
          "parameters": [
            {
              "name": "Name",
              "value": "={{ $('answers').first().json[\"Full Name\"] }}"
            },
            {
              "name": "Phone",
              "value": "={{ $('answers').first().json[\"Phone Number\"] }}"
            },
            {
              "name": "Email",
              "value": "={{ $('answers').first().json[\"Email Address\"] }}"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        -920,
        -80
      ],
      "id": "3c169d8d-88e1-4f49-90d9-c936722af525",
      "name": "Enrich Realtor Data"
    },
    {
      "parameters": {
        "amount": 2
      },
      "type": "n8n-nodes-base.wait",
      "typeVersion": 1.1,
      "position": [
        -700,
        -80
      ],
      "id": "3eeee8b3-134f-4ae9-97d4-361eacf31dec",
      "name": "Wait",
      "webhookId": "9dd7f964-20ff-4942-ad9b-9dcb3b3b1771"
    },
    {
      "parameters": {
        "resource": "databasePage",
        "operation": "getAll",
        "databaseId": {
          "__rl": true,
          "value": "1c81d08c-4f5a-80a7-bf00-efa7ae44e0d8",
          "mode": "list",
          "cachedResultName": "Realtor Enrichment",
          "cachedResultUrl": "https://www.notion.so/1c81d08c4f5a80a7bf00efa7ae44e0d8"
        },
        "filterType": "manual",
        "filters": {
          "conditions": [
            {
              "key": "Email|email",
              "condition": "equals",
              "emailValue": "={{ $('answers').first().json[\"Email Address\"] }}"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.notion",
      "typeVersion": 2.2,
      "position": [
        -480,
        -80
      ],
      "id": "b4c4708d-9cae-4843-91d5-7a0235e99f75",
      "name": "Notion1",
      "retryOnFail": true,
      "maxTries": 2,
      "credentials": {
        "notionApi": {
          "id": "3EhNxVoPGBbOY9vC",
          "name": "Notion account"
        }
      },
      "onError": "continueErrorOutput"
    },
    {
      "parameters": {
        "resource": "databasePage",
        "operation": "update",
        "pageId": {
          "__rl": true,
          "value": "={{ $('Notion').item.json.id }}",
          "mode": "id"
        },
        "propertiesUi": {
          "propertyValues": [
            {
              "key": "Realtor Enrichment|relation",
              "relationValue": [
                "={{ $json.id}}"
              ]
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.notion",
      "typeVersion": 2.2,
      "position": [
        -260,
        -80
      ],
      "id": "403fd53c-9177-4a91-b644-fff840557d88",
      "name": "Notion2",
      "credentials": {
        "notionApi": {
          "id": "3EhNxVoPGBbOY9vC",
          "name": "Notion account"
        }
      }
    },
    {
      "parameters": {
        "resource": "databasePage",
        "databaseId": {
          "__rl": true,
          "value": "1c31d08c-4f5a-801f-9b45-ce1f49d8b97f",
          "mode": "list",
          "cachedResultName": "Leadboy Sign Ups",
          "cachedResultUrl": "https://www.notion.so/1c31d08c4f5a801f9b45ce1f49d8b97f"
        },
        "title": "={{ $json[\"Full Name\"] }}",
        "propertiesUi": {
          "propertyValues": [
            {
              "key": "Brokerage|rich_text",
              "textContent": "={{ $json[\"Brokerage Name\"] }}"
            },
            {
              "key": "Email|email",
              "emailValue": "={{ $json[\"Email Address\"] }}"
            },
            {
              "key": "Market Location|rich_text",
              "textContent": "={{ $json[\"Primary Market Location\"] }}"
            },
            {
              "key": "Phone Number|phone_number",
              "phoneValue": "={{ $json[\"Phone Number\"] }}"
            },
            {
              "key": "Form Completion|select",
              "selectValue": "Partial"
            },
            {
              "key": "Submission Date|date",
              "date": "2025-04-23T10:32:24"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.notion",
      "typeVersion": 2.2,
      "position": [
        -1140,
        -80
      ],
      "id": "031cbe64-8b05-4fa7-9d6f-1bf62fa9c76c",
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
      "createdAt": "2025-04-23T13:42:48.433Z",
      "updatedAt": "2025-04-23T13:42:48.433Z",
      "role": "workflow:owner",
      "workflowId": "DRI2pTTOhCO3Rqnp",
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
  "tags": [
    {
      "createdAt": "2025-02-21T17:21:41.750Z",
      "updatedAt": "2025-02-21T17:21:41.750Z",
      "id": "hCxs00bYB7kqJnEo",
      "name": "WORKING"
    }
  ],
  "triggerCount": 1,
  "updatedAt": "2025-04-23T14:39:03.000Z",
  "versionId": "c00abf42-e7b9-4a10-9221-c4136a5835cf"
}