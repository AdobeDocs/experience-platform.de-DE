---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise April 2023 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e29bff2b8c576f92d239bb6c855710142df8db57
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 54%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 26. April 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Datenvorbereitung](#data-prep)
- [Experience-Datenmodell](#xdm)
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen** {#dashboards-new-updated-features}

| Funktion | Beschreibung |
| --- | --- |
| Benutzerdefinierte Dashboards | Sie können jetzt **historische Daten filtern** aus Ihren Widget-Einblicken und verwenden Sie entweder aktuelle Daten oder einen benutzerdefinierten Analysezeitraum.<br>Sie können jetzt auch **vorhandene Widgets duplizieren**. Wenn Sie ein Duplikat anpassen und dessen Attribute bearbeiten, können Sie vermeiden, bei der Erstellung eines neuen, eindeutigen Widgets von Anfang an neu zu beginnen. |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen des Aufstockungszeitraums für Adobe Analytics in Nicht-Produktions-Sandboxes | Die Aufstockungszeit für Adobe Analytics in Nicht-Produktions-Sandboxes wurde auf drei Monate reduziert. Die Aufstockung für Produktions-Sandboxes bleibt nach 13 Monaten unverändert. Diese Änderung gilt nur für neue Flüsse und hat keine Auswirkungen auf bestehende Flüsse. Weitere Informationen finden Sie im Abschnitt [Übersicht über Adobe Analytics](../../sources/connectors/adobe-applications/analytics.md). |
| Neue Zuordnungsfunktion zum Konvertieren von FPID-Zeichenfolgen in ECID | Verwenden Sie die `fpid_to_ecid` -Funktion zum Konvertieren von FPID-Zeichenfolgen in ECID zur Verwendung in Experience Platform- und Experience Cloud-Anwendungen. Weitere Informationen finden Sie im [Handbuch zu Datenvorbereitungsfunktionen](../../data-prep/functions.md). |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie in der [Übersicht zur Datenvorbereitung](../../data-prep/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemas) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Umschalten zwischen Anzeigenamen | Der Schema Editor bietet jetzt einen Schalter zum Ändern zwischen den ursprünglichen Feldnamen und den für Menschen lesbareren Anzeigenamen. Diese Flexibilität ermöglicht eine verbesserte Erkennung und Bearbeitung von Feldern Ihrer Schemata. Die Anzeigenamen für Standardfeldgruppen werden systemgeneriert, können aber bei Bedarf auch über die Benutzeroberfläche angepasst werden. |

{style="table-layout:auto"}

Weitere Informationen zu XDM in Platform finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Ablauf der Profildaten | Der Ablauf der pseudonymen Profildaten ist jetzt allgemein verfügbar! Mit dieser Version werden alte pseudonyme Profile kontinuierlich aus Ihrer Experience Platform-Instanz entfernt, sobald sie aktiviert wurden. Weitere Informationen zu dieser Funktion und den Pseudonymen Profilen finden Sie im Abschnitt [Anleitung zum Ablauf von Pseudonymen Profildaten](../../profile/pseudonymous-profiles.md). |

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