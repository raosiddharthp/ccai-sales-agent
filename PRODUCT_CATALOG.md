# PRODUCT_CATALOG.md

## Product: Configurable Medical Imaging Device Suite

This catalog defines the configurable medical imaging device suite for the Smart Configurator Sales Agent demo. The product is a high-end diagnostic imaging system (MRI, CT, Ultrasound, or X-Ray) sold to hospitals, clinics, and research institutions. All attributes, dependencies, validation rules, base pricing, and upsell/cross-sell logic are designed to mirror real-world MedTech/Healthcare CPQ complexity managed in ERP systems (e.g., SAP, Oracle).

### Core Modality Selection (Required – First Attribute)
| Modality      | Base Price | Description                              |
|---------------|------------|------------------------------------------|
| MRI           | $1,800,000 | Magnetic Resonance Imaging               |
| CT Scanner    | $1,200,000 | Computed Tomography                      |
| Ultrasound    | $250,000   | Diagnostic Ultrasound System             |
| Digital X-Ray | $150,000   | Digital Radiography System               |

### Attribute Configuration Options

#### 1. Performance Tier
| Tier              | Price Adder | Compatible Modalities       | Notes                                      |
|-------------------|-------------|-----------------------------|--------------------------------------------|
| Standard          | +$0         | All                         | Entry-level performance                    |
| Advanced          | +$300,000   | MRI, CT                     | Higher resolution, faster scan times       |
| Premium Research  | +$600,000   | MRI, CT                     | Cutting-edge for clinical trials           |
| Portable          | +$80,000    | Ultrasound, X-Ray only      | Mobile/cart-based deployment               |

#### 2. Field Strength / Resolution (MRI & CT only)
| Option              | Price Adder | Compatible Modality | Dependency Rule                          |
|---------------------|-------------|---------------------|------------------------------------------|
| 1.5T (MRI)          | +$0         | MRI                 | Default for MRI                          |
| 3T (MRI)            | +$800,000   | MRI                 | Requires Premium Research tier           |
| 64-slice (CT)       | +$0         | CT                  | Default                                  |
| 128-slice (CT)      | +$400,000   | CT                  | Requires Advanced or Premium tier        |
| 256-slice (CT)      | +$800,000   | CT                  | Requires Premium Research tier           |

#### 3. Software Packages
| Package                     | Price Adder | Description                                      |
|-----------------------------|-------------|--------------------------------------------------|
| Basic Imaging               | Included    | Core acquisition and viewing                     |
| AI Diagnostics Suite        | +$250,000   | Automated detection (tumor, fracture, etc.)      |
| 3D Reconstruction           | +$150,000   | Advanced volumetric rendering                    |
| Cardiac Analysis Module     | +$200,000   | Specialized cardiac gating and analysis          |
| Oncology Workflow           | +$300,000   | Tumor tracking and radiation therapy planning    |

#### 4. Installation & Environment
| Option                  | Price Adder | Dependency Rule                                  |
|-------------------------|-------------|--------------------------------------------------|
| Standard Fixed Room     | Included    | All modalities                                   |
| MRI Quench Pipe         | +$80,000    | Required for all MRI systems                     |
| Radiation Shielding     | +$150,000   | Required for CT and X-Ray                        |
| Mobile Trailer          | +$400,000   | Only available with Portable tier (Ultrasound/X-Ray) |

#### 5. Service & Support Level
| Level                   | Annual Cost | Description                                      |
|-------------------------|-------------|--------------------------------------------------|
| Standard Warranty (1 yr)| Included    | Parts & labor, 9×5 support                       |
| Premium Care (3 yr)     | +$180,000/yr| 24×7 support, preventive maintenance             |
| Uptime Guarantee (99.9%)| +$300,000/yr| Guaranteed uptime SLA with credits               |

### Validation & Compatibility Rules (Enforced in Webhook)
1. 3T MRI → must have Premium Research tier.
2. 128/256-slice CT → must have Advanced or Premium tier.
3. MRI → always requires Quench Pipe add-on.
4. CT or X-Ray → always requires Radiation Shielding.
5. Portable tier → only available for Ultrasound or X-Ray.
6. AI Diagnostics Suite → recommended when Oncology or Cardiac module selected.

### Upsell & Cross-Sell Logic (Triggered Contextually)
| Trigger Condition                                 | Recommendation                                   | Price Adder       | Rationale                                      |
|---------------------------------------------------|--------------------------------------------------|-------------------|------------------------------------------------|
| MRI or CT selected                                | AI Diagnostics Suite                             | +$250,000         | 82% of advanced imaging centers adopt AI       |
| Oncology Workflow module selected                 | Premium Care + Uptime Guarantee                  | +$480,000/yr      | Critical for cancer treatment continuity       |
| 3T MRI or 256-slice CT                            | Remote Monitoring & Predictive Maintenance       | +$120,000/yr      | Reduces downtime on high-value systems          |
| Any modality                                      | Clinical Training & Certification Package        | +$75,000          | Ensures staff proficiency                      |
| Portable Ultrasound/X-Ray                         | Extended Battery & Transport Case                | +$25,000          | Essential for mobile deployments               |
| Premium Research tier                             | Research Collaboration Portal access             | +$50,000/yr       | Enables multi-site clinical trials             |

### Dynamic Pricing Example (Base Calculation)
Total Price = Base Modality Price  
+ Performance Tier Adder  
+ Field Strength/Resolution Adder  
+ Sum of Selected Software Packages  
+ Installation Add-ons (mandatory based on modality)  
+ Annual Service Level (quoted separately)

**Example Build**: 3T MRI, Premium Research tier, AI Diagnostics + Oncology Workflow, Premium Care service  
→ ~$4,000,000 capital + $660,000 annual service

This catalog provides sufficient depth to demonstrate sophisticated rule enforcement, dynamic pricing, and contextual revenue optimization while remaining fully simulatable in a GCP Dialogflow CX webhook.