<style>
  body { font-family: 'Space Mono', monospace; }
</style>

# <span style="color: #0066FF;">Selling with Omni CCAI – Smart Configurator Sales Agent</span>

## <span style="color: #0066FF;">1. Description</span>
A GCP-native Dialogflow CX virtual agent designed to perform guided, attribute-based product configuration while actively driving revenue through intelligent upselling and cross-selling. The agent simulates a high-end gaming laptop configurator, enforcing real-world configuration rules (dependencies, compatibility, validation), calculating dynamic pricing, and proactively recommending complementary products and upgrades. All logic is self-contained within GCP services, demonstrating how Contact Center AI (CCAI) can evolve from cost-center support to revenue-generating sales conversations.

## <span style="color: #0066FF;">2. Executive Summary</span>
The Smart Configurator Sales Agent showcases the application of Dialogflow CX and Vertex AI generative capabilities to one of the most complex and valuable enterprise sales use cases: attribute-based configuration combined with guided selling. By replicating key CPQ behaviors (rule enforcement, dynamic pricing, bundle validation) in a conversational interface without requiring Salesforce or third-party CPQ systems, the prototype illustrates a lightweight, modern alternative for guided selling in omnichannel environments. The design emphasizes simplicity of deployment, transparency of logic, and extensibility toward production integration.

## <span style="color: #0066FF;">3. Business Strategy</span>

### <span style="color: #0066FF;">3.1 Strategic Value Proposition</span>
The agent reduces configuration errors, shortens sales cycles, and increases average order value through context-aware recommendations. It enables non-expert channels (web chat, voice, messaging) to handle complex configurable products traditionally requiring trained sales reps or heavy CPQ UIs. Primary value drivers include higher conversion rates, larger basket sizes via upsell/cross-sell, and improved customer experience through natural, guided conversations.

### <span style="color: #0066FF;">3.2 Regulatory Strategy</span>
No personal data is persisted beyond session parameters. All pricing and product rules are static and publicly derived. The prototype includes clear disclaimers that outputs are illustrative and not binding quotes. Future production paths will support configurable compliance controls (quote versioning, approval workflows) via GCP tooling.

## <span style="color: #0066FF;">4. Users</span>

### <span style="color: #0066FF;">4.1 Target User Personas</span>
- **End Customer (B2C/B2B Buyer)**: Seeks to configure and purchase a complex product online or via assisted channel without friction.
- **Sales Development Rep**: Uses the agent as a qualification and configuration assistant during live chat/voice interactions.
- **Channel Partner**: Embeds the agent in partner portals to maintain consistent guided selling.
- **Product Manager / Solutions Architect**: Evaluates modern conversational alternatives to traditional CPQ interfaces.

### <span style="color: #0066FF;">4.2 Lightweight Requirements and User Stories</span>
As a user, I want to:
- Configure a gaming laptop by answering natural-language questions.
- Receive immediate validation when selections are incompatible.
- See real-time price updates as options are chosen.
- Receive personalized upsell and cross-sell recommendations based on configuration.
- View a complete quote summary with line items and total price.
- Complete the flow without leaving the conversation channel.

### <span style="color: #0066FF;">4.3 User Journey Map</span>
1. User initiates chat (“I want to build a gaming laptop”).  
2. Agent greets, asks high-level needs (gaming type, budget range).  
3. Agent guides through attribute selection (CPU → GPU → RAM → Storage → Screen → Extras).  
4. Agent validates choices in real time and offers corrective suggestions.  
5. Agent interjects upsell/cross-sell recommendations contextually.  
6. Agent presents final configuration summary with dynamic pricing.  
7. User confirms or adjusts → agent generates quote and next steps.

## <span style="color: #0066FF;">5. Design and Architecture</span>

### <span style="color: #0066FF;">5.1 Phase A: Vision</span>
Create a conversational sales agent capable of replicating core CPQ functionality (attribute configuration, rule enforcement, dynamic pricing, guided selling) using only GCP CCAI services.

### <span style="color: #0066FF;">5.2 Phase B: Business</span>
Core capabilities: attribute-guided configuration, compatibility validation, dynamic pricing calculation, contextual upsell/cross-sell, quote generation. Success metrics: configuration completion rate, average order value uplift from recommendations, error-free rule enforcement.

### <span style="color: #0066FF;">5.3 Phase C: Information</span>
Session state maintained via Dialogflow CX parameters: selected attributes, current price, cart items, validation messages, recommendation history. Product catalog and rules stored as static JSON for transparency.

