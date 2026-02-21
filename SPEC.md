SPS Corps — Inventory Risk Prioritization Agent
Initial Project Specification
1. Business Problem Statement

Retail inventory teams require early warning signals when product demand increases significantly beyond normal levels. Sudden and abnormal demand spikes can increase the likelihood of stockouts if not identified and reviewed in time.

This project aims to design and implement a local LLM-powered decision-support tool that identifies state-category combinations exhibiting abnormal demand spikes on a weekly basis.

The system will assist inventory analysts in prioritizing review efforts by highlighting the Top 10 highest-risk state-category combinations each week.

2. Stakeholder & Decision

Primary User: Inventory Analyst

Weekly Decision:
Each week, the inventory analyst determines which state-category combinations demonstrate abnormal forecasted demand increases relative to recent historical patterns and therefore require operational review.

3. Risk Definition

The risk score represents the magnitude of forecasted demand increase relative to the recent 4-week average demand for a given state-category combination.

Formally:

Risk Score = Forecasted Demand ÷ 4-Week Moving Average

A higher ratio indicates a stronger abnormal demand spike and potentially increased stockout risk.

4. Tool Concept

The system will function as a local AI-powered agent that:

Loads weekly sales data from a local dataset.

Generates a one-week-ahead demand forecast for each state-category combination.

Computes the defined demand spike risk score.

Ranks all state-category combinations by risk score.

Returns the Top 10 highest-risk combinations.

Generates structured natural-language explanations grounded in computed numerical values using a local LLM.

The system will operate fully offline using a local LLM runtime (via Ollama).

5. Functional Requirements

The system shall:

Load structured weekly sales data from a local CSV file.

Aggregate data at the state-category level.

Compute a rolling 4-week moving average for each state-category pair.

Generate a one-week-ahead demand forecast.

Compute the risk score as defined above.

Rank all state-category combinations by descending risk score.

Return the Top 10 highest-risk combinations.

Display numerical values used in the risk computation.

Generate explanations that reference computed values.

Log tool execution steps for traceability.

Operate entirely offline without reliance on external cloud APIs.

6. Nonfunctional Requirements

Fully local execution (no external API calls).

Target runtime: complete Top 10 risk report generated within 60 seconds on a standard laptop (M4 MacBook Pro, 16GB RAM).

Reproducibility: deterministic forecasting where feasible.

Privacy: all data processing occurs locally.

Observability: system logs stored locally for inspection.

Maintainability: modular code structure separating forecasting, scoring, and explanation components.

7. Agentic Architecture (High-Level)
Components

User Interface: Streamlit-based local web application

Agent Orchestrator: Python module coordinating tool execution

Tools:

Forecasting tool

Risk scoring tool

Explanation generator

LLM Runtime: Ollama (local inference)

Dataset: Local CSV file

Agent Workflow

Interpret user request.

Execute forecasting tool.

Execute risk scoring tool.

Rank state-category pairs.

Select Top 10 highest-risk combinations.

Generate structured explanation.

Return formatted results to the user.

8. Evaluation Plan

The system will be evaluated using the following metrics:

Forecast Accuracy: Mean Absolute Percentage Error (MAPE).

Ranking Stability: Consistency of Top 10 results across adjacent weeks.

Runtime Performance: End-to-end execution time.

Scenario Testing: Controlled test cases using selected historical weeks to validate detection of abnormal spikes.

9. 9-Week Implementation Plan (High-Level)

Weeks 1–2: Finalize problem definition, select dataset, set up local LLM environment, scaffold repository structure.

Weeks 3–4: Implement forecasting tool and risk computation (vertical slice).

Weeks 5–6: Integrate agent orchestration and local UI.

Week 7: Implement logging, guardrails, and explanation validation.

Week 8: Conduct systematic evaluation and scenario testing.

Week 9: Finalize documentation, prepare demo script, and conduct end-to-end testing.
