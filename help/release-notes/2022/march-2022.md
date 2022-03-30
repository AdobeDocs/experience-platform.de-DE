---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: 04d35137a301492794ab8c0c67183cf5c76f2105
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 30%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 30. März 2022**

Neue Funktionen in Adobe Experience Platform:

- [Auditprotokolle](#audit-logs)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Experience-Datenmodell (XDM)](#xdm)
- [[!DNL Query Service]](#query-service)
- [Quellen](#sources)

## Auditprotokolle {#audit-logs}

Mit Experience Platform können Sie die Benutzeraktivität für verschiedene Dienste und Funktionen überprüfen. Die Prüfprotokolle enthalten Informationen darüber, wer wann was getan hat.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Prüfprotokolle für Datensatz, Schema, Klasse, Feldergruppe, Datentyp, Sandbox, Ziel, Segment, Zusammenführungsrichtlinie, berechnetes Attribut, Produktprofil und Konto (Adobe) | Dies sind die Ressourcen, die von Prüfprotokollen aufgezeichnet werden. Wenn die Funktion aktiviert ist, werden die Prüfprotokolle automatisch erfasst, sobald eine Aktivität stattfindet. Sie müssen die Protokollerfassung nicht manuell aktivieren. |
| Audit-Protokolle exportieren | Die Prüfprotokolle können als `CSV` oder `JSON` -Datei. Die erzeugten Dateien werden direkt auf Ihrem Computer gespeichert. |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Auditprotokollen in Platform finden Sie im Abschnitt [Übersicht über Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlch können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Warnhinweisregeln | Für Quellen, die mit der Datenerfassung in Verbindung stehen, stehen nun zwei neue Warnhinweisregeln zur Verfügung. Die aktualisierte Liste der Warnhinweistypen finden Sie in der Übersicht zu [Warnhinweisregeln](../../observability/alerts/rules.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnhinweise – Übersicht](../../observability/alerts/overview.md).

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere [!DNL dashboards] mit dem Sie wichtige Informationen zu den Daten Ihres Unternehmens anzeigen können, wie sie bei täglichen Momentaufnahmen erfasst werden.

### Profil-Dashboards

Im Dashboard &quot;Profile&quot;wird eine Momentaufnahme der Attributdaten (Datensatzdaten) angezeigt, die Ihr Unternehmen im Profilspeicher in der Experience Platform hat.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Widget &quot;Nicht segmentierte Profile&quot; | Das Widget stellt die Gesamtanzahl aller Profile bereit, die an kein Segment angehängt sind. Die generierte Zahl ist ab der letzten Momentaufnahme korrekt und stellt die Möglichkeit zur Profilaktivierung in Ihrer gesamten Organisation dar. Siehe [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets) für weitere Informationen. |
| Trend-Widget &quot;Nicht segmentierte Profile&quot; | Dieses Widget bietet eine grafische Darstellung der Anzahl der Profile, die in einem bestimmten Zeitraum nicht an ein Segment angehängt sind. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Siehe [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets) für weitere Informationen. |
| Nicht segmentierte Profile nach Identity Widget | Dieses Widget kategorisiert die Gesamtzahl der nicht segmentierten Profile anhand ihrer eindeutigen Kennung. Die Daten werden in einem Balkendiagramm visualisiert. Siehe [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets) für weitere Informationen. |
| Widget &quot;Einzelidentitätsprofile&quot; | Dieses Widget gibt einen Überblick über die Profile Ihrer Organisation, die nur über einen ID-Typ verfügen, der ihre Identität erstellt, entweder eine E-Mail oder eine ECID. Siehe [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets) für weitere Informationen. |

Weiterführende Informationen zu Profil-Dashboards finden Sie im Abschnitt [Profil-Dashboards - Übersicht](../../dashboards/guides/profiles.md).

### Ziele-Dashboards

Das Dashboard Ziele zeigt eine Momentaufnahme der Ziele an, die Ihr Unternehmen in Experience Platform aktiviert hat.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Widget zur Zielanzahl | Das Widget stellt die Gesamtzahl der verfügbaren Endpunkte bereit, an denen eine Zielgruppe im System aktiviert und bereitgestellt werden kann. Diese Zahl umfasst sowohl aktive als auch inaktive Ziele. Siehe [Dokumentation zum Standard-Widget für Ziele](../../dashboards/guides/destinations.md#standard-widgets) für weitere Informationen. |

Weiterführende Informationen zu Ziel-Dashboards in Platform finden Sie im Abschnitt [Ziele-Dashboards - Übersicht](../../dashboards/guides/destinations.md).

## Experience-Datenmodell (XDM) {#xdm}

Experience-Datenmodell (XDM) ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

| Funktion | Beschreibung |
| --- | --- |
| Hinzufügen oder Entfernen einzelner Standardfelder für ein Schema | Mit der Benutzeroberfläche des Schema-Editors können Sie nun Teile von Standardfeldgruppen zu Ihren Schemas hinzufügen und so mehr Flexibilität für die Felder bieten, die Sie einbeziehen möchten, ohne dass Sie benutzerdefinierte Ressourcen von Grund auf neu erstellen müssen.<br><br>Sie können jetzt auch benutzerdefinierte Ad-hoc-Felder direkt in der Schemastruktur definieren und sie einer neuen oder vorhandenen benutzerdefinierten Feldergruppe zuweisen, ohne die Feldergruppe zuvor erstellen oder bearbeiten zu müssen.<br><br>Siehe Handbuch unter [Erstellen und Bearbeiten von Schemata in der Benutzeroberfläche](../../xdm/ui/resources/schemas.md) für weitere Informationen zu diesen neuen Workflows. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu XDM in Platform finden Sie unter [XDM-System - Übersicht](../../xdm/home.md).

## Abfrage-Service {#query-service}

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| `table_exists` | Mit dem Befehl &quot;Neue Funktion&quot;wird bestätigt, ob im System derzeit eine Tabelle vorhanden ist. Der Befehl gibt einen booleschen Wert zurück: `true` , wenn die Tabelle **does** vorhanden und `false` , wenn die Tabelle **not** existieren. Siehe [SQL-Syntaxdokumentation](../../query-service/sql/syntax.md) für weitere Informationen. |

Weitere Informationen zu den verfügbaren Funktionen finden Sie im Abschnitt [Query Service - Übersicht](../../query-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Speichersystemen und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und die Datenerfassung überall verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Quellen für die B2B-Nutzung verfügbar | Sie können jetzt alle verfügbaren Quellen in Platform für B2B-Anwendungsfälle verwenden. Siehe [Quellkatalog](../../sources/home.md) für eine vollständige Liste der verfügbaren Quellen. |
| Allgemeine Verfügbarkeit neuer [!DNL Oracle Eloqua] source | Sie können jetzt die [!DNL Oracle Eloqua] -Quelle, um Daten aus Ihrem [!DNL Oracle Eloqua] -Instanz (Konto, Kampagne, Kontakte) zu Platform. Weitere Informationen finden Sie in der Dokumentation unter [Erstellen einer [!DNL Oracle Eloqua] Quellverbindung](../../sources/connectors/oracle-eloqua.md) für weitere Informationen. |
| API-Verbesserungen für [!DNL Data Landing Zone] | Die [!DNL Data Landing Zone] -Quelle unterstützt jetzt die automatische Erkennung von Dateieigenschaften bei Verwendung der [!DNL Flow Service] API. Weitere Informationen finden Sie in der Dokumentation unter [Erstellen einer [!DNL Data Landing Zone] Quellverbindung](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
