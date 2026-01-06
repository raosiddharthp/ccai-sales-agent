# UPSELL_RULES.md

## Upsell & Cross-Sell Rules Engine for Smart Configurator Sales Agent

This document defines the complete rules engine for proactive revenue optimization during medical imaging device configuration. The logic is designed to be implemented in the Dialogflow CX fulfillment webhook (Cloud Functions). Rules are triggered contextually based on current session parameters (selected modality, tier, software, etc.) and follow enterprise sales best practices: value-based, non-aggressive, and data-driven recommendations.

### Core Principles
- Recommendations are **contextual** — only triggered when relevant to the current configuration.
- Phrasing uses **social proof** ("Most customers with this setup...") and **value justification**.
- Recommendations are **optional** — user can decline without blocking flow.
- Multiple rules can fire in sequence if applicable.
- Priority order: Safety/Compliance → Performance Optimization → Operational Efficiency → Additional Services.

### Rule Definitions (Prioritized)

#### Rule 1: MRI Quench Pipe (Mandatory – Enforced as Required Add-on)
- **Trigger**: Modality = MRI (any field strength)
- **Action**: Automatically add Quench Pipe (+$80,000)
- **Agent Message**: "For safety compliance, all MRI systems include a quench pipe for emergency venting (+$80,000)."
- **Type**: Required (not upsell, but transparent inclusion)

#### Rule 2: Radiation Shielding for CT/X-Ray (Mandatory)
- **Trigger**: Modality = CT Scanner or Digital X-Ray
- **Action**: Automatically add Radiation Shielding (+$150,000)
- **Agent Message**: "Radiation shielding is required for all CT and X-Ray installations (+$150,000)."
- **Type**: Required

#### Rule 3: Performance Tier Upgrade for High-End Imaging
- **Trigger**: User selects 3T MRI or 256-slice CT
- **Current Tier**: Standard or Advanced
- **Action**: Prompt upgrade to Premium Research tier (+$600,000 from base)
- **Agent Message**: "The [3T MRI / 256-slice CT] delivers optimal performance with our Premium Research tier. Shall I upgrade your configuration (+$600,000)?"
- **Rationale**: Technical requirement for full capability and safety margins

#### Rule 4: AI Diagnostics Suite Recommendation
- **Trigger**: 
  - Modality = MRI (3T) or CT (128+ slice), OR
  - Any oncology/cardiac/neurology-related software selected
- **Action**: Recommend AI Diagnostics Suite (+$250,000)
- **Agent Message**: "82% of facilities with advanced imaging systems adopt our AI Diagnostics Suite for automated anomaly detection and workflow efficiency. Would you like to include it (+$250,000)?"
- **Acceptance Weight**: High (clinical productivity gain)

#### Rule 5: Premium Care & Uptime Guarantee for Critical Systems
- **Trigger**: 
  - 3T MRI, 256-slice CT, or Premium Research tier selected, OR
  - Oncology Workflow or Cardiac Analysis module added
- **Action**: Recommend Premium Care 3-year + Uptime Guarantee SLA
- **Agent Message**: "For systems used in critical diagnosis or research, most institutions choose our Premium Care package with 99.9% uptime guarantee and 24×7 support (+$480,000/year combined). Shall I include this for operational continuity?"
- **Rationale**: Minimizes downtime risk in high-stakes environments

#### Rule 6: Remote Monitoring & Predictive Maintenance
- **Trigger**: Capital cost > $2,000,000 or Premium Research tier
- **Action**: Recommend Remote Monitoring service (+$120,000/year)
- **Agent Message**: "Our Remote Monitoring and Predictive Maintenance service reduces unplanned downtime by up to 40% on high-value systems. Would you like to add it (+$120,000/year)?"
- **Rationale**: ROI-driven for expensive assets

#### Rule 7: Clinical Training & Certification Package
- **Trigger**: Any AI-enhanced software package selected (AI Diagnostics, Oncology, Cardiac)
- **Action**: Recommend Training Package (+$75,000)
- **Agent Message**: "To maximize clinical value from the AI modules, we offer a comprehensive staff training and certification program. Most customers include this — interested (+$75,000)?"
- **Rationale**: Ensures adoption and accuracy

#### Rule 8: Research Collaboration Portal
- **Trigger**: Premium Research tier + any research-oriented software
- **Action**: Recommend Research Collaboration Portal (+$50,000/year)
- **Agent Message**: "The Research Collaboration Portal enables secure multi-site data sharing and standardized protocols — proven to accelerate publication timelines. Shall I include access (+$50,000/year)?"
- **Target**: Academic medical centers and clinical trial sites

#### Rule 9: Portable Deployment Accessories
- **Trigger**: Performance Tier = Portable (Ultrasound or X-Ray)
- **Action**: Recommend Extended Battery & Transport Case (+$25,000)
- **Agent Message**: "For field and rural deployments, customers typically add the Extended Battery and rugged Transport Case for reliability (+$25,000). Would you like to include this?"
- **Rationale**: Practical necessity for mobile use

#### Rule 10: Volume Discount Prompt
- **Trigger**: Quantity ≥ 2 units (any modality)
- **Action**: Inform of tiered volume pricing
- **Agent Message**: "For multiple units, we offer progressive volume discounts. Your current quantity of [X] qualifies for [Y]% savings. Would you like to configure additional systems?"

### Implementation Notes for Webhook
- Rules evaluated in priority order after each attribute change.
- Use session parameters to track:
  - `triggered_rules` (array to prevent repeats)
  - `recommendation_accepted` (boolean per rule)
  - `current_price_capital` and `current_price_annual`
- Vertex AI Gemini used only for natural phrasing variations (not decision logic).
- All monetary values stored as integers (cents) to avoid floating-point errors.

This rules engine transforms the agent from a passive configurator into an active, value-driven sales partner — increasing average order value while maintaining clinical credibility and trust.
