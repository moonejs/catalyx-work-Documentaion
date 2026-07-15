

## 1. Objective
To recommend a technology stack and modeling tool for building an internal platform that enables cross-department collaboration on Model-Based Systems Engineering (MBSE), allowing teams (systems, mechanical, electrical, software, etc.) to work together on shared models.

## 2. Background: Key Concepts

| Term | What it is |
|------|-----------|
| **MBSE** | Model-Based Systems Engineering — a methodology for engineering complex systems using models instead of documents |
| **SysML** | A modeling *language/notation* (not software) used to represent systems — blocks, requirements, interfaces, behaviors |
| **Capella** | A free, open-source MBSE tool (Eclipse/Thales) using the Arcadia method, SysML-like |
| **Cameo Systems Modeler** | A paid, industry-standard MBSE tool with full SysML compliance (Dassault) |
| **Enterprise Architect** | A paid MBSE/UML tool by Sparx Systems, cheaper alternative to Cameo |
| **OSLC** | Open Services for Lifecycle Collaboration — a standard protocol for integrating engineering tools |

**Key distinction:** SysML/Capella/Cameo are tools used by individual engineers to *create* models. They are not built for real-time, multi-department collaboration — which is the gap the requested platform needs to fill.

## 3. Recommended Approach
Rather than building a modeling tool from scratch (a multi-year undertaking), the recommended approach is to build a **collaboration layer on top of an existing MBSE tool**:

1. Engineers create models in a dedicated MBSE tool (e.g., Capella)
2. Models are exported (XMI/JSON format)
3. The custom platform imports, stores, and displays this data
4. Departments collaborate, comment, review, and track changes through the web platform

## 4. Modeling Tool Recommendation

### Option A: Capella (Recommended)
- **Pros:** Free/open-source, actively maintained by Thales/Eclipse Foundation, strong API and plugin ecosystem (Java-based), growing industry adoption (esp. aerospace/defense), good enough SysML alignment for most use cases
- **Cons:** Uses Arcadia method (SysML-like, not 100% pure SysML), smaller community than Cameo

### Option B: Cameo Systems Modeler / MagicDraw
- **Pros:** Industry-standard, full SysML compliance, mature ecosystem, strong enterprise support
- **Cons:** Expensive licensing, steeper learning curve

### Option C: Enterprise Architect
- **Pros:** Cheaper than Cameo, supports SysML + UML, decent scripting/API support
- **Cons:** Less specialized for deep systems engineering, dated UI

**Recommendation:** Start with **Capella** — zero licensing cost while validating the platform's value, with solid enough API support for integration. Reconsider Cameo only if the company later needs strict SysML compliance for client/certification requirements.

## 5. Tech Stack Options for the Collaboration Platform

### Option 1: Node.js/TypeScript Stack (Recommended)
**React + Next.js + NestJS/Express + PostgreSQL + Socket.io**
- **Pros:** Fastest to build (huge ecosystem, ready-made diagramming libraries like React Flow/JointJS, built-in real-time collab via Socket.io), one language across frontend/backend
- **Cons:** Less mature for heavy scientific/simulation integration; less common in traditional enterprise systems-engineering environments

### Option 2: Python Stack
**React + FastAPI/Django + PostgreSQL + Celery**
- **Pros:** Best for future integration with engineering/scientific tools (MATLAB, Simulink, NumPy)
- **Cons:** Real-time features require more setup than Node; Django can be heavy for a fast MVP

### Option 3: Java/Enterprise Stack
**Angular + Spring Boot + PostgreSQL/Oracle**
- **Pros:** Best long-term fit for deep integration with Capella/Cameo (both Java/Eclipse-based); scales well for large, secure enterprise systems
- **Cons:** Slower to prototype, more boilerplate, steeper learning curve

### Option 4: Low-Code/BaaS Approach
**React + Supabase/Firebase**
- **Pros:** Fastest possible prototype (skips building auth/database/real-time sync from scratch)
- **Cons:** Less long-term control, potential vendor lock-in, likely needs replacing later

**Recommendation:** **Option 1 (Node.js/TypeScript)** for the primary build — best balance of speed and flexibility. **Option 4** can be mentioned as a way to produce a clickable prototype even faster for early stakeholder validation. **Option 3** noted as a future path if deep native Capella/Cameo plugin integration becomes necessary.

## 6. Summary Recommendation

| Layer                            | Recommendation                                                                                                 |
| -------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Modeling tool (SysML/MBSE)**   | Capella                                                                                                        |
| **Collaboration platform stack** | Node.js + React + PostgreSQL + Socket.io                                                                       |
| **Integration method**           | Capella model export (XMI/JSON) → platform backend parses & stores → web UI for cross-department collaboration |