### <span style="color: #0066FF;">5.4 Phase D: Technology</span>
- Orchestration: Dialogflow CX (flows, intents, parameters, fulfillment)  
- Generative responses: Vertex AI Gemini (natural upsell phrasing)  
- Business logic: Cloud Functions webhook (Python) for rules, pricing, recommendations  
- Product data: Static JSON catalog (attributes, dependencies, base prices, upsell rules)  
- Frontend demo: Dialogflow Messenger embedded in simple HTML page  
- Persistence (future): Firestore for quote logging

## <span style="color: #0066FF;">6. Rollout and Roadmap - Implementation Phases and PI Mapping</span>

### <span style="color: #0066FF;">6.1 Current State</span>
MVP with single product (gaming laptop), five core attributes, ten validation rules, three upsell/cross-sell triggers, Dialogflow Messenger demo.

### <span style="color: #0066FF;">6.2 Future State</span>
- Multi-product catalog support  
- Integration with real payment gateways  
- Voice channel enablement (CCAI Platform)  
- Quote export to PDF/email  
- Analytics dashboard for recommendation effectiveness

### <span style="color: #0066FF;">6.3 Agile Delivery - ART</span>
Program Increment structure:  
- PI-1: Dialogflow CX agent setup and basic configuration flow  
- PI-2: Webhook fulfillment with attribute validation and pricing logic  
- PI-3: Upsell/cross-sell recommendation engine  
- PI-4: Generative response integration and quote summary  
- PI-5: Web demo deployment and polish

### <span style="color: #0066FF;">6.4 Change Management</span>
Version-controlled product catalog and rules JSON. Clear separation of configuration data from conversational logic to enable non-technical updates.

### <span style="color: #0066FF;">6.5 Target Value Stream</span>
Inquiry → Need qualification → Guided attribute configuration → Validation & correction → Recommendation → Quote summary → Closure/hand-off

## <span style="color: #0066FF;">7. Multi-Agent Model</span>
Not applicable — single agent with webhook fulfillment. Future extensions could decompose into specialized sub-agents (Configurator, Pricer, Recommender) using Dialogflow CX mega-agent patterns.

## <span style="color: #0066FF;">8. Intelligence Platform</span>

### <span style="color: #0066FF;">8.1 Unified Intelligence Stack Architecture</span>
Dialogflow CX as primary orchestrator. Cloud Functions webhook as decision engine. Vertex AI Gemini called from webhook for generative phrasing only. All components serverless and GCP-native.

### <span style="color: #0066FF;">8.2 The RAG Component (Future Extension)</span>
Optional retrieval from product knowledge base (FAQs, feature explanations) using Vertex AI Retrieval for more natural explanations.

### <span style="color: #0066FF;">8.3 Observability Layer</span>
Cloud Logging for intent matches, parameter changes, webhook invocations. Exportable session traces for analysis of recommendation acceptance rates.

## <span style="color: #0066FF;">9. The Model Lifecycle</span>
- **Selection**: Gemini 1.5 Flash for speed; optional Gemini Pro for richer generative upsell text.  
- **Prompt Management**: Version-controlled prompt templates for recommendation phrasing.  
- **Evaluation**: Offline testing against curated configuration scenarios; metrics include rule enforcement accuracy and recommendation relevance.  
- **Continuous Improvement**: Planned feedback collection on recommendation acceptance to refine rules engine.

## <span style="color: #0066FF;">10. Infrastructure</span>

### <span style="color: #0066FF;">10.1 Blueprint</span>
- Dialogflow CX agent (standard edition)  
- Cloud Functions (2nd gen) webhook  
- Static hosting for demo page (Cloud Storage bucket or GitHub Pages)  
- Optional Firestore for quote persistence

### <span style="color: #0066FF;">10.2 Security</span>
No authentication required for demo. Production path would use Identity-Aware Proxy and service account least privilege.

### <span style="color: #0066FF;">10.3 Governance and Compliance</span>
Clear in-conversation disclaimer: “This is a demonstration configuration. Final pricing subject to change.” Transparent rule logic in public repository.

### <span style="color: #0066FF;">10.4 SRE</span>
Serverless components ensure auto-scaling. Webhook timeouts and retry logic configured. Monitoring via Cloud Monitoring alerts on error rates.

## <span style="color: #0066FF;">11. Impact & Outcomes</span>
Expected outcomes include:  
- Demonstration of revenue-generating potential of CCAI beyond support  
- Illustration of lightweight alternative to traditional CPQ for guided selling  
- Higher interviewer recognition due to relevance to real enterprise sales complexity  
- Foundation for production-grade conversational commerce on GCP  
- Contribution to portfolio differentiation in CPQ-adjacent and sales automation roles

This design provides a focused, high-impact prototype that directly addresses enterprise-grade selling challenges while remaining feasible to build and deploy entirely on Google Cloud Platform.