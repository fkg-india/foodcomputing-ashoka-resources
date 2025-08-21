# FKG.in-FCN (Food Claim-Traceability Network)

The **Food Claim Network Ontology (FCN)** models food-related entities, claims, and their context for misinformation detection and claim provenance.

### 1. Food Entity

The **Food Entity** class represents the main food entity mentioned in a claim which may be a dish/recipe or an individual ingredient. A **Food Entity** instance has all the properties of either the Recipe or Ingredient categories, depending on its classification. Occasionally, a Food Entity instance may turn out to be a meal like `Breakfast`, or a nutrient such a`Vitamin B` when the input text does not refer to a specific food item, leaving most of the above-mentioned properties empty.

Below are the key properties:

- **food_name**  
  *Description*: The commonly known name of the food item in the context of the claim.  
  *Example*: `Turmeric`

- **food_category**  
  *Description*: A broad category or class the food belongs to.  
  *Example*: `Spice`, `Vegetable`, `Dairy Product`

- **food_description**  
  *Description*: A short explanation or contextual background of the food item, including traditional uses, preparation, or significance.  
  *Example*: `A yellow-orange spice used in South Asian cooking and Ayurvedic medicine.`

- **food_group**  
  *Description*: Nutritional or culinary classification of the food as per standard dietary guidelines.  
  *Example*: `Protein`, `Cereal & Grains`, `Fruits & Vegetables`

- **food_alt_names**  
  *Description*: Common alternative names across regions, languages, or dialects.  
  *Example*: `Haldi`, `Curcuma`

- **food_scientific_name**  
  *Description*: The botanical or scientific name, typically in Latin.  
  *Example*: `Curcuma longa`

- **food_nutritional_value**  
  *Description*: Key macro- or micronutrient values or health-relevant components.  
  *Example*: `Rich in curcumin, antioxidants, and vitamin C`

- **food_region_of_production**  
  *Description*: The typical or dominant regions where the food is grown or produced.  
  *Example*: `India, Indonesia, Thailand`

- **food_varieties**  
  *Description*: Specific cultivars, types, or local variations.  
  *Example*: `Erode turmeric, Alleppey turmeric`

- **food_claim**  
  *Description*: The specific claim being made about this food item.  
  *Example*: `Drinking turmeric milk boosts immunity`

### 2. Food Claim

The **Food Claim** class is the core category of FCN wherein each food claim is represented as a structured object containing semantic and contextual components that help in interpretation, comparison, and validation.

Below, we describe the different grammatical components of the **Food Claim** instance:

- **claim_text**: The original sentence or phrase from which the claim is extracted.  

- **claim_subject**: The primary and singular entity that the claim is about, resolving to a specific instance of **Food Entity**, **Ingredient**, or **Recipe** categories, such as `dragon fruit`. Occasionally, it may also refer to a nutrient or compound, such as `Vitamin C in orange`.  

- **claim_property**: A qualitative or quantitative attribute or state of the subject being described. This differs from and often precedes the effect, as it describes what the subject has (characteristic) rather than what it does (an action verb), such as `rich in antioxidants` or `low in cholesterol`.  

- **claim_effect**: The action, change, or influence the subject (e.g., food, supplement, herb, nutrient) is claimed to cause in the body or mind, including physiological (e.g., `lowers blood pressure`), perceptual (e.g., `makes skin glow`), disease-related (e.g., `prevents cancer`), cognitive (e.g., `improves memory`), cultural (e.g., `cools the body`) or functional (e.g., `aids digestion`, `boosts energy`) effects.  

- **claim_effect_type**: High-level category of the effect to aid filtering, clustering, and analyzing claims. Multiple effect types may apply to a single claim.  
  *Examples*: `health`, `mental`, `skin`, `metabolism`, `detox`, `energy`, `weight`, `immunity`, `digestion`, etc.  

- **claim_mechanism**: Causal pathway or biological explanation behind how the effect occurs, typically starting with expressions like “by”, “via”, or “through”.  
  *Examples*: `by binding free radicals`, `through enhancing insulin sensitivity`.  

- **claim_condition**: Temporal, contextual, or situational qualifiers that enable, limit, or modify the claim’s applicability.  
  *Examples*: `on an empty stomach`, `if consumed daily`.  

- **claim_intent**: Epistemic classification based on truth-value and intent, strictly one from the following:
    - **Factual**: A claim supported by verifiable evidence or scientific consensus.  
    *Example*: `Leafy greens like spinach are rich in iron and folate.`

    - **Myth**: A widely held but false or unverifiable belief, often rooted in tradition or culture.  
    *Example*: `Eating mango and milk together is poisonous.`
    
    - **Misrepresentation**: A distortion or selective presentation of facts that leads to a misleading impression, whether intentional or not.  
    *Example*: `This snack is fat-free!` — while ignoring that it is loaded with added sugar.

    - **Misinformation**: False or inaccurate information shared without the intent to deceive.  
    *Example*: `Microwaving food destroys all its nutrients.` (commonly believed but incorrect)

    - **Disinformation**: Deliberately false information shared with the intent to mislead.  
    *Example*: `This herbal tea cures COVID-19.` — used to drive sales, despite no evidence.

    - **Malinformation**: Genuine information presented out of context or used maliciously to cause harm or mislead.  
    *xample*: Sharing a real study showing sugar spikes insulin to falsely claim that `all fruits are toxic.`


