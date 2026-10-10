# ASAR

Kotlin / Jetpack Compose / Material 3. Package com.asar.app. Android 13+.

Start with SUPABASE_SETUP_RU.md. The app now requires your own Supabase project; no demo account or seeded ratings are provided.
Backend migration: backend/001_initial.sql. Transactional verification: backend/002_verify.sql.
Connection example: supabase.properties.example; put real URL and publishable key into your existing local.properties.

Architecture:
- data: models, form rules, keyword suggestions, observable app state
- network: REST/Auth transport, repository, encrypted Android Keystore session store
- ui/screens: registration, home, tasks, creation, profiles, friendship, chat
- ui/components and ui/theme: shared Material 3 components, branding, palette
- res/values, values-ru, values-kk: English, Russian and Kazakh interface
- backend: PostgreSQL schema, RLS, authenticated transactional functions

Verification on 2026-10-10:
- compileDebugKotlin: passed.
- Four core JUnit tests run using the Kotlin compiler/JUnit runner: passed.
- SQL migration and backend verification run in isolated PGlite PostgreSQL: passed.
- assembleDebug/testDebugUnitTest Gradle run blocked at processDebugResources:
  Windows AAPT2 9.4.1-15978811 crashes with 0xC0000005 during link.
  An empty manifest linked against the installed android.jar reproduces this independently of ASAR.
  No APK or emulator UI verification is claimed.
- Live Supabase Auth/SMTP and a two-device chat test need the new project configuration.

Optional isolated backend verification (Node.js):
  cd backend/tests
  npm install
  npm test

The test dependency is development-only and is not included in the Android application.
Email confirmation/recovery use a code entered in the app; configure email templates as documented.
Chat polls while open; there are no background push notifications.
