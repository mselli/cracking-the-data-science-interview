# Torc Robotics MLE Interview Study Guide — **2026 Edition**

# Torc guidelines

For your January interviews, be prepared to position yourself as a data science–focused MLE who can **help define the *right* metrics and build effective checkers**, rather than emphasizing large-scale cloud deployment. 

- We will be asking topics around your **background and experience with ISO 26262, in how it informs your approach to software quality targets and safety assurance levels**. 

--> While ISO 26262 addresses functional safety (absence of unreasonable risk due to hazards caused by malfunctioning behavior), my work focused more on **behavioral safety.**

I’ve worked leading the IEEE 2846 standard that defined kinematic assumpionts to consider about the behavior of other road users and SAE J3237 V&V TF defining metrics for safety assessment of ADS. All this work can be used to specify driving behavior metrics and kinemtic conditions that can be specified to check for safety assurance within the operational design domain:

| Kinematic assumptions     | Safety metrics |
|:------------------------- | --------------:|
| Max accel                 | SERV           |
| min decel                 | SEV            |
| response time             | SEI            |
| Speed of occluded objects | SERTV          |

- Be ready to **discuss how you design and validate checkers** and how that work can interface effectively with safety-focused teams like PESS. There will also be high level conversations on your systems and software knowledge and how it enables strong collaboration with platform teams on shared checker infrastructure. 

- Lastly, we will be covering your Torc / Autonomy org match so come prepared to have more detailed answers on why join us from your own perspective and how it aligns with your career trajectory unique to you.

---

## My intro

--> During my 8 years at intel, Ive always been involved in automotive projects. I spent about 6 years at intel working on ADS safety before I moved towards a more strategy-focused role for automotive during my last 2 years at Intel. 

During the first 6 years at Intel, I was working for Mobileye, which Intel had aquired soon after I joined, and my job was to **advocate for their ADS safety approach across academia, industry, and regulation.**

    I've participated in standards organizations, like IEEE and SAE, where I got to lead the technical discussions for defining metrics for the safety performance assessment of ADS and also defining reasonably foreseeable behavioral assumptions that an ADS can make about other road users. ~~These were standards that were trying to contribute to behavioral specifications for ADS, complementing stndards like ISO 26262 and 21448.~~

    For example, at SAE we published a recommended practice document defining a taxonomy of safety metrics, including safety envelope-related metrics, that are implementation agnostic and that can help measure the overall safety performance of an ADS throught its entire lifecycle whether that's during development or for the safety case argumentation.

Another part of my job included doing research and collaborating with universities on all things related to our safety approach.

**The research we did was divided in two main categories: safety assessment metrics definition for ADS and parameter optimization for the RSS model.**

RSS, which is a set of physics-based equations that define what's the minimum distance that an ADS must keep from other road users in order to no be the cause of an accidents.

**SIM**: For example, we used the CARLA simulator and a set of NHTSA pre-crash scenarios to show when and how some of the metrics were failing to detect dangerous situations, highlighting the gaps that commonly used metrics like TTC have when you think of them in the context of cars or trucks that drive themselves. 

**NDS**: For calibrating the model's parameters, we looked at naturlistic driving data and used genetic algorithms to find the RSS' parameters that would minimize the difference between the distance kept by humans driving in the real world and the distance kept by the model. Also, we looked at human driver behavior distributions data from german highways and assigned values to the model's parameters in a way that 

Our safety approach (the RSS model) involved a series of kinematics equations with configurable parameters representing things like response time, and assumed braking capabilities of other vehicles, and so the research I did focused on quantifying and validating these equations against other surrogate safety metrics through a data-driven approach. A portion of the research focused on comparing the performance of different safety metrics, things like TTC vs RSS, etc,  and another portion of the research focused on using statistical analysis and optimization techniques to find optimal parameters for the equations based on simulation as well as real world data.

