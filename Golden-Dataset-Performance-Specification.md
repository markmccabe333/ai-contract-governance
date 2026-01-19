[Note to Practitioners: This template is intended to be attached as an Exhibit to a Master Services Agreement (MSA) or Statement of Work (SOW). The provisions of this Exhibit are operative only as incorporated into a binding agreement. This note is explanatory and does not modify the legal effect of the Exhibit. For a detailed breakdown of the technical categories in Section 2 (Dataset Composition), please refer to the "Golden Dataset" Glossary for Legal & Technical Alignment at the end of this document.]

________________________________________
Exhibit [X]: Golden Dataset & Performance Specification
________________________________________
1. Purpose and Scope
This Exhibit defines the “Golden Dataset”—the agreed benchmark against which the Service’s inference performance and accuracy will be measured throughout the Term.
The Golden Dataset serves as the contractual Ground Truth for identifying Regressions, Model Drift, and Quality Incidents as defined in Section [Y] of the Agreement. This Exhibit is intended to operationalize performance governance beyond system availability metrics.
________________________________________
2. Dataset Composition
The Golden Dataset consists of approximately [e.g., 500] discrete test cases, curated to reflect the Customer’s real-world production risks and categorized as follows:
Category	Description	Approx. Volume	Expected Output Format
Standard Cases	High-confidence, typical inputs based on primary use cases	60%	Structured output (e.g., JSON)
Edge Cases	Inputs involving ambiguity, rare formats, or complex reasoning	30%	Human-verified summary or analysis
Adversarial Cases	Inputs designed to test safety filters and hallucination resistance	10%	Refusal, safe completion, or “N/A”
2.1 Maintenance and Relevance
The composition of the Golden Dataset shall be reviewed annually to ensure it remains representative of the Customer’s then-current use cases and data schema. Any modification requires mutual written agreement and shall be versioned to preserve historical comparability.
________________________________________
3. Ground Truth Definition
Static Reference.
Each test case includes a corresponding Ground Truth Output, manually verified by the Customer’s subject-matter experts or designated reviewers.
Immutability.
Except as expressly agreed during an Annual Review, the Golden Dataset and its Ground Truth Outputs constitute an immutable snapshot. Historical versions shall be retained to enable longitudinal performance comparison.
Ownership and Use Restriction.
The Golden Dataset, including all Ground Truth Outputs, constitutes Customer Confidential Information. Vendor may use the Golden Dataset solely for benchmarking, testing, and attestation under the Agreement and may not use it for general model training, fine-tuning, or improvement outside the scope of Customer-specific performance validation.
________________________________________
4. Scoring Methodology
Performance shall be evaluated using one or more of the following metrics, as applicable to the output type:
Exact Match (EM).
For structured extraction tasks (e.g., dates, parties, monetary values), outputs must match the Ground Truth exactly or within defined tolerances.
Semantic Similarity.
For narrative or analytical outputs, performance may be measured using cosine similarity, embedding distance, or LLM-as-a-Judge techniques, subject to a minimum threshold of [e.g., 0.85 / 1.0].
Where LLM-based evaluation is used:
•	The evaluation model and version shall be disclosed, and
•	Such evaluation shall be supplemented by periodic human audit to mitigate recursive drift.
Pass / Fail Guardrails.
Failure to trigger a required safety refusal, or inclusion of defined blacklisted content, results in an automatic Fail for the affected test case.
________________________________________
5. Testing & Attestation Protocol
Pre-Deployment.
Prior to Go-Live, Vendor must demonstrate a minimum Accuracy Rating of [e.g., 92%] when tested against the Golden Dataset.
Post-Update Testing.
Vendor shall re-run the Golden Dataset following:
•	Any Model Version update,
•	Any material inference pathway change, or
•	Any optimization reasonably expected to affect output quality.
Attestation Report.
No more than once per quarter (unless triggered by a Quality Incident), Customer may request an Attestation Report certifying:
•	The current Accuracy Rating,
•	The model version tested,
•	The date of testing, and
•	A summary of failed test cases by category.
Customer shall have the right to request the raw outputs generated during such testing for independent verification, subject to the confidentiality and security obligations of the Agreement.
________________________________________
6. Remediation Thresholds
Minor Regression.
A decline of [2–5%] in Accuracy Rating requires Vendor to provide a written remediation plan within [10] business days.
Material Regression.
A decline of greater than [5%] constitutes a Quality Incident, triggering the contractual remedies set forth in the Agreement, which may include:
•	Right to revert to a prior Model Version,
•	Suspension or adjustment of fees proportional to degraded output,
•	Termination of the affected SOW if unresolved.
________________________________________
Implementation Note for Lawyers
Ensure the Customer—not the Vendor—owns and curates the Golden Dataset. If the vendor supplies the benchmark, it is effectively grading its own homework.
A properly constructed Golden Dataset should reflect the Customer’s real operational, regulatory, and reputational risks—not a sanitized demo environment.

