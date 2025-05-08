{
  "active": true,
  "connections": {
    "Webhook": {
      "main": [
        [
          {
            "node": "Convert to Config",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Convert to Config": {
      "main": [
        [
          {
            "node": "GitHub",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "GitHub": {
      "main": [
        [
          {
            "node": "GitHub1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Netlify": {
      "main": [
        [
          {
            "node": "Aggregate",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Aggregate": {
      "main": [
        [
          {
            "node": "OpenAI",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI": {
      "main": [
        [
          {
            "node": "Deploy to Netlify1",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Deploy to Netlify": {
      "main": [
        [],
        [
          {
            "node": "Netlify",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "GitHub1": {
      "main": [
        [
          {
            "node": "Deploy to Netlify",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-05-07T23:20:10.244Z",
  "id": "M1gcoDwtEFUHZeHm",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "Giveaway - Update Landing Page",
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "giveawayupdate",
        "options": {}
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2,
      "position": [
        -300,
        0
      ],
      "id": "9e721bf4-458d-49ff-9876-44fbbc5c4396",
      "name": "Webhook",
      "webhookId": "56a6fe4a-cbf2-4537-b398-2884c44c8ae5"
    },
    {
      "parameters": {
        "jsCode": "// n8n Code Node Snippet to format config.js content\n\n// 1. Get the JSON configuration data sent from the admin page\n//    Adjust '$('Webhook').first().json.body' if your webhook node has a different name\n//    or if the data structure is different.\nconst configData = $('Webhook').first().json.body;\n\n// 2. Check if data exists (basic validation)\nif (!configData || typeof configData !== 'object') {\n  throw new Error(\"Invalid or missing configuration data received from webhook.\");\n}\n\n// 3. Convert the JavaScript object (JSON) into a nicely formatted string\n//    'null' means no custom replacer function is used.\n//    '2' means use 2 spaces for indentation (adjust if you prefer tabs or different spacing).\nconst configJsonString = JSON.stringify(configData, null, 2);\n\n// 4. Construct the complete file content string\nconst fileContent = `const config = ${configJsonString};`;\n\n// 5. Return the formatted string in the n8n item structure.\n//    This makes 'fileContent' available to subsequent nodes (like the GitHub node).\n//    You can access it in the next node using an expression like: {{$json.fileContent}}\nreturn {\n  json: {\n    fileContent: fileContent\n  }\n};\n\n// Note: If you need to preserve other data from the incoming item, you might use:\n// return { json: { ...$item.json, fileContent: fileContent } };\n// However, for simply passing the content to a file update node, the above is usually sufficient.\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        -80,
        0
      ],
      "id": "05fa190b-aadf-4b16-bcd7-4f8ba85fc6a8",
      "name": "Convert to Config"
    },
    {
      "parameters": {
        "authentication": "oAuth2",
        "resource": "file",
        "operation": "edit",
        "owner": {
          "__rl": true,
          "value": "arslvn93",
          "mode": "list",
          "cachedResultName": "arslvn93",
          "cachedResultUrl": "https://github.com/arslvn93"
        },
        "repository": {
          "__rl": true,
          "value": "={{ $('Webhook').item.json.body.deploymentInfo.repoName }}",
          "mode": "name"
        },
        "filePath": "config.js",
        "fileContent": "={{ $json.fileContent }}",
        "commitMessage": "Update Site"
      },
      "type": "n8n-nodes-base.github",
      "typeVersion": 1.1,
      "position": [
        140,
        0
      ],
      "id": "10c2ecfc-dcef-4a0b-9711-c3e5c9d25ad6",
      "name": "GitHub",
      "webhookId": "b1ce1762-d639-4114-89e9-52cdbd9cf301",
      "credentials": {
        "githubOAuth2Api": {
          "id": "cAMFb9JqJCfPLpAg",
          "name": "GitHub account"
        }
      }
    },
    {
      "parameters": {
        "resource": "site",
        "operation": "getAll",
        "limit": 20
      },
      "type": "n8n-nodes-base.netlify",
      "typeVersion": 1,
      "position": [
        800,
        0
      ],
      "id": "f5313c35-59bc-4dbb-a14d-5151d338fa0a",
      "name": "Netlify",
      "credentials": {
        "netlifyApi": {
          "id": "s0lNLGUN6RJ2XWNm",
          "name": "Netlify account"
        }
      }
    },
    {
      "parameters": {
        "modelId": {
          "__rl": true,
          "value": "gpt-4o-mini",
          "mode": "list",
          "cachedResultName": "GPT-4O-MINI"
        },
        "messages": {
          "values": [
            {
              "content": "=find me the Netlify ID for the following name: {{ $('Webhook').item.json.body.deploymentInfo.repoName }}, return as netlify_id\n, nothing else\n\nHeres what to look through: {{ JSON.stringify($json[\"data\"]) }}"
            }
          ]
        },
        "jsonOutput": true,
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.openAi",
      "typeVersion": 1.8,
      "position": [
        1240,
        0
      ],
      "id": "21aba1e2-4522-4d08-8761-02bc4667b4f1",
      "name": "OpenAI",
      "credentials": {
        "openAiApi": {
          "id": "OLHtLOP5C47dG8d5",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "aggregate": "aggregateAllItemData",
        "options": {}
      },
      "type": "n8n-nodes-base.aggregate",
      "typeVersion": 1,
      "position": [
        1020,
        0
      ],
      "id": "17d3f209-8e74-46a0-abb5-678dc6781aeb",
      "name": "Aggregate"
    },
    {
      "parameters": {
        "method": "POST",
        "url": "=https://api.netlify.com/api/v1/sites/{{ $json.description }}/builds",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Authorization",
              "value": "Bearer nfp_gS8yuqjijxuzqwxXDh7qGeYZErfdrAic58d9"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        580,
        0
      ],
      "id": "7c030344-1bf3-496f-b0d3-be6b43e1572a",
      "name": "Deploy to Netlify",
      "onError": "continueErrorOutput"
    },
    {
      "parameters": {
        "method": "POST",
        "url": "=https://api.netlify.com/api/v1/sites/{{ $('OpenAI').first().json.message.content.netlify_id }}/builds",
        "sendHeaders": true,
        "headerParameters": {
          "parameters": [
            {
              "name": "Authorization",
              "value": "Bearer nfp_gS8yuqjijxuzqwxXDh7qGeYZErfdrAic58d9"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        1616,
        0
      ],
      "id": "850a5a16-9528-4b26-85bc-6e779d95bbe0",
      "name": "Deploy to Netlify1",
      "onError": "continueErrorOutput"
    },
    {
      "parameters": {
        "authentication": "oAuth2",
        "resource": "repository",
        "operation": "get",
        "owner": {
          "__rl": true,
          "value": "arslvn93",
          "mode": "list",
          "cachedResultName": "arslvn93",
          "cachedResultUrl": "https://github.com/arslvn93"
        },
        "repository": {
          "__rl": true,
          "value": "={{ $('Webhook').item.json.body.deploymentInfo.repoUrl }}",
          "mode": "url"
        }
      },
      "type": "n8n-nodes-base.github",
      "typeVersion": 1.1,
      "position": [
        360,
        0
      ],
      "id": "52ca3896-2244-43b3-aade-c106518c94b2",
      "name": "GitHub1",
      "webhookId": "b8f22add-ce5a-44aa-9689-4a5901e29300",
      "credentials": {
        "githubOAuth2Api": {
          "id": "cAMFb9JqJCfPLpAg",
          "name": "GitHub account"
        }
      }
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-05-07T23:20:10.260Z",
      "updatedAt": "2025-05-07T23:20:10.260Z",
      "role": "workflow:owner",
      "workflowId": "M1gcoDwtEFUHZeHm",
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
  "updatedAt": "2025-05-08T14:12:18.000Z",
  "versionId": "1fdbbdcc-a3a7-450b-81ef-89286a38f06b"
}