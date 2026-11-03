<!-- Copyright © 2026 David Wright und Inviatec GmbH
     Author: David Wright <david.wright@inviatec.de>
     SPDX-License-Identifier: Apache-2.0 -->
<div align="center">

# OrbitOne Server

**Wissen, Aufgaben, Dateien und Entwicklung in einem gemeinsamen Workspace.**

[Website](https://orbitone.io) · [Downloads](https://dist.orbitone.io) · [Entwickler](https://github.com/dwrightdev) · [Kontakt](mailto:david.wright@inviatec.de)

**PHP / MySQL · Self-Hosting · Docker Compose · Source Available**

</div>

OrbitOne verbindet Seiten, persönliche Notizen, Aufgaben, Git-Repositories und
Dateien über gemeinsame Workspaces, Spaces und Berechtigungen. Ein eigener Server
gibt dir die Kontrolle über die Instanz; der Desktop-Client verbindet auf Wunsch
mehrere Server und durchsucht die jeweils erlaubten Inhalte.

## Was der Server bereitstellt

| Bereich | Möglichkeiten |
| --- | --- |
| Wissen | Hierarchische Seiten, Rich-Text-Editor, Erwähnungen, Anhänge, Diagramme und PDF-Export |
| Zusammenarbeit | Workspaces, Space-Zugriffe, Kommentare, Verknüpfungen und persönliche Favoriten |
| Dateien | Mediathek, Ordner, thematische Galerien und optionaler S3-Speicher |
| Entwicklung | Git Smart HTTP in PHP, Repositories, Versionen und Commit-Verknüpfungen |
| Erweiterungen | Separat aktivierbare Plugins und ein eigenständiges Plugin-SDK |
| Integrationen | MCP, optionale KI-Anbindung, LDAP/LDAPS, Entra und Mailversand nach Konfiguration |

Plugins lassen sich passend zum Einsatz aktivieren. Projektmanagement, DMS,
Confluence-Import, Tresor, Archiv und Vorlagen sind eigenständige Pakete; sie
werden nicht durch die bloße Installation des Servers automatisch aktiviert.

## In wenigen Schritten starten

Aktuelle, veröffentlichte Pakete findest du unter **[dist.orbitone.io](https://dist.orbitone.io)**.
Unveröffentlichte Arbeitsstände sind dort nicht automatisch verfügbar.

### PHP-/MySQL-Hosting

1. Eine eigene MySQL-/MariaDB-Datenbank samt Benutzer anlegen.
2. Das PHP-/MySQL-Upload-Paket in den Dokumentenstamm entpacken.
3. `/setup.php` öffnen und Installationscode, Datenbankzugang, URL und Administrator eintragen.
4. Den privaten Datenordner außerhalb des Webroots prüfen und gewünschte Plugins konfigurieren.

Benötigt werden PHP 8.2+, PDO MySQL, Fileinfo, zlib und OpenSSL. HTML-Verarbeitung
benötigt DOM/XML, LDAP die LDAP-Erweiterung. Die gebaute Weboberfläche und die
PHP-Abhängigkeiten liegen dem Release bei; Node.js, Composer und ein Git-Programm
sind auf dem Hosting nicht erforderlich. Apache/PHP-FPM kann die mitgelieferten
Routingregeln verwenden. Bei nginx sind Routing und Schutz des Backendordners
entsprechend einzurichten. Plesk ist eine mögliche Umgebung, keine Voraussetzung.

### Docker Compose

Das separate Docker-Paket enthält eine bereits gebaute Anwendung sowie
Dockerfile und Compose-Konfiguration für PHP/Apache und MySQL.

```sh
sh configure.sh
docker compose up -d --build
docker compose exec -T web cat /var/lib/orbitone/INSTALLATION-CODE.txt
```

Unter Windows übernimmt `./configure.ps1` die Erstellung der privaten `.env`.
Danach `http://localhost:8080/setup.php` öffnen. Der Standard bindet nur an den
lokalen Host. Für öffentlichen Betrieb HTTPS über einen Reverse Proxy einrichten
und beim Setup die endgültige HTTPS-Adresse verwenden.

## Daten bleiben deine Daten

Konfiguration, Schlüssel und lokale Dateien liegen im privaten Instanzordner.
Unter Docker wird dieser unter `/var/lib/orbitone` als benanntes Volume erhalten;
die Datenbank hat ein eigenes Volume. **Beide Volumes, den Verschlüsselungsschlüssel
und die private `.env` zusammen sichern.**

Beim Update die bestehende Konfiguration und Daten erhalten, die neue Anwendung
einspielen beziehungsweise das Image neu bauen und anschließend als Administrator
`/update.php` ausführen. `docker compose down -v` ist kein Updatebefehl: Es entfernt
Volumes. Ein Git-Push installiert keine Serverinstanz.

## Lizenzmodell

Der eigene Server ist **Source Available unter Elastic License 2.0**. Private und
Unternehmen können ihn gemäß ELv2 kostenlos intern selbst betreiben, auch auf
gemieteten Servern. Die Lizenz beschränkt bestimmte gehostete oder verwaltete
Angebote für Dritte, die Zugang zu einem wesentlichen Teil der Funktionen eröffnen.
Sie verbietet nicht pauschal jede Installationshilfe, Beratung oder Betreuung.

Der eigenständige Client und das SDK stehen unter Apache-2.0. Die öffentlichen
Plugins Projektmanagement, DMS, Confluence-Import und Tresor verwenden ELv2;
Archiv und Vorlagen Apache-2.0. Drittanbieter-Code behält seine jeweiligen
Bedingungen. Maßgeblich sind die vollständigen Lizenztexte und die Zuordnung im
jeweiligen Paket. Der gesamte Produktverbund wird nicht pauschal als
OSI-konformes Open Source bezeichnet.

Professionelles Hosting und Service können gesondert vereinbart werden. Künftige
proprietäre SaaS-Komponenten sind separat zu kennzeichnen; die Lizenz eines
Connectors gewährt keine Rechte an deren serverseitiger Implementierung.

## Entwicklung und Beiträge

Dieses README beschreibt die tatsächlichen Release-Pakete. Repository-Aufteilung
und Buildpfade müssen dem jeweiligen bestätigten Quellstand entsprechen; es werden
keine neuen Repositorys oder Dienste vorausgesetzt. Eigenständige Plugins können
frei oder kommerziell lizenziert werden. Die Apache-Vorlage verpflichtet nicht
zur Apache-Lizenzierung neuer, eigenständiger Plugins.

Beiträge übertragen keine Urheberrechte automatisch. Abweichende Rechte für
proprietäre Nutzung oder Hosting müssen, soweit erforderlich, gesondert vereinbart
werden. Die Lizenzhinweise der jeweiligen Komponenten bleiben maßgeblich.

---

**Entwickelt von David Wright · dwrightdev · Inviatec GmbH**  
Copyright © 2026 David Wright und Inviatec GmbH  
[david.wright@inviatec.de](mailto:david.wright@inviatec.de) · [inviatec.de](https://inviatec.de)

[Impressum der Projektwebsite](https://orbitone.io/impressum/) · [Datenschutz der Projektwebsite](https://orbitone.io/datenschutz/)
