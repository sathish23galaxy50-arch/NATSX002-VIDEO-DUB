# NATSX002 VIDEO DUB — Android PWA starter

A mobile-first, installable Progressive Web App interface for an Indian-language video dubbing workflow.

## Included
- Installable PWA shell for Android Chrome
- Video picker and local preview
- Source auto-detection and target selectors for India's 22 Scheduled Languages plus English
- Options for voice preservation, lip-sync, subtitles, background music and processing quality
- Backend URL and optional bearer-token settings
- Manifest, service worker and app icon
- GitHub Actions workflow to publish the static PWA to GitHub Pages

## Important: current capability
This repository currently contains the **front end only**. It is not yet a working AI dubbing service. Translation, speaker separation, voice cloning, speech generation and lip-sync require a separately deployed AI backend. The language list in the interface does not guarantee model availability for every language or feature. Free GPU services have quotas and may sleep or queue jobs; unlimited free processing cannot be promised.

## Backend API contract
The app sends `multipart/form-data` to `POST {BACKEND_URL}/api/dub` with:
- `video` (file)
- `source_language` (`auto` or selected language)
- `target_language`
- `voice_clone` (boolean)
- `lip_sync` (boolean)
- `subtitles` (boolean)
- `keep_music` (boolean)
- `quality` (`balanced`, `high`, `fast`)
- `notes` (optional)

Return JSON either `{"video_url":"https://.../dubbed.mp4"}` or `{"job_id":"..."}`. A production backend should also implement job status, secure temporary storage, upload limits, authentication, deletion/retention controls and a processing queue. Never put model-provider secrets in the PWA.

## Publish on GitHub Pages
1. In the repository, open **Settings → Pages**.
2. Under **Build and deployment**, set **Source** to **GitHub Actions**.
3. The included workflow deploys the site automatically after a push to `main` (or when manually started under Actions).
4. After the workflow succeeds, the site URL will be `https://sathish23galaxy50-arch.github.io/NATSX002-VIDEO-DUB/`.
5. Open that HTTPS URL in Chrome on Android. Use Chrome menu → **Install app** / **Add to Home screen**.

## Configure the AI backend
After a backend is deployed, open **AI server connection settings** in the app and enter its HTTPS base URL and optional access token. The backend must expose `POST /api/dub` with the contract above. Do not enter secrets into a public repository.

## Languages listed
Assamese, Bengali, Bodo, Dogri, Gujarati, Hindi, Kannada, Kashmiri, Konkani, Maithili, Malayalam, Manipuri (Meitei), Marathi, Nepali, Odia, Punjabi, Sanskrit, Santali, Sindhi, Tamil, Telugu, Urdu, English.

## Watermark
The app does not add its own watermark. It does not remove watermarks already present in source videos or bypass another service's export restrictions.
