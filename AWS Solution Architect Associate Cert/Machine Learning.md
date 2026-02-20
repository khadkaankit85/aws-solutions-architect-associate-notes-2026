> [!abstract] What is it?
> AWS Machine Learning services provide managed intelligence capabilities that solve specific problems such as vision, speech, language understanding, recommendations, search, and document processing. These services expose ML functionality through APIs so applications can consume intelligence without building or training models.

---

## Amazon Rekognition
Amazon Rekognition analyzes images and videos to extract meaningful visual information. It processes media stored in S3 or streamed in real time and returns structured metadata describing what appears in the content.

Rekognition identifies objects, scenes, activities, and people, analyzes facial attributes, compares faces for similarity, detects text embedded in images, and flags unsafe or explicit content. Video analysis extends these capabilities to person tracking and activity detection across frames.

This service fits applications that need automated visual understanding such as identity verification, media moderation, security analytics, and content tagging, where building and maintaining a computer vision pipeline would be complex and expensive.

---

## Amazon Transcribe
Amazon Transcribe converts spoken audio into written text. Audio can be processed in real time or in batch, and the output includes timestamps, speaker labels, and punctuation.

Transcribe supports custom vocabularies to improve accuracy for domain specific terms and can identify multiple speakers within a conversation. It integrates naturally into pipelines where audio is the raw input and text analysis or storage is the next step.

This service is commonly used for call center recordings, meeting transcription, voice analytics, and any workflow that needs searchable or analyzable text derived from speech.

---

## Amazon Polly
Amazon Polly transforms text into natural sounding speech using neural text to speech models. It supports multiple languages and voices and can generate audio streams or files.

Polly provides fine control over pronunciation, pacing, and emphasis, and can emit speech marks that align audio with text timing. This makes it suitable for interactive and accessibility focused applications.

It is used in systems that need spoken output such as voice assistants, IVR systems, accessibility tools, and automated narration.

---

## Amazon Translate
Amazon Translate performs neural machine translation on text. It accepts plain or formatted text and returns translated output while preserving structure.

The service operates in real time or batch workflows and supports many language pairs. It removes the need to manage translation models or external services.

Translate is used in multilingual applications, content localization pipelines, and cross language communication systems where text must be understood across regions.

---

## Amazon Lex
Amazon Lex builds conversational interfaces using natural language understanding. It processes user input, maps it to intents, extracts structured data through slots, and manages dialog flow.

Lex maintains conversation state and handles clarification, retries, and branching logic. Fulfillment is typically handled by Lambda functions that execute business logic.

This service is used to build chatbots and voice bots that convert unstructured user input into structured actions such as booking, querying systems, or triggering workflows.

---

## Amazon Connect
Amazon Connect is a cloud native contact center platform that routes voice and chat interactions through programmable contact flows.

It integrates directly with Lex for conversational logic and Lambda for backend integration. Calls and chats are treated as events that can trigger workflows, analytics, and automation.

Connect replaces traditional call center infrastructure with a scalable, event driven system suitable for customer support, IVR systems, and AI assisted service desks.

---

## Amazon Comprehend
Amazon Comprehend analyzes text to extract meaning and structure. It identifies sentiment, entities, key phrases, language, and personally identifiable information.

The service processes unstructured text and returns structured insights that can be indexed, filtered, or acted upon programmatically.

Comprehend is used in feedback analysis, document classification, compliance workflows, and any system that needs to understand large volumes of text automatically.

---

## Amazon SageMaker
Amazon SageMaker is a full machine learning platform for building, training, and deploying custom models. It provides managed infrastructure for data preparation, training jobs, tuning, and inference endpoints.

Unlike pre trained AI services, SageMaker is used when the problem requires custom models, proprietary data, or specialized algorithms. It supports notebooks, built in algorithms, and custom containers.

This service fits advanced ML workflows where control over the entire model lifecycle is required.

---

## Amazon Kendra
Amazon Kendra is an intelligent search service designed for enterprise data. It indexes documents from multiple sources and uses machine learning to understand user intent and relevance.

Instead of keyword matching, Kendra returns ranked answers based on semantic understanding of queries and content.

It is used for internal knowledge bases, enterprise document search, and systems where users need accurate answers from large document collections.

---

## Amazon Personalize
Amazon Personalize builds real time recommendation systems using user behavior data. It ingests interaction data, trains recommendation models automatically, and serves personalized results through APIs.

The service continuously adapts recommendations as user behavior changes, without requiring manual model tuning.

Personalize is used in applications that need dynamic content or product recommendations driven by user activity.

---

## Amazon Textract
Amazon Textract extracts structured data from scanned documents. It detects text, tables, and form fields and returns results that preserve document structure.

Unlike basic OCR, Textract understands relationships between fields and values, enabling automated processing of complex documents.

It is used in invoice processing, form digitization, compliance workflows, and document automation pipelines.

---

## Mental Model Summary

| Problem | Service |
|---|---|
| Visual understanding | Rekognition |
| Speech to text | Transcribe |
| Text to speech | Polly |
| Language translation | Translate |
| Conversational interfaces | Lex |
| Contact centers | Connect |
| Text understanding | Comprehend |
| Custom ML models | SageMaker |
| Enterprise search | Kendra |
| Recommendations | Personalize |
| Document extraction | Textract |

<span style="float:left">← [[Data & Analytics]]</span><span style="float:right">[[Monitoring & Audit]] →</span>
