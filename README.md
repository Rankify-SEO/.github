<div align="center">
<!-- HERO BANNER — replace with actual screenshot at 1400×560 -->
<img src="https://your-cdn.com/rankify-hero-banner.png" alt="Rankify — Enterprise SEO Platform" width="100%" />
<br />
<img src="https://your-cdn.com/rankify-logo.png" alt="Rankify Logo" height="72" />
<h1>Rankify</h1>
<p><strong>The enterprise SEO intelligence platform that turns raw crawl data into ranked, actionable clarity — at cloud scale.</strong></p>
<!-- Badges -->
<p>
  <img alt="Build — Azure Static Web Apps" src="https://img.shields.io/github/actions/workflow/status/djtsingh/Rankify/azure-static-web-apps.yml?label=frontend%20build\&style=flat-square\&color=00e5d1" />
  <img alt="API Build" src="https://img.shields.io/github/actions/workflow/status/djtsingh/Rankify/main\_rankify-v1-src.yml?label=api%20build\&style=flat-square\&color=00e5d1" />
  <img alt="Worker Build" src="https://img.shields.io/github/actions/workflow/status/djtsingh/Rankify/deploy-python-worker.yml?label=worker%20build\&style=flat-square\&color=00e5d1" />
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-73%25-3178C6?style=flat-square\&logo=typescript\&logoColor=white" />
  <img alt="Python" src="https://img.shields.io/badge/Python-23%25-3776AB?style=flat-square\&logo=python\&logoColor=white" />
  <img alt="License" src="https://img.shields.io/badge/license-Proprietary-ff6b6b?style=flat-square" />
  <img alt="Platform" src="https://img.shields.io/badge/cloud-Azure-0078D4?style=flat-square\&logo=microsoftazure\&logoColor=white" />
  <img alt="Live" src="https://img.shields.io/website?url=https%3A%2F%2Fwww.rankify.page\&style=flat-square\&label=rankify.page\&color=00e5d1" />
</p>
<p>
  <a href="https://www.rankify.page"><strong>🌐 Live Platform</strong></a> ·
  <a href="#-quick-start"><strong>⚡ Quick Start</strong></a> ·
  <a href="#-architecture"><strong>🏗 Architecture</strong></a> ·
  <a href="#-roadmap"><strong>🗺 Roadmap</strong></a> ·
  <a href="#-contributing"><strong>🤝 Contribute</strong></a>
