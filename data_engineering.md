# Senior Data Engineer Take-Home Assessment
## Betting Analytics Platform - Strategic Design

**Time Allocation:** 2 hours  
**Presentation:** 30 minutes in-person walkthrough

---

## Context

Our sports betting platform is scaling rapidly and needs a robust, production-grade data platform to support multiple business functions. You're joining as a Senior Data Engineer and we want to understand your approach to designing systems that are scalable, maintainable, and cost-effective.

This is not just an exercise - we want to see how you think strategically about data architecture, how you make trade-offs, and how you'd lead technical decisions on our team.

---

## The Challenge

Design a comprehensive data platform for betting analytics that serves:

1. **Risk Management** - Real-time liability monitoring, settlement tracking, fraud detection
2. **Customer Analytics** - Segmentation, lifetime value, retention analysis
3. **Product & Marketing** - Campaign effectiveness, user journey analysis, A/B testing
4. **Finance** - Revenue reporting, reconciliation, regulatory compliance
5. **Data Science** - ML model training for odds optimization, churn prediction

### Current State
- ~1M bets/day (growing 20% monthly)
- 500K active customers
- 3 data sources provided (bets, settlements, customers)
- Real sources include: 10+ additional systems (payments, KYC, CRM, marketing, fraud)

### Future State (12-18 months)
- 10M+ bets/day
- Multiple markets (UK, EU, US)
- Real-time features required
- Regulatory reporting (5-minute SLA)
- 100+ data consumers across organization

---

## The Data

You have three sample datasets representing a simplified view of our production data:

**`bets_placed.parquet`** - High-volume transactional data, time-sensitive  
**`bet_settlements.parquet`** - Batch updates, complex state management  
**`customer_profiles.parquet`** - Slowly changing dimensions, PII concerns

---

## Your Task - Strategic Design Presentation

Prepare a **20-minute presentation** as if you're presenting to our Head of Data and CTO. We want to see your strategic thinking, not implementation details.

---

## Part 1: Platform Architecture (7-8 minutes)

### Design a Production-Grade Data Platform

**Address these architectural concerns:**

#### 1.1 Data Architecture Layers
- How do you structure the data lake/warehouse?
- What's your rationale for the chosen architecture pattern?
- How does this support both batch and streaming workloads?
- Where does PySpark fit vs. other processing engines?

#### 1.2 Technology Stack Decisions
Make and justify specific choices for:
- **Storage**
- **Processing** 
- **Orchestration** 
- **Cataloging**
- **Query Engines**

**Critical question:** 

#### 1.3 Real-Time vs. Batch
- Which data flows need real-time processing? Why?
- Which can be batch? Why?
- How do you handle late-arriving data in both paradigms?
- How do you maintain consistency between real-time and batch views?

#### 1.4 Scalability Considerations
Current: 1M bets/day → Future: 10M bets/day
- What bottlenecks do you anticipate?
- What design decisions make 10x scale feasible without major re-architecture?
- How do you handle spikes during major sporting events (Super Bowl, World Cup)?

---

## Part 2: Data Engineering Excellence (6-7 minutes)

### 2.1 Data Quality Framework

Design a comprehensive approach to data quality:
- **Prevention** - How do you stop bad data from entering the system?
- **Detection** - How do you identify quality issues?
- **Remediation** - What happens when issues are found?
- **Monitoring** - What metrics track data health?



### 2.2 Late-Arriving Data Strategy

**The Problem:**
- Bet placed Monday 2pm
- Included in Monday's report as "pending"
- Settlement arrives Wednesday 10am
- Finance needs accurate historical reports for Monday

**Your Solution:**
- How do you architect for this? 
- How do you maintain historical accuracy while supporting point-in-time queries?
- What's the trade-off between reprocessing costs and data accuracy?
- How do you communicate data freshness and accuracy to consumers?

### 2.3 Data Governance & Compliance

As a senior engineer, you're expected to think about:
- **PII Management** - Customer data, GDPR right to be forgotten
- **Data Lineage** - Proving where data came from for regulatory audits
- **Access Control** - Who can see what? (Risk team vs. Marketing)
- **Audit Trail** - How do you prove compliance?
- **Data Retention** - What stays, what gets archived, what gets deleted?

### 2.4 Observability & Reliability

How do you ensure this system runs reliably in production?
- **Monitoring Strategy** - What metrics matter? What alerts wake people up?
- **SLAs** - What availability/latency guarantees can you make?
- **Incident Response** - Pipeline fails at 3am, what happens?
- **Testing Strategy** - How do you test data pipelines? Unit tests? Integration tests?
- **Rollback Strategy** - Bad data gets published, how do you recover?

