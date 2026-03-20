# 🛡️ GigShield — Behavioral Parametric Insurance for India's Delivery Economy

> **Guidewire DEVTrails 2026 | AI-Powered Insurance for India's Gig Economy**
> Persona: Food Delivery Partners (Zomato)

---

## 🔥 What Makes GigShield Radically Different

Most teams will build: *"weather API triggers payout."*

**GigShield builds a Behavioral Digital Twin of every delivery partner.**

Instead of trusting GPS + weather data alone (which is trivially spoofable), GigShield constructs a continuously-updated **behavioral fingerprint** of each worker — their riding rhythm, delivery cadence, app interaction patterns, historical zone behavior, and passive device sensor streams. When an external disruption occurs, the system doesn't ask *"is it raining?"* — it asks *"does this worker's entire behavioral signature match someone who is genuinely stranded in rain?"*

This is not incremental fraud detection. This is a paradigm shift: **from location-based parametric triggers to behavior-verified parametric triggers.**

No competitor, no existing insurance company, and no other hackathon team will have this architecture.

---

## 📌 Table of Contents

1. [Problem Statement](#-problem-statement)
2. [Our Unique Solution](#-our-unique-solution--behavioral-digital-twin-insurance)
3. [Persona & Scenarios](#-persona--scenarios)
4. [Weekly Premium Model](#-weekly-premium-model)
5. [Parametric Triggers](#-parametric-triggers)
6. [AI/ML Architecture](#-aiml-architecture)
7. [Adversarial Defense & Anti-Spoofing Strategy](#-adversarial-defense--anti-spoofing-strategy)
8. [System Architecture](#-system-architecture)
9. [Tech Stack](#-tech-stack)
10. [Database Schema](#-database-schema)
11. [API Design](#-api-design)
12. [Development Roadmap (Phase-wise)](#-development-roadmap-phase-wise)
13. [UX Flow](#-ux-flow)
14. [Business Viability](#-business-viability)

---

## 🎯 Problem Statement

India has **15 million+ gig delivery workers** across Zomato, Swiggy, Amazon, Blinkit, and Zepto. These workers earn ₹500–₹1,200/day and operate in some of the most volatile environmental conditions in the world — extreme monsoons, heatwaves topping 45°C, sudden curfews, and major civic events that shut down entire city zones.

**When disruption hits, a delivery partner loses 100% of their income for that day with zero safety net.**

Existing solutions fail because:
- Traditional insurance is monthly, requires documentation, and is designed for salaried workers.
- Current parametric pilots use only weather API triggers — easily gamed and falsely triggered.
- No platform has connected a worker's **behavioral reality** to their claim validity.

---

## 💡 Our Unique Solution — Behavioral Digital Twin Insurance

### Core Innovation: The Behavioral Digital Twin (BDT)

A **Behavioral Digital Twin** is a real-time, ML-constructed model of what a "normal working day" looks like for a specific delivery partner — not just where they are, but *how* they behave.

The BDT is built from:

| Signal Type | Data Collected | Purpose |
|---|---|---|
| **Kinetic Signature** | Accelerometer + gyroscope (riding pattern, stop frequency) | Distinguish resting-at-home from riding-in-rain |
| **App Heartbeat** | Delivery app foreground/background state, ping frequency | Is the app actively being used for deliveries? |
| **Thermal Context** | Device CPU temperature + battery drain rate | Correlates with outdoor activity vs. indoor rest |
| **Zone-History Embedding** | Worker's historical geofences and routes over 30 days | Flags when claimed location is outside normal zone |
| **Peer Cluster Signal** | Anonymized behavior of 20 nearest workers in same zone | If 18/20 peers are also inactive → disruption confirmed |
| **Network Topology** | Cell tower transitions, WiFi SSID patterns | Home WiFi detected = not on a route |
| **Time-Series Deviation Score** | Today's behavior vs. 30-day baseline model | Core fraud signal: how much has behavior deviated? |

When a disruption is detected (rain API, AQI spike, curfew), the system cross-references the BDT to compute a **Genuine Disruption Probability (GDP) Score (0–100)**.

- GDP ≥ 75 → **Auto-Approved Payout** (no human needed)
- GDP 40–74 → **Soft Review** (worker notified, 1-tap confirmation, pays out in 2 hours)
- GDP < 40 → **Flagged** (held for review, worker shown reason, appeal possible)

This is the core loop that no competitor has.

---

## 👤 Persona & Scenarios

### Chosen Persona: Food Delivery Partners (Zomato / Swiggy)

**Why Food Delivery?**
Food delivery workers are the most time-pressure-sensitive persona — they work across lunch and dinner peaks, are the most likely to work during rain (orders surge during rain), and are therefore most vulnerable to income loss when conditions become unsafe. Their behavioral patterns are also the most consistent and ML-learnable.

---

### Scenario 1 — The Genuine Worker: Raju, Mumbai

> *Raju is a Zomato partner operating in Andheri East. At 3 PM on a Tuesday, Mumbai receives a Red Alert heavy rainfall warning. Raju, mid-route, is forced to stop under a flyover. His device shows: accelerometer is near-zero (stationary), app is still in foreground (he's checking for orders), cell tower data places him 400m from his usual route, and 17 of his 22 nearest peer cluster members are also stationary.*
>
> **GigShield GDP Score: 91** → Claim auto-approved. ₹320 credited to UPI within 4 minutes. Raju receives a notification: "Rain disruption detected. Your earnings are protected. ₹320 credited."

---

### Scenario 2 — The Fraudster: "Amit" (actually home in Goregaon)

> *Amit is part of a fraud ring. He installs a GPS spoofer, places his fake GPS in the Red Alert zone (Dharavi), and submits a claim. However: his accelerometer shows zero motion for 3 hours (he's on his couch), his home WiFi SSID is detected, his device CPU temp is low (no outdoor riding), his delivery app has been in the background for 90 minutes, and NONE of the peer cluster workers from his claimed zone match his behavior profile.*
>
> **GigShield GDP Score: 11** → Claim flagged and blocked. Fraud pattern logged. If this pattern occurs 3 times, account is suspended and referred for investigation.

---

### Scenario 3 — The Edge Case: Priya, genuine but network issues

> *Priya is delivering in Powai during a heatwave. AQI crosses 300. She has genuinely stopped working, but her phone's GPS is intermittent due to the storm. Her app shows no location pings for 40 minutes.*
>
> **GigShield approach:** GDP Score: 58 (uncertain). System sends a "1-tap check-in" notification: "We noticed you may be affected by today's severe heat alert. Tap to confirm you've stopped working." Priya taps. Score recalculates to 82. Payout approved in 2 hours with a message: "We gave you the benefit of the doubt — your protection matters to us."

This UX pattern — **"innocent until the data says otherwise"** — is what makes GigShield ethical, not just smart.

---

## 💰 Weekly Premium Model

### Philosophy: Dynamic Risk Pricing, Not Flat Premiums

GigShield uses a **Weekly Dynamic Premium** calculated every Monday morning for the upcoming week. This is NOT a fixed ₹X/week for all workers. It's personalized.

### Premium Formula

```
Weekly Premium = Base Rate × Zone Risk Multiplier × Behavioral Reliability Score × Seasonal Factor
```

| Variable | Description | Range |
|---|---|---|
| **Base Rate** | Minimum premium for food delivery persona | ₹25/week |
| **Zone Risk Multiplier** | Historical disruption frequency of worker's operating zone (pulled from 2-year weather + event data) | 0.8× – 2.5× |
| **Behavioral Reliability Score** | Inverse of past fraud flags; honest workers with clean history pay less | 0.7× – 1.3× |
| **Seasonal Factor** | Monsoon season (June–Sept): 1.4×; Winter fog (Dec–Jan): 1.2×; Summer (Apr–May): 1.3× | 1.0× – 1.4× |

### Example Premiums

| Worker Profile | Weekly Premium | Weekly Coverage |
|---|---|---|
| Veteran Zomato partner, 18 months, low-risk zone (Koramangala) | ₹29 | Up to ₹1,800 |
| New partner, high-risk zone (Kurla, Mumbai) | ₹58 | Up to ₹1,800 |
| Partner with 1 prior soft-flag (cleared) | ₹45 | Up to ₹1,800 |

### Coverage Structure

- **Tier 1 — Partial Disruption** (2–4 hours lost): 50% of average daily earnings
- **Tier 2 — Full Day Disruption** (4+ hours lost): 100% of average daily earnings (capped at ₹600/day)
- **Tier 3 — Multi-Day Event** (e.g., flood, 3-day curfew): Daily payouts, up to 5 consecutive days, reviewed by admin on day 3

**Average daily earnings** are computed from the worker's platform-reported delivery data over the past 30 days (or platform API / worker-inputted estimate for new users).

---

## ⚡ Parametric Triggers

These are the external event thresholds that, when crossed, **initiate** a GDP assessment (not directly a payout):

| Trigger | Source API | Threshold | Disruption Type |
|---|---|---|---|
| **Heavy Rainfall** | OpenWeatherMap / IMD API | > 15mm/hr OR Red/Orange Alert declared | Environmental |
| **Extreme Heat** | OpenWeatherMap | Temperature > 43°C for > 2 hrs | Environmental |
| **Severe AQI** | OpenAQ / CPCB API | AQI > 300 (Hazardous) in worker's city | Environmental |
| **Flood Zone Alert** | NDMA / State disaster APIs (mocked) | Worker's zone overlaps flood-declared area | Environmental |
| **Civic Curfew / Section 144** | News NLP monitor (Google News API + keyword triggers) | "Section 144", "curfew", city name match | Social |
| **Platform Downtime** | Zomato/Swiggy platform API heartbeat (mocked) | API returns 5xx > 3 min OR app status = "degraded" | Platform |

> **Key Principle:** A trigger does NOT automatically create a payout. It opens a GDP Assessment Window for all active workers in the affected zone. GDP score determines payout, not the trigger alone.

---

## 🤖 AI/ML Architecture

### Model 1: Behavioral Digital Twin Engine (Core)

**Type:** Per-worker time-series anomaly detection
**Algorithm:** Isolation Forest + LSTM Autoencoder (hybrid)
**Training Data:** 30-day rolling window of worker's own behavioral signals
**Output:** Real-time deviation score from their personal baseline

**Why LSTM Autoencoder?** The model learns to reconstruct "normal" behavior sequences. When behavior during a claimed disruption cannot be reconstructed (high reconstruction error), it's anomalous — likely fraud. When behavior IS consistent with "stranded in rain" patterns learned from legitimate historical claims, reconstruction error is low — likely genuine.

```
Input Vector (per 5-minute window):
[accelerometer_variance, app_state, gps_jump_score, 
 cell_tower_change_rate, wifi_ssid_match_home, 
 device_temp_delta, battery_drain_rate, 
 delivery_app_active_time_ratio]

Output: Reconstruction_Error → maps to Fraud_Probability
```

---

### Model 2: Peer Cluster Consensus Engine

**Type:** Spatial clustering + consensus voting
**Algorithm:** DBSCAN for real-time zone clustering + weighted majority vote
**Input:** Anonymized behavior snapshots of workers within 2km radius
**Output:** Zone-level Disruption Confidence Score (0–1)

This model answers: *"Are other workers in this zone also genuinely affected?"*
A single person claiming disruption is suspicious. 15/20 workers in the same zone all showing disruption-consistent behavior is strong corroborating evidence.

---

### Model 3: Dynamic Premium Pricing Model

**Type:** Supervised regression
**Algorithm:** XGBoost Regressor
**Features:** Zone historical data, worker tenure, seasonal calendar, claim history, behavioral score
**Output:** Personalized weekly premium in ₹

---

### Model 4: Fraud Ring Detection (Graph Neural Network)

**Type:** Graph-based anomaly detection
**Algorithm:** GraphSAGE (Graph Sample and Aggregate)
**Graph Construction:** Workers = nodes; edges = shared Telegram-like group signals (similar device, same IP subnet, correlated claim timing)
**Output:** Fraud Ring Probability Score per cluster of workers

**This is the layer that catches coordinated fraud rings**, not just individual bad actors. When 20 workers all submit claims within 3 minutes of each other from the same zone, with all their devices showing the same GPS-spoofing artifact (unrealistic precision, no cell-tower transitions), the GNN flags the entire cluster.

---

### Model 5: News/Event NLP Monitor

**Type:** Real-time text classification
**Algorithm:** Fine-tuned DistilBERT (lightweight, runs on edge/server)
**Input:** Google News RSS feed + Twitter API streaming (filtered by city + keywords)
**Output:** Civic Disruption Alert with city/zone tag and confidence score

---

## 🛡️ Adversarial Defense & Anti-Spoofing Strategy

> *This section directly addresses the Phase 1 Market Crash scenario: 500 delivery workers using GPS spoofing apps to fake their location in a Red Alert zone while resting at home.*

---

### The Differentiation: How We Tell the Genuine from the Fake

Simple GPS verification checks one thing: "Is the worker's reported location inside the disruption zone?" GPS spoofers trivially defeat this.

GigShield's BDT verifies **11 independent behavioral signals simultaneously**. Spoofing GPS is easy. Spoofing your accelerometer, your home WiFi detection, your device thermals, your app foreground state, your peer cluster's consensus, AND your personal 30-day behavioral baseline — all at the same time — is computationally and logistically impossible at scale.

**The core principle: Make the cost of spoofing higher than the value of the payout.**

A spoofer would need to:
1. Fake GPS (easy — they're already doing this)
2. Shake their phone in rain-like patterns for 4 hours (possible, but detected by pattern mismatch)
3. Disconnect from home WiFi and disable known SSID detection (detectable absence pattern)
4. Spoof accelerometer data in a way that matches their 30-day historical riding profile (very hard)
5. Coordinate with 15+ nearby workers to all show consistent fake behavior (detectable as coordinated cluster anomaly)

**No fraudster can realistically beat all 11 signals simultaneously.**

---

### The Data: Beyond GPS — What We Actually Analyze

| Signal | What Genuine Workers Show | What GPS Spoofers Show |
|---|---|---|
| **Accelerometer Variance** | High variance (riding/walking in rain) OR near-zero with occasional shuffle (sheltering) | Near-zero flat (sitting on couch) |
| **GPS Jump Score** | Smooth, physics-consistent movement OR stationary at a non-home location | Teleportation artifacts, unrealistic precision (0.0001° accuracy = app artifact) |
| **Cell Tower Transitions** | Tower transitions consistent with movement, OR single tower (stationary in field) | Home tower constant — location never actually changed |
| **WiFi SSID Scan** | No known SSIDs (outdoor) OR no WiFi detected | Home SSID present in scan log |
| **Device Thermal Delta** | Elevated (outdoor riding in heat/rain) OR normal (sheltering) | Low (indoor, AC, couch) |
| **App Foreground Time** | Delivery app active, checking for orders | App backgrounded, user is on YouTube/gaming |
| **Peer Consensus** | Zone-mates also showing disruption-consistent patterns | Zone-mates mostly working normally (fraud ring didn't recruit everyone) |
| **Claim Timing Pattern** | Claim submitted after genuine disruption window | Claim submitted within 90 seconds of trigger firing (bot-like speed) |
| **Historical Zone Match** | Claimed location is within worker's normal operating zone | Claimed location is 15km from any historical route |
| **Behavioral Sequence** | Behavior sequence matches past genuine disruption events | Behavior sequence has no prior precedent in worker's history |
| **Device ID Consistency** | Single device, consistent hardware fingerprint | Multiple claims from same hardware fingerprint across different accounts (ring detection) |

---

### Coordinated Fraud Ring Detection

The Phase 1 scenario involves **500 workers coordinating via Telegram**. This coordination leaves detectable fingerprints:

**Signal 1 — Temporal Clustering:** Fraud rings receive the trigger alert on Telegram and all submit claims within a narrow time window (e.g., 300 claims in 4 minutes). Genuine workers discover disruption organically — their claim times are spread over 30–90 minutes. We flag any zone where claim submission rate exceeds 3σ above the historical norm for that zone.

**Signal 2 — Device Subnet Correlation:** Workers organizing via the same Telegram group often share the same mobile data subnet or have used the same WiFi hotspot. We hash and cross-reference IP subnet data (not storing IPs, just subnet hashes) to detect unusual co-location patterns.

**Signal 3 — GPS Spoofing App Artifacts:** Popular GPS spoofing apps (Fake GPS, Floater) leave detectable artifacts: location precision is unrealistically high (real GPS has natural ±5–10m noise; spoofed GPS often shows 0.00001° precision), altitude is fixed at sea level, location updates arrive at perfectly uniform intervals (real GPS has jitter). We run a spoofing artifact classifier on every GPS stream.

**Signal 4 — Graph Community Detection:** We build a real-time graph where workers who have: (a) submitted claims in the same time window, (b) operate in the same declared zone, and (c) share 2+ anomalous behavioral signals, are connected. GraphSAGE identifies communities in this graph. A community of 20+ workers with high internal similarity and high individual anomaly scores = a fraud ring.

---

### The UX Balance: Protecting Honest Workers

The greatest risk in any fraud system is **false positives** — blocking a genuine worker's claim because they had a weak GPS signal in bad weather. This is both unethical and destroys trust.

**GigShield's Three-Tier Response:**

**Tier 1: Auto-Approve (GDP ≥ 75)**
No friction. Worker gets a push notification: "Disruption detected in your area. ₹X protected." Money arrives in 4 minutes via UPI. Zero clicks required from the worker.

**Tier 2: Soft Confirmation (GDP 40–74)**
System sends a single gentle notification: *"We noticed you may be affected by [event]. Tap to confirm you've paused work."* One tap. No forms, no photos, no documentation. The act of confirmation (combined with device signals at that moment) recalculates GDP. If it clears 65, payout in 2 hours. This handles the "genuine but ambiguous signal" case (like Priya in Scenario 3).

**Tier 3: Held for Review (GDP < 40)**
Worker is notified: *"Your claim is under review. We'll update you within 4 hours."* A human reviewer sees the behavioral anomaly summary (not raw data, just flags). Worker can submit a 30-second voice note explaining their situation (optional). If review clears them, payout is released with a ₹50 "sorry for the wait" bonus to acknowledge the friction.

**Appeals Process:**
Every blocked claim has a one-tap appeal. Appeals are reviewed within 24 hours. If a worker is blocked 3 times and all 3 are reversed on appeal, their Behavioral Reliability Score is upgraded and they receive a ₹100 credit.

**The Principle:** We treat every flagged worker as innocent until proven otherwise. The burden of proof is on our system, not on the worker.

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         GigShield Platform                                  │
├──────────────────────────┬──────────────────────────────────────────────────┤
│    WORKER MOBILE APP     │          ADMIN / INSURER DASHBOARD               │
│  (React Native / PWA)    │           (React Web App)                        │
│                          │                                                   │
│  • Passive sensor SDK    │  • Real-time disruption map                      │
│  • Policy dashboard      │  • Fraud ring visualization (graph)              │
│  • Claim status          │  • Loss ratio analytics                          │
│  • 1-tap confirmation    │  • Weekly payout ledger                          │
│  • UPI payout display    │  • Premium pricing override                      │
└──────────┬───────────────┴──────────────┬──────────────────────────────────┘
           │ HTTPS / WebSocket             │ HTTPS
           ▼                               ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         API Gateway (Node.js / Express)                     │
│                         Rate Limiting · JWT Auth · HTTPS                    │
└──────┬──────────┬──────────┬────────────┬───────────────────────────────────┘
       │          │          │            │
       ▼          ▼          ▼            ▼
┌──────────┐ ┌─────────┐ ┌──────────┐ ┌──────────────────────┐
│  Worker  │ │  Policy │ │  Claims  │ │  Fraud Detection     │
│  Service │ │ Service │ │ Service  │ │  Service             │
│(Node.js) │ │(Node.js)│ │(Node.js) │ │  (Python FastAPI)    │
└────┬─────┘ └────┬────┘ └────┬─────┘ └──────────┬───────────┘
     │             │           │                   │
     └─────────────┴─────┬─────┘                   │
                         ▼                         ▼
              ┌──────────────────┐     ┌────────────────────────┐
              │  PostgreSQL DB   │     │   ML Inference Engine  │
              │  (Primary Store) │     │   (Python + FastAPI)   │
              │                  │     │                        │
              │  • Workers       │     │  • BDT LSTM Autoenc.   │
              │  • Policies      │     │  • Peer Cluster DBSCAN │
              │  • Claims        │     │  • GraphSAGE (rings)   │
              │  • Payouts       │     │  • XGBoost Premium     │
              │  • BDT Profiles  │     │  • DistilBERT NLP      │
              └──────────────────┘     └───────────┬────────────┘
                         ▲                         │
                         │              ┌──────────▼──────────┐
              ┌──────────┴───┐          │  Redis Cache        │
              │  Supabase    │          │  (GDP scores,       │
              │  (Auth +     │          │   active triggers,  │
              │   Realtime)  │          │   session state)    │
              └──────────────┘          └─────────────────────┘
                                                   │
                         ┌─────────────────────────┘
                         ▼
              ┌──────────────────────────────────────────────┐
              │          External API Integrations           │
              │                                              │
              │  OpenWeatherMap API → Rainfall / Temp        │
              │  OpenAQ API → AQI data                       │
              │  NDMA Mock API → Flood alerts                │
              │  Google News API → Civic event NLP           │
              │  Razorpay Sandbox → UPI payouts (mock)       │
              │  Zomato/Swiggy Mock API → Delivery data      │
              └──────────────────────────────────────────────┘
```

---

### Data Flow: A Claim Being Processed

```
[External Trigger Fires] (e.g., OpenWeatherMap: Red Alert, Mumbai)
         │
         ▼
[Trigger Service identifies all workers in affected zone]
         │
         ▼
[For each worker: Pull last 60-min behavioral telemetry from Redis]
         │
         ▼
[BDT Engine runs LSTM reconstruction → Fraud Probability]
         │
         ▼
[Peer Cluster Engine runs DBSCAN on zone → Zone Confidence Score]
         │
         ▼
[Combine scores → GDP Score computed]
         │
    ┌────┴────┐
    │         │
   ≥75       40-74      <40
    │         │           │
    ▼         ▼           ▼
[Auto     [1-tap      [Hold for
 Payout]   confirm]    Review]
    │         │           │
    └────┬────┘           │
         ▼                ▼
[Razorpay Sandbox    [Human Review
 UPI Transfer]        Queue + Appeal]
         │
         ▼
[Worker Push Notification + DB record update]
```

---

## 🛠️ Tech Stack

### Frontend
| Layer | Technology | Reason |
|---|---|---|
| Worker App | React Native (Expo) | Cross-platform (Android primary for Indian gig workers) |
| Admin Dashboard | React + Vite + TailwindCSS | Fast, modern, component-driven |
| State Management | Zustand | Lightweight, no boilerplate |
| Real-time UI | Supabase Realtime subscriptions | Push updates without polling |
| Charts / Analytics | Recharts + D3.js | Flexible data visualization |

### Backend
| Layer | Technology | Reason |
|---|---|---|
| API Server | Node.js + Express.js | Fast HTTP layer, familiar ecosystem |
| ML/AI Services | Python + FastAPI | PyTorch, scikit-learn, transformers ecosystem |
| Auth | Supabase Auth (JWT) | Built-in OTP via phone — ideal for gig workers |
| Database | PostgreSQL via Supabase | Relational integrity for financial data |
| Cache | Redis (Upstash) | Sub-millisecond GDP score reads, session data |
| Message Queue | BullMQ (Redis-based) | Async claim processing without blocking API |
| Scheduler | node-cron | Weekly premium recalculation every Monday 5 AM |

### AI / ML
| Model | Framework | Purpose |
|---|---|---|
| BDT Anomaly Engine | PyTorch (LSTM Autoencoder) | Behavioral fingerprint reconstruction |
| Isolation Forest | scikit-learn | Fast first-pass anomaly filtering |
| Peer Cluster Engine | scikit-learn (DBSCAN) | Zone-level consensus scoring |
| Premium Pricing | XGBoost | Dynamic weekly premium regression |
| Fraud Ring Detection | PyTorch Geometric (GraphSAGE) | Graph-based ring identification |
| News NLP Monitor | HuggingFace Transformers (DistilBERT) | Civic event classification |
| GPS Artifact Classifier | scikit-learn (Random Forest) | Spoofing app fingerprint detection |

### Infrastructure & DevOps
| Tool | Purpose |
|---|---|
| Supabase | Postgres + Auth + Realtime + Storage |
| Railway.app | Backend Node.js + Python service hosting |
| Vercel | React Admin Dashboard hosting |
| GitHub Actions | CI/CD pipeline |
| Docker | ML service containerization |

### External APIs
| API | Usage | Tier |
|---|---|---|
| OpenWeatherMap | Rainfall, temperature, alerts | Free tier |
| OpenAQ | AQI data India | Free public API |
| Google News RSS | Civic event monitoring | Free |
| Razorpay Sandbox | Mock UPI payouts | Test mode (free) |
| NDMA (mocked) | Flood zone alerts | Mock JSON server |

---

## 🗄️ Database Schema

### Core Tables (PostgreSQL)

```sql
-- Workers / Delivery Partners
workers (
  id UUID PRIMARY KEY,
  phone VARCHAR(15) UNIQUE,  -- Primary identity (OTP login)
  name VARCHAR(100),
  platform VARCHAR(20),       -- 'zomato' | 'swiggy'
  operating_zone_id UUID,
  monthly_avg_earnings DECIMAL(10,2),
  behavioral_reliability_score DECIMAL(3,2) DEFAULT 1.0,
  created_at TIMESTAMP
)

-- Policies (one active policy per worker at a time)
policies (
  id UUID PRIMARY KEY,
  worker_id UUID REFERENCES workers,
  week_start DATE,
  week_end DATE,
  premium_amount DECIMAL(8,2),
  coverage_tier INT,           -- 1 | 2 | 3
  max_weekly_payout DECIMAL(10,2),
  status VARCHAR(20),          -- 'active' | 'expired' | 'suspended'
  zone_risk_multiplier DECIMAL(4,2),
  seasonal_factor DECIMAL(4,2),
  created_at TIMESTAMP
)

-- Claims
claims (
  id UUID PRIMARY KEY,
  worker_id UUID REFERENCES workers,
  policy_id UUID REFERENCES policies,
  trigger_event_id UUID REFERENCES disruption_events,
  claimed_at TIMESTAMP,
  gdp_score DECIMAL(5,2),
  status VARCHAR(20),          -- 'auto_approved' | 'pending_confirm' | 'held' | 'paid' | 'rejected' | 'appealed'
  payout_amount DECIMAL(10,2),
  disruption_hours DECIMAL(4,1),
  fraud_flags JSONB,           -- Array of triggered fraud signals
  reviewed_by UUID,            -- NULL if auto-approved
  payout_reference VARCHAR(100)
)

-- Behavioral Telemetry (time-series, high volume)
worker_telemetry (
  id BIGSERIAL,
  worker_id UUID,
  recorded_at TIMESTAMP,
  accel_variance DECIMAL(6,4),
  gps_jump_score DECIMAL(5,3),
  app_foreground BOOLEAN,
  wifi_home_detected BOOLEAN,
  device_temp_delta DECIMAL(5,2),
  cell_tower_id VARCHAR(20),
  battery_drain_rate DECIMAL(5,3)
)
-- Partitioned by week, retained 90 days

-- Disruption Events (external triggers)
disruption_events (
  id UUID PRIMARY KEY,
  event_type VARCHAR(30),      -- 'rainfall' | 'heat' | 'aqi' | 'curfew' | 'flood' | 'platform_down'
  severity VARCHAR(10),        -- 'orange' | 'red'
  affected_zone_ids UUID[],
  started_at TIMESTAMP,
  ended_at TIMESTAMP,
  source_api VARCHAR(50),
  raw_trigger_data JSONB
)

-- BDT Profiles (ML model state per worker)
bdt_profiles (
  worker_id UUID PRIMARY KEY REFERENCES workers,
  model_version VARCHAR(20),
  baseline_vectors JSONB,      -- Compressed 30-day baseline
  last_trained_at TIMESTAMP,
  reconstruction_threshold DECIMAL(6,4)
)

-- Fraud Ring Log
fraud_rings (
  id UUID PRIMARY KEY,
  detected_at TIMESTAMP,
  member_worker_ids UUID[],
  ring_probability DECIMAL(5,3),
  trigger_event_id UUID,
  status VARCHAR(20)           -- 'investigating' | 'confirmed' | 'cleared'
)
```

---

## 📡 API Design

### Key Endpoints

```
POST   /api/auth/otp/send          # Send OTP to worker phone
POST   /api/auth/otp/verify        # Verify OTP, return JWT

POST   /api/workers/onboard        # Worker registration + initial BDT setup
GET    /api/workers/:id/profile    # Worker profile + active policy

POST   /api/policies/subscribe     # Subscribe to weekly policy (triggers premium calc)
GET    /api/policies/:id           # Policy details

POST   /api/telemetry/batch        # Mobile SDK batches sensor data every 5 min
GET    /api/telemetry/:workerId/latest  # Latest telemetry for worker

GET    /api/disruptions/active     # Active disruption events in worker's zone
POST   /api/claims/initiate        # Triggered by disruption engine (internal)
POST   /api/claims/:id/confirm     # Worker 1-tap confirmation
POST   /api/claims/:id/appeal      # Worker appeals rejected claim

GET    /api/admin/dashboard        # Insurer analytics summary
GET    /api/admin/fraud-rings      # Active fraud ring detections
GET    /api/admin/claims/review    # Claims queue for human review
```

---

## 📅 Development Roadmap (Phase-wise)

### Phase 1 (March 4–20): Ideation & Foundation ✅
- [x] Problem research and persona definition
- [x] BDT architecture design
- [x] Anti-spoofing strategy (this README section)
- [x] Database schema design
- [x] Tech stack finalization
- [x] Weekly premium model design
- [ ] Mockup wireframes (Figma)
- [ ] Repository setup with folder structure

### Phase 2 (March 21–April 4): Automation & Protection
**Week 3 Goals:**
- [ ] Worker onboarding flow (React Native app, OTP auth via Supabase)
- [ ] PostgreSQL schema migration via Supabase
- [ ] OpenWeatherMap + OpenAQ integration (live triggers)
- [ ] Baseline telemetry SDK (React Native background sensors)
- [ ] XGBoost premium pricing model (trained on synthetic data)

**Week 4 Goals:**
- [ ] LSTM Autoencoder BDT training pipeline (Python, PyTorch)
- [ ] Claims service + GDP score computation
- [ ] Razorpay Sandbox UPI payout integration
- [ ] Admin dashboard Phase 1 (active disruptions, claim queue)
- [ ] 3 automated disruption trigger scenarios end-to-end

### Phase 3 (April 5–17): Scale & Optimize
**Week 5 Goals:**
- [ ] GraphSAGE fraud ring detection model
- [ ] GPS spoofing artifact classifier
- [ ] Peer cluster consensus engine (DBSCAN, real-time)
- [ ] News NLP monitor (DistilBERT civic event classifier)
- [ ] Full appeals UX flow

**Week 6 Goals:**
- [ ] Intelligent worker + insurer dashboard (full analytics)
- [ ] End-to-end simulated disruption demo (fake rainstorm scenario)
- [ ] Performance optimization + edge case handling
- [ ] 5-minute demo video recording
- [ ] Final pitch deck (PDF)

---

## 🎨 UX Flow

### Worker Onboarding (< 3 minutes)

```
1. Enter phone number → OTP verification (30 sec)
2. Select delivery platform (Zomato / Swiggy) + city
3. Confirm average weekly earnings (pre-filled from platform data OR manual)
4. Allow sensor permissions (accelerometer, location) — explained with value prop
5. View personalized weekly premium → Subscribe (UPI AutoPay)
6. Done. BDT starts training in background silently.
```

### Weekly Experience (Zero Touch, Ideally)

```
Monday: "Your policy for this week is active. Premium: ₹37 deducted."
Working normally: App runs silently, no interruption.
Disruption occurs: Automatic detection → Auto-payout OR gentle 1-tap.
Worker sees: "₹280 credited to UPI. Stay safe."
Friday: Weekly summary: "You were protected 2× this week."
```

### Admin Insurer Dashboard

```
• Live map: Zone-wise active disruptions (color-coded severity)
• Real-time counter: Claims processed / pending / flagged this week
• Fraud ring graph: Visual network of flagged coordinated actors
• Financial overview: Premium collected vs. payouts vs. projected loss ratio
• Predictive panel: Next week's likely high-risk zones (ML forecast)
```

---

## 📊 Business Viability

### Unit Economics (Per Worker, Per Week)

| Metric | Value |
|---|---|
| Average weekly premium | ₹42 |
| Average claim payout | ₹340 |
| Expected disruption frequency | ~0.8 qualifying events/worker/month |
| Expected monthly claim cost | ₹272/worker |
| Expected monthly premium | ₹168/worker |
| **Platform margin (reinsurance model)** | **Covered by reinsurance pool + 15% margin on premium** |

### Why This Is Viable
- Low premium-to-payout ratio is standard in parametric insurance (no assessment cost)
- Fraud detection directly protects loss ratio (estimated 12–18% reduction in fraudulent claims vs. GPS-only systems)
- At scale (100,000 workers), premium pool per month = ₹1.68 Cr → sustainable loss ratio at 65–70%
- B2B2C model: Partner with Zomato/Swiggy to bundle GigShield as a worker benefit (premium deducted from weekly earnings automatically — zero friction signup)

---

## 🔒 Privacy & Compliance

- All telemetry data is **stored as processed features only**, not raw GPS tracks
- Workers explicitly consent to behavioral monitoring during onboarding, with a clear value explanation
- Data is retained for 90 days only (rolling)
- DPDP Act 2023 (India's Data Protection Act) compliant: no biometric data, purpose limitation enforced
- Workers can download and delete their data at any time from the app

---

## 👥 Team

> *[Team name and member details to be added]*

---

## 📎 Links

- **GitHub Repository:** *[link]*
- **Demo Video (Phase 1):** *[link]*
- **Figma Wireframes:** *[link]*

---

*Built with ❤️ for India's 15 million gig workers. GigShield — because the road doesn't stop for rain, but your livelihood shouldn't have to.*