**RSS:** RSS provides guidelines such that, absent other system failures, a driving policy which adheres to its rules is formally guaranteed not to cause a collision. Furthermore, RSS defines **parameters through which one can draw the line between reasonable driving decisions** and lapse of judgement. The RSS model is particularly useful for handling uncertainties and therefore balancing the tradeoff between safety and usefulness.

## Behavioral

**Why torc?**

First because Im passionate about self riving tehcnology in general. I think it is still a very complex and interesting problem that the industry needs to solve and I want to be part of a company that is trying to solve this. 

compny that is constanly innovating and developing cutting edge technology that has inmense socio-economic benefits. useful benefits

First because Im very passionate about self driving technology. I think it is one of the most useful automation and optimization that  of technology 

It is a very high impact and challenging problem to solve from all angles (societal, economical, technological, etc)  I think it is something that will happen and I want to be part of a company that is dedicated to iterate as much as needed . 

In a company like Torc, you

a company that is looking at that. On one side you have cutting edge technology being deployed in these systems and on the other side you have strong  point of view. in the samethink youI am t point in my career where Mainly because I find the problem of building a self driving something that goes on the roads, moves at highspeeds, and doesnt causes harm very interesting and challenging, and with the advances in AI now realized that the commercialization of self-driving technology is a problem that we as a society will solve very soon and I want to be a part of that. I think that self driving technology is no longer a research project, but also it is not yet a full product, but it will get there eventually. I find that problem very interesting and challenging and I want to be closer to the actual development of it. While I was at Intel i was very much involved in all things AVs, but always from the side, because intel is a HW supplier and

People know very well the potential benefits this technology brings, so it's time to work on a solution that can provide those benefits without compromising safety. 

---

## 1. **Role Positioning – Data Science-Focused MLE**

#### Role Overview

- **Traditional MLE:** Often focused on model design and deployment at scale.
- **Data Science-Focused MLE:**
  - Defines and iterates on **metrics** that measure system health, safety, and performance.
  - Designs and validates independent **checker systems** (tools or models that monitor, flag, and validate system behavior).
  - Balances requirements from product, safety, and platform teams—acting as a bridge.
  - **Emphasizes verification, safety, reliability, and explainability, not just accuracy and deployment.**

#### Why This Matters for Torc

- AVs operate in mission-critical domains with zero tolerance for catastrophic errors.
- Torc expects you to *shape safety* by quantifying risks, defining the right metrics, and validating tools/checkers in real-world contexts.

---

#### 2. **ISO 26262, ISO 21448 (SOTIF), and Safety Cases**

### 2.1. **ISO 26262 — Functional Safety**

#### What is it?

- **ISO 26262** is the international standard for *functional safety* of automotive electrical/electronic (E/E) systems.
- Focus: Identifies and mitigates risks from **malfunctions** due to systematic or random faults.

#### Core Concepts

- **Hazard Analysis and Risk Assessment (HARA):**
  - Identification of operational situations, potential hazards, their risks, and assignment of **Automotive Safety Integrity Levels (ASILs)** from A (lowest) to D (highest).
- **Requirements Allocation:**
  - Safety goals and requirements flow from hazard analysis down to technical requirements and specific component responsibilities, such as ML model checkers.
- **V-Model Lifecycle:**
  - Emphasizes traceability: every requirement must be validated/tested and verified.
- **Focus:**
  - **Malfunctioning behavior that is due to faults/flaws in hardware or software.**

---

### 2.2. **ISO 21448 — SOTIF (Safety Of The Intended Functionality)**

#### What is it?

- **ISO 21448 (SOTIF)** is a newer international standard that deals with *safety of the intended functionality* in vehicles.
- Focus: Hazards **not** primarily caused by malfunctions, but by limitations in the technology or its “intended” operation.
- Examples of SOTIF concerns:
  - A camera-based perception system that misses pedestrians in fog (even though hardware/software works as designed).
  - ML system that fails in scenarios not seen/trained for (Out-of-Distribution, OOD, behavior).
  - Sensor fusion failing to detect an unusual construction vehicle shape.

