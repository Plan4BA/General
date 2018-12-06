 # Datenschutz
 - dürfen die Campus Dual-Hashs gespeichert werden
 - wenn ja, dann automatisches Löschen nach X-Tagen
 - wenn nein, dann einmaliger Abruf beim Aktualisieren
 - Prüfungstermine filtern
 - HTTPS-Zertifikat mit Let's Encrypt
# Datenstruktur
- Zuordnung von Campus Dual Benutzername zu BA bzw. Seminargruppe/Studiengang
 # Architektur/Backend
- Docker
- MySQL/Postgresql
- Datenbank abgeschottet
- Hash und Matrikelnummer verschlüsselt ablegen
- Backup-Strategie
- Erhaltung der HTTP-Sessions
# Caching
- automatische Aktualiserung der induviduellen Kalender(wenn Hash gespeichert)
# Apps
- PlayStore/iOS Appstore
- Kosten?
# TODO
- Abruf der Prüfungsangebote
- Push-Service
# Nice to have
- Link zur Evaluierungsplatform
- Verlinkung von Dozent zu Materialverzeichnis
- eigene Termine erstellen
- Lerngruppen bilden
- allgemeine Links(Modulhandbuch, Email, ...)
- NFC-Funktionalität der Mensa-Karte