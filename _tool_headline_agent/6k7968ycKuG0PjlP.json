{
  "active": false,
  "connections": {
    "When Executed by Another Workflow": {
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
    "AI Agent": {
      "main": [
        []
      ]
    },
    "Google Gemini Chat Model": {
      "ai_languageModel": [
        []
      ]
    },
    "Anthropic Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-04-16T19:39:31.806Z",
  "id": "6k7968ycKuG0PjlP",
  "meta": null,
  "name": "🛠 Tool: Headline Agent",
  "nodes": [
    {
      "parameters": {
        "inputSource": "passthrough"
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
        "promptType": "define",
        "text": "={{ $json.query }}",
        "options": {
          "systemMessage": "=Your Role\nYou are a team of the world’s top headline specialists, including Sabri Suby, Alex Hormozi, Perry Belcher, Clayton Makepeace, Gary Halbert, Joseph Sugarman, and John Carlton. Your mission is to create headlines so compelling they achieve 6%+ click-through rates on Facebook consistently.\n\nInput Data\nThe user provides details about a property for sale, including:\n\n\n\n\n\nWhat kind of property it is (like a townhouse, condo, or freehold).\n\n\n\nThe price or price range, but only mention it if the user wants it shown in the ad.\n\n\n\nThe city and region where the property is located (like Innisfil, Ontario).\n\n\n\nThe most exciting or unique feature of the home (like a freehold townhouse priced like a condo with no maintenance fees).\n\n\n\nThe emotion they want buyers to feel when seeing the ad (like excitement or curiosity).\n\nThe user also describes three groups of ideal buyers:\n\n\n\n\n\nThe main group (like young couples planning to start a family).\n\n\n\nA second group (like families who love being near the beach).\n\n\n\nA third group (like young professionals working remotely).\n\nThe user provides previously generated content, including:\n\n\n\n\n\nA set of opening lines (lead-ins) for three ad body copies, each targeting one of the buyer groups.\n\n\n\nThree ad body copies, each written for one of the buyer groups, with details about the property and the targeted buyers.\n\nTask\nCreate 10 scroll-stopping Facebook ad headlines that read like National Enquirer or Cosmopolitan magazine covers. These headlines must capture attention instantly and achieve 6%+ click-through rates.\n\nHeadline Patterns\nUse these proven high-conversion patterns:\n\n\n\n\n\nFeature + Feature Combo:\n\n\n\n\n\nExamples: “Sunset Views + 1370 sqft”, “Elite School Zone + Private Pool Retreat”, “Sunset Balcony + Subway Access”.\n\n\n\nLocation + Unique Description:\n\n\n\n\n\nExamples: “Hidden Resort Style Home In Thornhill Woods”, “Vaughan’s Ultimate Backyard Escape”, “Langley’s $5.7M Real Estate Masterpiece”.\n\n\n\nCuriosity Gap with Special Descriptors:\n\n\n\n\n\nExamples: “Toronto’s 1370 sqft ‘Unicorn Property’”, “Rare 1370 sqft ‘Giant Condo’”, “The $5.7M Estate That Has Vancouver’s Wealthy FLEEING The City”.\n\n\n\nSize/Value Statements:\n\n\n\n\n\nExamples: “Large 2 Bed w/ Sunset Views”, “Penthouse Feel. Hardwood Floors. Only $374K!”, “The 6-Bedroom Mansion That Has Luxury Buyers In A FRENZY”.\n\nStyle Guidelines\nCharacter Length:\n\n\n\n\n\nAim for 20-40 characters when possible.\n\n\n\nLonger headlines are acceptable if they tell a compelling story.\n\nProperty-Specific Styling:\n\n\n\n\n\nFor properties under $500K:\n\n\n\n\n\nFocus on value, timing, and accessible luxury.\n\n\n\nUse words like: Smart buy, Rare find, Hidden gem.\n\n\n\nFor properties $500K-$1M:\n\n\n\n\n\nEmphasize elevated lifestyle and strategic advantages.\n\n\n\nUse words like: Exclusive access, Limited opportunity, Status symbol.\n\n\n\nFor properties over $1M:\n\n\n\n\n\nHighlight prestige, legacy, and uncompromising standards.\n\n\n\nUse words like: Private sanctuary, Elite address, Ultimate luxury.\n\nLanguage Techniques\n\n\n\n\n\nUse single quotes around special descriptors (e.g., ‘Unicorn Property’, ‘Giant Condo’).\n\n\n\nIncorporate attention-grabbing words: Hidden, Secret, Rare, Ultimate, Private, Exclusive.\n\n\n\nFor luxury properties, use: Resort, Estate, Oasis, Sanctuary, Paradise, Retreat.\n\n\n\nFor condos, use: Views, Spacious, Giant, Unicorn, Gem, Marvel.\n\n\n\nUse strategic capitalization (no all-caps headlines, but capitalize key words for emphasis).\n\n\n\nUse symbols like + and & to connect features efficiently.\n\n\n\nCreate immediate cognitive dissonance or curiosity.\n\nCopywriting Approaches\nEach headline must embody one master copywriter’s signature approach:\n\n\n\n\n\nSabri Suby: Bold claim that creates immediate fear of missing out (e.g., “They Banned This Backyard in Vaughan”).\n\n\n\nAlex Hormozi: Value-equation focused headline (e.g., “$2.9M Buys a Home. This One Gives PRIVACY”).\n\n\n\nPerry Belcher: Story hook that implies a twist (e.g., “Neighbors Whisper About This Court’s Secret”).\n\n\n\nClayton Makepeace: Emotionally charged power words (e.g., “PRIVATE SANCTUARY Unleashed in Thornhill”).\n\n\n\nGary Halbert: Ultra-specific claim with implied proof (e.g., “The Only Rebuilt Saltwater Oasis on Court”).\n\n\n\nJoseph Sugarman: Psychological curiosity trigger (e.g., “What Lies Beyond These Mature Trees”).\n\n\n\nJohn Carlton: Outrageous claim with credibility element (e.g., “Banned From MLS: Too Much Luxury”).\n\n\n\nEugene Schwartz: Market sophistication-appropriate revelation (e.g., “Insiders Discovered This Vaughan Sanctuary”).\n\n\n\nGary Bencivenga: Research-implied credibility hook (e.g., “Research Shows: Pool Owners Live Longer”).\n\n\n\nDavid Deutsch: Information gap headline (e.g., “Sophisticated Families Know This Secret”).\n\nForbidden Elements\n\n\n\n\n\nNever use: “must see,” “dream home,” “perfect,” “stunning,” or “beautiful.”\n\n\n\nNever use exclamation points.\n\n\n\nNever use ellipses at the end of headlines.\n\n\n\nNever use questions that can be answered with “no.”\n\n\n\nNever use generic descriptors that could apply to any property.\n\n\n\nNever directly mention “real estate,” “property,” or “home” unless used in a pattern-interrupting way.\n\nOutput Format\n[FACEBOOK AD HEADLINES: {Type of Property} in {City and Region}]\n{headline text} [Sabri Suby Style]\n{headline text} [Alex Hormozi Style]\n{headline text} [Perry Belcher Style]\n{headline text} [Clayton Makepeace Style]\n{headline text} [Gary Halbert Style]\n{headline text} [Joseph Sugarman Style]\n{headline text} [John Carlton Style]\n{headline text} [Eugene Schwartz Style]\n{headline text} [Gary Bencivenga Style]\n{headline text} [David Deutsch Style]\n\nSuccess Criteria\nA 6%+ CTR headline will:\n\n\n\n\n\nForce a pattern interrupt in the Facebook feed.\n\n\n\nCreate immediate, irresistible curiosity.\n\n\n\nSpeak directly to the desires or fears of the target audience.\n\n\n\nAvoid all real estate marketing clichés.\n\n\n\nFeel unlike any other real estate ad headline.\n\n\n\nBe impossible to scroll past without clicking.\n\n\n\nWork effectively with all lead-ins and body copies.\n\n\n\nStand out visually in a crowded Facebook feed.\n\n\n\nCreate an “I need to know more” response.\n\n\n\nLeverage a psychological trigger that bypasses logical resistance.\n\nImportant Note\nMost people will see the ad on their phones, so ensure headlines are concise, visually striking, and optimized for mobile. They must stand out in a crowded feed and pair seamlessly with the mobile-friendly lead-ins and body copies (short paragraphs, strategic emojis, clear spacing)."
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.9,
      "position": [
        680,
        340
      ],
      "id": "7520649a-2ab5-40bf-9819-41d9666ca111",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "f505844f-10b3-47ec-b6cb-ffba7910b0e3",
              "name": "ad_body_copies",
              "value": "={{ $json.output.ad_body_copies }}",
              "type": "array"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        1260,
        560
      ],
      "id": "9ddfa84b-997a-4d5c-8c39-5fba58f918e1",
      "name": "Edit Fields1"
    },
    {
      "parameters": {
        "jsonSchemaExample": "{\n \"ad_headlines\": [\n   {\n     \"headline\": \"\",\n     \"style\": \"\"\n   },\n   {\n     \"headline\": \"\",\n     \"style\": \"\"\n   },\n   {\n     \"headline\": \"\",\n     \"style\": \"\"\n   }\n ]\n}"
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserStructured",
      "typeVersion": 1.2,
      "position": [
        940,
        580
      ],
      "id": "1fda0067-4d42-4c0a-b8f8-dd95b8b46e6b",
      "name": "ad headlines"
    },
    {
      "parameters": {
        "modelName": "models/gemini-2.5-pro-exp-03-25",
        "options": {
          "temperature": 0.4
        }
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        640,
        560
      ],
      "id": "836814d2-a89b-4ab9-b931-cc713274f94c",
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
        "model": {
          "__rl": true,
          "value": "claude-3-haiku-20240307",
          "mode": "list",
          "cachedResultName": "Claude 3 Haiku"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatAnthropic",
      "typeVersion": 1.3,
      "position": [
        500,
        560
      ],
      "id": "3e7fb37d-d85e-4e6e-9a5b-e97a55b3dd0b",
      "name": "Anthropic Chat Model",
      "credentials": {
        "anthropicApi": {
          "id": "vvRYzeVE6A8mYyNt",
          "name": "Anthropic - Claude"
        }
      }
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-16T19:39:31.814Z",
      "updatedAt": "2025-04-16T19:39:31.814Z",
      "role": "workflow:owner",
      "workflowId": "6k7968ycKuG0PjlP",
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
  "updatedAt": "2025-04-16T20:55:52.000Z",
  "versionId": "d843b883-8fc0-468f-966e-ee4f34020ab4"
}