- **claim_type**: Captures the conceptual nature of the claim for organization and comparison across domains. Multiple claim types may apply to a single claim, with the value being the types identified below:
    - **Scientific/Medical**
    - **Cultural/Traditional**  
    - **Moral/Political**
    - **Sustainability/Regulatory**
    - **Aesthetic/Sensory**
    - **Religious/Ritualistic** 
    - **Social/Symbolic**  
    - **Origin/Authenticity**  
    - **Marketing/Advertising**  
    - **Digital/Influencer**  


    See [Appendix A: Claim Types](#appendix-a-claim-types) for examples.

- **claim_validity_status**: Coarse-grained judgment about the scientific validity of the claim, marked as strictly one of:  
  - `true` (if backed by a source)  
  - `false` (if debunked)  
  - `unverified` (e.g., traditional beliefs with no evidence)  

### 3. Claim Source

The **Claim Source** class captures the origin or initial reporting of a food-related claim, such as a research article, newspaper, blog post, regulatory document, social media post, etc. It anchors each claim to a tangible source, allowing us to track how claims first enter the public domain or information ecosystem. While some claims originate in formal publications or official channels, many emerge in informal or in culturally embedded ways. Thus, this category accommodates diverse source types with flexible metadata to describe a claim’s first appearance or point of capture. This foundational anchoring enables downstream analysis of claim propagation, mutation, or contestation across contexts.

Below are the key properties:

- **source_text**: The name of the platform, publication, or institution that produced or hosted the validating content.  
  *Example*: `Reddit`, `World Health Organization`, `Times of India`

- **source_type**: The type or medium of the validating content.  
  *Example*: `forum post`, `scientific paper`, `news article`, `YouTube video`

- **source_url**: A placeholder or representative URL for the source content.  
  *Example*: https://example.com/source123

- **source_author**: A person or entity credited with originating the content.  
  *Examples*: `Neha’s Kitchen`, `TOI Health Desk`, `Dr. R. Kapoor`

- **source_date**: Date when the claim was made or the content was published.  
  *Examples*: `2022-03-15`, `Last week`, `During COVID-19 wave 2`

---

### 4. Claim Context

The **Claim Context** class provides semantic grounding for a claim by situating it in its geographic, cultural, temporal, or epistemic setting in which it is typically made or believed. For instance, `curd should not be eaten at night` is prevalent in parts of South Asia, while `milk and fish should not be eaten together` spans multiple cultures with varying justifications. Geographic and sociocultural tagging disambiguates similar claims with different foundations, supporting comparative studies on regional variation, cultural specificity, or localization of health and food beliefs. By modeling where, when, and in what context a claim is situated or most salient, the **Claim Context** layer enables richer reasoning about credibility, relevance, and stakeholder perspectives.

Below are the key properties:

- **context_geographic**: Geographic region or setting relevant to the claim.  
  *Examples*: `Kerala`, `South India`, `Urban Delhi`

- **context_cultural**: Cultural, religious, or traditional background informing the claim.  
  *Examples*: `Ayurveda`, `Islamic dietary rules`, `Tamil food customs`

- **context_temporal**: Time period or historical moment contextualizing the claim.  
  *Examples*: `Post-partum period`, `Winter`, `Colonial era`

- **context_community**: Specific social group or demographic associated with the claim.  
  *Examples*: `Punjabi Sikhs`, `Elderly in Maharashtra`, `Fitness influencers`

---

### 5. Validating Source

The **Validating Source** class captures the web of commentary and scrutiny that surrounds a food claim after it enters discourse. It includes external sources that support, challenge, request evidence for, question, or clarify a given claim, whether from scientific studies, expert statements, regulatory comments, anecdotal testimonies, or online discussions. Each validation entry records stance, medium, speaker, and source type, allowing claims to be contextualized within diverse knowledge communities and preserving multiple perspectives. E.g., a claim may be simultaneously challenged by a scientific review, supported by a traditional knowledge, and hedged by consumer anecdotes - all of which are stored as linked but independent viewpoints. Thus, each claim may have more than one validating source. The inclusion of confidence indicators, provenance metadata, and stance classification enables users to trace how different types of evidence and authority interact around a claim. Unlike **Claim Source**, which records where a claim first appears, **Validating Source** traces how it is subsequently evaluated, interpreted, or contested. The overarching aim is to treat validation not as a binary truth check but as a layered ecosystem of commentary, traceability, credibility, and source fidelity.

Below are the key properties:

- **validity_text**: Verbatim snippet expressing validation, debunking, or clarification.  
  *Example*: `There’s no actual study proving this works.`

- **validity_stance**: The position taken by the validating source on the claim — one of the following: `supports`, `challenges`, `requests evidence`, `clarifies`, `unsure`.  
  *Example*: `Challenges`

- **validity_evidence_reference**: Any textual reference to supporting or opposing evidence, authority, or anecdote.  
  *Example*: `PubMed article`, `My doctor told me`, `A study I read`

- **validity_organization**: Name of any institution or body associated with the source.  
  *Example*: `WHO`, `Harvard Medical School`

- **validity_source_type**: The nature of the validating source.  
  *Examples*: `Scientific study`, `Expert quote`, `Meta-analysis`, `Reddit comment`

- **validity_source_url**: URL to the original validation source, if available.  
  *Example*: `https://www.reddit.com/r/nutrition/comments/xyz`

- **validity_confidence_expression (optional)**: Qualitative description of how confident the speaker or author is.  
  *Examples*: `Sounds very sure`, `Hedges with ‘I think’`

- **validity_confidence_score**: Numerical score (1–5) indicating the speaker’s or author’s confidence in the reliability or credibility of the validation statement. This score reflects how convincing, well-supported, or internally consistent the validation appears in context, not whether the claim itself is true and adheres to the following scale:  
  - 1 — Very low confidence: The statement appears vague, speculative, or unsupported.  
  - 2 — Low confidence: The statement contains weak or anecdotal justification; unclear source.  
  - 3 — Moderate confidence: Some relevant evidence is cited, but clarity or authority is limited.  
  - 4 — High confidence: The validation is coherent and aligns with known sources or expert views.  
  - 5 — Very high confidence: Statement is strongly grounded in authoritative, well-cited evidence (e.g., peer-reviewed study, WHO guidelines).  
  *Example*: `4 — “This is supported by a recent meta-analysis in JAMA.”`

- **validity_linked_claim**: Identifier of the claim being supported or challenged.  
  *Example*: `dragon_fruit_reddit-uwchqg_c01`

- **validity_author**: Name or username of the person who issued the validating statement.  
  *Examples*: `u/SciMedic`, `Harvard paper`, `Dr. Ahuja`

- **validity_date**: Date when the validation statement or reference was made.  
  *Example*: `2023-05`

- **validity_medium**: The platform or channel where the validation appears.  
  *Examples*: `Reddit`, `PubMed`, `YouTube`

- **validity_outcome**: A brief summary of the conclusion of the validating source.  
  *Examples*: `No clinical evidence for this`, `Supported by meta-study`, `Tradition, but no proof`

## Appendix A: Claim Types

[Table: Different Types and Examples of Food and Health Claims Common in India](#table-different-types-and-examples-of-food-and-health-claims-common-in-india)

| No. | Claim Type             | Claim Example 1                                                                 | Claim Example 2                                                                 |
|-----|-------------------------|---------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| 1   | Scientific/Medical      | White rice has a high glycemic index and spikes insulin levels.                  | Curcumin in turmeric inhibits inflammatory pathways in the body.                |
| 2   | Cultural/Traditional    | Eating curd at night causes a cold.                                              | Rice cools the body and should be avoided during winter illnesses.              |
| 3   | Moral/Political         | Chicken *tikka* made from factory-farmed poultry is harmful to health.           | Consuming beef pollutes the body and violates *dharmic* (virtuous) principles.  |
| 4   | Sustainability/Regulatory | Millets require less water than wheat and are better for the environment.       | Sugar-free biscuits labeled as 'diabetic-friendly' do not cause spikes in blood sugar levels. |
| 5   | Aesthetic/Sensory       | Aged cheddar cheese develops a sharper, more desirable flavor.                   | Freshly cut mango contains more *prana* (life energy) than packaged mango juice. |
| 6   | Religious/Ritualistic   | Temple-prepared *aloo sabzi* (potato curry) as *prasad* (sacred offering) excludes garlic and onion because they are *tamasic* (dullness-inducing). | *Halal*-certified chicken *biryani* is permissible for consumption during Islamic festivals. |
| 7   | Social/Symbolic         | Tofu is a healthier and more ethical substitute for paneer.                      | Millets are rural or ancient food, not fit for urban or modern diets.            |
| 8   | Origin/Authenticity     | *Basmati* rice grown in the Himalayan foothills is more aromatic than other varieties. | *Goan vindaloo* (curry preparation) must use toddy (fermented palm sap) vinegar for authentic flavor. |
| 9   | Marketing/Advertising   | Almond milk boosts brain function and contains no cholesterol.                   | Cold-pressed beetroot juice detoxifies the liver and promotes weight loss.       |
| 10  | Digital/Influencer      | Avocado toast is the perfect brain food for productivity.                        | Intermittent fasting with bulletproof coffee resets your gut.                   |
