# Features:
### 1. Onboarding
- Auth
  - Quick Auth
  - Link Auth
  - Group Auth
- Owner profile
  - Name
  - Gender
  - Birthday
- Pet profile
  - Name
  - Gender
  - Type
  - Birthday
 
### 2. Social graph
- Add/invite friend
- Sync contact
- CRUD group
- Offline with friend. Photo + Video after capture will store location & time -> landmark data

### 3. Capture
- Capture image:
  - Only Dog/Cat video, no human -> using AI model to validate on client/server
  - Image editor:
    - filter
    - basic edit (flip, zoom-in,...)
    - sticker
    - AI  generate [(price)](#ai-generate-price)
- Capture video:
  - Only Dog/Cat video, no human -> using AI model to validate on client/server
  - Short video: 10s
  - Video editor:
    - filter
    - basic edit (flip, zoom-in,...)
    - sticker
    - AI  generate [(price)](#ai-generate-price)
   
### 4. Send
- Send to person
- Send to group

### 5. Widget/View
- View image/video
  - Widget view
  - App view
 
### 6. Response
- Reaction: Like/Haha/Wow...
- Comment/Quick response
- Reply by capture
- Seen by

### 7. History

### 8. Notification

### 9. Setting
- Privacy
- Block/Report
- Hide user/post
- Cache cleaning

# Biz Model
### Free

### Premium


### AI generate price
| Platform                    | Resolution | 5s video          | 10s video   | 15s video | Price/s     |
| --------------------------- | ---------- | ----------------- | ----------- | --------- | ----------- |
| Seedance 2.0 (EvoLink 480p) | 480p       | $0.46             | $0.92       | $1.38     | $0.092 ⭐    |
| Seedance 2.0 (EvoLink 720p) | 720p       | $0.995            | $1.99       | $2.985    | $0.199 ⭐    |
| Pika 2.0 (720p)             | 720p       | $0.20             | -           | -         | $0.04 ⭐     |
| Pika 2.0 (1080p)            | 1080p      | $0.45             | -           | -         | $0.09       |
| Kling AI (Standard 720p)    | 720p       | $0.14             | $0.28       | -         | $0.028      |
| Kling AI (Standard 1080p)   | 1080p      | $0.20-$0.40       | $0.28-$0.56 | -         | $0.04-$0.08 |
| Luma Ray 2 Flash            | 720p       | $0.60             | -           | -         | $0.12       |
| Luma Ray 2                  | 1080p      | $0.95             | -           | -         | $0.19       |
| Runway Gen-4 Turbo          | any        | $0.25             | $0.50 (10s) | -         | $0.05       |
| ElevenLabs (TTS)            | N/A        | ~$0.0025/50 chars | -           | -         | per char    |
