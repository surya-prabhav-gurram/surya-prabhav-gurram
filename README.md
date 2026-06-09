<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a1a2e,100:0f3460&height=200&section=header&text=Surya%20Prabhav%20Gurram&fontSize=40&fontColor=58a6ff&fontAlignY=38&desc=AI%20Systems%20Engineer%20%7C%20ML%20Researcher%20%7C%20Blockchain%20Developer&descAlignY=58&descSize=16&descColor=8b949e&animation=fadeIn" width="100%" />

<img src="https://readme-typing-svg.demolab.com?font=Space+Mono&size=16&duration=2500&pause=800&color=58A6FF&center=true&vCenter=true&multiline=false&width=600&height=40&lines=Building+Intelligent+AI+Systems;Researching+Medical+Imaging+%26+Deep+Learning;Engineering+Blockchain+Infrastructure;Optimizing+Distributed+Database+Systems;Designing+Edge+AI+%26+IoT+Platforms" />

<br/>

[![Portfolio](https://img.shields.io/badge/Portfolio-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://suryaprabhavgurram.com)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/suryapgurram)
[![ResearchGate](https://img.shields.io/badge/ResearchGate-00CCBB?style=for-the-badge&logo=researchgate&logoColor=white)](https://www.researchgate.net/profile/Surya-Prabhav-Gurram)
[![Email](https://img.shields.io/badge/Email-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:suryaprabhavg@gmail.com)

<br/>

![Profile Views](https://komarev.com/ghpvc/?username=surya-prabhav-gurram&style=for-the-badge&color=0e75b6&label=PROFILE+VIEWS)

</div>

---

## About

Computer Science graduate student at the **University of Oklahoma** specializing in recommendation systems, ML infrastructure, multi-agent LLM systems, full-stack engineering, blockchain infrastructure, and medical AI.

---

## Research Domains

<div align="center">

| Recommendation Systems | AI Agents & LLMs | ML Infrastructure |
|:---:|:---:|:---:|
| Two-Tower · BERT4Rec · Cross-Attention · IPS Debiasing | Claude API · Multi-Agent · RAG · LLM-as-Judge | Airflow · Kafka · Redis · Feature Stores · Streaming |

| Blockchain | Medical AI | Database Systems |
|:---:|:---:|:---:|
| Ethereum · Smart Contracts · Merkle Trees | MRI Analysis · ECG · Tumor Detection | Query Optimization · Columnstore · Star Schema |

</div>

---

## Publications

### Credit Card Fraud Detection using Hidden Naive Bayes and Bayesian Belief Network
**IEEE 9th International Conference for Convergence in Technology (I2CT)**

Developed probabilistic machine learning systems using Hidden Naive Bayes (HNB) and Bayesian Belief Networks (BBN) for intelligent financial fraud detection and anomaly detection in highly imbalanced financial datasets.

### Technical Explanation
The system integrates probabilistic inference, Bayesian dependency modeling, transaction feature engineering, fraud likelihood scoring, and causal relationship analysis to identify suspicious financial transactions while minimizing false positives. The workflow includes preprocessing pipelines, imbalance handling, feature extraction, probabilistic learning, and comparative model evaluation for high-risk fraud monitoring systems.

<div align="center">

| Model | Accuracy |
|:---:|:---:|
| Hidden Naive Bayes | **86.87%** |
| Bayesian Belief Network | **89.59%** |

</div>

**Publication:**  
https://ieeexplore.ieee.org/document/10544328

---

### Enhancing Smart Farming Techniques through IoT and Machine Learning
**International Conference on Smart Systems and Green Energy Technologies**

Designed an IoT-enabled intelligent agriculture platform integrating predictive analytics, sensor-based monitoring, disease detection systems, and ML-driven crop management workflows.

### Technical Explanation
The platform combines IoT sensor pipelines, climate-aware prediction models, CNN-based disease classification systems, weather analytics, and machine learning recommendation engines to support precision agriculture and smart farming workflows.

**Publication:**  
https://www.riverpublishers.com/pdf/ebook/chapter/RP_9788770229647C14.pdf

---

## Projects

### UserLens — Adaptive Recommendation System
> Production-grade three-stage neural RecSys trained on MovieLens-25M (162,541 users, 32,720 items) — BERT4Rec pretrain → Two-Tower retrieval → Cross-Attention ranking with LLM re-ranking and continual learning.

- Stage 1: BERT4Rec Transformer (d=256, 2 layers, 4 heads, 10M params) via self-supervised masked item prediction
- Stage 2: Two-Tower model with InfoNCE contrastive loss (temperature=0.07) — Recall@10 = 0.51; HNSW indexing for sub-millisecond ANN retrieval
- Stage 3: Cross-Attention Ranker with IPS-weighted BPR loss for popularity debiasing — pairwise accuracy = 0.97
- Cold-start routing via sentence-transformer retrieval for users with fewer than 3 interactions
- LLM re-ranking: top-20 neural candidates passed to Claude with chain-of-thought reasoning
- LLM-as-judge eval framework scoring relevance, diversity, novelty, and serendipity
- Continual learning via incremental fine-tuning on new interaction batches

[![Live Demo](https://img.shields.io/badge/Live_Demo-000000?style=flat-square&logo=vercel&logoColor=white)](https://userlens-mu.vercel.app)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/userlens)
[![API Docs](https://img.shields.io/badge/API_Docs-005A8E?style=flat-square&logo=swagger&logoColor=white)](https://userlens-production.up.railway.app/docs)

`PyTorch` `BERT4Rec` `Two-Tower Retrieval` `Cross-Attention Ranking` `InfoNCE` `BPR + IPS` `Claude API` `FastAPI` `pgvector` `HNSW` `React` `MLflow` `Railway` `Vercel` `Continual Learning`

---

### SignalFlow — Production Real-Time Feature Store for RecSys
> Dual-pipeline feature store backing UserLens — handling the full feature lifecycle from raw interactions to sub-5ms online reads at inference time, fully deployed on Railway.

- Nightly Airflow DAG materializes windowed user features, IPS debiasing weights (√(1/propensity), normalized, clipped [0.01, 10]), and cold-start flags into partitioned Parquet — cutting compute from ~60s to under 1s
- Kafka + Faust streaming pipeline at 50 events/sec maintaining session sequences (LPUSH + LTRIM), recency decay (exp(−λ·t), half-life 2d), and sliding 24h popularity windows per event
- FastAPI feature server via pipelined Redis (HGETALL + LRANGE + GET) in one round trip — sub-5ms latency
- Same FeatureClient on write and read paths — eliminates training-serving skew entirely
- Partition metadata persisted to PostgreSQL surviving ephemeral filesystem redeploys

[![Live Dashboard](https://img.shields.io/badge/Live_Dashboard-000000?style=flat-square&logo=vercel&logoColor=white)](https://respectful-compassion-production.up.railway.app)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/signalflow)
[![API Docs](https://img.shields.io/badge/API_Docs-005A8E?style=flat-square&logo=swagger&logoColor=white)](https://signalflow-production-d56d.up.railway.app/docs)

`Apache Airflow` `Apache Kafka` `Faust` `Redis 7` `FastAPI` `Parquet / PyArrow` `PostgreSQL` `React` `Docker` `IPS Debiasing` `Cold-Start Routing` `Streaming Pipelines` `Feature Store` `Railway`

---

### Agentforce Field Intelligence Platform
> Production-grade multi-agent system built on Claude, GraphQL subscriptions, pgvector, and TypeScript — simulating what Salesforce deploys for Fortune 500 enterprise sales teams.

- Router → CRM / Research / Synthesis agent pipeline with parallel execution via `Promise.all`
- Real-time per-token streaming over GraphQL WebSocket subscriptions with 8 typed event types
- Human-in-the-loop approval flow for destructive CRM writes — 5-minute polling window
- pgvector RAG on conversation history with cosine similarity search
- Prompt versioning + LLM-as-judge eval runner with agent-specific eval cases
- Deployed on Railway: frontend (React + nginx), backend (Apollo Server), managed PostgreSQL

[![Live Demo](https://img.shields.io/badge/Live_Demo-000000?style=flat-square&logo=vercel&logoColor=white)](https://feisty-magic-production-6828.up.railway.app)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/agentforce-platform)

`Claude API` `Multi-Agent Systems` `GraphQL` `WebSockets` `Apollo Server` `React` `TypeScript` `PostgreSQL` `pgvector` `Prisma` `Railway`

---

### ServiceSense — AI Case Resolution Agent
> Agentforce-style AI customer support agent built on Salesforce Service Cloud, Claude API, pgvector, and React — fully automated case classification and response drafting in under 10 seconds.

- CaseTrigger + CaseAIHandler (Queueable + Database.AllowsCallouts) intercepts Cases on AFTER INSERT — 7 custom AI fields written back automatically
- Claude classifies cases by sentiment, urgency, category, and confidence
- pgvector knowledge base retrieval for category-matched draft response generation
- Human-in-the-loop: cases with confidence below 70% flagged as AI_Needs_Review and routed to Pending Review
- LLM-as-judge eval runner scoring across 5 dimensions — 79.7% avg quality score across 32 production evals (range 66–91%)
- CaseResolutionAction @InvocableMethod for native Agentforce flow integration

[![Live Demo](https://img.shields.io/badge/Live_Demo-000000?style=flat-square&logo=vercel&logoColor=white)](https://discerning-inspiration-production-7528.up.railway.app)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/ServiceSense)

`Salesforce Apex` `Claude API` `Node.js` `pgvector RAG` `React` `PostgreSQL` `Human-in-the-Loop` `LLM-as-Judge Evals` `Railway` `Named Credentials`

---

### RetailVault — SQL Server Edition
> Enterprise-grade retail data warehousing and analytics platform on Microsoft SQL Server 2022.

- Dual SQL Server 2022 databases: OLTP source + star schema warehouse
- All analytics and ETL in T-SQL stored procedures (`usp_RunEtlPipeline`, `usp_GetKpiSummary`, etc.)
- Nonclustered Columnstore Index on `fact_sales` for OLAP performance
- SCD Type 2 dimension tracking, window functions, TRY/CATCH transaction management
- React frontend + Spring Boot backend as thin JDBC wrapper

[![Live Demo](https://img.shields.io/badge/Live_Demo-000000?style=flat-square&logo=vercel&logoColor=white)](https://invigorating-inspiration-production-578b.up.railway.app/dashboard)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/retailvault_sqlserver)

`React` `Spring Boot` `SQL Server 2022` `T-SQL` `Stored Procedures` `Columnstore Index` `Star Schema` `SCD Type 2` `Azure SQL` `Docker`

---

### RetailVault Query Performance Lab
> DBA-level query performance tuning case study — 92.5% execution time reduction across 7 stored procedures.

- Reduced total execution time from 41s to 3s on 100k row Azure SQL warehouse
- Designed 7 targeted indexes (covering, filtered, composite) with `INCLUDE` columns
- Rewrote correlated subqueries as CTEs, replaced cursors with `OUTER APPLY`
- Applied `OPTION(RECOMPILE)` cutting inventory turnover query by 94.1% (11,618ms to 692ms)
- Queried `sys.dm_os_buffer_descriptors`, `sys.dm_exec_query_stats`, `sys.dm_os_wait_stats` for engine internals analysis

[![Live Dashboard](https://img.shields.io/badge/Live_Dashboard-000000?style=flat-square&logo=vercel&logoColor=white)](https://animated-frangipane-a7d565.netlify.app)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/retailvault-performance-lab)

`Azure SQL` `T-SQL` `Execution Plans` `Index Tuning` `DMVs` `CTEs` `OPTION(RECOMPILE)` `Filtered Index` `Buffer Pool` `Wait Statistics`

---

### StockBase — Enterprise Inventory Management System
> Full-stack inventory management platform with JWT auth, role-based access, and analytics dashboards.

- React + Spring Boot + PostgreSQL across Netlify, Render, Docker, and Neon
- JWT authentication, RBAC, RESTful API, Spring Security
- Recharts-based analytics, CSV export, inventory transaction auditing

[![Live Demo](https://img.shields.io/badge/Live_Demo-000000?style=flat-square&logo=vercel&logoColor=white)](https://fanciful-narwhal-46443d.netlify.app/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/stockbase)

`React` `Spring Boot` `PostgreSQL` `JWT` `Docker` `Render` `Netlify` `Neon`

---

### SoonerBoomer-ERC20-dApp
> Decentralized ERC-20 token claiming application with Merkle tree-based allowlist verification.

- Solidity smart contracts with OpenZeppelin ERC-20 standards
- Merkle tree allowlist verification — cryptographic eligibility without storing every wallet on-chain
- Hardhat deployment, Ethers.js blockchain interaction, MetaMask authentication

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/SoonerBoomer-ERC20-dApp)
[![Demo](https://img.shields.io/badge/Demo-FF0000?style=flat-square&logo=youtube&logoColor=white)](https://youtu.be/QgrpUbpq9ck)

`Solidity` `Ethereum` `OpenZeppelin` `Hardhat` `Ethers.js` `MetaMask`

---

### StressLab — On-Device HRV Stress Estimation
> iOS health analytics app estimating stress from Apple Watch ECG-derived RR intervals — fully on-device.

- Processes HRV signals on-device: RMSSD, SDNN, pNN50, SD1/SD2 features
- Privacy-preserving: no raw biometric data sent externally
- Interpretable heuristic scoring + personalized logistic regression stress estimation
- Structured for IoT telemetry and MQTT streaming workflows

[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/surya-prabhav-gurram/StressLab)
[![Demo](https://img.shields.io/badge/Demo-FF0000?style=flat-square&logo=youtube&logoColor=white)](https://youtu.be/pwPaB8Ufl2U)

`Swift` `SwiftUI` `HealthKit` `Edge ML` `MQTT` `Logistic Regression` `HRV` `IoT`

---

### AI-Powered PostgreSQL Index Optimization
> Intelligent database optimization framework using LLMs to recommend indexes for PostgreSQL workloads.

- TPC-H benchmarking workloads with automated before-after performance testing
- Query feature extraction: predicates, joins, grouping, ordering, cardinalities
- Considers storage overhead and write-performance tradeoffs like enterprise DBA tools

`PostgreSQL` `TPC-H` `LLMs` `Benchmarking` `Python`

---

### Brain Tumor Detection — MRI & Hyperspectral Imaging
> Deep learning system for automated brain tumor detection across MRI and hyperspectral imaging data.

- CNN-based classification and segmentation with normalization, denoising, augmentation
- MRI pipeline for structural tumor detection
- Hyperspectral component analyzes wavelength-based tissue signatures for healthy vs. abnormal tissue

`TensorFlow` `OpenCV` `CNN` `Medical Imaging` `Deep Learning`

---

### Smart Farming via IoT & Machine Learning
> IoT + ML system for crop health, yield prediction, and disease detection.

- Sensor-driven agricultural data + weather inputs + CNN plant disease detection
- Flask/Django prediction services trained on soil, climate, crop, and image datasets

[![Publication](https://img.shields.io/badge/Publication-005A8E?style=flat-square&logo=bookstack&logoColor=white)](https://www.riverpublishers.com/pdf/ebook/chapter/RP_9788770229647C14.pdf)

`TensorFlow` `Scikit-learn` `Flask` `Django` `CNN` `IoT`

---

### Credit Card Fraud Detection — HNB & BBN
> Probabilistic fraud detection combining Hidden Naive Bayes and Bayesian Belief Networks.

- Captures probabilistic feature relationships and causal dependencies
- Handles imbalanced financial datasets with precision/recall-aware evaluation

[![IEEE](https://img.shields.io/badge/IEEE-00629B?style=flat-square&logo=ieee&logoColor=white)](https://ieeexplore.ieee.org/document/10544328)

`Machine Learning` `Bayesian Models` `Anomaly Detection` `Python` `WEKA`

---

### ECG Cardiovascular Disease Detection
> CNN-based deep learning system for early detection of cardiovascular disease from ECG signals.

- QRS morphology extraction and rhythm-level pattern recognition
- ECG preprocessing, image/signal transformation, convolutional model training

`CNN` `ECG Analysis` `Healthcare AI` `TensorFlow` `Signal Processing`

---

## Technical Stack

<div align="center">

| Domain | Technologies |
|:---:|:---|
| **Languages** | Python · TypeScript · JavaScript · Java · SQL · Solidity · Swift |
| **AI / ML** | PyTorch · TensorFlow · Scikit-learn · Transformers · BERT4Rec · CNN · Bayesian Models · MLflow |
| **Recommendation Systems** | Two-Tower Retrieval · Cross-Attention Ranking · Sequence Learning · InfoNCE · BPR + IPS Debiasing · Cold-Start Routing · Continual Learning · HNSW / pgvector ANN |
| **ML Infrastructure** | Apache Airflow · Apache Kafka · Faust · Redis 7 · Feature Store Design · Parquet / PyArrow · Streaming Pipelines · Batch Pipelines · Recency Decay |
| **AI Agents & LLMs** | Claude API · Multi-Agent Orchestration · LLM Re-ranking · LLM-as-Judge Evals · Human-in-the-Loop · Prompt Versioning · pgvector RAG |
| **Full Stack** | React · Node.js · FastAPI · Spring Boot · Apollo Server · GraphQL · WebSockets · Prisma · JWT Auth · REST APIs |
| **Databases** | PostgreSQL · pgvector · SQL Server 2022 · T-SQL · MySQL · MongoDB · Star Schema · SCD Type 2 · ETL Pipelines |
| **Salesforce** | Apex · Service Cloud · Triggers · Queueable Jobs · @InvocableMethod · Named Credentials · Flow Builder |
| **Cloud & DevOps** | Docker · Railway · Vercel · AWS · Azure SQL · Render · Netlify · CI/CD · Git |
| **Blockchain** | Solidity · Hardhat · Ethers.js · OpenZeppelin · MetaMask · ERC-20 |
| **Mobile & IoT** | Swift · SwiftUI · HealthKit · Core Data · MQTT · Edge ML |

</div>

---

## Experience

**Student Supervisor — University of Oklahoma** `Aug 2024 — Present`

**Software Engineering Intern — Made For Few** `Aug 2023 — Nov 2023`

---

## Education

<div align="center">

| Degree | Institution | Duration |
|:---:|:---:|:---:|
| MS Computer Science | University of Oklahoma | 2024 to 2026 |
| BTech CS (AI & Machine Learning) | Vardhaman College of Engineering | 2020 to 2024 |

</div>

---

<div align="center">

```yaml
Building at the intersection of:
  AI · Scalable Infrastructure · Research · Real-World Impact
```

</div>
