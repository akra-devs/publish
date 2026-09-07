# stillstamp Privacy Policy

Version: 1.1.0

Effective date: 2026-09-07

## 1. Operator and scope

stillstamp is operated by AkraDev Studio. Privacy questions may be sent to
help@akra.kr. This policy describes the Android production app, the planned iOS
production app, and the web distribution. The web surface is a SAMPLE experience;
it does not use the production Firebase identity, advertising, credit wallet,
or OpenAI image-generation path.

## 2. Information kept on the device

The selected original photo, editing state, postcard message, finished postcard
PNG, and local library records remain on the device unless the user explicitly
requests image generation, saving, or sharing. The message added in the editor
is composited locally and is not included in the image-generation request.
After cloud-account deletion is requested, a small local lifecycle marker is
kept so the app can finish an interrupted deletion and does not silently create
a replacement anonymous identity. It is removed when app data is cleared or the
app is uninstalled.

## 3. Information sent from the app

For the real mobile service, stillstamp starts with a screenless anonymous
Firebase identity and no signup form. A user may optionally link Google so the
same account can recover server credits and purchase benefits. Firebase
Authentication, App Check, and the selected social provider may process the
Firebase UID, provider account identifiers, email/profile information,
authentication metadata, IP address or user-agent security signals, and
app/device attestation material. The AKRA server uses the Firebase UID as its
authorization boundary and never receives the social-account password. Apple
linking may be offered separately on a supported iOS release.

When the user confirms image generation, the app makes a request-only copy of
the selected photo. It always decodes and re-encodes that copy as PNG, removes
source container metadata such as EXIF, preserves the aspect ratio, and limits
the longest edge to 768 pixels without changing the original. The request
contains that copy, a fixed service profile, Firebase credentials, an App Check
token, and an idempotency key. It does not include the local photo key, editor
message, source filename, EXIF location, or EXIF capture time.

The AWS service receives the request copy in memory and does not intentionally
store the input photo. It forwards the image and the reviewed stillstamp prompt
to OpenAI's `/v1/images/edits` API. OpenAI states that API data is not used to
train its models unless the API customer opts in. Under the default data
controls, image-edit inputs and outputs may be retained in abuse-monitoring logs
for up to 30 days. The project has not claimed that Zero Data Retention is
enabled.

The generated image is stored in a private AWS S3 bucket for retry recovery and
expires after 8 days. A generation record containing hashed request/input
references, status, model request ID, usage, and output object key expires after
7 days. These AWS result and generation records are also deleted when cloud
account deletion completes. The server credit wallet, attendance entries,
rewarded-ad receipts, purchase intents and transaction identifiers, ad-free
entitlements, and related anti-replay records have no automatic expiry while
the account remains active and are deleted with the cloud account.

For a Google Play purchase, the app and server verify the product ID, purchase
token, obfuscated account/profile binding, and transaction state with the
Google Play Developer API. AKRA does not receive complete card or payment-method
details. Purchase and refund records may be retained as needed for duplicate
grant prevention, recovery, accounting, and legal obligations.

To prevent delayed advertising callbacks or stale requests from recreating a
deleted wallet, AWS keeps a deletion fence keyed only by a SHA-256-derived
account reference. It does not contain the raw Firebase UID. The fence is
scheduled to expire after 30 days; DynamoDB may physically remove an expired
item within the following days rather than at an exact instant.

When advertising is enabled, Google Mobile Ads and Google User Messaging
Platform may process IP-derived approximate location, app launches, taps and
video views, diagnostics, advertising IDs, app-set IDs, device or account
identifiers, and consent choices for ad delivery, measurement, analytics, fraud
prevention, and privacy controls. A privacy-options entry is shown when Google
reports that it is required.

Firebase Crashlytics is integrated on Android behind the AKRA diagnostics
boundary, but upload collection is disabled because no reviewed diagnostics
consent has been granted. No diagnostic event is intentionally uploaded in the
current build. Enabling it later requires an updated policy, store declarations,
and an in-app consent path.

## 4. Permissions

Android uses the system photo picker and does not request broad photo-library
permission. Network access is used for remote configuration, anonymous
authentication, ads, the server credit wallet, and user-requested generation.
iOS declares photo-library read access for choosing one photo and add access
only for a user-requested save. A denied optional photo permission disables the
related choose or save action, not the local library.

## 5. Service providers and international processing

The service uses Google Firebase Authentication and App Check, Google Mobile
Ads and UMP, Amazon Web Services in the Seoul region, OpenAI's API, Google Play
billing, and GitHub's
Pages hosting for AKRA configuration delivery. The app verifies configuration signatures with its bundled public key before applying remote settings. Google Play
and Apple may process distribution and store activity under their own policies.
These providers may process information outside the user's country. Data in
transit is sent over HTTPS/TLS; stored AWS result objects use server-side
encryption. No security method can guarantee absolute protection.

Provider information:

- Firebase privacy: https://firebase.google.com/support/privacy
- Google privacy: https://policies.google.com/privacy
- Google Mobile Ads disclosure: https://developers.google.com/admob/android/privacy/play-data-disclosure
- OpenAI API data controls: https://developers.openai.com/api/docs/guides/your-data
- AWS privacy: https://aws.amazon.com/privacy/
- GitHub privacy: https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement

## 6. Retention, deletion, and choices

Users can delete individual postcards from the local library. Clearing app data
or uninstalling the app removes the local library and local settings. Users can
also use operating-system advertising controls and the in-app advertising
privacy entry when it is available.

The Android production path includes **Delete cloud account** on the home
screen. After confirmation, the app locks cloud features, deletes the AWS
wallet, attendance and generation records, purchase and rewarded-ad ledgers,
ad-free entitlements, and temporary generated results, and then deletes the
Firebase identity. It does not delete the user's underlying Google or Apple
account. The
operation is idempotent and resumes after interruption. Postcards saved in the
local library are deliberately not deleted and remain available on that device.

Deletion of AKRA-controlled records does not override a service provider's
independent legal, security, fraud-prevention, backup, or abuse-monitoring
retention. In particular, an OpenAI API request already accepted before deletion
may remain under the data controls described above. Questions may be sent to
help@akra.kr without attaching photos, credentials, advertising receipts, or
other unnecessary personal information. This release candidate must not be publicly distributed
until the deletion flow is verified on a signed device and the reviewed deletion and policy URLs
are published.

## 7. Children, user responsibility, and rights

stillstamp is intended for users aged 13 and over and is not a child-directed
service. Exact Google Play target-age bands remain a store review item. Users must have the right to upload
the selected photo and should obtain permission from identifiable people where
required. Depending on applicable law, users may request access, correction,
restriction, objection, portability, or deletion and may complain to the
relevant privacy authority.

## 8. Changes and contact

This policy may change when the app, providers, law, or store rules change.
Material changes and any required renewed consent will be described in the app
or on the eventual public policy page. This first release-candidate version has
no previous public version.

Contact: help@akra.kr
