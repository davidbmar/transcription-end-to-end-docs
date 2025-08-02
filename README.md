# transcription-end-to-end-docs

These are the docs to integrate three repos.

create the root directory.
1. git clone https://github.com/davidbmar/smart-transcription-router.git
2. git clone https://github.com/davidbmar/cognito-lambda-s3-webserver-cloudfront.git
3. git clone https://github.com/davidbmar/eventbridge-orchestrator.git

# setup the event-bridge:
This repository implements a serverless orchestration platform using AWS EventBridge as the central event bus, structured via JSON schemas, Terraform, and auxiliary Lambda utilities. Acting as the "central nervous system," it decouples independent microservices—e.g. frontend, transcription, and search—by routing only validated, versioned event types such as AudioUploaded and TranscriptionCompleted through a shared EventBridge bus. The setup includes automatic schema validation, a custom bus deployed with Terraform, two lightweight Lambda utilities (an event logger and DLQ processor), and SQS-based error handling. This design simplifies adding or updating services—each only needs to publish or subscribe to known event types—while preserving modularity, flexibility, and backward‑compatibility during schema evolution.




# setup the UI
