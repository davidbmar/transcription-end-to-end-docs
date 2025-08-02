# transcription-end-to-end-docs

These are the docs to integrate three repos.

create the root directory.
1. git clone https://github.com/davidbmar/smart-transcription-router.git
2. git clone https://github.com/davidbmar/cognito-lambda-s3-webserver-cloudfront.git
3. git clone https://github.com/davidbmar/eventbridge-orchestrator.git

# setup the event-bridge:
This repository implements a serverless orchestration platform using AWS EventBridge as the central event bus, structured via JSON schemas, Terraform, and auxiliary Lambda utilities. Acting as the "central nervous system," it decouples independent microservices—e.g. frontend, transcription, and search—by routing only validated, versioned event types such as AudioUploaded and TranscriptionCompleted through a shared EventBridge bus. The setup includes automatic schema validation, a custom bus deployed with Terraform, two lightweight Lambda utilities (an event logger and DLQ processor), and SQS-based error handling. This design simplifies adding or updating services—each only needs to publish or subscribe to known event types—while preserving modularity, flexibility, and backward‑compatibility during schema evolution.

This project **builds a clean orchestration layer** on top of AWS EventBridge.
You get a **custom event bus**, created by Terraform.
You also get **versioned JSON schemas**, registered in AWS EventBridge’s Schema Registry so every message is typed and validated before sending. 

Two helper Lambdas run quietly in the background.
One logs all events.
The other reads from the SQS dead‑letter queue, if any delivery fails.
This keeps the system visible and safe. 

Each service only needs to **emit typed events** into the bus or **subscribe via clean rules**.
EventBridge itself matches messages and routes them.
There’s no central controller or chain of service calls.

When you want to add something new—whether that’s a schema, event type, target, or service—you change a schema or rule.
Terraform updates the system.
No service needs to know about others.
The architecture stays **flexible**, **fault‑tolerant**, and **easy to evolve**.

