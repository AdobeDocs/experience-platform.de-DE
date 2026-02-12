---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: eceafa1852fc7c17660263d6ef7878a3e7bd0841
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 23%

---

# Hinweise zu Vorabversionen von Adobe Experience Platform

>[!IMPORTANT]
>
>Dieses Dokument ist als **Vorschau** der Versionshinweise für den aktuellen Monat gedacht. Release-Elemente können sich ändern und in der endgültigen Version hinzugefügt oder entfernt werden.

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/latest)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: Februar 2026**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Agent Orchestrator](#agent-orchestrator)
- [Warnhinweise](#alerts)
- [Datenerfassung](#data-collection)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Abfrage-Service](#query-service)
- [Quellen](#sources)

## Agent Orchestrator {#agent-orchestrator}

Mit Agent Orchestrator können Sie KI-gestützte Agenten erstellen und bereitstellen, die Workflows automatisieren und kanalübergreifend mit Kunden interagieren können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Data Onboarding Agent | Verwenden Sie den Data Onboarding Agent, um Quellverbindungen zu konfigurieren, die Datenqualität zu validieren, eine semantische Anreicherung anzuwenden, Schemas zu überprüfen und zu validieren und die Datenaufnahme durchzuführen. Folgen Sie den Schritt-für-Schritt-Workflows für B2C- und B2B-Flüsse, überprüfen Sie erwartete Ausgaben und beheben Sie häufige Probleme. |
| Data Distiller Agent | Verwenden Sie den Data Distiller-Agenten, um SQL-Aufträge aus natürlicher Sprache zu erstellen, die SQL-Leistung zu optimieren, SQL-Fehler zu beheben, SQL-Aufträge zu planen und zu verwalten und den Auftragsstatus zu überwachen. Lesen Sie Leitplanken, erforderliche Berechtigungen und Anleitungen zur Fehlerbehebung, um loszulegen. |
| Datenerfassungsagent | Verwenden Sie den Datenerfassungsagenten, um kontextbezogene Anleitungen für komplexe Datenerfassungskonfigurationen zu erhalten und Herkunft, Abhängigkeiten und Beziehungen in Ihren Datenerfassungsobjekten durch Konversationseinblicke zu untersuchen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der Dokumentation zu [Agent Orchestrator](https://experienceleague.adobe.com/de/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Alerts] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Slack] Integration für Warnhinweise für Kunden | Sie können jetzt kundenorientierte Warnhinweise an [!DNL Slack] senden. Folgen Sie der schrittweisen Anleitung, um die [!DNL Slack]-Integration einzurichten und Warnhinweise direkt in Ihrem [!DNL Slack] Workspace zu erhalten. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [[!DNL Observability Insights] Übersicht](../observability/home.md).

## Datenerfassung {#data-collection}

Die Adobe Experience Platform-Datenerfassung bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an die Adobe Experience Platform Edge Network und andere Ziele senden können.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verwaltung der Adobe Platform Tags-Erweiterung | Verwenden Sie die neue Funktion „Erweiterungsverwaltung“, um die Erweiterungen Ihres Unternehmens hochzuladen, zu verpacken und für die Entwicklung, die private und die öffentliche Verteilung freizugeben. Suchen Sie in der Ansicht des Unternehmens der obersten Ebene nach freigegebenen privaten Erweiterungen neben Ihren eigenen Erweiterungen. Diese Funktion unterstützt Erweiterungen für Web, Edge und Mobilgeräte. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Dokumentation zur Datenerfassung](https://experienceleague.adobe.com/de/docs/experience-platform/collection/home).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [!DNL Snowflake] Batch allgemein verfügbar | Das [!DNL Snowflake] Batch-Ziel wurde auf „Allgemeine Verfügbarkeit“ verschoben. Sie können jetzt die Spalte mit der Zusammenführungsrichtlinien-ID in Ihren exportierten Daten neben vorhandenen Spalten wie Zeitstempel, Zuordnungsattribute und Zielgruppenzugehörigkeit anzeigen. |
| AES256-Verschlüsselungsunterstützung für [Amazon S3](../destinations/catalog/cloud-storage/amazon-s3.md#destination-details)-Ziele | Sie können jetzt die AES256-Verschlüsselung für Ihre Amazon S3-Exporte konfigurieren. Wählen Sie aus zwei Optionen: <ul><li>**[!UICONTROL Default]**: Experience Platform verschlüsselt Daten im Ruhezustand mit dem standardmäßigen Verschlüsselungsalgorithmus, der auf Ihrem Bucket festgelegt ist.</li><li>**[!UICONTROL SSE-S3/AES256]**: Experience Platform fügt den `s3:x-amz-server-side-encryption": "AES256`-Header zum Export hinzu und verschlüsselt Daten im Ruhezustand mit dem AES256-Algorithmus, wenn sie in S3 landen. **Diese Option hat Vorrang vor allen Standard-Verschlüsselungsalgorithmen, die Sie auf Ihrem S3-Bucket konfigurieren**.</li></ul> |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Schema-Inventarorganisation und -Suche | Die Seite zum Durchsuchen von Schemata enthält jetzt erweiterte Such- und Filterfunktionen, Inline-Aktionen und Unterstützung für benutzerdefinierte Tags und Ordner. Diese Aktualisierungen erleichtern das Auffinden, Organisieren und Verwalten von Schemata in Sandboxes und reduzieren gleichzeitig den manuellen Navigations- und Wartungsaufwand. |
| Eingeschränkte Bearbeitung für Schemata mit Datensätzen | Bearbeitungsvorgänge, die zu grundlegenden Änderungen führen, sind jetzt eingeschränkt, sobald ein Datensatz für ein Schema vorhanden ist. Wenn ein Datensatz zugeordnet ist, können Sie Felder nicht mehr umbenennen oder löschen, Felddatentypen oder -formate ändern, Identitätsdeskriptoren ändern, verwandte Felder zum Entfernen vorhandener Felder verwalten oder die zugewiesene Klasse ändern. Additive Änderungen und das Verwerfen von Feldern werden weiterhin unterstützt. |

Weitere Informationen finden Sie in der [[!DNL XDM] Übersicht](../xdm/home.md).

## Abfrage-Service {#query-service}

Der Abfrage-Service ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Data Distiller Annual Compute Reset Date Alignment (Eingeschränkte Veröffentlichung) | Die Jahresberechnungszeiten für Data Distiller werden jetzt am Jahrestag Ihres Data Distiller-Vertrags zurückgesetzt, je nachdem, wann die Lizenz erworben oder erneuert wurde. Dadurch wird die Berichterstattung zur Lizenznutzung an Ihren Vertragsbedingungen ausgerichtet und kann zu einer einmaligen Anpassung der aktuellen Nutzungswerte führen. |
| Daten-Distiller-Sitzungsverwaltung (eingeschränkte Version) | Als autorisierter Administrator können Sie aktive Sitzungen für Query Service und Data Distiller in Ihrem Unternehmen und Ihrer Sandbox über die Benutzeroberfläche anzeigen und verwalten. Verwenden Sie das Sitzungsmanagement, um inaktive Sitzungen zu identifizieren und zu beenden und so Kapazitäten freizugeben. Integrierte Sicherheitsfunktionen verhindern, dass Sie Sitzungen mit aktiven Abfragen beenden können. Die Funktion protokolliert alle Räumungsaktionen für die Prüfung und benachrichtigt die betroffenen Benutzer. Sie benötigen die Berechtigung **Abfragesessions verwalten**, um auf diese Funktion zugreifen zu können. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Query Service - Übersicht](../query-service/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Quellen**

| Quelle | Beschreibung |
| --- | --- |
| Unterstützung des Unity-Katalogs [!DNL Databricks] Quell-Connector | Der [!DNL Databricks]-Quell-Connector unterstützt jetzt den Unity-Katalog. Lesen Sie die aktualisierte [[!DNL Databricks]](../sources/connectors/databases/databricks.md)-Dokumentation , um zu erfahren, wie Sie beim Konfigurieren Ihrer Quellverbindung den Unity-Katalog verwenden. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).
