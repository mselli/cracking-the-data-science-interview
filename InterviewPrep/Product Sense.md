# Meta mock up

## **Meta Data Science Mock Interview: Product Analytics**

This guide mimics the structure of a Meta (Facebook) Data Science interview, focusing on the three core pillars: **Product Sense**, **Analytical Execution**, and **SQL**.

At Meta, the "proper" answer is less about the final number and more about the **structured path** you take to get there. They value hypothesis-driven thinking over guessing.

---

### **Section 1: Product Sense (The "North Star")**

**Goal:** Test your ability to turn vague product ideas into concrete, measurable goals.

#### **Question:**

> "We are thinking of launching a new 'Stories' feature for Facebook Groups where members can post temporary video updates visible only to that grow up. How would you measure the success of this feature?"

#### **How to Answer Properly:**

Do not jump straight to "I would track Daily Active Users." Instead, use a framework like **GAME** (Goals, Actions, Metrics, Evaluations).

**Example Response Strategy:**

1. **Clarify the Goal:**
   
   - *Candidate:* "First, I want to align on the goal. Is this feature intended to increase overall time spent on Facebook, or is it specifically to deepen community connection within Groups?"
   
   - *Interviewer:* "Let's say it's to deepen community connection."

2. **Define Success Metrics (The "North Star"):**
   
   - *Candidate:* "If the goal is connection, mere 'views' aren't enough. I would look at **active participation**.
   
   - *Primary Metric:* **Number of Stories posted per Group DAU** (measures creation).
   
   - *Secondary Metric:* **Reply/Reaction rate per Story** (measures interaction quality)."

3. **Identify Guardrail (Counter) Metrics:**
   
   - *Candidate:* "We need to ensure this doesn't cannibalize other behaviors.
   
   - *Guardrail:* **Main Feed engagement.** Are users spending time on Group Stories *instead* of the News Feed? If Feed ad revenue drops, that's a trade-offs discussion."

4. **Ecosystem View:**
   
   - *Candidate:* "I’d also watch for **negative sentiment**, such as 'Hide Story' clicks or Group exits, to ensure we aren't spamming users."

---

### **Section 2: Analytical Sense (The "Detective")**

**Goal:** Test your ability to solve a business problem using data logic (Root Cause Analysis).

#### **Question:**

> "You come in on Monday morning and see that the 'Comment Rate' on Instagram posts has dropped by 10% globally over the weekend. How do you investigate?"

#### **How to Answer Properly:**

Avoid guessing ("Maybe it was a holiday?"). Use a systematic **"Split & Isolate"** approach.

**Example Response Strategy:**

1. **Sanity Check (Data vs. Reality):**
   
   - *Candidate:* "First, is this a data pipeline failure or a real user behavior change? I would check the data engineering logs to see if the table `comments_daily` was updated correctly or if there are null values."

2. **Segment the Data (The "Where"):**
   
   - *Candidate:* "If the data is real, I need to isolate *where* the drop happened. I’ll break it down by:
   
   - **Platform:** iOS vs. Android? (Did we ship a buggy app update on Friday?)
   
   - **Region:** Is this global or specific to a country (e.g., a holiday or internet outage in India/Brazil)?
   
   - **Feature:** Is it affecting all posts or just Reels/Stories?"

3. **Internal vs. External Factors (The "Why"):**
   
   - *Candidate:* "If it's only on iOS, I suspect a bad release. If it's global across all devices, I look at **External Factors**:
   
   - Did a competitor launch a big feature?
   
   - Was there a major cultural event that distracted users (e.g., Super Bowl, World Cup)?"

4. **Actionable Conclusion:**
   
   - *Candidate:* "Hypothesis: If the drop is only on Android, I’d check the latest release notes for UI changes to the comment button. If confirmed, I’d recommend an immediate rollback."
