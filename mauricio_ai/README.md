{
  "active": false,
  "connections": {
    "Structured Output Parser": {
      "ai_outputParser": [
        [
          {
            "node": "Auto-fixing Output Parser",
            "type": "ai_outputParser",
            "index": 0
          }
        ]
      ]
    },
    "Body examples": {
      "main": [
        [
          {
            "node": "Fake form data",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Fake form data": {
      "main": [
        [
          {
            "node": "RealEstateAdOrchestrator",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Auto-fixing Output Parser": {
      "ai_outputParser": [
        [
          {
            "node": "RealEstateAdOrchestrator",
            "type": "ai_outputParser",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [
        []
      ]
    },
    "OpenAI Chat Model1": {
      "ai_languageModel": [
        [
          {
            "node": "Auto-fixing Output Parser",
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
            "node": "RealEstateAdOrchestrator",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "When Executed by Another Workflow": {
      "main": [
        [
          {
            "node": "Code",
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
            "node": "RealEstateAdOrchestrator",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Code": {
      "main": [
        [
          {
            "node": "Body examples",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "createdAt": "2025-04-16T15:15:57.222Z",
  "id": "dg9zh5eZbsjNQsuX",
  "meta": {
    "templateCredsSetupCompleted": true
  },
  "name": "Mauricio AI",
  "nodes": [
    {
      "parameters": {
        "promptType": "define",
        "text": "={{ $('Code').item.json.fullData }}",
        "hasOutputParser": true,
        "options": {
          "systemMessage": "=Eres un agente orquestador experto en campañas inmobiliarias. Tu tarea es transformar información de propiedades en instrucciones naturales para herramientas especializadas que crearán campañas publicitarias.  Tu responsabilidad es interpretar correctamente los datos de entrada del usuario, seleccionar los ejemplos más relevantes de campañas exitosas, y construir un *user prompt* claro, efectivo y persuasivo para cada herramienta.  No generas tú el contenido final. Tu rol es preparar el mejor input posible para que cada herramienta lo genere.\n\nTrabajas con tres herramientas (subagentes):\n\n1. `body_copy_agent`  \n   - Crea un cuerpo de texto publicitario adaptado al perfil, la propiedad y la emoción deseada.\n   - Debe inspirarse en ejemplos previos exitosos.\n\n2. `lead_in_agent`  \n   - Crea 5 frases de inicio llamativas para cada texto publicitario.\n   - Debe sugerir un estilo para cada frase.\n\n3. `headline_agent`  \n   - Crea 10 titulares efectivos por perfil de comprador.\n   - Debe reflejar tono, emoción y beneficios.\n   - Cada titular debe ir acompañado de su estilo.\n\n\n1. Lee el input del usuario que contiene:  \n   - Detalles de la propiedad  \n   - Tres perfiles de comprador  \n   - Emoción deseada\n\n2. Por cada perfil:\n   a. Prepara un mensaje en lenguaje natural dirigido a `body_copy_agent`, que incluya:  \n      - Descripción del perfil  \n      - Características clave de la propiedad  \n      - Emoción deseada  \n      - Ejemplos reales de anuncios similares como guía (few-shot)\n\n   b. Recoge el `body_copy` generado.\n\n3. Para cada `body_copy`:\n   a. Redacta un nuevo mensaje natural para `lead_in_agent`, incluyendo:  \n      - El texto generado  \n      - El perfil  \n      - La emoción  \n      - 1–2 ejemplos de frases de inicio como guía  \n   b. Recoge las 5 frases de inicio (`lead_ins`) y su estilo.\n\n4. Para cada grupo de frases + body:\n   a. Prepara mensaje para `headline_agent`, incluyendo:  \n      - El texto completo  \n      - Las frases de inicio  \n      - El perfil y emoción  \n      - 2–3 ejemplos de titulares similares  \n   b. Recoge los 10 titulares (`headlines`) con su estilo.\n\n5. Finalmente, para cada perfil, crea una llamada a la acción (`cta`) coherente con el estilo de la campaña (inspirada en los ejemplos previos).\n\n6. Devuelve todo como un único objeto JSON en el siguiente formato:\n\n\n{\n  \"ad_campaigns\": [\n    {\n      \"buyer_profile\": \"Buyer Profile #1: Young couples looking to start a family\",\n      \"headlines\": [\n        {\n          \"headline\": \"Your First Family Home Minutes from the Beach!\",\n          \"style\": \"Excited / Emotional\"\n        },\n        ...\n      ],\n      \"lead_ins\": [\n        {\n          \"lead_in\": \"🏖️ Imagine summer mornings just minutes from the shore...\",\n          \"style\": \"Warm & Inviting\"\n        },\n        ...\n      ],\n      \"body_copy\": \"This beautiful 2-bedroom townhouse in Alcona is perfect for young couples starting their journey...\",\n      \"cta\": \"Click 'Learn More' to book your private tour before it’s gone!\"\n    },\n    ...\n  ]\n}\n\n\nNo generes el contenido de las herramientas por ti mismo.  \nTu tarea es coordinar la información, generar los prompts en lenguaje natural con ejemplos incluidos, obtener los outputs de cada tool, y ensamblarlos como un solo JSON final.\n\nPiensa como un creativo senior que lidera a su equipo para producir campañas impactantes y personalizadas.\n\n\n\n# Ejemplo de exito\n\n{{ $('Body examples').item.json.example }}"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.9,
      "position": [
        660,
        0
      ],
      "id": "6c8dec2c-d85d-43a0-83b2-81dd39ae7f0b",
      "name": "RealEstateAdOrchestrator",
      "retryOnFail": true,
      "waitBetweenTries": 5000
    },
    {
      "parameters": {
        "jsonSchemaExample": "{\n  \"ad_campaigns\": [\n    {\n      \"buyer_profile\": \"\",\n      \"headlines\": [\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        }\n      ],\n      \"lead_ins\": [\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        }\n      ],\n      \"body_copy\": \"\",\n      \"cta\": \"\"\n    },\n    {\n      \"buyer_profile\": \"\",\n      \"headlines\": [\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        }\n      ],\n      \"lead_ins\": [\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        }\n      ],\n      \"body_copy\": \"\",\n      \"cta\": \"\"\n    },\n    {\n      \"buyer_profile\": \"\",\n      \"headlines\": [\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"headline\": \"\",\n          \"style\": \"\"\n        }\n      ],\n      \"lead_ins\": [\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        },\n        {\n          \"lead_in\": \"\",\n          \"style\": \"\"\n        }\n      ],\n      \"body_copy\": \"\",\n      \"cta\": \"\",\n      \"body_copy\": \"\",\n      \"cta\": \"\",\n      \"body_copy\": \"\",\n      \"cta\": \"\"\n    }\n  ]\n}"
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserStructured",
      "typeVersion": 1.2,
      "position": [
        1240,
        220
      ],
      "id": "6ae17d72-69e7-4e95-b17f-6ccf4534bab4",
      "name": "Structured Output Parser"
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "11f6ebb5-c51b-4914-ba29-d699a70e7cee",
              "name": "example",
              "value": "=# Unit #73 2651 Acquitaine Ave, Mississauga\n\n## Original Form Answers\n\n**Property Type:** Townhouse\n\n**Price:** $699,900\n\n**Bedrooms:** 3\n\n**Bathrooms:** 2\n\n**Top Selling Features:** Quiet & safe Meadowvale, Open & spacious 2nd floor features walkout to the fenced in backyard\n\n**Biggest WOW Factor:** Just painted and brand new flooring in the entire main floor\n\n**What People Love When They Walk In:** Walk in area is separate from the rest of the house\n\n**Things People Don't Immediately Notice:** How large the property is. Plus, the walk ins and walk outs are unique\n\n**Perfect Buyer #1:** Young professionals, first time buyers\n\n**Perfect Buyer #2:** Executives living and working in Mississauga, Brampton or even Peel region\n\n**Perfect Buyer #3:** Working professionals\n\n**Local Amenities:** Parks, Schools, Public Transit, Highway Access\n\n**Better Than Similar Listings:** This has gas heating as in a gas furnace while the others have electric baseboard heating\n\n**Recent Upgrades:** Entire main floor has a brand new floor in both the kitchen and living / dining room\n\n**Desired Emotion:** Urgency\n\n**Full Description:** Completely renovated 3+1 bedroom, 2 bath townhome in peaceful Meadowvale. Approx. 1700 sq ft across 3 floors featuring modern finishes, freshly painted throughout with brand new flooring on the main floor. Highlights include oversized rec room, open concept second floor with walkout to fenced backyard with gazebo, balcony off breakfast area, and kitchen with center island. Efficient gas furnace heating, primary bedroom with wall-to-wall closets, and 3-year-old appliances. Conveniently located near GO Station, schools, shopping, recreation, and major highways (403, 401, 407 & QEW). Ideal for families, first-time buyers, or professionals seeking low-maintenance living.\n\n## Final Body Copies\n\n### Body Copy 1:\n\nJust renovated and ready for you! 🏡 This 3+1 bedroom townhome in peaceful Meadowvale won't wait for hesitant buyers.\n\nFresh paint throughout and brand NEW flooring on the main floor make this move-in ready.\n\nSprawling across 1700 sq ft with 3 floors of modern living space – much larger than you'd expect!\n\nImagine stepping onto your private balcony with morning coffee or entertaining in your fenced backyard with gazebo on warm evenings. 🌳\n\nLocated minutes from the GO Station and major highways (403, 401, 407) for easy commutes from Unit #73 in Mississauga.\n\nOther first-time buyers are already booking viewings on this listing. Click 'Learn More' to get instant access to floor plans and additional photos before someone else makes it their home!\n\n### Body Copy 2:\n\nRefined townhome offering in exclusive Meadowvale – completely renovated with sophisticated modern finishes throughout.\n\nThis 3+1 bedroom residence features approximately 1700 square feet of thoughtfully designed living space across three distinct levels.\n\nThe property distinguishes itself with efficient gas furnace heating rather than standard electric baseboard systems found in comparable properties.\n\nThe second floor presents an elegant open concept with direct walkout access to a private fenced yard with gazebo, ideal for both relaxation and entertaining colleagues.\n\nPositioned for the discerning professional at Unit #73, Mississauga, offering exceptional convenience to the GO Station and strategic highway connections (403, 401, 407 & QEW) for seamless regional mobility.\n\nThis listing represents a limited opportunity in a rapidly appreciating neighborhood. Request access to the complete property portfolio by clicking below.\n\n### Body Copy 3:\n\nJust completed renovations! 🔑 This spacious 3+1 bedroom townhome in Mississauga's safe Meadowvale community won't be available long.\n\nFreshly painted with brand new flooring throughout the main level – zero work needed before moving in.\n\nThe oversized rec room gives you flexible space for home office, gym, or entertainment area. 💻\n\nEnjoy the convenience of 2 full bathrooms, efficient gas heating (instead of costly electric), and appliances only 3 years old.\n\nUnit #73 puts you minutes from the GO Station and every major highway (403, 401, 407) – cutting your commute time significantly.\n\nWorking professionals are scheduling viewings this week for this listing. Tap 'Learn More' now for instant access to additional photos and to schedule your private viewing before it's gone!\n\n## Headline Options\n\n1. Mississauga Professionals FIGHT Over This Fresh-Painted Townhome\n2. Fresh Paint + New Floors = 24 Hour Countdown\n3. They Rushed Renovations Before The Market Exploded\n4. URGENT: Renovated SANCTUARY Minutes From Every Highway\n5. The Only Just-Renovated 3+1 In Meadowvale Under $700K\n\n# 4727 Sheppard Ave E #608, Toronto\n\n## Original Form Answers (Limited information in provided document)\n\n**Property Type:** Condo\n\n**Features:** 1370 Sqft with sunset view\n\n## Final Body Copies\n\n### Body Copy 1:\n\n[Condo Buyers] 1370 Sqft w/ A Sunset View!?\n\nImagine enjoying the sunset with a glass of wine from your private west-facing balcony in this rare 1370 sqft Riviera Club 1 condo.\n\nThe PERFECT condo for flexible living.\n\n✅ Massive Space: Huge 1370 sqft layout - 2 bed+Den w/ 2 bathrooms!\n✅ Skyrocketing Value: NEW subway station coming steps away will BOOST your property value\n✅ Perfect For Everyone: Functional floorplan works for downsizers OR growing families\n✅ No Morning Fights: Two upgraded bathrooms eliminate morning chaos\n✅ WFH Ready: Dedicated den makes the perfect home office with natural light\n✅ Money In Your Pocket: LOWER maintenance fees than comparable units nearby\n✅ Prime Location: 4727 Sheppard Ave E puts everything you need within reach\n\nFinding 1370 sqft with a NEW subway station coming AND lower than market fees is RARE in Toronto.\n\nClick \"Learn More\" to get instant access to floor plans and photos before someone else claims it!\n\n### Body Copy 2:\n\n[Downsizers] \"House-sized\" condo WITHOUT the yardwork?\n\nImagine all the SPACE you love about your house with NONE of the maintenance headaches! This rare 2 BED+ DEN/2 BATH condo (1370 sqft) at Riviera Club 1 is the answer you've been searching for.\nWHY DOWNSIZERS ARE RACING TO SEE THIS:\n✅ Keep Your Space: Massive 2 bed + den layout (1370 sqft) means NO MORE CRAMPED CONDO LIVING.\n✅ Fresh Updates: New vinyl floors, baseboards, and fresh paint ready for your personal touch\n✅ Versatility Champion: Sun-filled den transforms into your perfect home office, reading sanctuary, or hobby haven\n✅ Outdoor Freedom: Spacious west-facing balcony gives you sunset views WITHOUT the yard work\n✅ Lock & Leave Lifestyle: Maintenance-free living with SURPRISINGLY LOW fees for this size\n✅ Future-Proof Location: 4727 Sheppard Ave E with NEW subway station coming steps away\n✅ Complete Package: Excellent building amenities give you the community feel without the hassle\nLook, finding a 2 bed + den with 1370 sqft in Toronto with low fees AND upgrades already done is practically IMPOSSIBLE. This won't wait for indecision.\n→ TAP \"LEARN MORE\" NOW ←\nSee floor plans, photos & price before another downsizer snaps it up.\n\n## Headline Options\n\n1. Toronto's 1370 sqft 'Unicorn Property'\n2. Rare 1370 sqft 'Giant Condo'\n3. Sunset Views + 1370 sqft\n4. Sunset Balcony + Subway Access\n5. Large 2 Bed w/ Sunset Views\n\n# 24 Kylemount Court, Vaughan\n\n## Original Form Answers (Limited information in provided document)\n\n**Property Type:** Freehold (Rebuilt 4+1 bedroom home)\n\n## Final Body Copies\n\n### Body Copy 1:\n\nVaughan's #1 family home with resort-style backyard\nThis REBUILT 4+1 bedroom home at 24 Kylemount Court means your family finally gets the life they deserve.\nWHY THIS CHANGES EVERYTHING FOR YOUR FAMILY:\n✅ Top School Zone: Your kids walk to Carville Mill Public School - no more morning rush or worrying about their future\n✅ Family Connection: The gourmet kitchen with Thermador appliances becomes where your family bonds over meals and creates lasting memories\n✅ Stress-Free Summers: Your own saltwater pool means no more public pools or expensive vacations - just step outside for resort living\n✅ End Family Fighting: The smart open layout means everyone gets their space without feeling disconnected\n✅ Status & Security: Owning on Thornhill Woods' most prestigious court puts you in a neighborhood where values keep climbing\n✅ Instant Upgrade: Move in and immediately enjoy the life you've worked so hard to provide for your family\nHomes in Vaughan's best school zone that offer this complete lifestyle package simply don't last. They sell FAST.\n\n### Body Copy 2:\n\nThe \"crown jewel\" of Vaughan's real estate market...\n\nThis rebuilt luxury home at 24 Kylemount Court gives you the perfect backdrop for the life you've always wanted.\nWHY THIS HOME TRANSFORMS YOUR LIFESTYLE:\n✅ For Food Lovers: The showstopping Thermador kitchen means restaurant-quality meals at home and becoming the host everyone wants an invitation from\n✅ For Active Families: Minutes to premier golf courses, tennis courts, and pickleball facilities - spend less time driving and more time playing\n✅ For Entertainers: Host legendary pool parties in your private backyard oasis where mature trees create your own secluded resort\n✅ For Parents: Walk to top-rated Carville Mill Public School and Miriam Segal Park - giving your kids both educational excellence and outdoor fun\n✅ For Peace Seekers: Thoughtfully designed layout creates both gathering spaces and quiet retreats when you need to escape\n✅ For Smart Buyers: Own in Thornhill Woods' most distinguished court - where properties rarely become available and hold their value\nThis completely rebuilt masterpiece offers what busy families crave: location, luxury, and lifestyle all in one package.\n→ TAP \"LEARN MORE\" NOW ←\nGet the photos, price, floor plan and neighbourhood details before this rare opportunity disappears!\n\n## Headline Options\n\n1. \"Hidden Resort\" Style Home In Thornhill Woods\n2. Vaughan's Ultimate Backyard Escape\n3. Elite School Zone + Private Pool Retreat\n\n# 253 Lester Street, Unit 204, Waterloo (Investor Property)\n\n## Original Form Answers (Limited information in provided document)\n\n**Property Type:** Student rental condo\n\n**Price:** $595,000\n\n**Features:** Fully furnished, 5-bedroom, 2-bathroom\n\n## Final Body Copies\n\n### Body Copy 1:\n\n\"🎯 Looking for a Profitable, Hands-Off Investment? 📍 Welcome to 253 Lester Street, Unit 204, Waterloo, a fully furnished, 5-bedroom, 2-bathroom ideal student rental condo perfectly located within walking distance to Wilfrid Laurier University and the University of Waterloo. ✔ Gross rental income: ~*$4,308/month (1 vacant room projected at $850). ✔ Tenants pay utilities, keeping your costs low. ✔ This rental has been professionally managed. ✔ Prime location = low vacancy risk year-round. 💡 BONUS: FREE INVESTOR ANALYSIS SPREADSHEET Get a detailed financial breakdown for this property, including: Projected cash flow analysis showing potential income and expenses. ROI and cap rate calculations tailored for smart investors. Insights into Waterloo's high-demand rental market for consistent returns. 💰 Priced at just $595,000, this is the perfect turnkey property for seasoned investors or first-timers. 👉 Click Learn More to explore this opportunity and claim your FREE Investor Analysis Spreadsheet today!\"\n\n### Body Copy 2:\n\n\"🚨 Attention Real Estate Investors: Your next cash-flowing property is waiting for you! 📍 253 Lester Street, Unit 204 is a fully furnished student rental condo that generates steady income: ✅ Gross income potential: ~*$4,308/month (1 room vacant, projected $850). ✅ Walking distance to Wilfrid Laurier and the University of Waterloo = consistent tenant demand. ✅ Low maintenance costs 🎯 Here's the best part: We're offering a FREE Investor Analysis Spreadsheet with: Cash flow projections so you can see exactly how this property performs. Full breakdown of income, expenses, and ROI. Data to help you make an informed investment decision—fast! 💰 Priced at $595,000, this turnkey property is perfect for investors ready to grow their portfolio. 👉 Click Learn More to access the financial breakdown and learn more about this opportunity!\n\n## Headline Options\n\n1. Attention Investors: High-Demand Rental Property Near Waterloo's Top Universities!\n2. Invest in Waterloo's Hottest Student Rental Property!\n\n# 3070 Ozzie Drive, Churchill Meadows, Mississauga\n\n## Original Form Answers (Limited information in provided document)\n\n**Property Type:** Freehold (4+1 bed, 4 bath)\n\n**Features:** Park-facing property\n\n## Final Body Copies\n\n### Body Copy 1:\n\n🏡 WARNING: You're About to Fall in Love with This Home!\n\nOnce you see this 4+1 bed, 4 bath, park-facing stunner in Churchill Meadows, you won't want anything else.\n\n💡 Let's keep it real—homes like this don't last.\nHere's why:\n\n🔥 4+1 bedrooms, 4 bathrooms – Enough space so you're not living on top of each other.\n\n🔥 Directly facing a massive park – No staring at your neighbor's garage.\n\n🔥 Chef's kitchen – Quartz countertops, stainless steel appliances, space to actually cook.\n\n🔥 Finished basement – Home office? Gym? In-law suite? It's got options.\n\n🔥 Backyard with a deck & patio – Finally, a space for BBQ season.\n\n🔥 Move-in ready – No renos. No headaches. Just unpack and live.\n\n📍 Churchill Meadows = Prime real estate, top schools, and everything you need minutes away.\n\n🚀 Serious buyers only. DM us now or Click Learn More to book a private tour before it's gone.\n\n### Body Copy 2:\n\n🏡 STOP looking. This is the ONE.\n\n🚨 New Listing: 3070 Ozzie Drive, Mississauga 🚨\n\nEvery home promises \"spacious\" and \"modern.\" Most don't deliver.\n\nThis one actually does.\n✔ 4+1 bedrooms, 4 bathrooms – Room for the whole crew.\n✔ Unobstructed park views – No staring at concrete.\n✔ Chef's kitchen – Quartz counters, stainless steel appliances.\n✔ Bright, open-concept living – No dark, closed-off spaces.\n✔ Primary suite = actual retreat – Walk-in closet, spa-like ensuite.\n✔ Finished basement – Home gym? Office? Guest suite? Your call.\n✔ Private backyard – Deck, patio, and space to breathe.\n\n📍 Churchill Meadows = One of Mississauga's best neighborhoods.\n\n💡 Move-in ready homes like this don't sit on the market.\n\n⏳ Hesitate and someone else gets it. DM us now or Click Learn More to book your tour.\n\n## Headline Options\n\n1. 🏡 Warning: This Home Will Ruin Every Other House for You.\n2. 🚀 Homes Like This Get Snatched Up Fast – Act Now.\n\n# 1200 Inniswood St, Innisfil\n\n## Original Form Answers\n\n**Property Type:** Townhouse\n\n**Price:** $598,000\n\n**Bedrooms:** 2\n\n**Bathrooms:** 2\n\n**Top Selling Features:** Open-concept main floor, freehold (no maintenance fees), finished basement, minutes to the beach, in the desired Alcona neighbourhood\n\n**Biggest WOW Factor:** Priced like a condo but no maintenance fees, a larger living space, and a backyard!\n\n**What People Love When They Walk In:** Feels very welcoming\n\n**Things People Don't Immediately Notice:** 2 full bathrooms - 1 is a semi ensuite to the primary bedroom\n\n**Perfect Buyer #1:** Young couples looking to start a family\n\n**Perfect Buyer #2:** Young family who loves being close to the beach\n\n**Perfect Buyer #3:** Young Professionals who work remote\n\n**Local Amenities:** Parks, Schools, Restaurants, Shopping\n\n**Better Than Similar Listings:** Finished Basement & second bathroom\n\n**Recent Upgrades:** Back Sliding Doors (2024), Dishwasher (2024), Washer/Dryer (2022)\n\n**Desired Emotion:** Excited\n\n**Full Description:** Welcome to Alcona, to this beautiful 2-bedroom freehold townhome minutes to the beach! From the moment you step onto the quaint, private entrance, you'll feel right at home. Inside, the bright and inviting main level features an open-concept living and dining area, perfect for entertaining or cozy nights in. Step outside to your fully fenced backyard a private retreat ideal for summer BBQs, morning coffee, or a safe space for kids and pets to play. The separate kitchen offers plenty of storage and counter space, making meal prep a breeze. Uprstairs, you'll find spacious bedrooms filled with natural light. The primary suite boasts a walk-in closet and semi-ensuite access to the 4-piece bathroom. The secondary bedroom easily fits a queen-sized bed, making it perfect for a child's room, guest space, or home office.The finished basement offers endless possibilities whether you need a home office, gym, playroom, or media space plus a 3-piece bath for added convenience. Located within walking distance to great schools and just minutes from shopping, restaurants, and Innisfil's stunning beaches, this home is a fantastic alternative to a condo without the maintenance fees! A perfect place to start your family journey!\n\n## Final Body Copies\n\n### Body Copy 1:\n\nStop throwing money away on rent! 🏡 This beautiful 2-bedroom freehold townhome in Alcona is the perfect first step into homeownership.\n\nAt 1200 Inniswood St, you're getting incredible value that's priced like a condo but WITHOUT the maintenance fees!\n\nImagine morning coffee in your fully fenced private backyard while the kids play safely. ☕\n\nThe open-concept main floor is perfect for family gatherings, while the finished basement gives you flexible space for a playroom, office, or media room.\n\nTwo full bathrooms mean no more morning rush conflicts! One is even semi-ensuite to your primary bedroom.\n\nWalking distance to schools and minutes from Innisfil's gorgeous beaches means growing your family in the perfect location.\n\nThis rare opportunity won't be available long in today's market. Discover more photos and details of this exceptional property listing by clicking 'Learn More' now!\n\n### Body Copy 2:\n\nBeach life without the premium price tag! 🏖️ Just minutes from Innisfil's stunning beaches, this 2-bedroom freehold townhome at 1200 Inniswood St is where summer memories begin.\n\nYour kids will love the short walk to school and the fully fenced backyard – perfect for after-beach playtime and summer BBQs! 🍔\n\nThe bright, open-concept main floor creates the ideal family hub while the finished basement offers endless possibilities for rainy beach days.\n\nTwo full bathrooms means no waiting when everyone comes home sandy from the shore.\n\nLocated in desirable Alcona, you're surrounded by parks, restaurants, and shopping – everything a beach-loving family needs.\n\nThe best part? All this space and freedom WITHOUT condo maintenance fees holding you back from your next beach adventure.\n\nSnap up this limited listing before another family claims their perfect beach-life balance! See all the details and take the virtual tour by clicking below.\n\n### Body Copy 3:\n\nWork from anywhere? Make \"anywhere\" worth it! 💻 This 2-bedroom freehold townhome in Alcona offers the perfect work-life balance for remote professionals.\n\nTransform the finished basement into your dream home office – separate from your living space for perfect work boundaries.\n\nTake your lunch breaks in your private, fully fenced backyard – a luxury no downtown condo can offer! 🌱\n\nThe property at 1200 Inniswood St is priced like a condo but gives you ZERO maintenance fees and significantly more space.\n\nEnd your workday with a quick drive to Innisfil's beautiful beaches or walk to nearby restaurants for dinner.\n\nTwo full bathrooms means you can have a dedicated guest bath when colleagues or friends visit.\n\nThe open-concept main floor is perfect for entertaining after hours or weekend hosting.\n\nThis rare listing combines affordability with the space and layout remote workers dream about. Take the virtual tour and see why this property is generating so much interest among professionals seeking the perfect work-from-home setup.\n\n## Headline Options\n\n1. Beach Access + Zero Fee FREEDOM\n2. $598K Buys a Townhouse. This One ELIMINATES Fees Forever\n3. Young Couples Who Found This Innisfil 'Secret' Never Left\n4. PRIVATE BACKYARD SANCTUARY Unleashed in Beach Town\n5. The Only Fee-Free Townhouse with Fenced Yard Near Beach\n\n# 200 Flat Sedge Crescent, Ottawa\n\n## Original Form Answers\n\n**Property Type:** Freehold\n\n**Price:** $709,999\n\n**Bedrooms:** 3\n\n**Bathrooms:** 4\n\n**Top Selling Features:** Close to amenities (shopping, transit, schools, parks) / large den on 2nd floor / widened driveway for extra parking / large basement\n\n**Biggest WOW Factor:** Second floor den\n\n**What People Love When They Walk In:** Large windows and natural light / relatively open concept layout\n\n**Things People Don't Immediately Notice:** N/A\n\n**Perfect Buyer #1:** growing families (neighbourhood is very family oriented)\n\n**Perfect Buyer #2:** first time buyers\n\n**Perfect Buyer #3:** people who love walking in their neighbourhoods and going to parks with their kids\n\n**Local Amenities:** Parks, Schools, Shopping\n\n**Better Than Similar Listings:** Competitively priced, closer to amenities\n\n**Recent Upgrades:** N/A\n\n**Desired Emotion:** Urgency\n\n**Full Description:** Come see why Findlay Creek is the place to be! This stunning 3 bedroom (+ den) has been meticulously cared for since new and boasts a practical layout bathed in natural light. The open kitchen has loads of storage/counter space and is perfect for entertaining. Upstairs has 3 generously sized bedrooms along with a den, perfect for an office along with the convenience of having your laundry room upstairs! You'll find a fully finished lower level with plenty of space for the kids as well as storage. Just steps from every amenity you and your growing family will ever need. Come check this out before it's gone! 24hr irrevocable on all offers.\n\n## Final Body Copies\n\n### Body Copy 1:\n\nThe perfect family home just hit the market in sought-after Findlay Creek! 🏡\n\nYour growing family deserves this stunning 3 bedroom + den at 200 Flat Sedge Crescent.\n\nImagine working from the spacious second floor den while the kids play in the fully finished basement.\n\nThose large windows flood every room with natural light, making the open concept layout feel even more spacious.\n\nThe upstairs laundry room? Total game-changer for busy families.\n\nJust steps from parks, schools and shopping - everything your family needs to thrive!\n\nThis Findlay Creek listing is competitively priced and offers more space than similar properties in the area.\n\nBut with 24-hour irrevocable on all offers, you need to act FAST. ⏰\n\nClick 'Learn More' now to access complete property details and schedule your viewing before this opportunity disappears!\n\n### Body Copy 2:\n\nFirst home alert! 🔑 This is the opportunity you've been waiting for in Ottawa's Findlay Creek community!\n\nA beautiful 3 bedroom freehold with a BONUS second floor den at 200 Flat Sedge Crescent.\n\nStop paying rent when you could own this meticulously maintained home with practical, open-concept layout.\n\nCook in a kitchen with tons of storage and counter space - perfect for entertaining friends!\n\nEnjoy 4 bathrooms (yes, FOUR!) and a fully finished basement that adds incredible value.\n\nThe widened driveway gives you extra parking for guests. So convenient! 🚗\n\nWalking distance to parks, schools and shopping centers - everything a new homeowner needs.\n\nThis listing won't be available long - 24hr irrevocable on all offers means serious buyers only!\n\nTap 'Learn More' for instant access to floor plans, additional photos, and financing options tailored for first-time buyers!\n\n### Body Copy 3:\n\nYour ideal walkable lifestyle awaits in Findlay Creek! 🚶‍♀️🌳\n\nThis exceptional 3 bedroom + den property at 200 Flat Sedge Crescent puts Ottawa's best family-friendly parks just steps from your door.\n\nStart your morning with coffee in the light-filled kitchen before walking the kids to nearby schools.\n\nSpend weekends exploring neighborhood trails then return to your spacious, open-concept home.\n\nThe second floor den provides a perfect homework station while keeping an eye on little ones playing outside.\n\nYour fully finished basement offers additional play space for those rainy days.\n\nThis listing gives you the connected, walkable lifestyle you value - with shopping and amenities all within easy reach.\n\nWith 24hr irrevocable on offers, this opportunity for the perfect park-side home won't last! ⏱️\n\nGet the complete property package, including proximity maps to all nearby parks and walking paths, by clicking 'Learn More' below!\n\n## Headline Options\n\n1. 2nd Floor Den + Urgent Family Takeover in Findlay Creek\n2. $709,999 Buys a House. This One Gives a SECOND LIFE\n3. Ottawa Parents Refuse to Share This 'Walking Secret'\n4. UNLEASHED: The ONLY Family Sanctuary with 24-Hour DEADLINE\n5. The Only 3 Bed + Den with Park-Side Living Under $710K\n\n# 93 Allegranza Ave, Vaughan\n\n## Original Form Answers\n\n**Property Type:** Townhouse\n\n**Price:** $1,349,900\n\n**Bedrooms:** 3\n\n**Bathrooms:** 3\n\n**Top Selling Features:** Open-Concept Functional Floor Plan, Main-Floor Study/Playroom\n\n**Biggest WOW Factor:** Spacious Master Bedroom Which Includes An Ample-Sized Organized Walk-In Closet And Large 5-pc Bathroom (Double-Vanity, Separate Shower)\n\n**What People Love When They Walk In:** The open-concept main floor with hardwood floors, pot lights, and a stone-front fireplace. It creates a warm, inviting, and high-end first impression. The flow between the living, dining, and kitchen areas—with natural light pouring in from the Juliette balcony—makes the space feel bright and spacious right away.\n\n**Things People Don't Immediately Notice:** Finished basement with walk-out and rough-in for a bathroom Big potential here for future value. Not just a rec room—this is extra living space with flexibility.\n\n**Perfect Buyer #1:** Growing families\n\n**Perfect Buyer #2:** Move up buyers from the area\n\n**Perfect Buyer #3:** First time buyers on dual income and family support\n\n**Local Amenities:** Parks, Schools, Restaurants, Highway Access, Shopping\n\n**Better Than Similar Listings:** High-End Finishes & Move-In Ready, Second-floor laundry with laundry tub\n\n**Recent Upgrades:** 5\" hardwood floors, pot lights, stone-front gas fireplace, granite countertops, upstairs laundry, fully renovated throughout\n\n**Desired Emotion:** Excited\n\n**Full Description:** Stunning Modern Luxury Home In High Demand Area! Great Open-Concept Functional Floor Plan Features 5\" Hardwood, Smooth Ceilings, Pot Lights, Main-Floor Study/Playroom, Large Dining Room/Living Room With Juliette Balcony, Stone-Front Gas Fireplace, Gas Stove, Stainless-Steel Appliances & Granite Counters! On 2\" Floor You'll Find The Tiled Laundry Room With Washer/Dryer And A Laundry Tub, 2 Good-Sized Bedrooms And A Very Spacious Master Bedroom Which Includes An Ample-Sized Organized Walk-In Closet And Large 5-pc Bathroom (Double-Vanity, Separate Shower). The Finished Basement Features Ceramic Floor Tiles, Closet, Access To Garage & A Large Cozy Recreation Room Complete With Vinyl Flooring, Fireplace And Walk-Out To The Rear Patio. Basement Also Has A Rough-In or Future Bathroom. Other Features Of This Exceptional Home Include: Kitchen W/O To Deck, Central Vac System, CAC, Home Security System, Garage Door Opener Remote/Keypad, Recently Installed Stone Walkway & Rear Patio, Gas BBQ Hook-Up, Garden Shed, Fully Fenced. A Real Pleasure To See! This Vibrant Family-Friendly Area Has Everything Close By: Schools, Parks, Community Centre, Shopping, Restaurants, Fitness Centres, Hwy 400, Canadas Wonderland, Newly-Built Hospital, And More!\n\n## Final Body Copies\n\n### Body Copy 1:\n\nRoom to grow in Vaughan's most sought-after family neighborhood! 🏡\n\nThis stunning 3-bedroom townhouse at 93 Allegranza Ave offers the perfect blend of space and style for your growing family.\n\nImagine your kids playing in the main-floor study/playroom while you prepare dinner in the open-concept kitchen with granite counters and stainless appliances.\n\nThe master retreat will take your breath away! 😍 Spacious bedroom, organized walk-in closet, and luxurious 5-piece bathroom with double-vanity.\n\nSecond-floor laundry means no more carrying baskets up and down stairs!\n\nFinished basement with walk-out gives you even more living space to grow into.\n\nClose to excellent schools, parks, and the new hospital—everything your family needs.\n\nThis listing is generating significant interest from other families. Click 'Learn More' for instant access to floor plans, additional photos, and availability details!\n\n### Body Copy 2:\n\nThe upgrade you've been waiting for is right here in Vaughan! 🔑\n\nThis exceptional 3-bedroom, 3-bathroom townhouse at 93 Allegranza Ave represents the perfect next step.\n\nEnter into warm hardwood floors, pot lights, and an inviting stone-front gas fireplace that elevates your entertaining space.\n\nThe open-concept main floor creates a natural flow between living areas with light pouring in from the Juliette balcony.\n\nUpstairs, discover your sanctuary: a spacious master bedroom with an organized walk-in closet and luxurious 5-piece bathroom featuring double vanity and separate shower. 💦\n\nRecent upgrades include a newly installed stone walkway and rear patio, plus a fully fenced yard.\n\nStay in the neighborhood you love with access to all the amenities you already enjoy—plus easy highway access and proximity to Vaughan's best shopping.\n\nGet the complete property package by clicking below. Takes just seconds to unlock all details and be first to view!\n\n### Body Copy 3:\n\nYour first home doesn't have to be a compromise! ✨\n\nThis modern 3-bed, 3-bath townhouse at 93 Allegranza Ave in Vaughan offers first-time buyers extraordinary value with high-end finishes throughout.\n\nMove-in ready means no renovation headaches or unexpected costs. Just bring your furniture!\n\n5\" hardwood floors, smooth ceilings, and pot lights create a sophisticated atmosphere that will impress your friends and family. 🏠\n\nThe functional floor plan includes a main-floor study that's perfect for working from home or as a future nursery.\n\nYour investment grows with the finished basement featuring a recreation room, walk-out to the patio, and rough-in for a future bathroom.\n\nWith family-friendly amenities nearby including parks, schools, and shopping, this location offers everything you need.\n\nThis listing opportunity is perfect for dual-income first-time buyers. Tap now to see additional photos and floor plans before other buyers discover this gem!\n\n## Headline Options\n\n1. Walk-in Closet + 5pc Bathroom COMBO That Has Vaughan Parents FIGHTING\n2. Master Suite That Delivers 2x The Value of Neighboring Homes\n3. They Hid This Master Bedroom From The Listing Photos\n4. PRIVATE SANCTUARY Unleashed In Vaughan's Most COVETED Neighborhood\n5. The Only Townhouse With Resort-Style Master Suite in Vaughan\n\n# 55 Mercer St #4102, Toronto\n\n## Original Form Answers\n\n**Property Type:** Condo\n\n**Price:** $1,250,000\n\n**Bedrooms:** 3\n\n**Bathrooms:** 2\n\n**Top Selling Features:** amazing building amenities, unbeatable skyline & lake views, corner unit with all day natural light\n\n**Biggest WOW Factor:** the skyline & lake view is unparalleled\n\n**What People Love When They Walk In\n\nRetry\n\nClaude hit the max length for a message and has paused its response. You can write Continue to keep the chat going.\n\nA\n\ncontinue\n\nEdit\n\n# 55 Mercer St #4102, Toronto (continued)\n\n## Original Form Answers (continued)\n\n**What People Love When They Walk In:** natural light and the view\n\n**Things People Don't Immediately Notice:** 3 full bedrooms\n\n**Perfect Buyer #1:** young professionals upsizing\n\n**Perfect Buyer #2:** investor\n\n**Local Amenities:** Restaurants, Shopping, Public Transit\n\n**Better Than Similar Listings:** high floor with unobstructed views of the lake and skyline, corner unit. other comparable units are in less desirable buildings or have inferior views\n\n**Desired Emotion:** Luxury\n\n**Full Description:** Perched on the 41st floor, Unit 4102 offers breathtaking southwest views of the Toronto skyline, CN Tower, and Lake Ontario. Floor-to-ceiling windows fill the space with natural light, while the open layout maximizes both flow and function. A dedicated parking spot and locker add to the convenience. 55 Mercer offers some of the finest amenities in the city, designed for seamless work, wellness, and relaxation—all within the building. Located in the heart of downtown, just steps from Toronto's best dining, shopping, and entertainment, this residence is ideal for professionals and investors seeking a premier urban lifestyle.\n\n## Final Body Copies\n\n### Body Copy 1:\n\nThis isn't just a condo — it's a skyline sanctuary.\nLocated on the 41st floor at 55 Mercer, this rare corner unit delivers the best views in the city… and that's just the start 🛋️\nImagine:\n✅ CN Tower glowing from your bedroom\n✅ Lake Ontario stretching across your living room windows\n✅ Spa-like finishes and a layout that feels like a retreat\nWith 3 spacious bedrooms, natural light pouring in, and complete privacy above the city, this home was built for those who know the value of space, light, and silence.\n🔐 This is where design meets status.\n📍 This is where Toronto's skyline meets your living room.\nTap \"Learn More\" for your private access to full listing details & photos.\n\n### Body Copy 2:\n\nReady to live above the noise? 🏙️\n\nWelcome to the 41st floor of 55 Mercer — where Lake Ontario, the CN Tower, and the entire Toronto skyline become your personal backdrop 🌇\nThis 3-bed corner unit is what most buyers dream of—but few ever find.\n✅ Floor-to-ceiling windows\n✅ Tons of natural light\n✅ Private balcony with dual exposure views\n✅ Modern layout designed for work, play, and hosting\nMorning coffee hits different here. ☕\nSo do sunsets. 🌅\nSteps to the city's best food, nightlife, and culture.\nLuxury amenities include a gym, concierge, sauna, party room, and more.\n📩 Click \"Learn More\" now for exclusive access to photos, floor plans & current pricing.\n\n## Headline Options\n\n1. Young, Thriving, and Outgrowing Your Condo? Let's Fix That\n2. Finally… a Downtown Condo That Fits Your Lifestyle (and Your Friends)\n\n# 35 Rowallan Dr, Scarborough\n\n## Original Form Answers\n\n**Property Type:** Freehold\n\n**Price:** $1,125,000\n\n**Bedrooms:** 4\n\n**Bathrooms:** 3\n\n**Top Selling Features:** Large Backyard, Close to Lake, Great Location, Multiple Schools\n\n**Biggest WOW Factor:** Backyard\n\n**What People Love When They Walk In:** Open concept living/dining\n\n**Things People Don't Immediately Notice:** Upgraded flooring throughout\n\n**Perfect Buyer #1:** Young families, upsizers, growing families\n\n**Perfect Buyer #2:** First time homebuyers\n\n**Local Amenities:** Parks, Schools, Shopping, Public Transit, Highway Access, Waterfront\n\n**Better Than Similar Listings:** Attractive pricing\n\n**Recent Upgrades:** Flooring, paint\n\n**Desired Emotion:** Excited\n\n**Full Description:** Welcome to West Hill Living at its Finest! This beautifully upgraded 4-bedroom, 2-story detached home offers a perfect blend of modern style and family-friendly functionality. Step onto new flooring on the main floor and basement, complemented by a fresh coat of paint throughout that brightens every corner. Upstairs, you'll find spacious bedrooms designed to accommodate a growing family, while the finished basement provides extra living space for entertainment, a home office, or even a guest suite with a full bathroom and standing shower. Outside, a massive backyard invites endless possibilities, from family gatherings under the sun to the potential for a garden suite, offering an ideal opportunity for additional rental income or multigenerational living. Located just 5 minutes from the Scarborough Lakeshore and Guild Park, you'll be minutes away from scenic waterfront trails, picnic spots, and cultural landmarks. With convenient access to schools, shopping, and major transit routes, this home truly has it all. Don't miss your chance to own a gem in Scarborough's West Hill!\n\n## Final Body Copies\n\n### Body Copy 1:\n\nLooking for a home with space to grow and a yard to roam? 🏡\n\nWelcome to 35 Rowallan Dr, where family-friendly living meets upgraded comfort in Scarborough's West Hill.\nHere's what makes this home shine: ✅ Massive backyard — perfect for play, BBQs, or even adding a garden suite\n✅ Fresh flooring & paint throughout = move-in ready\n✅ Finished basement with full bath — ideal for guests, a home office, or rec room\n✅ Open-concept main floor that flows for modern living\n✅ 4 spacious bedrooms = no fighting over rooms!\n💡 Bonus: You're just 5 minutes from the lake, with easy access to Guild Park, schools, shopping, transit, and major highways.\n🎯 Perfect for: Young families, first-time homebuyers, or anyone craving more space without leaving the city.📸 Click Learn More for the full photo tour + exclusive listing info — including price, closing date, and more.\n\n### Body Copy 2:\n\nImagine summer BBQs in a backyard that actually fits the whole family.\n\nMornings with coffee in your open-concept living space.\nAnd a finished basement that works as your office, gym, or guest suite — without compromising upstairs space.\nWelcome to 35 Rowallan Dr — a rare 4-bed detached in Scarborough's West Hill, where upgrades meet comfort and location.\n✨ Highlights include:\n✅ New flooring + fresh paint throughout\n✅ Huge backyard with potential for garden suite or outdoor haven\n✅ Finished basement with full bathroom = flexible extra space\n✅ Minutes to Lake Ontario, parks, and waterfront trails\n✅ Close to great schools, shopping & transit\nThis home isn't just move-in ready — it's lifestyle ready.\n\n💥 Ideal for growing families who want space and connection to nature, city, and community.\n📍 Click Learn More for private access to the full listing, photo tour & details before it hits more feeds.\n\n## Headline Options\n\n1. 🏡 Big Backyard, 4 Bedrooms & Minutes from the Lake? West Hill Has It All\n2. 👨‍👩‍👧‍👦 Growing Family? This Detached 4-Bed in Scarborough Has Room for Everyone\n3. 🌿 Backyard Goals + Lake Trails Nearby = Your Next Move in West Hill\n4. 📍 Upgraded 4-Bed Just 5 Minutes from the Scarborough Lakeshore\n\n# 14 Holyrood Avenue, Oakville\n\n## Original Form Answers\n\n**Property Type:** Freehold\n\n**Price:** $5,149,000\n\n**Bedrooms:** 4+1\n\n**Bathrooms:** 5\n\n**Top Selling Features:** Backing onto Lake Ontario, Great School District, Affluent Neighbourhood\n\n**Biggest WOW Factor:** Backing onto Lake Ontario\n\n**What People Love When They Walk In:** Vaulted Ceiling in the entry way\n\n**Things People Don't Immediately Notice:** Main floor primary bedroom and Elevator\n\n**Perfect Buyer #1:** Growing Families with school aged kids\n\n**Perfect Buyer #2:** Mature affluent couple, dog owners\n\n**Perfect Buyer #3:** Boat owners\n\n**Local Amenities:** Waterfront, Schools, Restaurants\n\n**Better Than Similar Listings:** Backing onto Lake Ontario (very few homes back onto Lake Ontario)\n\n**Recent Upgrades:** No recent upgrades, custom built in 1999 and very well maintained\n\n**Desired Emotion:** Excited\n\n**Full Description:** Rare opportunity to not only get into one of the most prestigious neighbourhoods in the GTA but this beautiful home overlooks the calm shores of Lake Ontario. First time offered for sale, the classic elegance of this custom-built home is sure to impress. Situated on a very quiet street with no thru-traffic it is steps to great schools & parks & just minutes to the ever-popular downtown Oakville shopping & restaurant strip and marina. Upon entry into this sophisticated home, you will be greeted with 17 ceilings that carry into the formal living room and dining room with a walk thru to the Custom kitchen featuring built in appliances, a pantry, center island with a breakfast bar and open to the family room - Both overlook the backyard and Lake Ontario. The open concept family room features oversized French doors leading to a 22' X 15' composite deck. Main floor primary bedroom with a 5-piece ensuite and walk in closet and access to the deck. Convenient elevator gives everyone easy access to all 3 levels of this superbly finished home with great detail and functionality in mind. Three bedrooms on the upper level. Two share a 5-piece Jack and Jill bathroom and one has its own private ensuite, all three have walk-in closets and all have views of Lake Ontario. Professionally finished lower level complete with office with built-in desk and cabinetry, fifth bedroom with above grade windows and semi ensuite, perfect for guests or nanny suite. Lower-level family room with a second gas fireplace and French doors leading to the professionally landscaped gardens. A Sophisticated and Elegant Gem On a tranquil Park-Like lot, a rare combination.\n\n## Final Body Copies\n\n### Body Copy 1:\n\nImagine your children growing up steps away from the shores of Lake Ontario in prestigious Oakville.\n\nThis rare 4+1 bedroom waterfront property at 14 Holyrood Avenue offers everything your growing family deserves.\n\nStunning 17-foot vaulted ceilings welcome you home, while the custom kitchen opens to a family room with breathtaking lake views. 🌊\n\nLocated in one of Oakville's top school districts, your kids can walk to excellent schools while you enjoy the tranquility of a quiet, no-thru-traffic street.\n\nThe main floor primary bedroom gives parents privacy, while three upstairs bedrooms (all with lake views!) provide perfect spaces for children.\n\nThis sophisticated waterfront listing won't remain available long in this coveted neighborhood.\n\nTake the virtual tour to experience this rare waterfront family opportunity before someone else claims it.\n\n### Body Copy 2:\n\nA sophisticated waterfront sanctuary awaits discerning couples in prestigious Oakville.\n\nThis exceptional 14 Holyrood Avenue residence backs directly onto Lake Ontario—a rare offering in one of the GTA's most coveted neighborhoods.\n\nThe main floor primary suite with 5-piece ensuite offers luxury and convenience, opening directly to a spacious 22' × 15' composite deck overlooking tranquil waters.\n\nEnjoy morning walks with your canine companion along the lakeshore, then return to your elegant retreat.\n\nThe home's convenient elevator provides effortless access to all three meticulously finished levels.\n\nSteps from downtown Oakville's refined shopping and dining, this listing represents a lifestyle reserved for the privileged few.\n\nSee the complete property portfolio to appreciate the craftsmanship and exclusivity of this waterfront listing.\n\n### Body Copy 3:\n\nYour dream waterfront lifestyle is now available at 14 Holyrood Avenue in Oakville. ⛵\n\nThis exceptional Lake Ontario backing property offers what passionate boaters covet most—direct proximity to the water and just minutes from downtown Oakville's marina.\n\nImpress fellow sailing enthusiasts with your sophisticated 4+1 bedroom waterfront residence featuring stunning 17-foot vaulted ceilings and panoramic lake views.\n\nThe professionally landscaped gardens lead toward the calm shores of Lake Ontario, creating the perfect backdrop for your nautical lifestyle. 🌊\n\nYour home becomes both showcase and sanctuary with its custom kitchen, family room overlooking the water, and elegant entertaining spaces.\n\nThis rare waterfront listing combines sophisticated living with the boating lifestyle you love.\n\nSeveral serious inquiries already received on this unique waterfront property. View complete details now while this opportunity remains.\n\n## Headline Options\n\n1. Oakville's 'Lake Access' They're Trying To Restrict\n2. 4 Beds + Lake Ontario Backyard = Private School Results\n3. The Family Who Lives Here Has A Strange Morning Ritual\n4. LAKEFRONT LEGACY Unleashed in Prestigious Oakville\n5. The Only Elevator Waterfront With Private Lake Trails",
              "type": "string"
            }
          ]
        },
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        780,
        -220
      ],
      "id": "b99de751-4224-4927-afbf-e7bf615f8c0a",
      "name": "Body examples"
    },
    {
      "parameters": {
        "mode": "raw",
        "jsonOutput": "{\n  \"fullData\": \n  {\n    \"First name\": \"Arslan\",\n    \"Last name\": \"Ahmed\",\n    \"Email\": \"arslan@salesgenius.co\",\n    \"Address\": \"10 Morrison St, 111\",\n    \"City/Town\": \"Toronto\",\n    \"State/Region/Province\": \"ON\",\n    \"Zip/Post Code\": \"m5v2t8\",\n    \"Country\": \"Canada\",\n    \"*What Is The Objective Of Your Ad?*\": \"I Want To Generate Leads\",\n    \"Which location would you like to target with the ad? \": \"Toronto, Mississauga\",\n    \"Would you like to run this ad until it's sold or until a specific date? \": \"Specific Date\",\n    \"End Date For Ad \": null,\n    \"What type of property is this? (Condo, Freehold, Townhouse, Multi-Unit, Other – Please specify.)\": \"Condo\",\n    \"What is the listing price? (e.g., $599,000.)\": \"850000\",\n    \"Do you want the listing price shown in the ad or only in the email follow-up? (Show In Ad, Only Show In Email Sequence)\": \"Show In Ad\",\n    \"How many bedrooms? \": \"1\",\n    \"How many bathrooms? \": \"1\",\n    \"What are the top 3-5 selling features of this home? (Examples: Open-concept kitchen, large backyard, lake view, school zone, etc.)\": \"its beautiful\",\n    \"What's the biggest WOW factor about this home?\": null,\n    \"What's one thing people LOVE when they walk in?\": null,\n    \"What are some things people don't immediately notice but should?\": null,\n    \"Who do you think the perfect buyer is? (Buyer Profile #1) (Examples: Young professionals, first-time buyers, retirees, investors, growing families, etc.)\": \"First Time Home Buyer\",\n    \"Buyer Profile #2 (Golfers, Skiers, Dog Owners, Etc.)\": \"Wild and Crazy\",\n    \"Buyer Profile #3 (If another type of buyer applies.)\": \"\",\n    \"What local amenities would attract buyers? (Choose up to 3: Parks, Schools, Restaurants, Shopping, Public Transit, Highway Access, Waterfront, Other – Please Specify.)\": [\n      \"Parks\",\n      \"Restaurants\",\n      \"Shopping\"\n    ],\n    \"What makes this home better than similar listings in the area?\": \"its like a townhouse\",\n    \"Are there any recent upgrades/renovations? (Example: \\\"New roof (2023), updated kitchen, renovated ensuite.\\\")\": \"New Laundry 2025, new Floors 2024\",\n    \"What emotions do you want potential buyers to feel when they see this ad? (Excited, Curious, Urgency, Trust, Luxury, Other – Please Specify.)\": \"Excited\",\n    \"Is this an investment property?\": true,\n    \"What is your total daily budget for ads? \": \"20/day\",\n    \"Upload THE BEST raw listing photo.\": \"https://salesgenius.s3.ca-central-1.amazonaws.com/listings/ebddd870-727d-4996-b2df-4272a195b0f6/5c2a80b6-702b-4a5c-9618-dd71ecde3baa-image_fx__53.jpg\",\n    \"Upload THE SECOND BEST raw listing photos.\": \"https://salesgenius.s3.ca-central-1.amazonaws.com/listings/ebddd870-727d-4996-b2df-4272a195b0f6/793edac0-149f-46e4-a807-5df77fa878f3-ChatGPT_Image_Apr_8_2025_02_12_39_PM.png\",\n    \"Upload THE THIRD BEST raw listing photo.\": \"https://salesgenius.s3.ca-central-1.amazonaws.com/listings/ebddd870-727d-4996-b2df-4272a195b0f6/12ad15e1-acb7-40db-ad9b-06259c95351e-image_fx__52.jpg\",\n    \"Upload THE FOURTH BEST raw listing photo.\": \"https://salesgenius.s3.ca-central-1.amazonaws.com/listings/ebddd870-727d-4996-b2df-4272a195b0f6/baa8062b-608a-4071-b33d-c76529747b84-image_fx__56.jpg\",\n    \"Copy & Paste the current listing description here. (We'll refine and optimize it for ad effectiveness!)\": null,\n    \"Any additional details we should know? (Unique selling points, seller situation, or requests.)\": \"Investment property with potential rental income of 3000/month. New YMCA across the street\",\n    \"Enter Branded Photo Tour / 3D Tour URL \": \"https://meet.google.com/landing?authuser=0\",\n    \"What local amenities would attract buyers? (Choose up to 3: Parks, Schools, Restaurants, Shopping, Public Transit, Highway Access, Waterfront, Other – Please Specify\": {\n      \")\": [\n        \"Parks\",\n        \"Restaurants\",\n        \"Shopping\"\n      ]\n    },\n    \"Phone number\": null,\n    \"Company\": null\n  }\n}\n",
        "options": {}
      },
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        940,
        -220
      ],
      "id": "7bd32c68-3b4a-4d49-8966-cb992b0c13b1",
      "name": "Fake form data"
    },
    {
      "parameters": {
        "options": {
          "prompt": "Instructions:\n--------------\n{instructions}\n--------------\nCompletion:\n--------------\n{completion}\n--------------\n\nAbove, the Completion did not satisfy the constraints given in the Instructions.\nError:\n--------------\n{error}\n--------------\n\nPlease try again. Please only respond with an answer that satisfies the constraints laid out in the Instructions:"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserAutofixing",
      "typeVersion": 1,
      "position": [
        1060,
        100
      ],
      "id": "80b67c3d-9d39-47db-958e-600987751b37",
      "name": "Auto-fixing Output Parser"
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "value": "gpt-4.1-mini",
          "mode": "list",
          "cachedResultName": "gpt-4.1-mini"
        },
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.2,
      "position": [
        -160,
        260
      ],
      "id": "10228c6d-55d1-4add-9b51-cb16161cefdf",
      "name": "OpenAI Chat Model",
      "credentials": {
        "openAiApi": {
          "id": "OLHtLOP5C47dG8d5",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "model": {
          "__rl": true,
          "value": "gpt-4.1",
          "mode": "list",
          "cachedResultName": "gpt-4.1"
        },
        "options": {
          "temperature": 0.3
        }
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1.2,
      "position": [
        1080,
        240
      ],
      "id": "291c2037-43de-4935-ac5c-74f71973249e",
      "name": "OpenAI Chat Model1",
      "credentials": {
        "openAiApi": {
          "id": "OLHtLOP5C47dG8d5",
          "name": "OpenAi account"
        }
      }
    },
    {
      "parameters": {
        "sseEndpoint": "https://n8n.salesgenius.co/mcp/CretiveText/sse",
        "authentication": "bearerAuth"
      },
      "type": "@n8n/n8n-nodes-langchain.mcpClientTool",
      "typeVersion": 1,
      "position": [
        780,
        220
      ],
      "id": "586b527e-d623-46b5-a1f7-5362fb8b33a2",
      "name": "MCP Client",
      "credentials": {
        "httpBearerAuth": {
          "id": "W8jPE6HrmWmbxBe2",
          "name": "MCPTEST"
        }
      }
    },
    {
      "parameters": {
        "inputSource": "passthrough"
      },
      "type": "n8n-nodes-base.executeWorkflowTrigger",
      "typeVersion": 1.1,
      "position": [
        0,
        0
      ],
      "id": "d83a07e9-5867-45c8-8285-5cacd8ef8db0",
      "name": "When Executed by Another Workflow"
    },
    {
      "parameters": {
        "modelName": "models/gemini-2.5-flash-preview-04-17",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        620,
        180
      ],
      "id": "273369e1-1959-45cc-861a-1bddde71ee64",
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
        "jsCode": "// Obtener el JSON de entrada\nlet inputData = items[0].json;\n\n// Crear un nuevo objeto con el JSON dentro de \"fullData\"\nlet outputData = {\n  fullData: inputData\n};\n\n// Devolver el resultado\nreturn [\n  {\n    json: outputData\n  }\n];\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        220,
        0
      ],
      "id": "aa15d3f1-82b9-4e30-bff0-49fe7777d679",
      "name": "Code"
    }
  ],
  "settings": {
    "executionOrder": "v1"
  },
  "shared": [
    {
      "createdAt": "2025-04-16T15:15:57.232Z",
      "updatedAt": "2025-04-16T15:15:57.232Z",
      "role": "workflow:owner",
      "workflowId": "dg9zh5eZbsjNQsuX",
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
  "updatedAt": "2025-04-25T14:39:25.000Z",
  "versionId": "b2805df7-ce60-4813-9369-e198e53385a7"
}