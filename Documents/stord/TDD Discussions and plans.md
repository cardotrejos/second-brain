
just noting: largely agree with @Rodrigo Lessa thoughts. i'd just mention that as we lean in on focusing on the contracts/schemas, that's the core problem to solve. and then perhaps we can generalize a chat-ui, a recommendations-ui, etc. edit: obligatory, IMO.

# Grooming

Tue, 03 Feb 26

### Exception Aggregator System Architecture

- Two-service approach for handling exceptions across OMS, Product Catalog, and potentially WMS
- Exception Aggregator: ingestion engine running via cron job 3x daily
    - Calls existing APIs to collect exceptions from each service
    - Translates to unified data model and stores in aggregator storage
    - Avoids double-ingestion through deduplication logic
- Exception Resolver: generates suggestions using AI agent with registered tools
    - Picks up new exceptions from aggregator storage
    - Uses tools like customer order history matching, Google Maps API for address completion
    - Updates exception records with suggestion field when solutions found

### Technical Implementation Decisions

- **Trade-off: Kafka events vs polling approach**
    - Kafka events not currently fired for exceptions
    - Polling architecture chosen over event-driven due to existing API availability
    - Hybrid approach: scheduled pulls 3x daily + on-demand when users access inbox
- API access preferred over direct database connections
    - Need to create network-scoped exception endpoints for OMS
    - Leverage existing product catalog exception APIs
- New Elixir service required since functionality spans multiple existing services

### Exception Resolution Strategy

- Summarization and manual suggestions for all exception types initially
- Smart auto-actionable suggestions tackled one exception type at a time
- **Incomplete address chosen as first target**:
    - Easiest to conceptualize and implement
    - Clear solution path: identify missing fields → infer from ZIP/order history → apply fix
    - Three-step process: AI identifies issue → tool finds solution → action applies fix
- Tools registered per exception category rather than generic LLM tool selection
- High-confidence suggestions can be auto-applied, lower confidence requires user approval

### Next Steps

- Nick: Add user stories to epic by Thursday for task estimation
- Zach: Pull volume metrics for each exception type to prioritize development
- Rodrigo: Investigate existing OMS address validation logic and capabilities
- Team: Review product scenarios document for detailed exception handling flows
- Focus on incomplete address as first full end-to-end implementation

---

# Rodrigo Syncs

Tue, 03 Feb 26

ti

### Kafka Exception Handling Approach

- OMS team doesn’t send exceptions via Kafka
    - Original approach no longer viable
    - Alternative: create new endpoint in OMS service to list latest exceptions
- Polling strategy decided:
    - 3 scheduled polls per day via cron job
    - On-demand polling when users visit inbox page
    - Similar to Nick’s example using Elasticsearch queries

### New Service Architecture

- Team agreed to build dedicated new service
- Need to check for service templates/skeletons
    - Testing frameworks and CI configurations
    - YAML files for automated testing
- Rodrigo will confirm service creation approval on AI channel

### Task Division

- Ricardo: Handle AI components
    - Tool creation and agent setup
    - LLM API requests and AI integrations
- Rodrigo: Infrastructure and data layer
    - Ingestor development
    - Database schema setup
    - Overall architecture

### Next Steps

- Rodrigo: Discuss OMS endpoint implementation with Zach
- Make TDD more concrete based on confirmed approach
- Sync meeting tomorrow morning before Thursday ticket creation
- Ricardo available to help with TDD documentation

---
tbh it's been 10,000 years since i last set up a new service.

i don't think we're 100% sold on a new service for this or what the scope of it should be if we do go that route. i want to make sure @Matt Sutkowski has a chance to weigh in

@Matt Sutkowski
yea, need more info