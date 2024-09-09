---
title: Access and use AI models with Aiven for AlloyDB Omni®
sidebar_label: Access AI models
---

Enable and use AI models in Aiven for AlloyDB Omni® to build and deploy generative AI
applications directly on your operational data.

Aiven for AlloyDB Omni® allows you to integrate and use AI models such as OpenAI, Hugging
Face, or Gemini.

## Prerequisites

- Aiven for AlloyDB Omni® service running
- [`psql` CLI client installed](https://www.postgresql.org/download/)
- [`gcloud` CLI client installed](https://cloud.google.com/sdk/docs/install)
- [Google service account credentials uploaded into Aiven for AlloyDB Omni](/docs/products/alloydb-omni/manage-credentials)
- `google_ml_integration` extension installed using the `psql` CLI:

  ```sql
  CREATE EXTENSION google_ml_integration VERSION '1.3';
  ```

## Use OpenAI

1. Record your OpenAI user API key as a secret in Google Secret Manager.

1. Grant your Google service account access to the created secret using the `gcloud` CLI:

   ```bash
   gcloud secrets add-iam-policy-binding SECRET_ID
     --member="serviceAccount:GOOGLE_SERVICE_ACCOUNT_PRINCIPAL"
     --role="roles/secretmanager.secretAccessor"
   ```

   Replace the following:
   - `SECRET_ID` with the ID of you newly created secret recorded in the Google Secret
     Manager
   - `GOOGLE_SERVICE_ACCOUNT_PRINCIPAL` with your Google service account principal,
     for example `abc-vertex-ai-sa@sample-project-name.iam.gserviceaccount.com`

1. Declare the secret for the integration using the `psql` CLI:

   ```sql
   CALL google_ml.create_sm_secret(
       secret_id=>'DECLARED_SECRET_ID',
       secret_path=>'projects/GOOGLE_CLOUD_PROJECT_NAME/secrets/SECRET_ID/versions/1');
   ```

   Replace the following:
   - `DECLARED_SECRET_ID` with the local identifier for your secret
   - `GOOGLE_CLOUD_PROJECT_NAME` with the name of your Google Cloud project where the
     secret in stored
   - `SECRET_ID` with the ID of the secret created in Google Secret Manager

1. Define the AI model using the `psql` CLI:

   ```sql
   CALL google_ml.create_model(
       model_id => 'gpt-4o',
       model_provider => 'open_ai',
       model_request_url =>'https://api.openai.com/v1/chat/completions',
       model_type => 'generic',
       model_auth_type => 'secret_manager',
       model_auth_id => 'DECLARED_SECRET_ID',
       model_qualified_name => 'gpt-4o');
   ```

   Replace `DECLARED_SECRET_ID` with the local identifier for the secret declared for the
   integration.

1. Use the model by running:

   ```sql
   SELECT google_ml.predict_row('gpt-4o','{"model" : "gpt-4o", "messages" : [{"role": "user", "content": "What is Aiven?"}]}')->'choices'->0->'message'->'content';
   ```

## Use Gemini

1. Grant the service user access to utilize Vertex AI using the `gcloud` CLI:

   ```bash
   gcloud projects add-iam-policy-binding GOOGLE_CLOUD_PROJECT_NAME
     --member="serviceAccount:GOOGLE_SERVICE_ACCOUNT_PRINCIPAL"
     --role="roles/aiplatform.user"
   ```

   Replace the following:
   - `GOOGLE_CLOUD_PROJECT_NAME` with the name of your Google Cloud project
   - `GOOGLE_SERVICE_ACCOUNT_PRINCIPAL` with your Google service account principal,
     for example `abc-vertex-ai-sa@sample-project-name.iam.gserviceaccount.com`.

1. Define the AI model on your Aiven for AlloyDB Omni service using the `psql` CLI:

   ```sql
   CALL google_ml.create_model(
       model_id => 'gemini-1.0-pro',
       model_request_url => 'https://us-central1-aiplatform.googleapis.com/v1/projects/GOOGLE_CLOUD_PROJECT_NAME/locations/us-central1/publishers/google/models/gemini-1.0-pro:streamGenerateContent',
       model_provider => 'google',
       model_auth_type => 'alloydb_service_agent_iam');
   ```

   Replace `GOOGLE_CLOUD_PROJECT_NAME` with the name of your Google Cloud project.

1. Use the model by running:

   ```sql
   SELECT google_ml.predict_row(
     model_id =>'gemini-1.0-pro',
     request_body =>'{ "contents": { "role": "user", "parts": { "text": "What is Aiven?" }  }}');
   ```

## Use Hugging Face

1. Record your [Hugging Face access token](https://huggingface.co/docs/hub/en/security-tokens)
   as a secret in Google Secret Manager.

1. Grant your Google service account access to the created secret using the `gcloud` CLI:

   ```bash
   gcloud secrets add-iam-policy-binding SECRET_ID
     --member="serviceAccount:GOOGLE_SERVICE_ACCOUNT_PRINCIPAL"
     --role="roles/secretmanager.secretAccessor"
   ```

   Replace the following:
   - `SECRET_ID` with the ID of you newly created secret recorded in the Google Secret
     Manager
   - `GOOGLE_SERVICE_ACCOUNT_PRINCIPAL` with your Google service account principal,
     for example `abc-vertex-ai-sa@sample-project-name.iam.gserviceaccount.com`

1. Declare the secret for the integration using the `psql` CLI:

   ```sql
   CALL google_ml.create_sm_secret(
       secret_id=>'DECLARED_SECRET_ID',
       secret_path=>'projects/GOOGLE_CLOUD_PROJECT_NAME/secrets/SECRET_ID/versions/1');
   ```

   Replace the following:
   - `DECLARED_SECRET_ID` with the local identifier for your secret
   - `GOOGLE_CLOUD_PROJECT_NAME` with the name of your Google Cloud project where the
     secret in stored
   - `SECRET_ID` with the ID of the secret created in Google Secret Manager

1. Define the AI model using the `psql` CLI:

   ```sql
   CALL google_ml.create_model(
       model_id => 'Mistral-7B-Instruct-v0.3',
       model_provider => 'custom',
       model_request_url =>'https://api-inference.huggingface.co/models/mistralai/Mistral-7B-Instruct-v0.3',
       model_type => 'generic',
       model_auth_type => 'secret_manager',
       model_auth_id => 'DECLARED_SECRET_ID',
       model_qualified_name => 'Mistral-7B-Instruct-v0.3');
   ```

   Replace `DECLARED_SECRET_ID` with the local identifier for the secret declared for the
   integration.

1. Use the model by running:

   ```sql
   SELECT google_ml.predict_row('Mistral-7B-Instruct-v0.3','{"inputs" : "What is Aiven?"}')->0->'generated_text';
   ```

## Bring your own model (BYOM)

1. Record your AI model token as a secret in Google Secret Manager.

1. Grant your Google service account access to the created secret using the `gcloud` CLI:

   ```bash
   gcloud secrets add-iam-policy-binding SECRET_ID
     --member="serviceAccount:GOOGLE_SERVICE_ACCOUNT_PRINCIPAL"
     --role="roles/secretmanager.secretAccessor"
   ```

   Replace the following:
   - `SECRET_ID` with the ID of you newly created secret recorded in the Google Secret
     Manager
   - `GOOGLE_SERVICE_ACCOUNT_PRINCIPAL` with your Google service account principal,
     for example `abc-vertex-ai-sa@sample-project-name.iam.gserviceaccount.com`

1. Declare the secret for the integration using the `psql` CLI:

   ```sql
   CALL google_ml.create_sm_secret(
       secret_id=>'DECLARED_SECRET_ID',
       secret_path=>'projects/GOOGLE_CLOUD_PROJECT_NAME/secrets/SECRET_ID/versions/1');
   ```

   Replace the following:
   - `DECLARED_SECRET_ID` with the local identifier for your secret
   - `GOOGLE_CLOUD_PROJECT_NAME` with the name of your Google Cloud project where the
     secret in stored
   - `SECRET_ID` with the ID of the secret created in Google Secret Manager

1. Define the AI model using the `psql` CLI:

   ```sql
   CALL google_ml.create_model(
       model_id => '',
       model_provider => 'custom',
       model_request_url =>'',
       model_type => 'generic',
       model_auth_type => 'secret_manager',
       model_auth_id => 'DECLARED_SECRET_ID',
       model_qualified_name => '');
   ```

   Replace `DECLARED_SECRET_ID` with the local identifier for the secret declared for the
   integration.

1. Use your model by running:

   ```sql
   SELECT google_ml.predict_row();
   ```

## Next step

With an AI model integrated, you can
[build generative AI applications using AlloyDB AI](https://cloud.google.com/alloydb/docs/ai).
