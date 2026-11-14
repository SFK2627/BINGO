BINGO LIVE — Free Multiplayer Bingo Web App
===========================================

WHAT IS INCLUDED
- index.html            : Full responsive app: Host and Player, no npm.
- qr-local.js           : Included offline QR generator (no CDN needed).
- LICENSE-qr.txt        : Open-source QR generator license notices.
- firebase-config.js    : Fill in this file once to enable Firebase Live.
- database.rules.json   : Firebase Realtime Database Security Rules.
- README-SETUP.txt      : These instructions.

FIRST: TRY THE FREE DEMO
1. Unzip this folder.
2. Double-click index.html on your computer.
3. Choose "Local demo", then click "Create Bingo Room".
4. Click "+ 12 demo guests" to simulate cards and players.
5. Press "Start Game" > "Draw Next" and try stage changes.
6. Reset Draws and verify all guest cards remain assigned.

NOTE: Multi-tab demonstration uses localStorage and may be browser-dependent
with file:// pages. Single-tab host demo is the easiest test. QR scanning
across phones DOES NOT work from a file:// path, because other phones cannot
access files stored on your computer.

TO ENABLE REAL MULTI-DEVICE PLAY (FIREBASE SPARK / FREE)
1. Sign in to https://console.firebase.google.com/ and create a project.
2. Add a Web app inside Project Settings. Copy the Web App SDK config.
3. In Firebase Console > Build > Authentication > Sign-in method:
   enable Anonymous authentication. This does not ask players for passwords.
4. In Firebase Console > Build > Realtime Database:
   create a database on the Spark plan; copy its exact databaseURL.
5. Open firebase-config.js in Notepad. Fill in apiKey, authDomain,
   databaseURL, projectId, and appId. Keep the JS syntax exactly as shown.
6. In Realtime Database > Rules: paste database.rules.json and Publish.
   Never publish open public-read/public-write rules.
7. Publish the whole extracted folder (index.html and firebase-config.js)
   on HTTPS static hosting, e.g. Cloudflare Pages direct-upload.
8. Open the HTTPS app. Select "Firebase Live" > "Create Bingo Room".
9. Share the host QR code / join link with guests. They enter a name.
10. Players receive host-assigned random cards (locked after assignment).

IMPORTANT HOST/PLAYER SETUP
- Use ONE host browser tab for a room. Keep it online to assign cards and
  validate/announce winners. If host disconnects, players can still view
  their last public state but new draws/winners pause until host reconnects.
- Players use Firebase Auth + REST polling every 2.8 sec, so 100 guests
  do not each hold a persistent Realtime Database WebSocket connection.
- This design targets 100 free guests plus one host but has not been
  load-tested at 100 real devices. Free monthly bandwidth still applies.
- The app needs internet for Firebase and its CDN browser SDKs.
- A free Firebase project is subject to Spark limits: 100 simultaneous
  persistent RTDB connections, 1 GB storage and 10 GB/month downloads.
- Firebase web apiKey is public client configuration, NOT an admin secret.
- NEVER put Firebase Admin service-account keys in this folder.
- No npm, no Node.js, no build script needed to run or deploy it.

GAME BEHAVIOR
- 75-ball classic 5x5 Bingo: B=1-15, I=16-30, N=31-45,
  G=46-60, O=61-75. Center square is FREE.
- Original cards remain unchanged after: Continue, Change Stage, End
  Event, Reopen, Reset Draws, or page refresh (same anonymous identity).
- Reset Draws clears called balls, progress MARKS and prize awards only.
  It also returns to the first prize stage. Cards stay unchanged.
- Continuous stage changes DO NOT clear called numbers or current marks.
- All existing drawn numbers count toward the next stage's pattern.
- Winner eligibility is per stage: Everyone / Never won before /
  Previous winners only. Host can configure confirmation & winner limit.
- Winner limits are "first 1 + ties", "first 3 + ties", or unlimited;
  those validated at the same draw are awarded together.
- Marking modes: AUTO marks called numbers and announces qualified
  winners; HYBRID lets guests tap while host automatically verifies;
  MANUAL requires tapped called numbers and a BINGO submission.
- Host-assigned random cards are unique within one room.
- New player joins close when the host starts; existing players can
  reconnect with the same browser's anonymous Firebase identity.

IMPORTANT SECURITY / HONEST LIMITS
- Host-only room changes and card assignment are enforced by Firebase
  Realtime Database Rules. Players can write only their own signup and
  own manual Bingo claims. Cards, draws, prize stages, winners are
  assigned or changed by the host.
- Since this is a frontend-only project, a determined attacker could
  still abuse anonymous signups or replay public requests. Do not use
  for cash gambling, high-value prizes, or security-critical contests.
- Room names are public to authenticated anonymous users with the room
  code. Avoid entering private personal information.
- Realtime Database REST polling is near-live (up to ~3 seconds delay),
  not instant simultaneous socket delivery to each phone.
- Automatic wins depend on the host browser being connected.
- All round data is stored until you manually remove it from Firebase.
  Firebase's free storage quota therefore needs occasional cleanup.

LICENSE
- BINGO LIVE application is provided as a standalone demo prototype.
- QR generation is bundled locally in qr-local.js, adapted from an
  open-source QR implementation. MIT / Apache 2.0 notices are preserved
  in qr-local.js and LICENSE-qr.txt.
