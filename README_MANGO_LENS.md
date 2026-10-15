# MANGO LENS — Product Intelligence v1.3

Arabic-first Flutter app for identifying products from a photo, searching the web for price references, and keeping local scan history.

## What's improved
- More useful Gemini 429/quota diagnostics: the app now shows Google's original error message and available details instead of hiding them behind a generic warning.
- Settings action **Test key & load models** calls the models-list endpoint and builds a list of models that advertise `generateContent`. This does not run a generation request or consume generation output tokens; Google may still apply request/rate limits to the endpoint.
- Quota-conscious defaults: product images are resized/compressed before upload, and response-token limits are reduced for Fast and Detailed modes. There is no automatic retry loop on 429, because repeating quota-limited requests can waste requests.
- Arabic/English interface switch (Arabic is the default), light/dark theme switch, and MANGO company/founder credits in settings.
- Seller profit calculator for cost, selling price, fees and shipping. It runs locally and does not call Gemini.
- Existing product photo analysis, Google Search grounding sources, report copy, local history, market/category/condition controls remain.

## Run/build
1. Install Flutter stable (the included GitHub Actions workflow is set up to build a release APK).
2. From this folder run `flutter pub get`.
3. Run on a device with `flutter run`, or build with `flutter build apk --release`.

## Important quota note
A new API key does not reset the quota of the Google Cloud project it belongs to. If the detailed error says `RESOURCE_EXHAUSTED`, inspect the project selected in Google AI Studio, its model-specific RPM/TPM/RPD limits, billing status, and quota reset time. This app cannot increase Google's quota. The settings test is a model-list request, not a guarantee that generation quota is available.

## API key safety
This build stores the key locally on the device for personal testing. Do not ship an app to the public with a shared embedded key; a public commercial release should proxy requests through a server and enforce per-user rate limits.
