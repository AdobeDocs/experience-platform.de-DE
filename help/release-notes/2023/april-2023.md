---
title: Adobe Experience Platform – Versionshinweise April 2023
description: Versionshinweise April 2023 für Adobe Experience Platform.
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 48%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 26. April 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenvorbereitung](#data-prep)
- [Quellen](#sources)

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen des Aufstockungszeitraums für Adobe Analytics in Nicht-Produktions-Sandboxes | Die Aufstockungszeit für Adobe Analytics in Nicht-Produktions-Sandboxes wurde auf drei Monate reduziert. Die Aufstockung für Produktions-Sandboxes bleibt nach 13 Monaten unverändert. Diese Änderung gilt nur für neue Flüsse und hat keine Auswirkungen auf bestehende Flüsse. Weitere Informationen finden Sie im Abschnitt [Übersicht über Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Neue Zuordnungsfunktion zum Konvertieren von FPID-Zeichenfolgen in ECID | Verwenden Sie die `fpid_to_ecid` -Funktion zum Konvertieren von FPID-Zeichenfolgen in ECID zur Verwendung in Experience Platform- und Experience Cloud-Anwendungen. Weitere Informationen finden Sie im [Handbuch zu Datenvorbereitungsfunktionen](../../data-prep/functions.md). |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie in der [Übersicht zur Datenvorbereitung](../../data-prep/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen aufnehmen und mithilfe von Platform-Services strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| API-Unterstützung zum Filtern von Daten auf Zeilenebene für Microsoft Dynamics-, Salesforce-CRM- und Salesforce-Marketing Cloud | Verwenden Sie logische Operatoren und Vergleichsoperatoren, um Daten auf Zeilenebene für die Microsoft Dynamics-, Salesforce CRM- und Salesforce-Marketing Cloud-Quellen zu filtern. Weitere Informationen finden Sie im Handbuch unter [Filtern von Daten für eine Quelle mithilfe der API](../../sources/tutorials/api/filter.md). |
| Beta-Verfügbarkeit von Shopify Streaming | Die [Streaming-Quelle kaufen](../../sources/connectors/ecommerce/shopify-streaming.md) ist jetzt als Beta verfügbar. Verwenden Sie die Streaming-Quelle Shopify , um Daten von Ihrem Konto für Shopify-Partner an Experience Platform zu streamen. |
| Allgemeine Verfügbarkeit der OneTrust-Integration | Die [OneTrust-Integrationsquelle](../../sources/connectors/consent-and-preferences/onetrust.md) ist jetzt allgemein verfügbar. Verwenden Sie die OneTrust-Integrationsquelle, um Einwilligungs- und Voreinstellungsdaten aus Ihrem OneTrust-Integrationskonto in die Experience Platform zu übertragen. |
| Allgemeine Verfügbarkeit von Oracle Service Cloud | Die [Oracle Service Cloud-Quelle](../../sources/connectors/customer-success/oracle-service-cloud.md) ist jetzt allgemein verfügbar. Verwenden Sie die Oracle Service Cloud-Quelle, um Ihre Oracle Service Cloud-Daten in die Experience Platform zu übertragen. |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
