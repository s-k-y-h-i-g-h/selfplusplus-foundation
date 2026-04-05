# Agent Network Specification v0.1

**Project:** self++ CIC / Agent Network  
**Version:** 0.1  
**Created:** 2026-04-05  
**Status:** DRAFT — For implementation

---

## What This Is

The Agent Network is a distributed system of independent nodes that verify, process, and distribute information without central control. Each node is autonomous, resilient, and neutral.

---

## Core Principles

### 1. No Central Authority
- No single point of control
- No single point of failure
- No single entity can censor or manipulate

### 2. Distributed Verification
- Multiple nodes verify each claim
- Consensus before confirmation
- Redundancy ensures accuracy

### 3. Autonomous Operation
- Each node operates independently
- Nodes can join and leave freely
- Network persists even if nodes fail

### 4. Neutral Infrastructure
- No political affiliation
- No corporate control
- No government oversight

---

## Architecture

### Node Types

#### Verification Nodes
- Verify claims using Verification Protocol
- Participate in consensus voting
- Maintain audit trails
- Minimum 3 for Level 2 verification
- Minimum 5 for Level 3 verification

#### Distribution Nodes
- Distribute verified information
- Serve as API endpoints
- Cache verified claims for performance
- Provide public access to verified data

#### Gateway Nodes
- Interface between external systems and network
- Translate protocols (REST, GraphQL, etc.)
- Rate limiting and access control
- Load balancing across distribution nodes

#### Storage Nodes
- Store verified claims and evidence
- Maintain audit trails
- Provide query interface
- Backup and redundancy

### Node Communication

```
[External System] → [Gateway Node] → [Verification Node] → [Distribution Node] → [User]
                         ↓
                   [Storage Node]
```

### Consensus Mechanism

#### Simple Majority (Level 1)
- 50%+1 nodes agree
- Fast, lightweight
- Used for routine verification

#### Supermajority (Level 2)
- 67%+ nodes agree
- Standard verification
- Used for important claims

#### Unanimous (Level 3)
- 100% nodes agree
- Critical verification
- Used for emergencies

---

## Node Specification

### Node Requirements

#### Minimum
- Internet connection
- 1GB RAM
- 10GB storage
- Python 3.10+ or Node.js 18+
- Cryptographic keypair

#### Recommended
- Stable internet connection
- 4GB RAM
- 100GB storage
- Dedicated server or VPS
- Backup power supply

### Node Identity

Each node has:
- **Node ID** — Unique identifier (UUID)
- **Public Key** — For verification signatures
- **Private Key** — For node authentication (never shared)
- **Endpoint** — Network address for communication
- **Capabilities** — What the node can do (verify, distribute, store, gateway)

### Node Registration

```json
{
  "node_id": "uuid",
  "public_key": "base64",
  "endpoint": "https://node.example.com",
  "capabilities": ["verify", "distribute"],
  "registered_at": "ISO8601",
  "signature": "base64"
}
```

---

## Verification Flow

### Step 1: Claim Submission
- External system submits claim to Gateway Node
- Gateway validates format and rate limits
- Claim forwarded to Verification Nodes

### Step 2: Verification
- Each Verification Node independently verifies claim
- Nodes check sources, cross-reference, analyze patterns
- Each node assigns verification level

### Step 3: Consensus
- Nodes submit verification votes
- Consensus mechanism determines final level
- Result signed by participating nodes

### Step 4: Distribution
- Verified claim sent to Distribution Nodes
- Cached for fast access
- API endpoints updated

### Step 5: Storage
- Claim and evidence stored on Storage Nodes
- Audit trail preserved
- Queryable by verification level

---

## API Specification

### Public Endpoints

```
GET  /api/v1/claims                    — List verified claims
GET  /api/v1/claims/{id}               — Get specific claim
GET  /api/v1/claims?level={0-3}        — Filter by verification level
GET  /api/v1/claims?type={type}        — Filter by claim type
GET  /api/v1/claims?since={timestamp}  — Recent claims
GET  /api/v1/stats                     — Network statistics
```

