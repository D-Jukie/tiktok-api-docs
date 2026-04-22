# 🚀 TikTok Premium API Documentation

Welcome to the **TikTok Premium API**! This high-performance API provides comprehensive access to TikTok content, including videos, users, live streams, music, and more. It is designed to be fast, reliable, and easy to integrate into your applications.

---

## 🔐 Authentication

All requests to the API must include the following security header for validation:

| Header Name | Type | Description |
| :--- | :--- | :--- |
| `x-rapidapi-key` | String | Your unique x-rapidapi-key. |
| `x-rapidapi-host` | String | tiktok-video-no-watermark5.p.rapidapi.com |

---

## 🌐 Base URL
The base URL for all API requests is:
`https://tiktok-video-no-watermark5.p.rapidapi.com`

---

## 📺 Video Endpoints
Manage and retrieve TikTok video content, comments, and search results.

### 1. Get Video Information
`GET /video/info`
Retrieve detailed metadata for a specific TikTok video.
- **Parameters**:
  - `aweme_id` (required): The unique ID of the TikTok video.

### 2. Search Videos
`GET /video/search`
Search for videos based on keywords with advanced filtering.
- **Parameters**:
  - `keyword` (required): Search query.
  - `cursor`: Pagination offset (default: 0).
  - `count`: Number of results (default: 10).
  - `search_id`: Required for pagination (returned from previous search).
  - `sort_type`: `0` (Relevance), `1` (Most Liked), `2` (Most Recent).
  - `publish_time`: `0` (All), `1` (24h), `7` (Week), `30` (Month), `90` (3 Months), `180` (6 Months).

### 3. Get Video Comments
`GET /video/comments`
Retrieve the comment list for a specific video.
- **Parameters**:
  - `aweme_id` (required): Video ID.
  - `cursor`: Pagination offset.
  - `count`: Number of comments (default: 20).

### 4. Get Comment Replies
`GET /video/replies`
Retrieve replies to a specific comment.
- **Parameters**:
  - `aweme_id` (required): Video ID.
  - `comment_id` (required): The ID of the parent comment.
  - `cursor`: Pagination offset.

### 5. Explore Videos
`GET /video/explore`
Retrieve trending or categorized videos.
- **Parameters**:
  - `rule_id`: Content category ID:
    - `2100`: All
    - `2105`: Entertainment
    - `2108`: Sports
    - `2106`: Anime & Comics
    - `2107`: Gaming
    - `2102`: Daily Life
    - `2101`: Comedy
    - `2104`: Fashion
    - `2103`: News & Insights
  - `region`: Country code (default: `VN`).

---

## 👤 User Endpoints
Retrieve profile information, videos, and social lists for TikTok users.

### 1. Get User Info
`GET /user/info`
Get profile details by handle, UID, or SEC UID.
- **Parameters**:
  - `uniqueId`: User handle (without @).
  - `userId`: Numeric user ID.
  - `secUserId`: Secure user ID.

### 2. Search Users
`GET /user/search`
Search for TikTok creators.
- **Parameters**:
  - `keyword` (required): Search query.
  - `follower_count`: Filter by follower count range:
    - `ZERO_TO_ONE_K`: 0 - 1,000 followers
    - `ONE_K_TO_TEN_K`: 1,000 - 10,000 followers
    - `TEN_K_TO_ONE_H_K`: 10,000 - 100,000 followers
    - `ONE_H_K_PLUS`: 100,000+ followers
  - `is_verified`: Filter only verified accounts (`true`/`false`).

### 3. Get User Videos/Music
`GET /user/videos` | `GET /user/music`
Retrieve the list of videos posted by a user or the music tracks they created.
- **Parameters**:
  - `secUserId` (required): User SEC UID.
  - `cursor` / `count`: Pagination control.

### 4. Social Lists (Followers/Following)
`GET /user/followers` | `GET /user/following`
Retrieve social connections for a user.
- **Parameters**:
  - `secUserId` (required): User SEC UID.
  - `pageToken`: Token for the next page.

---

## 🔴 Live Endpoints
Real-time information about TikTok live streams.

### 1. Search Live Streams
`GET /live/search`
Search for active live streams.
- **Parameters**:
  - `keyword` (required): Search keyword.
  - `search_id`: For pagination.

### 2. Room Detail
`GET /live/room_detail`
Get real-time stream data (including FLV/HLS links) by username.
- **Parameters**:
  - `uniqueId` (required): TikTok username.

### 3. Check Alive
`POST /live/check_alive`
Check the live status of multiple rooms at once.
- **Body**:
  ```json
  { "room_ids": ["7361138402123516677", "7361138402123516678"] }
  ```

---

## 🎵 Music Endpoints
Explore music tracks and find videos using specific sounds.

### 1. Search Music
`GET /music/search`
- **Parameters**: `keyword`, `cursor`, `count`.

### 2. Music Detail
`GET /music/detail`
Retrieve comprehensive data about a track, including play URLs and author info.
- **Parameters**: 
  - `music_id` (required): TikTok music ID.

### 3. Get Music Videos
`GET /music/videos`
Retrieve videos that use a specific music track.
- **Parameters**:
  - `music_id` (required): Music ID.
  - `cursor` / `count`: Pagination.

---

## 🏷️ Hashtag Endpoints
Retrieve challenge details and trending hashtags.

### 1. Get Hashtag Info
`GET /hashtag/info`
Retrieve hashtag metadata and statistics.
- **Parameters**: 
  - `challengeName`: Name of the hashtag (without #).
  - `challengeId`: Numeric challenge ID.

### 2. Search Hashtags
`GET /hashtag/search`
Search for hashtags by keyword.
- **Parameters**: `keyword`, `cursor`, `count`.

---

## 📥 Download Endpoints
Specialized endpoints for high-quality media extraction.

### 1. Bulk Download Info
`POST /download/bulk-info`
Retrieve specialized download metadata for multiple videos.
- **Body**: 
  ```json
  { "aweme_ids": ["7312345678901234567", "7312345678901234568"] }
  ```

### 2. Music Download
`GET /download/music`
Get a direct download link for a music track.
- **Parameters**: `music_id`.

### 3. User Videos (Download Ready)
`GET /download/user-videos`
Retrieve a compact list of a user's videos optimized for bulk downloading.
- **Parameters**: `secUserId`, `cursor`, `count`.

---

## 🛠️ Tool Endpoints
Utility functions for link processing and device management.

### 1. Get Video ID
`GET /tool/get-video-id`
Extract the numeric Video ID from any TikTok URL (including shortened links like vt.tiktok.com).
- **Parameters**: `url`.

### 2. Shorten Link
`POST /tool/shorten-link`
Generate a shortened TikTok link for any long URL.
- **Body**: `{ "url": "https://..." }`

### 3. Device Registration
`POST /tool/device-register`
Register a new virtual device. You can provide optional overrides for brand, model, etc., or leave it empty for a fully randomized device.
- **Parameters**: `region` (default: VN).


---

## 📦 Response Format
All responses follow a consistent JSON structure:

```json
{
  "success": true,
  "statusCode": 200,
  "message": "Operation description",
  "data": { ... },
  "error": null
}
```
