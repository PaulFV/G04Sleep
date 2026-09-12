# Play-Store-Vorbereitung

G04Sleep ist bereits als installierbare PWA vorbereitet. Für eine Veröffentlichung im Google Play Store wird zusätzlich eine Android-Verpackung benötigt, zum Beispiel als Trusted Web Activity (TWA).

## Vor dem Upload

- In `privacy.html` und `copyright.html` alle Angaben in eckigen Klammern ersetzen.
- Die Seiten unter einer dauerhaft erreichbaren HTTPS-Adresse veröffentlichen. Nach dem GitHub-Pages-Deploy lautet die Datenschutz-URL voraussichtlich `https://paulfv.github.io/G04Sleep/privacy.html`.
- Bild- und Logo-Rechte sowie die Lizenznachweise prüfen und dokumentieren.
- In der Play Console die Data-Safety-Angaben mit der tatsächlichen Konfiguration abgleichen. Das optionale Mikrofon ist sensible Gerätedaten; optionale Push-Benachrichtigungen übertragen technische Push-Daten und Weckerzeiten an den konfigurierten Dienst.
- Store-Eintrag, Altersfreigabe, Supportkontakt, Screenshots und Testzugang vervollständigen.

## TWA-Wrapper erzeugen

Mit einer aktuellen Node.js-/Java-/Android-SDK-Installation kann Bubblewrap aus dem Web-Manifest ein Android-Projekt erzeugen:

```bash
npx @bubblewrap/cli init --manifest https://paulfv.github.io/G04Sleep/manifest.json
npx @bubblewrap/cli build
```

Dabei eine endgültige, noch nicht verwendete Paket-ID wählen, zum Beispiel `com.deinname.g04sleep`, und den Release-Schlüssel sicher aufbewahren. Vor dem Upload die aktuelle Bubblewrap- und Play-Console-Anforderung für ein signiertes Android App Bundle prüfen.

## Digital Asset Links

Damit die TWA als vertrauenswürdige Vollbild-App läuft, muss nach dem Signieren eine Datei unter `/.well-known/assetlinks.json` auf der Website veröffentlicht werden. Die Vorlage liegt in `play-store/assetlinks.json.template`. Paket-ID und SHA-256-Fingerabdruck des Release-Zertifikats dürfen nicht als Platzhalter verbleiben.

## Technischer Stand im Repository

- `manifest.json` enthält Installationsmodus, Portrait-Ausrichtung, Kategorien, App-Icon und App-Shortcuts.
- `sw.js` cached die App sowie die Rechtstexte offline.
- Datenschutz- und Copyright-Links sind in „Profil“ und im App-Footer erreichbar.
- „Alle lokalen Daten löschen“ entfernt die G04Sleep-Daten im Browser und versucht, die optionale Push-Registrierung beim Dienst zu löschen.

Diese Datei ersetzt keine rechtliche Prüfung und keine Prüfung der Play-Console-Formulare.