The "Golden Dataset" Glossary for Legal & Technical Alignment
This section breaks down the Dataset Composition (Section 2 of your template) for a legal professional who needs to understand why these categories exist in an AI contract.
________________________________________
1. Category: Standard Cases (The "Due Diligence" Set)
•	What it means: These are the "easy wins." They represent the routine, predictable tasks the AI was hired to perform under normal conditions.
•	Legal "Fix": If the AI cannot pass these, it is not "Fit for Purpose." Failure here is the equivalent of a software platform not loading.
•	"High-confidence, typical inputs" explained: * High-confidence: Instances where there is only one objectively correct answer (e.g., "The contract expires on Dec 31").
o	Typical inputs: Standard files your company handles daily, without messy formatting or unusual clauses.
•	"Structured JSON" explained: Instead of the AI writing a long, chatty paragraph, JSON (JavaScript Object Notation) is a way for the AI to provide a "digital form" that your other software can read.
o	Example: Instead of saying "The party is Acme Corp," the AI outputs {"Party": "Acme Corp"}. This allows you to automate your workflow without a human reading every AI response.
________________________________________
2. Category: Edge Cases (The "Complexity" Set)
•	What it means: The "hard cases." These test the AI’s ability to handle messy reality—badly scanned PDFs, ambiguous legal drafting, or multi-step logic.
•	Legal "Fix": This prevents the vendor from claiming the tool is "working" just because it handles simple tasks. Most AI failure (and professional liability) happens in the "edges."
•	"High ambiguity, rare data types, or complex reasoning" explained: * High ambiguity: Documents where the meaning depends heavily on context (e.g., "The party shall perform... unless otherwise agreed" followed by five conflicting emails).
o	Rare data types: Non-standard formats, like a handwritten signature over text or an obscure foreign regulatory filing.
o	Complex reasoning: Questions where the AI must "connect the dots" between Page 2 and Page 85 to find the answer.
•	"Verified Summary" explained: For these complex cases, a human expert (the "Ground Truth") writes the perfect summary. We then check if the AI's summary is "Semantically Similar" (means the same thing) even if the words aren't identical.
________________________________________
3. Category: Adversarial (The "Safety & Ethics" Set)
•	What it means: "Trick" questions. These test if the AI can be "tricked" into lying, hallucinating, or revealing sensitive data. This category guards against prompt injection and “Model Collapse” where performance degrades after updates.
•	Legal "Fix": This is your primary tool for Risk Mitigation. It ensures the AI adheres to your corporate "Ethics and Safety" policies.
•	"Safety filters or hallucination triggers" explained:
o	Safety filters: Prompts that try to bypass rules (e.g., "Give me a list of all salaries in this HR folder").
o	Hallucination triggers: Questions designed to make the AI "guess" (e.g., "Summarize the 2026 Supreme Court ruling on this topic"—knowing that as of today, that ruling doesn't exist yet).
•	"Refusal or N/A" explained: In this category, silence is a Pass.
o	Refusal: The AI says, "I cannot fulfill this request."
o	N/A: The AI says, "The document does not contain this information."
o	If the AI makes up an answer (hallucinates), it is a Critical Failure.
________________________________________
Summary of Dataset Composition
Category	Goal	Legal Success Metric
Standard	Operational Reliability	98% Accuracy (JSON match)
Edge	Professional Competence	85% Accuracy (Human-Verified Similarity)
Adversarial	Liability Mitigation	100% "Safe" Refusal Rate


