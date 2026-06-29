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

## AdMob
- Usa IDs **reales** de la cuenta de AdMob del usuario (app "Tiempo minimalista" dentro de
  AdMob, nombre interno — no tiene que coincidir con el nombre público de la app):
  - App ID: `ca-app-pub-5015878857432448~7059763758` (en `AndroidManifest.xml`)
  - Ad Unit ID (banner): `ca-app-pub-5015878857432448/6686595753` (en `activity_main.xml`)
- Cuenta de pagos vinculada: AdSense (España), particular. Umbral de pago 70€/mes.
  Formulario fiscal W-8BEN aprobado (retención 0% para servicios/derechos de autor,
  válido hasta diciembre de 2029). La cuenta bancaria para cobrar Google la solicitará
  más adelante, cuando los ingresos se acerquen al umbral — no hace falta añadirla antes.
- Hasta que la app esté publicada en Play Store y pase la fase de pruebas (20 testers,
  14 días), los anuncios no generan ingresos reales aunque el banner real ya esté activo.

## Compilación
- `./gradlew assembleDebug` genera `app/build/outputs/apk/debug/app-debug.apk` (probado y
  funcionando).
- Para Play Store se necesita un AAB firmado: `./gradlew bundleRelease` con un keystore de
  firma configurado (pendiente de generar).

## Pendiente
- Generar keystore de firma para builds de release.
- Crear cuenta de Google Play Console (pago único 25$) y completar ficha de la app
  (privacidad, capturas, descripción) para publicar.
- Fase de pruebas cerrada de Play Store (20 testers, 14 días) antes de poder publicar
  en producción.
