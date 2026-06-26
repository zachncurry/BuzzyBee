# BuzzyBee

## Multi-Node Honeypot Orchestrator & Sigma Rule Generator/ Mini-SIEM (Security Information and Event Management) Ingestion Pipeline
   - **Goal:** Generate real time threat intelligence to detect new tools and techniques generating compensating Sigma rules
   - **Client Benefits:**
       - Zero Production Footprint: The honeypot architecture is entirely decoupled from client operational network. It contains zero client data, hosts no corporate assets, and shares no authentication pathways with your active environment.
       - Safe-Zone Engagement: Threat actors are seamlessly diverted into an isolated "digital sandbox." This allows us to observe, document, and study active attack methodologies in real time without risking data integrity, compliance posture, or business continuity.
       - Proactive Defenses, Zero Friction: Your organization receives all the strategic benefits of advanced, real-time threat intelligence such as custom, localized detection rules, with absolutely zero operational risk.
   - **Tools:** [AWS](AWS.Amazon.com), [Wazuh](https://wazuh.com/), [GNS3](https://www.gns3.com/), [Cowrie🐝](https://www.cowrie.org/), [OpenSecOps - SOAR](https://www.opensecops.org/soar.html), [Sigma Rules](https://github.com/SigmaHQ/sigma/tree/master/rules)
   - **Key Features:**
      - Concurrent Multi-Honeypot Orchestration: Deploy and manage multiple, geographically or logically distinct decoy nodes simultaneously to isolate and triangulate coordinated campaigns.
      - Real Time TPP Profiling: Log and document attacker tools, tactics, and procedures (TTPs) aligned with the MITRE ATT&CK framework.
      - Automated Threat Intelligence: Aggregate live telemetry to build dynamic adversary profiles and behavioral history.
      - Dynamic Sigma Rule Genreation: Translate captured attack methodologies directly into production ready Sigma rules to update Client SIEM/EDR defenses instantly.
   - **High Level Architecture**
      - The Trap: An attacker enters through a GSN3 virtual gateaway and targets one of multiple Cowrie nodes
      - The Collection: Cowrie traps the session, loggin shell execution, source data, and malware hashes
      - The Transport: The Wazuh agent captures these local JSON logs and streams them to the Central Wazuh Manager
      - The Trigger & Orchestration: Wazuh detects a high severity incident and drops an alert event. OpenSecOps ingest the finding via a GSN3 bridge via AWS API Gateway/SQS Queue
      - The Action (Sigma Generation): OpenSecOps triggers a pipeline (like a serverless script) to extract the attacker's specific TTPs from the log and auto-generates a structured Sigma rule, ready for defense   


https://sigmahq.io/docs/basics/rules.html