#### Key SOTIF Concepts

- **Functionality Limitations:** Addresses “known unknowns” (recognized limitations) and “unknown unknowns” (emergent hazards).
- **Scenario Analysis:** Requires systematic search and assessment of edge cases, rare events, and edge operational domains.
- **Improvement Loop:** Process for continuous data collection, scenario discovery, and system refinement/mitigation.

---

### 2.3. **How ISO 26262 and 21448 Work Together**

- **ISO 26262**: Ensures failures from *hardware/software malfunctions* are made acceptably rare.
- **ISO 21448 (SOTIF)**: Ensures the system is also safe when “working as designed”—by exploring and addressing limitations in the functionality (e.g., ML blindness to certain objects, environmental edge cases).
- **Both are crucial for AVs:**
  - Autonomous vehicles must be safe in the presence of faults **and** in all intended (and a-priori unintuitive) situations where they may not work, even if no fault exists.

#### Example for Checkers

- An ML-based checker that monitors for missed vehicle detections must be validated both for:
  - **Faulty software/hardware** (ISO 26262, e.g., misconfigured algorithm parameters)
  - **Known and unknown scenario limitations** (ISO 21448, e.g., new object types, weather conditions)

---

### 2.4. **Relation to the Safety Case**

#### What is a Safety Case?

- A **safety case** is a structured argument (with supporting evidence) that a system is acceptably safe to deploy in its intended environment. Often expressed as a "goal-structured" document:
  - “The system is safe”  
    —because→ “all hazards are identified and controlled”  
    —because→ “all malfunctions (ISO 26262) and functional limitations (ISO 21448/SOTIF) are addressed with process and evidence.”

#### How the Standards Feed a Safety Case

- **ISO 26262 and 21448 processes generate work products:** hazard logs, scenario analysis, requirements lists, test results, traceability, risk assessments.
- **The safety case collects and organizes this evidence:** Each claim about system safety is backed by experiments, test data, and analyses showing
  - Malfunction-based hazards are controlled (per ISO 26262).
  - Behavior is safe even in all intended and reasonably foreseeable scenarios, with known and unknown limitations mitigated (per ISO 21448).

#### Why is This Important for ML Engineers/Checker Developers?

- Your **checker design, metric definition, and validation artifacts** become **evidence** in the safety case.
- For every checker or metric, you should be able to show:
  - Which hazards or SOTIF scenarios it addresses.
  - How you validated its performance (*including adversarial or OOD cases*).
  - Relevant test results and edge case coverage.
- You must work with systems and safety engineers to ensure that your ML artifacts are **traceable**, **auditable**, and **justifiable** within the larger safety argument.

## ISO 26262: HARA

- **HARA (Hazard Analysis and Risk Assessment)** is a *required* core activity in ISO 26262.
  - Objective: Identify hazards that could result from *malfunctions* (i.e., faults or failures) in the system, evaluate their risk, and assign Automotive Safety Integrity Levels (ASIL).
  - Approach:
    1. List all operating situations.
    2. Identify possible malfunctions and the hazards they could cause.
    3. Assess severity, exposure, controllability.
    4. Assign ASIL.
  - Focus: Malfunctioning behavior **due to faults**.

## ISO 21448/SOTIF: STPA and Beyond

- **SOTIF (ISO 21448)** addresses *hazards not caused by malfunctions*, but by limitations or insufficiencies in the intended functionality (e.g., ML perception missing unseen situations, sensor limitations, OOD scenarios).
- **STPA (System-Theoretic Process Analysis)** is a modern hazard analysis technique particularly useful for SOTIF, but not mandated by ISO 21448—it is one *possible* approach among others (you could also use similar scenario-based analysis).
  - STPA, developed by Nancy Leveson, identifies unsafe control actions or process flaws even when there are no feature/hardware “faults”. It is popular for **SOTIF/21448** work because it can uncover “unsafe-as-designed” behaviors, especially in complex or ML-driven systems.
