{
  "active": false,
  "connections": {
    "get_db_structure": {
      "ai_tool": [
        [
          {
            "node": "MCP Server Trigger",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "get_db_data": {
      "ai_tool": [
        [
          {
            "node": "MCP Server Trigger",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "update_db_description_info": {
      "ai_tool": [
        [
          {
            "node": "MCP Server Trigger",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "insert_db_page_data": {
      "ai_tool": [
        [
          {
            "node": "MCP Server Trigger",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "update_db_page_data": {
      "ai_tool": [
        [
          {
            "node": "MCP Server Trigger",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "get_page_db_data_by_id": {
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
  "createdAt": "2025-04-28T13:46:58.443Z",
  "id": "XRNaPYvVL41Vn6ID",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "MCP Notion",
  "nodes": [
    {
      "parameters": {
        "authentication": "bearerAuth",
        "path": "notiondb"
      },
      "type": "@n8n/n8n-nodes-langchain.mcpTrigger",
      "typeVersion": 1,
      "position": [
        0,
        0
      ],
      "id": "f52a4410-b920-45a6-8b44-a823664996c4",
      "name": "MCP Server Trigger",
      "webhookId": "d578a497-0e6e-4fc2-86ba-e83cf7629ac6",
      "credentials": {
        "httpBearerAuth": {
          "id": "W8jPE6HrmWmbxBe2",
          "name": "MCPTEST"
        }
      }
    },
    {
      "parameters": {
        "description": "description:\n  title: \"Query a Notion Database\"\n  purpose: \"Allows querying any Notion database using a dynamically provided ID, retrieving specific data for use in other workflows.\"\n  when_to_use: |\n    - When you need to fetch records from a Notion database whose ID is known at runtime.\n    - Before performing analysis, validations, or transformations based on data stored in Notion.\n    - Whenever another workflow requires updated information from a specific record.\n  how_to_use: |\n    1. Make sure to provide as input the 'id' of the Notion database you want to query.\n    2. Upon execution, the tool sends an authenticated HTTP request to Notion using the provided ID.\n    3. The extracted data is transformed into three main fields:\n       - `properties`: All properties of the record.\n       - `name`: The content of the main title (`title[0].text.content`).\n       - `description`: The description text (`description[0].plain_text`).\n    4. The processed data becomes available for the next steps in the workflow.\n  important_notes: |\n    - The database ID must be valid and correspond to an existing database in Notion.\n    - Currently, the ID is hardcoded only for testing; in production, it is expected to be received dynamically.\n    - This tool performs read-only queries; it does not modify data in Notion.\n  quick_summary: |\n    🔹 Use this tool to read specific information from a Notion database.\n    🔹 Always provide a valid database ID.\n    🔹 Results will be ready for immediate use in your workflow.",
        "workflowId": {
          "__rl": true,
          "value": "RVaKvWHomNUggHgf",
          "mode": "list",
          "cachedResultName": "get_db_structure"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {
            "id": "={{ $fromAI('id', `El id de la db en Notion`, 'string') }}"
          },
          "matchingColumns": [
            "id"
          ],
          "schema": [
            {
              "id": "id",
              "displayName": "id",
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
        -260,
        280
      ],
      "id": "b364a748-fca6-4116-b74c-3a33c6c61089",
      "name": "get_db_structure"
    },
    {
      "parameters": {
        "description": "**description:**  \n  **title:** \"Generate Notion Database Query Using Natural Language\"  \n  **purpose:** \"Enables an agent to dynamically generate the body of a query for a Notion database using natural language. Based on a natural language description provided by the user, the tool generates a valid JSON object that will be used to query the Notion database.\"  \n  **when_to_use:** |  \n    - When you want to query a Notion database using a natural language description, without having to write the query directly in JSON format.  \n    - If you want the agent to generate custom queries based on parameters such as filters, sorts, and pagination specified by the user in natural language.  \n    - When a workflow needs to perform dynamic and flexible queries to Notion without predefined query parameters.  \n  **how_to_use:** |  \n    1. Provide a natural language input that describes what you want to retrieve from the database (e.g., \"Get the last 5 completed task records\").  \n    2. The agent processes the natural language input and automatically generates the query body in JSON format.  \n    3. The generated query includes appropriate parameters for querying the Notion database, such as filters (e.g., \"completed tasks\"), sorts (e.g., \"last 5 records\"), and pagination limits.  \n    4. The agent uses this query to fetch data from Notion automatically, without manual intervention.  \n    5. The query results are returned ready for use in other steps of the workflow.  \n  **important_notes:** |  \n    - The agent requires a clear and precise natural language input to generate a valid query for Notion.  \n    - The Notion database must be known, and its ID must be provided dynamically at runtime.  \n    - The agent does not validate the logic of the parameters; it only generates them based on the natural language description provided.  \n    - Although the agent can handle dynamic queries, the Notion database structure must be compatible with the filters and sorts the user wishes to apply.  \n    - The database ID must be valid and belong to an existing database in Notion.  \n  **quick_summary:** |  \n    🔹 Use this tool to generate custom queries against a Notion database using natural language.  \n    🔹 The agent converts your request into a ready-to-execute JSON object.  \n    🔹 Get the data you need without writing JSON directly — just describe your request in natural language.",
        "workflowId": {
          "__rl": true,
          "value": "MQ4jUvEfrheJ4nFl",
          "mode": "list",
          "cachedResultName": "get_db_data"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {
            "id": "={{ $fromAI('id', `id de la db`, 'string') }}",
            "query": "={{ $fromAI('query', `Consulta que se quiere realizar`, 'string') }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "id",
              "displayName": "id",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string"
            },
            {
              "id": "query",
              "displayName": "query",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string"
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        }
      },
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow",
      "typeVersion": 2.2,
      "position": [
        40,
        280
      ],
      "id": "c405b4e8-a771-4959-8777-be21857e7f3a",
      "name": "get_db_data"
    },
    {
      "parameters": {
        "description": "**description:**  \n  **title:** \"Update a Notion Database Description\"  \n  **purpose:** \"Allows dynamically modifying the description of a Notion database using its ID, facilitating the update of contextual information without manually interacting with the platform.\"  \n  **when_to_use:** |  \n    - When you need to automatically update the description of a Notion database within a workflow.  \n    - Whenever you want to reflect changes or add relevant information to an existing database without manual editing.  \n    - When another flow dynamically provides new descriptive text that must be synchronized with Notion.  \n  **how_to_use:** |  \n    1. Provide the following inputs:  \n       - `id`: The ID of the Notion database you want to update.  \n       - `description`: The new text you want to set as the database's description.  \n    2. The tool sends an authenticated `PATCH` HTTP request to the Notion API, submitting the new description content.  \n    3. After the update, the tool processes the response, extracting the following fields:  \n       - `properties`: All properties of the database.  \n       - `name`: The main title of the database (`title[0].text.content`).  \n       - `description`: The updated description text (`description[0].plain_text`).  \n    4. The updated data becomes available for use in subsequent steps of the workflow.  \n  **important_notes:** |  \n    - The provided ID must correspond to a valid and existing database in Notion.  \n    - The update only modifies the description field; it does not affect other properties of the database.  \n    - An active and valid Notion credential must be configured to execute the PATCH request.  \n    - Make sure the new description text does not exceed the limits allowed by the Notion API.  \n  **quick_summary:** |  \n    🔹 Use this tool to automatically update the description of a Notion database.  \n    🔹 You only need to provide the database ID and the new description content.  \n    🔹 Changes are reflected in real-time in Notion, and the updated data is ready for further use.",
        "workflowId": {
          "__rl": true,
          "value": "O6SPqC4lsVgdfyH6",
          "mode": "list",
          "cachedResultName": "update_db_description_info"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {
            "id": "={{ $fromAI('id', `El id de la db`, 'string') }}",
            "description": "={{ $fromAI('description', `La descripcion a cargar`, 'string') }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "id",
              "displayName": "id",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string"
            },
            {
              "id": "description",
              "displayName": "description",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string"
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        }
      },
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow",
      "typeVersion": 2.2,
      "position": [
        -100,
        280
      ],
      "id": "83aca76e-2fee-4b49-927e-134c08ccbc52",
      "name": "update_db_description_info"
    },
    {
      "parameters": {
        "description": "**title:** Create New Records in Notion from Natural Language Instructions  \n**purpose:** Enables dynamically recording information into a Notion database based on a natural language description, interpreting the content and automatically adapting it to the specific schema of the database.  \n**when_to_use:** |  \n  - When you want to create a new record in Notion by simply describing what you want to save, without needing to know the exact structure of the database.  \n  - If you need to automate the creation of tasks, ideas, notes, or other items in Notion from simple text inputs.  \n  - When another workflow generates data that must be automatically translated into a new item in a Notion database.  \n**how_to_use:** |  \n  1. Provide the ID of the Notion database where you want to create the new record.  \n  2. Send an instruction in natural language that describes the content of the new record.  \n  3. The tool will interpret the text, identify which fields should be filled, and automatically build a valid record compliant with the database schema.  \n**important_notes:** |  \n  - It is not necessary to know the database schema in advance; the tool detects it and adapts the record accordingly.  \n  - The title field must always be inferable from the description, since it’s mandatory in Notion.  \n  - Only fields whose content can be clearly deduced from the description will be included in the record.  \n**quick_summary:** |  \n  🔹 Use this tool to create records in Notion from natural language instructions.  \n  🔹 You only need the database ID and a description of the content to be recorded.  \n  🔹 Ideal for automating data entry without worrying about schema details.",
        "workflowId": {
          "__rl": true,
          "value": "WpgegqVk9wnmBrZT",
          "mode": "list",
          "cachedResultName": "insert_db_data"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {
            "id": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('id', ``, 'string') }}",
            "data": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('data', ``, 'string') }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "id",
              "displayName": "id",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string"
            },
            {
              "id": "data",
              "displayName": "data",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string"
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        }
      },
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow",
      "typeVersion": 2.2,
      "position": [
        320,
        280
      ],
      "id": "43e73e51-1a72-444b-bdbd-9b199e1e3e46",
      "name": "insert_db_page_data"
    },
    {
      "parameters": {
        "description": "Aquí tienes la traducción al inglés del *system prompt*, manteniendo exactamente el mismo formato que el original:\n\n---\n\n**title:** \"Create Record in Notion Database Using Natural Language\"  \n**purpose:**  \nAllows an agent to automatically generate the body of a JSON-formatted request to create a new record in a Notion database, using only a natural language description provided by the user and the corresponding database ID as input. The tool dynamically adapts the structure of the request based on the actual schema of the database.\n\n**when_to_use:** |  \n  - When you need to register new information in a Notion database without manually defining the JSON format required by the API.  \n  - If a user describes a task, activity, or other content in natural language and you want to automatically translate it into a Notion-compatible record.  \n  - In workflows where you want to automate record creation in Notion without assuming the field structure in advance.\n\n**how_to_use:** |  \n  1. Provide the following inputs:  \n     - The ID of the Notion database.  \n     - A clear natural language description of what you want to record (e.g., \"Register a high-priority task to review the weekly report\").  \n  2. The agent automatically queries the database schema to identify available fields, their types, and any valid options.  \n  3. Based on the description, the agent identifies relevant properties (such as title, status, date, etc.) and assigns values compatible with the schema.  \n  4. A JSON object is built that strictly follows the structure and validations required by the Notion API.  \n  5. The generated JSON body is used to send the request for creating the new record in Notion.\n\n**important_notes:** |  \n  - The database ID must be valid and correspond to a database accessible by the agent.  \n  - The title field will always be generated if required, even if not explicitly mentioned in the description.  \n  - Only properties that can be clearly inferred from the user's message will be included in the request.  \n  - The tool dynamically adapts to the database schema; it does not assume fixed properties or predefined formats.  \n  - Properties are validated according to their type (e.g., ISO date format, valid select lists), avoiding type mismatches or empty fields.\n\n**quick_summary:** |  \n  🔹 Use this tool to add new items to a Notion database using only natural language.  \n  🔹 The agent analyzes the actual database schema and generates a valid JSON body for Notion.  \n  🔹 Save time and avoid errors: no need to know the database structure or write JSON manually.",
        "workflowId": {
          "__rl": true,
          "value": "1oSNKAvsISWkUSlP",
          "mode": "list",
          "cachedResultName": "update_db_page_data"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {
            "id": "={{ $fromAI('id', `id del registro a actualizar`, 'string') }}",
            "data": "={{ $fromAI('data', `LA información a actualizar`, 'string') }}"
          },
          "matchingColumns": [],
          "schema": [
            {
              "id": "id",
              "displayName": "id",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string"
            },
            {
              "id": "data",
              "displayName": "data",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "canBeUsedToMatch": true,
              "type": "string"
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        }
      },
      "type": "@n8n/n8n-nodes-langchain.toolWorkflow",
      "typeVersion": 2.2,
      "position": [
        500,
        280
      ],
      "id": "e0136efb-6fe0-4a7c-a15b-ffef9e539c4d",
      "name": "update_db_page_data"
    },
    {
      "parameters": {
        "description": "Aquí tienes la traducción al inglés del *system prompt*, manteniendo exactamente el mismo formato que el original:\n\n---\n\n**description:**  \n  **title:** \"Get Notion Page by ID\"  \n  **purpose:** \"Allows an agent to dynamically retrieve the information of a Notion page using its unique ID. Given the provided ID, the tool fetches the complete JSON object of the page.\"  \n  **when_to_use:** |  \n    - When you need to query a specific Notion page using its ID, without writing the request manually.  \n    - If a workflow requires inspecting or processing page data before proceeding with other actions.  \n    - When extracting metadata or properties from a page for use in subsequent automated steps.  \n  **how_to_use:** |  \n    1. Provide as input the ID of the Notion page you want to retrieve.  \n    2. The tool sends a GET request to the Notion API's v1/pages/{id} endpoint using configured credentials.  \n    3. A JSON object is received containing all the properties, metadata, and structure of the page.  \n    4. The agent delivers the retrieved data ready for use in the next steps of the workflow.  \n  **important_notes:** |  \n    - The page ID must be valid and correspond to an existing page in Notion.  \n    - The Notion credential must have read permissions on the requested page.  \n    - The tool does not filter or transform the response; it returns the full JSON object.  \n    - You can check the archived status using the `archived` field in the response.  \n  **quick_summary:** |  \n    🔹 Dynamically retrieve a Notion page by its ID.  \n    🔹 Returns a complete JSON object with all properties and metadata.  \n    🔹 Useful for inspecting and preparing data before other processes.",
        "workflowId": {
          "__rl": true,
          "value": "HVUF21XJwErOq8WK",
          "mode": "list",
          "cachedResultName": "get_db_data_by_id"
        },
        "workflowInputs": {
          "mappingMode": "defineBelow",
          "value": {
            "id": "={{ $fromAI('id', `id de la db`, 'string') }}"
          },
          "matchingColumns": [
            "id"
          ],
          "schema": [
            {
              "id": "id",
              "displayName": "id",
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
        680,
        280
      ],
      "id": "fef1d575-b4e9-4f14-8d0f-73d2ca405bbd",
      "name": "get_page_db_data_by_id"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-28T13:46:58.448Z",
      "updatedAt": "2025-04-28T13:46:58.448Z",
      "role": "workflow:owner",
      "workflowId": "XRNaPYvVL41Vn6ID",
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
  "updatedAt": "2025-04-30T16:55:37.000Z",
  "versionId": "ba7786ce-5742-432f-9e8c-0769b643489d"
}