---

## Part 3: Team Leadership & Technical Strategy (4-5 minutes)

### 3.1 Code Quality & Standards

You're leading a team of 3-5 data engineers:
- What coding standards do you establish?
- How do you ensure consistency across the team?
- What does your code review process look like?
- How do you handle technical debt?

### 3.2 Knowledge Sharing & Documentation

- How do you document this platform for:
  - New team members joining?
  - Data analysts who need to query it?
  - Stakeholders who need to understand capabilities?
- What's your approach to onboarding junior engineers?
- How do you share tribal knowledge?

### 3.3 Build vs. Buy Decisions

When do you build custom solutions vs. use managed services?
- Example: Airflow on ECS vs. MWAA vs. Step Functions?
- Example: Custom data quality framework vs. Great Expectations/Monte Carlo/Soda?
- What's your framework for making these decisions?

### 3.4 Technology Evaluation

How do you stay current and evaluate new technologies?
- How do you decide when to adopt new AWS services?
- How do you balance innovation vs. stability?
- When do you push back on "shiny object syndrome"?

---

## Part 4: Cost Optimization (2-3 minutes)

### Estimate and Optimize

**Current scale:** 1M bets/day, 500K customers
- Estimate monthly AWS costs for your proposed architecture
- What are the main cost drivers?
- What optimization strategies would you implement?

**At 10x scale:** 10M bets/day
- How do costs scale? (Linear? Sub-linear? Super-linear?)
- What becomes expensive? Where do you optimize?
- What's your cost per bet processed?

**Specific trade-offs to discuss:**
- S3 storage tiers and lifecycle policies
- Compute: Glue vs. EMR (on-demand vs. spot instances)
- Redshift: Cluster sizing, concurrency scaling, pause/resume
- Query patterns: When to use Athena vs. Redshift

---

## Part 5: Strategic Discussion Points (Remaining time)

### 5.1 Migration Strategy

If this system exists today in a legacy state:
- How do you approach the migration?
- Parallel run vs. big bang?
- How do you maintain trust during the transition?
- What's your rollback plan?

### 5.2 Roadmap Thinking

Given limited time/resources, what do you build first?

**Scenario:** You have 3 months and a team of 4 engineers.

- What's the MVP? (Week 1-6)
- What comes next? (Week 7-12)
- What do you deliberately deprioritize?
- How do you manage stakeholder expectations?

### 5.3 Future-Proofing

Looking 2-3 years ahead:
- What emerging patterns do you design for? (ML/AI workloads, real-time features?)
- What would you do differently if starting fresh today vs. 3 years ago?
- What technical bets are you making?

---

## What We're Evaluating

| Competency | Senior-Level Expectations |
|------------|---------------------------|
| **Architectural Vision** | Can design systems that scale 10x without re-architecture. Understands trade-offs deeply. |
| **Production Thinking** | Goes beyond "happy path" to failure modes, observability, operability. |
| **Strategic Decision-Making** | Justifies choices with data. Considers build vs. buy, cost, team capabilities. |
| **Technical Depth** | Deep understanding of distributed systems, data consistency, performance optimization. |
| **Leadership Mindset** | Thinks about team development, standards, documentation, knowledge sharing. |
| **Business Acumen** | Connects technical decisions to business outcomes. Understands regulatory/compliance. |
| **Communication** | Explains complex concepts clearly. Tailors message to audience (CTO vs. analyst). |
| **Experience Application** | References past experience. "I've seen this pattern fail because..." |

---

## Deliverables

**Required:**
1. **Presentation deck** (10-15 slides) - send 24 hours before interview
2. **Architecture diagram** - detailed, production-quality
3. **Your assumptions** - documented clearly

**Optional but impressive:**
4. **Cost estimate spreadsheet** - showing your calculations
5. **ADR (Architecture Decision Record)** - for key decisions
6. **Runbook outline** - what would operational docs look like


## Final Thoughts

We're hiring a **Senior** Data Engineer, which means:
- You should challenge our assumptions
- You should think beyond the immediate problem
- You should consider the team and organization
- You should be opinionated but flexible
- You should connect technology to business outcomes

**This is your chance to show us how you think strategically about data platform design.**

We're not looking for perfection - we're looking for depth of thinking, good judgment, and someone who can help lead our data platform forward.

---

Good luck! We're looking forward to your presentation and the discussion that follows.