- **Scenario-based analysis** (such as SOTIF’s “Hazard Identification and Assessment”) is mandatory in ISO 21448. Tools like STPA, FMEA, or combinatorial scenario generation are recommended.

### So in practice:

- **ISO 26262:**
  
  - Do **HARA** to identify/assess hazards from malfunctions (you may *supplement* with FMEA, etc.).

- **ISO 21448/SOTIF:**
  
  - Do **systematic scenario analysis** to explore limitations ("known/unknown unknowns") of the intended system—not from faults, but from *design or environmental limits*.
  - Use tools like **STPA** to formalize and structure this process, especially for complex, software/ML systems.

**STPA is not required by either standard**, but is increasingly used for SOTIF (ISO 21448) or mixed-method assurance work because of its power to find non-fault-based hazards.

---

## 3. **Checker Theory, Metrics, and Design**

#### What is a Checker?

- A **checker** is a rule-based or ML/AI system that monitors outputs from main AV subsystems (perception, planning, etc.) for:
  - Unexpected values
  - OOD situations
  - Missed detections or classification errors
  - Safety rule violations

#### Types of Checkers

- **Rule-Based:** Hard-coded physics or logic constraints (e.g., speed < 120km/h, bounding box cannot be negative).
- **ML-Based:** Models trained to spot anomalies, OOD inputs, or unusual system signals.

#### Key Theory for Effective Checkers

- **Requirements:** Must be clear, scenario-specific, and derived from safety analysis—e.g., “No hazardous objects within 5m left undetected for more than 200ms.”
- **Metrics:**
  - **Recall (Sensitivity):** % of hazards or failures detected (Minimize false negatives!).
  - **Precision:** Avoid too many false alarms (but for safety, recall is often prioritized).
  - **Latency:** Time taken to flag or react to a hazard.
  - **Robustness:** Checker continues to function or fail-safe under edge conditions or sensor faults.
- **Coverage:** Checkers must be validated against both in-distribution data and edge/rare/OOD cases.

#### Testing and Validation

- **Scenario-Based Testing:** Use real, simulated, and synthetic “edge cases”—night, rain, construction, rare pedestrian positions.
- **Fault Injection:** Artificially introduce errors (e.g., sensor dropout).
- **Statistical Validation:** Cross-validation, ROC/PR curves, scenario-wise breakdown.
- **Continuous Monitoring:** Use logs/telemetry; real-world data is used to update challenge sets and drive further improvements.

---

## 4. **Checker Integration and System Interface (Collaboration with Safety, Platform, and Tools Teams)**

#### Integration Best Practices

- **Clear APIs:** Use well-defined inputs/outputs—e.g., with proto definitions or JSON schema.
- **Version Control:** Interface changes must be clearly managed to avoid system-wide errors.
- **Automated CI/CD:** Every checker update tested for safety, latency, and right-correctness before merging.
- **Documentation:** Document all assumptions, safety requirements, limitations, and test results.

#### Safety and Platform Team Interface

- Regular reviews with PESS and platform teams to:
  - Ensure traceability to safety requirements.
  - Maintain up-to-date hazard coverage.
  - Address deployment or runtime integration issues.

#### Tools and Tech Familiarity

- Familiarity with:
  - **Simulation environments** (e.g., CARLA, LG SVL).
  - Logging/telemetry (data lakes, stream processing).
  - CI/CD, code review, test harnesses (GitHub Actions, Jenkins, pytest/GoogleTest).

---

## 5. **ML Safety – High Assurance Principles for AVs (2026 Update)**

#### Recent Trends (2025–2026)

