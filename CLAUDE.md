# Temperatura — APK Android (WebView + AdMob)

App Android nativa que envuelve la PWA de [temperatura](https://github.com/diegohgc/temperatura)
en un WebView, igual que `diegohgc/tandas-2` hace con la app de halterofilia. Carga
`https://diegohgc.github.io/temperatura/` y añade un banner de AdMob nativo abajo para
monetización.

## Arquitectura
- Proyecto Android Studio estándar (Kotlin, Gradle Kotlin DSL).
- `MainActivity.kt`: WebView a pantalla completa cargando la PWA + `AdView` (banner) fijo
  en la parte inferior.
- Permisos `ACCESS_FINE_LOCATION` / `ACCESS_COARSE_LOCATION`: la PWA usa geolocalización del
  navegador; dentro de WebView eso requiere conceder permiso nativo de Android primero
  (gestionado en `onGeolocationPermissionsShowPrompt` + `onRequestPermissionsResult`).
- Para cambiar la funcionalidad de la app, normalmente basta con editar el repo
  `diegohgc/temperatura` (la PWA) — esta APK no necesita recompilarse salvo que cambie algo
  nativo (permisos, anuncios, icono, etc.), igual que con `tandas-2`.

## AdMob — IMPORTANTE antes de publicar
- Actualmente usa los **IDs de prueba oficiales de Google** (App ID y Ad Unit ID), tanto en
  `AndroidManifest.xml` (`com.google.android.gms.ads.APPLICATION_ID`) como en
  `activity_main.xml` (`ads:adUnitId`). Sirven para compilar y ver el banner de "Test Ad",
  pero **no generan ingresos reales**.
- Antes de publicar en Play Store:
  1. Crear cuenta en https://admob.google.com (puede vincularse a la misma cuenta de
     Google Play Console).
  2. Crear la app dentro de AdMob y un bloque de anuncios "Banner".
  3. Sustituir el App ID de prueba en `AndroidManifest.xml` y el Ad Unit ID en
     `activity_main.xml` por los reales.

## Compilación
- `./gradlew assembleDebug` genera `app/build/outputs/apk/debug/app-debug.apk` (probado y
  funcionando).
- Para Play Store se necesita un AAB firmado: `./gradlew bundleRelease` con un keystore de
  firma configurado (pendiente de generar).

## Pendiente
- Generar/elegir icono propio (actualmente reutiliza el icono genérico por defecto de
  Android Studio, copiado de `tandas-2`).
- Generar keystore de firma para builds de release.
- Sustituir IDs de prueba de AdMob por los reales.
- Crear cuenta de Google Play Console (pago único 25$) y completar ficha de la app
  (privacidad, capturas, descripción) para publicar.
