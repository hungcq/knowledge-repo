# Machine learning
## Rekognition
- Find objects, people, text, scenes in images & videos
- Facial analysis & facial search to verify user, count people
- Can create DB of familiar faces or compare against celebrities DB
- Use case highlight: content moderation:
  - Detect inapt/offensive content
  - Flow: image -> Rekognition check against confidence threshold (set by user) -> optional manual review
## Transcribe
- Auto convert speech to text using auto speech recognition (deep learning)
- Features:
  - Auto remove personally identifiable info using Redaction
  - Auto lang identification for multi lingual audio
## Polly
- Turn text to speech
- Lexicon: customize pronunciation of words:
  - Stylized words (eg 3=e)
  - Acronyms: AWS = Amazon Web Service
- -> Upload & use in SynthesizeSpeech operation
- SSML: generate speech from plain text/documents marked up with Speech Synthesis Markup Language (SSML)
- -> More customization: eg emphasis, breathing sounds
## Translate
- Def: natural & accurate language translation
- Use case:
  - Localize content for international users
  - Translate large volume of text
## Lex
- Def: technology powering Alexa
- Features:
  - Auto speech recognition: speech -> text
  - Natural language understanding: recognize intent of text, callers
  - Build chatbots, call center bots
## Connect
- Receive calls, create contact flows, cloud-based virtual contact center
- Can integrate with other customer relationship management (CRM) systems/AWS
- On-demand, cheap
- Flow: client -> Connect -> Lex: recognize intent -> Lambda -> CRM
## Comprehend
- Natural language processing (NLP)
- Managed, server less service to find insights/rela in text
- Use cases:
  - Sentiment analysis
  - Create & group articles by topics
## Comprehend Medical
- Detect & return useful info in unstructured clinical text
- Use NLP to detect Protected Health Info (PHI) via DetectPHI API
## SageMaker
- Managed service for devs/data scientists to build ML models
## Forecast
- Managed service using ML to deliver forecasts
## Kendra
- Managed document search service using ML
- Flow: doc -> Kendra: index -> answers to users' questions
## Personalize
- Provide realtime personalize recommendations
## Textract
- Extract text/data from scanned docs