- **Self-Supervised and Synthetic Data:** Increased use for edge case/rare event simulation.
- **Formal Verification for ML Components:** Emerging tools for provable robustness/safety contracts.
- **Explainable AI (XAI):** ML outputs must be auditable and interpretable by safety engineers.
- **Continuous Learning:** Frameworks for real-time field monitoring and post-processing; new ODD cases are cycled back into model/checker updates.

## 1. What is Inferential Statistics?

Inferential statistics is the branch of statistics concerned with **drawing conclusions or making predictions about a large population based on analyzing a smaller sample of that population.**

- **The Problem:** In AV safety, the *population* is all possible miles the truck will ever drive across all possible ODD conditions (infinite). The *sample* is the finite number of test miles and scenarios collected (e.g., 5 million miles).
- **The Goal:** We use inferential methods to take the data from our 5 million test miles and make a reliable statement about the safety risk over the total operational lifetime (e.g., 500 million miles).

**Key Tools of Inference:**

1. **Hypothesis Testing:** Testing a claim about a population parameter (e.g., proving the new system's failure rate is lower than the old system's failure rate).
2. **Confidence Intervals (CI):** Providing a range of plausible values for a population parameter (e.g., stating with 99% certainty that the true failure rate is between A and B).
3. **Modeling and Extrapolation:** Using collected data to predict outcomes in unobserved conditions (e.g., Extreme Value Analysis).

---

## 2. The Role of Inferential Statistics in AV Safety V&V

Inferential statistics is essential because it quantifies the **uncertainty** and **generalizability** of safety claims—both of which are required by ISO 26262/SOTIF.

### A. Quantifying Verification (V)

Verification proves that the system was built correctly (e.g., the checker code executes as intended). Inferential statistics is used here to prove the robustness of the safety mechanisms.

| Inferential Role     | Method Example                         | AV Safety V&V Application                                                                                                                                                                                                                                               |
| -------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Testing Efficacy** | **Z-Test / Chi-Squared (Proportions)** | In **Fault Injection Testing**, we test the ASIL Checker against N injected faults. Inferential statistics proves the observed success rate (Recall) generalizes, assuring that the checker will maintain a high probability of detection in future, non-tested faults. |
| **Timing Assurance** | **Confidence Intervals**               | Proving the maximum execution latency of the safety checker. If 1,000 tests yield a mean latency of 8.2ms, a CI proves we can be 99.9% sure the worst-case latency will not exceed the 10ms hard deadline.                                                              |

### B. Quantifying Validation (V)

Validation proves that the system meets the high-level safety goals (i.e., that the system is safe to operate in the ODD). This requires extrapolation to the vast, unobserved population of driving miles.

| Inferential Role                 | Method Example                                | AV Safety V&V Application                                                                                                                                                                                                                              |
| -------------------------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Residual Risk Quantification** | **Poisson Confidence Interval**               | This is the core of ASIL validation. We use the small sample of observed failures (k) over test miles (N) to infer the **worst-case true failure rate (λUB​)** over the total population of miles, providing the guarantee needed for the safety case. |
| **Proving Safety Improvement**   | **Hypothesis Testing (Z-Test, T-Test)**       | Required for system upgrades. The Z-test infers whether the observed reduction in near-misses during shadow mode testing is a reliable, generalizable improvement across all future operating miles.                                                   |
| **Modeling Extremes**            | **Extreme Value Analysis (EVA)**              | EVA infers the likelihood and severity of catastrophic events that have *never* been observed (e.g., TTC <0.5s). This uses the collected sample data to model the long-term behavior of the population's tail risks.                                   |
| **Controlling for Bias**         | **Regression Models (Poisson/Neg. Binomial)** | Inferential statistics helps generalize safety claims by controlling for confounding factors. We infer the true safety impact of the ADS, holding variables like weather, traffic, and road type constant.                                             |

---

## 6. **Torc Organization and Your Career Match**

#### Torc’s Unique Value