</p>
---
</div>
✦ Executive Summary
> \*\*Rankify is the SEO platform that doesn't lie to you.\*\* While every other tool hands you a vanity score, Rankify runs a comprehensive, multi-signal analysis — Core Web Vitals via Google PageSpeed API, TF-IDF keyword extraction, Flesch-Kincaid readability, security header auditing, and full on-page intelligence — then delivers it in one coherent dashboard you can share with a link. It's serverless, auto-scaling, and built for teams who ship fast and rank higher.
---
✦ The Problem We're Solving
The SEO tooling landscape is broken. You have:
Agency tools locked behind $299/month paywalls with dashboards that take 45 minutes to load
Free checkers that flag 3 issues and call it done
Dev-focused CLI tools with zero UX and no shareable output
Fragmented workflows — one tool for Core Web Vitals, another for keyword density, another for security headers
Rankify unifies all of it. One URL, one scan, one dashboard — and a shareable link your client can open without a login.
---
✦ Key Features
🔍 Deep SEO Audit Engine
Category	What Rankify Checks
Core Web Vitals	LCP, FID, CLS, INP, TTFB, FCP via Google PageSpeed Insights API
Technical SEO	HTTPS/SSL, robots.txt, XML sitemap, canonical URLs, mobile viewport, Schema.org structured data
On-Page Intelligence	Title tags, meta descriptions, H1–H6 hierarchy, image alt text, internal/external link analysis
Content Analysis	TF-IDF keyword extraction (scikit-learn), word count, Flesch-Kincaid readability (textstat)
Security Headers	CSP, X-Frame-Options, HSTS, mixed content detection
Social SEO	Open Graph tags, Twitter Cards
📊 Beautiful, Shareable Reports
Interactive score gauges with animated radial visualizations
Tabbed dashboard — navigate between Technical, On-Page, Content, and Social audits
Issue prioritization — critical blockers surface first, not buried in a wall of text
Export to PDF / CSV — one-click report generation for clients
Shareable link — no login required for recipients
Print-optimized layout — for the rare humans who still print things
⚡ Async at Scale
Scans are handled by a dedicated Python worker on Azure Container Apps — decoupled from the API via Azure Storage Queue. The worker auto-scales from 0 to 3 replicas based on queue depth, meaning you pay nothing during idle periods and never miss a job under load.
🎨 UI That Doesn't Look Like Every Other Dev Tool
Dark theme, cyan `#00e5d1` / coral `#ff6b6b` accent palette — intentional, not an afterthought
Smooth `anime.js` animations on gauges, card reveals, and loading states
Fully responsive — audit your competitor's site from your phone
Toast notifications, progress visualization, micro-interactions throughout
---
✦ Tech Stack
<div align="center">
Frontend
Technology	Version	Role
Next.js	15	React framework, App Router, static export
TypeScript	5.x	End-to-end type safety
Tailwind CSS	3.x	Utility-first styling
anime.js	latest	Animations & micro-interactions
Lucide React	latest	Icon system
API Layer
Technology	Version	Role
Azure Functions	Node.js 22	Serverless REST API
Prisma ORM	5.x	Database abstraction layer
PostgreSQL	Azure Flexible Server	Persistent scan storage
Azure Storage Queue	—	Async job dispatch
Analysis Engine
Technology	Version	Role
Python	3.11	SEO extraction runtime
BeautifulSoup4	latest	HTML parsing
scikit-learn	1.4.0	TF-IDF keyword extraction
textstat	0.7.3	Flesch-Kincaid readability
NLTK	3.8.1	NLP preprocessing
Google PageSpeed API	v5	Real Core Web Vitals
Infrastructure
Service	Role
Azure Static Web Apps	Frontend hosting + edge CDN
Azure Functions App	API hosting
Azure Container Apps	Python worker — auto-scales 0–3 replicas
Azure PostgreSQL Flexible Server	Primary database
Azure Storage Queue	`scan-jobs` job queue
Azure Container Registry	Private Docker image registry
GitHub Actions	CI/CD — 3 independent pipelines
Application Insights	Distributed tracing & monitoring
</div>
---
✦ Architecture
Rankify is built as a proper event-driven, serverless system — not a monolith wearing a serverless costume.
```
┌──────────────────────────────────────────────────────────────────────┐
│                     RANKIFY SYSTEM ARCHITECTURE                      │
└──────────────────────────────────────────────────────────────────────┘

  User Browser
      │
      │  HTTPS
      ▼
┌─────────────────────────────────────┐
│     Azure Static Web Apps (CDN)     │
│     Next.js 15 — Static Export      │
│     https://www.rankify.page        │
└───────────────┬─────────────────────┘
                │
                │  REST API calls
                ▼
┌─────────────────────────────────────┐
│       Azure Functions App           │
│  POST /api/v1/scans → enqueue job   │
│  GET  /api/v1/scans/:id → poll      │
└──────┬──────────────────────┬───────┘
       │                      │
  enqueue                  read/write
       ▼                      ▼
┌──────────────┐     ┌────────────────────┐
│  Azure Queue │     │  Azure PostgreSQL  │
│  (scan-jobs) │     │  (rankify-v1-data) │
└──────┬───────┘     └────────────────────┘
       │                      ▲
  poll (FIFO)                 │ write results
       ▼                      │
┌──────────────────────────────────────┐
│     Azure Container Apps             │
│     Python 3.11 SEO Worker           │
│                                      │
│  ┌──────────────────────────────┐    │
│  │  ComprehensiveMetricsExtract │    │
│  │  ├── text\_analyzer.py        │    │
│  │  │   └── TF-IDF, readability │    │
│  │  ├── security\_headers.py     │    │
│  │  │   └── CSP, HSTS, X-Frame  │    │
│  │  └── pagespeed\_insights.py   │    │
│  │      └── Google CWV API      │    │
│  └──────────────────────────────┘    │
│                                      │
│  Auto-scales: 0 → 3 replicas        │
└──────────────────────────────────────┘
```
Why This Architecture?
Concern	Decision	Why
Scan latency	Async queue + polling	Scans can take 10–30s; synchronous would timeout
Cost at zero load	Scale-to-zero Container Apps	Pay nothing when no scans are running
Frontend hosting	Static export on Azure SWA	Global CDN, near-zero cost, no server to manage
Database	PostgreSQL via Prisma	Full relational model for scan history and user data
Decoupled analysis	Python worker in Docker	scikit-learn / textstat ecosystem, isolated from Node.js
---
✦ Project Structure
```
Rankify/
│
├── 📂 apps/web/                         # Next.js 15 Frontend
│   └── src/
│       ├── app/
│       │   ├── page.tsx                 # Landing page
│       │   └── website-audit/
│       │       └── results/\[scanId]/    # Dynamic results page
│       ├── components/
│       │   ├── audit/                   # Score gauges, issue cards
│       │   ├── layout/                  # Navbar, footer
│       │   └── ui/                      # Primitives (buttons, tabs)
│       └── lib/
│           ├── api/                     # API client
│           ├── hooks/                   # Custom React hooks
│           └── types/                   # TypeScript interfaces
│
├── 📂 api/                              # Azure Functions (Node.js 22)
│   ├── src/functions/
│   │   ├── scans.ts                     # POST /scans, GET /scans/:id
│   │   └── health.ts                    # GET /health
│   └── prisma/
│       └── schema.prisma                # Database schema
│
├── 📂 backend/SEO-checker/
│   └── py-services/                     # Python SEO Worker
│       ├── extractor/
│       │   ├── comprehensive\_extractor.py   ← Orchestrator
│       │   ├── text\_analyzer.py             ← TF-IDF + readability
│       │   ├── security\_headers.py          ← CSP, HSTS, X-Frame
│       │   └── pagespeed\_insights.py        ← Google CWV API
│       ├── worker/
│       │   └── queue\_worker.py              ← Azure Queue consumer
│       └── Dockerfile
│
├── 📂 .github/workflows/
│   ├── azure-static-web-apps.yml        # Frontend → SWA
│   ├── main\_rankify-v1-src.yml          # API → Functions
│   └── deploy-python-worker.yml         # Worker → Container Apps
│
├── docker-compose.local.yml             # Local dev stack
├── pnpm-workspace.yaml                  # Monorepo config
└── staticwebapp.config.json             # SWA routing + CSP headers
```
---
✦ Quick Start
Prerequisites
Requirement	Version
Node.js	≥ 20
pnpm	≥ 9
Python	≥ 3.11
Docker	≥ 24
1. Clone & Install
```bash
git clone https://github.com/djtsingh/Rankify.git
cd Rankify
pnpm install
```
2. Configure Environment
```bash
# API layer
cp api/local.settings.example.json api/local.settings.json
# Fill in your Azure Storage + PostgreSQL connection strings

# Python worker
cp backend/SEO-checker/py-services/.env.example backend/SEO-checker/py-services/.env
# Fill in AZURE\_STORAGE\_CONNECTION\_STRING, DATABASE\_URL, GOOGLE\_PAGESPEED\_API\_KEY
```
3. Spin Up Local Stack
```bash
# Option A: Docker Compose (recommended)
docker compose -f docker-compose.local.yml up

# Option B: Manual
# Terminal 1 — Frontend
cd apps/web \&\& pnpm dev

# Terminal 2 — API (requires Azure Functions Core Tools)
cd api \&\& npm run start

# Terminal 3 — Python worker
cd backend/SEO-checker/py-services
pip install -r requirements.txt
python worker/queue\_worker.py
```
4. Run Your First Scan
```bash
# Submit a scan job
curl -X POST http://localhost:7071/api/v1/scans \\
  -H "Content-Type: application/json" \\
  -d '{"url": "https://example.com"}'

# Response:
# { "scanId": "abc123", "status": "queued" }

# Poll for results
curl http://localhost:7071/api/v1/scans/abc123
```
Open `http://localhost:3000` in your browser — paste a URL, hit scan, watch the dashboard populate in real time.
---
✦ Deployment
Rankify is configured for automatic deployment via GitHub Actions. Push to `main` and all three pipelines fire independently based on which paths changed.
CI/CD Pipelines
Pipeline	Trigger Path	Target	Approx. Time
`azure-static-web-apps.yml`	`apps/web/\*\*`	Azure Static Web Apps	~2 min
`main\_rankify-v1-src.yml`	`api/\*\*`	Azure Functions	~3 min
`deploy-python-worker.yml`	`backend/\*\*`	Azure Container Apps	~5 min
Required GitHub Secrets
```bash
# Azure Identity (OIDC preferred)
AZURE\_CLIENT\_ID
AZURE\_TENANT\_ID
AZURE\_SUBSCRIPTION\_ID

# Static Web Apps
AZURE\_STATIC\_WEB\_APPS\_API\_TOKEN

# Azure Functions
AZURE\_FUNCTIONAPP\_PUBLISH\_PROFILE

# Database \& Queue
DATABASE\_URL
AZURE\_STORAGE\_CONNECTION\_STRING

# Container Registry
ACR\_USERNAME
ACR\_PASSWORD

# Optional — enables real Core Web Vitals
GOOGLE\_PAGESPEED\_API\_KEY
```
Manual Deploy Commands
```bash
# Frontend
cd apps/web
pnpm build
# Output in 'out/' → upload to Azure Static Web Apps

# API
cd api
npm run build
func azure functionapp publish rankify-v1-src

# Python Worker
cd backend/SEO-checker/py-services
docker build -t rankifyacr.azurecr.io/seo-worker:latest .
docker push rankifyacr.azurecr.io/seo-worker:latest
az containerapp update \\
  --name seo-worker \\
  --resource-group rankify-v1 \\
  --image rankifyacr.azurecr.io/seo-worker:latest
```
Build Commands Reference
```bash
pnpm build          # Build all packages
pnpm build:web      # Frontend only
cd api \&\& npm run build   # API only
```
---
✦ SEO Metrics Reference
Core Web Vitals (via Google PageSpeed Insights v5)
Metric	Good	Needs Improvement	Poor
LCP — Largest Contentful Paint	≤ 2.5s	2.5–4.0s	> 4.0s
FID — First Input Delay	≤ 100ms	100–300ms	> 300ms
CLS — Cumulative Layout Shift	≤ 0.1	0.1–0.25	> 0.25
INP — Interaction to Next Paint	≤ 200ms	200–500ms	> 500ms
TTFB — Time to First Byte	≤ 800ms	800ms–1.8s	> 1.8s
FCP — First Contentful Paint	≤ 1.8s	1.8–3.0s	> 3.0s
Content Intelligence (TF-IDF + textstat)
Signal	Method	Output
Keyword density	scikit-learn TF-IDF	Top-N keywords with relevance score
Readability	textstat Flesch-Kincaid	Reading grade level (target: 8–10)
Word count	NLP tokenization	Raw count + content-to-HTML ratio
Security Headers Audit
Header	Why It Matters
`Content-Security-Policy`	Prevents XSS injection
`X-Frame-Options`	Blocks clickjacking
`Strict-Transport-Security`	Forces HTTPS
`X-Content-Type-Options`	Prevents MIME sniffing
Mixed Content	HTTP assets on HTTPS pages hurt SEO ranking
---
✦ Roadmap
> Built in public. Shipping fast.
✅ v1.0 — Foundation (Shipped)
[x] Comprehensive SEO audit engine (Python + BeautifulSoup4)
[x] Core Web Vitals via Google PageSpeed Insights API
[x] TF-IDF keyword extraction + readability scoring
[x] Security header analysis
[x] Azure serverless infrastructure (SWA + Functions + Container Apps)
[x] Async scan queue with auto-scaling worker
[x] Shareable scan results via direct link
[x] PDF / CSV export
🔨 v1.1 — Intelligence Layer (In Progress)
[ ] Google PageSpeed API key integration for 100% accurate CWV
[ ] Historical scan comparison ("your LCP improved by 0.4s this week")
[ ] Bulk URL scanning (up to 50 URLs per job)
[ ] Competitor comparison dashboard
🗺 v2.0 — Platform (Planned)
[ ] User accounts + scan history
[ ] Team workspaces with role-based access
[ ] Scheduled monitoring — scan your site weekly, get alerts on regressions
[ ] Slack / email alert integration
[ ] Backlink profile integration (Ahrefs / Moz API)
[ ] White-label reports (agency tier)
🔭 v3.0 — Intelligence (Vision)
[ ] AI-generated fix recommendations (not just issue detection)
[ ] NLP-powered content gap analysis vs. competitors
[ ] Keyword ranking tracker with SERP position history
[ ] API access for programmatic audits
---
✦ Contributing
Rankify is currently a founder-led project, but the door is open to contributors who want to build the future of SEO tooling.
How to Contribute
```bash
# 1. Fork the repo
# 2. Create a feature branch
git checkout -b feature/your-feature-name

# 3. Make your changes
# 4. Commit with a clear message
git commit -m "feat: add bulk URL scanning support"

# 5. Push and open a PR
git push origin feature/your-feature-name
```
Contribution Areas
Area	What's Needed
Python Extractor	New SEO signals, better NLP analysis
Frontend	Dashboard improvements, data visualizations
API	New endpoints, performance optimizations
Docs	Tutorials, architecture diagrams
DevOps	Terraform IaC for full Azure provisioning
Code Standards
TypeScript: Strict mode enabled — no `any`, no compromises
Python: Type hints required, PEP 8, docstrings on public methods
Commits: Conventional Commits format (`feat:`, `fix:`, `docs:`, `chore:`)
PRs: Must include a description of what changed and why
---
✦ Monitoring & Operations
Tool	Purpose
Azure Application Insights	Distributed tracing across all three services
Azure Monitor	Alerts for queue depth, error rates, latency
Log Analytics Workspace	Centralized log aggregation
Azure Automated Backups	PostgreSQL point-in-time recovery
Health Check
```bash
curl https://rankify-v1-src.azurewebsites.net/api/health
# Expected: { "status": "ok", "db": "connected", "queue": "reachable" }
```
---
✦ Security
All secrets stored in GitHub Secrets / Azure Key Vault — never in source
OIDC-based Azure authentication for CI/CD (no long-lived service principal passwords)
CSP headers configured in `staticwebapp.config.json`
HTTPS enforced across all Azure services by default
Non-root Docker container for the Python worker
`.gitignore` covers all `.env`, `local.settings.json`, `\_\_pycache\_\_`, and publish profiles
> ⚠️ \*\*Security Disclosure\*\*: Found a vulnerability? Open a private security advisory on GitHub or email the maintainer directly. We take security seriously and will respond within 48 hours.
---
✦ Contact & Support
<div align="center">
Channel	Link
🌐 Live Platform	rankify.page
🐛 Bug Reports	GitHub Issues
💡 Feature Requests	GitHub Discussions
👤 Founder	github.com/djtsingh
🌍 Portfolio	daljeetsingh.me
</div>
---
✦ License
This project is proprietary software. All rights reserved © 2026 Rankify.
Usage, distribution, or modification without explicit written permission from the maintainer is prohibited.
---
✦ Acknowledgments
This project is built on the shoulders of excellent open source work:
Next.js — the React framework that made the frontend painless
Tailwind CSS — because life is too short for naming CSS classes
anime.js — for animations that don't feel like PowerPoint transitions
Prisma — ORM that actually has good DX
scikit-learn — TF-IDF in three lines of Python
textstat — readability scoring done right
BeautifulSoup4 — HTML parsing without the headaches
Azure — serverless infrastructure that scales to zero and back
---
<div align="center">
<br />
Built with precision by Daljeet Singh
If Rankify saved you time, give it a ⭐ — it costs you nothing and means a lot.
<br />
🌐 rankify.page · GitHub
</div>
