# vani-content-manager

The **vani-content-manager** module has the following responsibilities:
1. **YouTube Content Delivery**:
   - Fetch YouTube videos (TV shows, funny videos, forwards) using the YouTube Data API.
   - Support user requests (e.g., “Telugu comedy video”) and personalized recommendations based on user preferences (stored in AWS RDS).
   - Filter videos by language (Kannada, Hindi, Telugu) and relevance.
2. **AI-Generated Avatar Videos**:
   - Generate 30-second videos (5-10MB) using Synthesia API (or equivalent, e.g., D-ID).
   - Personalize videos based on user profile (age, gender, preferences) and context (weather via OpenWeatherMap, local events via web scraping).
   - Include festive videos (e.g., Diwali, Ugadi) and service nudging (e.g., “Need groceries?” every 5th video).
   - Store videos in AWS S3; pre-generate 80% as templates to reduce costs.
3. **Daily Forwards**:
   - Deliver daily content (videos, memes, quotes) at 8 AM to opted-in users.
   - Allow users to customize content type (e.g., “Kannada jokes”).
   - Schedule delivery using AWS Lambda.
4. **Content Moderation**:
   - Moderate user-submitted videos/images using Google Vision API to ensure appropriateness.
   - Store approved content in AWS RDS.

### **Technical Specifications**
- **Language**: Python 3.9+.
- **Dependencies**:
  - External: `google-api-python-client` (YouTube), `synthesia-api` (hypothetical, replace with D-ID if needed), `requests`, `google-cloud-vision`, `boto3` (AWS S3/RDS/Lambda), `python-dotenv` (environment variables).
  - Internal: None.
- **APIs**:
  - YouTube Data API (free, 10,000 units/day).
  - Synthesia API (~₹100/video, optimize with templates).
  - OpenWeatherMap API (weather data).
  - Google Vision API (image moderation).
  - AWS S3 (video storage, 100GB), RDS (user/content data), Lambda (scheduling).
- **Constraints**:
  - Optimize videos for WhatsApp (5-10MB, <3-second delivery).
  - Handle vernacular language nuances (e.g., Hinglish, Telugu slang).
  - Keep costs within budget (₹6,00,000/year for video generation, ₹24,000 for S3).
  - Target 5,000 users, ~20 videos/user/month, 1,000 user-submitted images/month.