- Leading the field in safe, on-highway L4 trucks; emphasis on transparency, safety, and high-bar functional assurance.
- Deep partnerships with OEMs, strong regulatory relationships.

#### Your Pitch

- I want to solve high-impact problems and be in the middle of it.
- I care a lot about ADS and ADS safety in particular. I take safety very seriously because it's still an open problem and a problem that if we dont get it right, it could hinder the scalable deployment of these systems (not just for torc, but for the entire industry). Sometimes **non-technical barriers** (economics, public trust, regulation) can be just as important as technology.

## 7. **Example Technical Questions & Detailed Answers (2026)**

---

**Q1:** *What is an ASIL, and how should it affect your approach to checker validation?*

**A1:**  
ASIL, or Automotive Safety Integrity Level, rates the risk of hazards from A (lowest) to D (highest) based on severity, exposure, and controllability. For ASIL D software/checkers, I must provide rigorous evidence: exhaustive scenario/edge-case testing, complete traceability to hazards, and robust fail-safe behavior. The scope and granularity of testing, plus level of documentation, scale in proportion to ASIL.

---

**Q2:** *Describe how you would validate an ML-based checker designed to detect missed objects in camera perception.*

**A2:**  
I would:

- Derive requirements from safety analysis: e.g., “Checker must catch 99.9% of missed objects within defined ODD.”
- Build high-quality test sets including real-world and synthetic OOD (night, occlusion, construction zones, rare object shapes).
- Run scenario-based testing, cross-validation, and realistic “fault injection.”
- Log checker performance post-deployment, and set up automated feedback so every discovered false negative is reviewed, annotated, and added to the validation corpus.

---

**Q3:** *Give an example of a checker metric you would use and why.*

**A3:**  
Recall at low false positives (e.g., recall > 99.9% when FPR < 1%) and scenario coverage (percentage of hazardous scenarios where the checker triggers a warning). These emphasize safety over operational discomfort, yet screen out checker spam. Latency (time to flag) is also critical, since slow alerts are ineffective for real-time mitigation.

---

**Behavioral/Organizational Practice:**

- “Why safety-first ML is my focus: reflections from your past work.”
- STAR stories on alignment and compromise between speed, accuracy, and safety.

---

## Statistical Proof for New Perception Model Deployment

The goal is to prove two things: (1) The new model is **significantly safer** than the baseline, and (2) The new model’s **worst-case failure rate** meets the predetermined ASIL residual risk target.

### Phase 1: Preparation and Data Collection (Shadow Mode)

1. **Define the Critical Safety Metric:** We use the rate of **Critical Event Triggers (E)** caused by the perception system.
   - *Example Event:* Perception failure that results in the **Independent Obstacle Clearance Checker** triggering an immediate safety buffer increase (TTCChecker​<3.0s).
2. **Establish Exposure (N):** The new model (SNew​) and the baseline model (SBaseline​) must run simultaneously in **Shadow Mode** on test fleet vehicles for a predetermined mileage (N).
   - *Example:* N=1,000,000 miles.
3. **Data Collection:** Record the number of critical events k triggered by each system:
   - kB​ (Baseline triggers)
   - kN​ (New system triggers)

### Phase 2: Hypothesis Testing (Z-Test) — Proving Improvement

We use the Z-Test for Two Proportions to demonstrate that the reduction in observed failures is statistically significant, not due to chance.

**Scenario:** We observe kB​=200 triggers and kN​=120 triggers over N=1,000,000 miles.

1. **Calculate Observed Rates:**
   - P^B​=200/1,000,000=2.0×10−4
   - P^N​=120/1,000,000=1.2×10−4 (40% reduction)
2. **Formulate Hypothesis:**
   - H0​ (Null Hypothesis): The true event rate is the same or worse (λN​≥λB​).
   - Ha​ (Alternative Hypothesis): The true event rate is significantly lower (λN​<λB​).