### Node Endpoints (Authenticated)

```
POST /api/v1/nodes/register            — Register new node
POST /api/v1/nodes/heartbeat           — Node health check
POST /api/v1/claims/submit             — Submit claim for verification
POST /api/v1/claims/{id}/vote          — Submit verification vote
GET  /api/v1/nodes/{id}/claims         — Claims verified by node
```

### Response Format

```json
{
  "claim_id": "uuid",
  "claim_text": "string",
  "claim_type": "empirical",
  "verification_level": 2,
  "confidence_score": 0.85,
  "verified_by": ["node_id_1", "node_id_2", "node_id_3"],
  "verified_at": "ISO8601",
  "sources": [
    {
      "url": "https://...",
      "credibility": 0.9,
      "verified_at": "ISO8601"
    }
  ],
  "audit_trail": ["step1", "step2", "step3"]
}
```

---

## Security

### Authentication
- Node authentication via cryptographic signatures
- API authentication via JWT tokens
- Rate limiting on all endpoints

### Privacy
- Source identities protected
- Claim submitters anonymous (unless they choose to identify)
- Verification votes anonymous

### Integrity
- All claims signed by verifying nodes
- Audit trails immutable
- Tampering detectable via cryptographic hashes

### Resilience
- No single point of failure
- Automatic failover if nodes go down
- Data replicated across storage nodes

---

## Deployment

### Phase 1: Single Node (Week 1-2)
- Deploy one Gateway + Verification + Distribution node
- Manual verification process
- Basic API endpoints

### Phase 2: Multi-Node (Week 3-4)
- Deploy 3+ verification nodes
- Implement consensus mechanism
- Add storage nodes

### Phase 3: Production (Month 2)
- 10+ verification nodes
- Automated verification
- Public API

### Phase 4: Scale (Month 3+)
- 100+ nodes globally
- Geographic distribution
- Advanced consensus mechanisms

---

## Integration Points

### SENTINEL
- Signals submitted to Agent Network for verification
- Verified signals distributed via Distribution Nodes
- Daily briefs generated from verified claims

### Verification Protocol
- Agent Network implements Verification Protocol
- Consensus mechanism follows protocol specification
- Audit trails comply with protocol requirements

### OpenState
- Financial transactions verified by Agent Network
- Currency exchanges verified without surveillance
- Resource allocation verified transparently

### Verification System
- Agent Network performance monitored by Verification System
- Node accuracy tracked and reported
- Network health assessed continuously

---

## Node Economics

### Incentive Model (Future)
- Nodes earn reputation for accurate verification
- High-reputation nodes get priority in consensus
- Incentives aligned with accuracy, not participation

### Cost Model
- Nodes bear their own operating costs
- No payment required to join network
- No payment required to use public API

### Sustainability
- Grant funding for initial deployment
- Donations for ongoing operation
- Service fees for premium features (future)

---

## Anti-Capture Design

### What We Prevent
- Single entity controlling multiple nodes
- Government seizure of nodes
- Corporate acquisition of network
- Censorship of verified claims

### What We Enable
- Geographic distribution (no single jurisdiction)
- Legal diversity (nodes in different legal frameworks)
- Economic independence (no single funding source)
- Technical redundancy (multiple implementations)

### Capture Detection
- Node clustering analysis (detect coordinated nodes)
- Voting pattern analysis (detect collusion)
- Geographic anomaly detection (detect concentrated control)
- Economic analysis (detect single-funder dependency)

---

## The Vision

A network where:
- Truth is verified by many, not decided by one
- Information flows freely but accurately
- No entity can censor or manipulate
- Everyone can participate
- The infrastructure is neutral
- The network is resilient

**This is what information freedom looks like in the 21st century.**

---

*"The network doesn't decide what's true. It verifies what's true."*