3. **Perform Z-Test:** Calculate the Z-statistic and the one-sided p-value.
   - *Result:* The Z-test will likely yield a large negative Z-score (e.g., Z≈−4.7), resulting in a very small p-value (e.g., p<10−6).
4. **Safety Case Conclusion:**
   - "We **reject H0​**. The new perception model provides a statistically significant reduction in the critical safety trigger rate. The observed 40% reduction is real, with confidence exceeding 99.99%."

### Phase 3: Residual Risk Bounding (Poisson λUB​) — Proving Adequacy

We use the Poisson upper bound calculation to determine the worst-case failure rate we can guarantee for the new system, which is required by the ASIL safety case.

1. **Define Safety Target:** Consult the PESS team for the ASIL residual risk target for this function.
   - *Example Target:* The maximum acceptable residual risk is λtarget​=5.0×10−5 failures per mile.
2. **Select Confidence Level:** Typically high for safety (e.g., C=0.99).
3. **Calculate Upper Bound (λUB​):** Use the Chi-Squared distribution based on the observed failures (kN​=120) and exposure (N=1,000,000).  
   λUB​=2Nχ2(kN​+1),C2​​
   - *Calculation:* Using the Chi-Squared table for 2(120+1)=242 degrees of freedom at C=0.99, the value is χ2≈287.
   - λUB​=2×1,000,000287​≈1.435×10−4 failures per mile.
4. **Safety Case Conclusion:**
   - **"Our calculated λUB​ is 1.435×10−4 failures/mile.** This means we are 99% confident the true failure rate is no worse than this.
   - **Compliance Check:** We compare this to the required λtarget​ (5.0×10−5). In this example, the model *failed* the target because 1.435×10−4>5.0×10−5.

### Phase 4: Interface and Action (The MLE Recommendation)

Since the analysis showed improvement but *failed* the absolute safety target, the MLE recommendation to PESS must be clear:

- **Recommendation:** "We cannot deploy the model yet. The evidence confirms it is better (statistically significant reduction), but the worst-case risk guarantee (λUB​) still exceeds the ASIL target.
- **Next Steps:** Recommend integrating a **second layer of checking** (e.g., a simple radar-based velocity tracker) to further reduce kN​, or increase the validated mileage N to tighten the confidence interval, thereby potentially lowering λUB​.

# End-to-end Training @ TORC

ML Sfety - ML attacks (adversarial attacks) robust and secure. 

HW Safety - SAE, redundancies (breaking, steering), tolerances 

SW Safety - cybersecurity.

safety case bsed on Miles drivens, disengagements, how did they happen, accidents.

data: 

20min drive - 600TB of data generated

**End to End training:**

2. annotation schema / annotation guide. deifne set of rules and guidelines for annotators and data colleectors. define scenarios for data to becollected. "data collection efforts should focus on night time". Send the trucks collectign data. Annotators are actual humans that draw and annotate the frames. this could be outsources or done internally

3. Q/A: human verifiers if data is good, no missed lables, no wrong annotations. 

4. ML: data engineering teams: RAW->processed. data is prepped following different schemas that the ML models need for handling the data. ExtractTransformLoad pipeline 

5. Training: few hours vs few days (foundation models). big trainning uses thousand of GPUs. downstream finetuning of smaller models based on specific tasks, e.g.: improve performance for night time - freeze some layers and finetune on certain layers. 

6. Testing/Eval: test set secert set. updated every 2 weeks. lots of diverse scenarios, challenging situations. 
   
   1. the model must fit in the target HW, so they quantize it to make it smaller

7. Close loop testing: driving test

8. Final Truck deployment + fianl test

9. safety driver drive

10. safety checks about the real world drive

11. final release. before finaly release: A/B testing, scaled rollouts

enhanced the ML model to see thru fog. Paper Seeing thru Fog. 

 80K lbs of vehicle. 
