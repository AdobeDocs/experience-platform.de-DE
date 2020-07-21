---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zu Experience Platform vom 8. April 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 64%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 8. April 2020**

Neue Funktionen in Adobe Experience Platform:
* [!DNL Intelligent Services](#intelligent)

Aktualisierungen vorhandener Funktionen:
* [!DNL Experience Data Model (XDM)](#xdm)
* [!DNL Data Governance](#governance)
* [!DNL Destinations](#destinations)
* [!DNL Privacy Service](#privacy)
* [!DNL Sources](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services]Mit können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsbeispielen mit Kundenerlebnissen nutzen. So erhalten Marketing-Analysten die Möglichkeit, mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für den Bedarf einer Firma erstellen, ohne Fachwissen aus dem Bereich Data Science zu benötigen. Darüber hinaus können Marketing-Experten Prognosen in Adobe Experience Cloud, Adobe Experience Platform und Anwendungen anderer Anbieter aktivieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] bietet Marketing-Experten die Möglichkeit, Kundenprognosen auf individueller Ebene inklusive Erläuterungen zu generieren. With the help of influential factors, [!DNL Customer AI] can tell you what a customer is likely to do and why. Additionally, marketers can benefit from [!DNL Customer AI] predictions and insights to personalize customer experiences by serving the most appropriate offers and messaging. |
| [!DNL Attribution AI] | [!DNL Attribution AI] ist ein algorithmischer Attributionsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. With [!DNL Attribution AI], marketers can measure and optimize marketing and advertising spend by understanding the impact of every individual customer interaction across each phase of the customers’ journeys. |

**Bekannte Probleme**

* Derzeit gibt es keine bekannten Probleme.

For more information on [!DNL Intelligent Services] and what it has to offer, see the [Intelligent Services overview](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardization and interoperability are key concepts behind [!DNL Experience Platform]. [!DNL Experience Data Model]Das von Adobe unterstützte  (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Automatische alternative Anzeigeinformationen | The [!DNL Schema Registry] automatically applies the customized title and description values configured in the `alternateDisplayInfo` descriptor. |
| Skalare Feldbeschränkungen | The [!DNL Schema Registry] does not allow more than 6000 scalar fields in a single schema. |
| Leistungsüberholung | The [!DNL Schema Registry] has been overhauled to perform and meet the demands of [!DNL Experience Platform] better. |

**Fehlerkorrekturen**

* Aktualisiertes XDM in XED umgewandelt, um ein saubereres XED-Format für verschachtelte URI-Felder in Standard-XDM zu unterstützen.

**Bekannte Probleme**

* Bekannt

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

Die ersten Schritte mit Data Governance setzen ein grundlegendes Verständnis der Vorschriften, vertraglichen Pflichten und Unternehmensrichtlinien voraus, die für Ihre Kundendaten gelten. Anschließend lassen sich Daten mithilfe der entsprechenden Datennutzungsbezeichnungen klassifizieren und ihre Verwendung durch Definition von Datennutzungsrichtlinien steuern.

The DULE framework simplifies and streamlines the process of categorizing data and creating data usage policies through the [!DNL Experience Platform] user interface and DULE [!DNL Policy Service] API.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datennutzungsrichtlinien in der Benutzeroberfläche verwalten | Datennutzungsrichtlinien können jetzt im Arbeitsbereich _Richtlinien_ der Benutzeroberfläche von verwaltet werden. [!DNL Experience Platform] Weiterführende Informationen finden Sie im [Benutzerhandbuch zu Richtlinien](../../data-governance/policies/user-guide.md). |

**Bekannte Probleme**

* Keine.

Weiterführende Informationen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).


## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

Adobe Real-time CDP now supports data activation to over fifty [!DNL Experience Cloud Launch] extensions, enabling analytics, personalization, and other use cases. Weiterführende Informationen finden Sie unter:

| Dokumentation | Beschreibung |
|--- | ---|
| [Zieltypen und Kategorien](/help/rtcdp/destinations/destination-types.md) | In diesem Artikel wird der Unterschied zwischen Verbindungen und Erweiterungen in der Benutzeroberfläche der Adobe Echtzeit-Kundendatenplattform erläutert und empfohlen, welches Ziel wann verwendet werden sollte. |
| [Experience Platform Launch-Erweiterungen](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | This page explains what [!DNL Launch] extensions are, lists use cases for using them, and links to documentation for each [!DNL Launch] extension in Adobe Real-time CDP. |

Weiterführende Informationen finden Sie in der [Übersicht zu Zielen](/help/rtcdp/destinations/destinations-overview.md).

## [!DNL Privacy Service] {#privacy}

Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen. Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface to help you manage these data requests from your customers. With [!DNL Privacy Service], you can submit requests to access and delete private or personal customer data from Adobe Experience Cloud applications, facilitating automated compliance with legal and organizational privacy regulations.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| PDPA-Unterstützung | Datenschutzanfragen können nun im Rahmen des thailändischen Personal Data Protection Act (PDPA) gestellt und verfolgt werden. Bei Datenschutzanfragen in der API akzeptiert das `regulation`-Array nun den Wert „pdpa_tha“. |
| Namespace-Typen in der Benutzeroberfläche | You can now specify different namespace types in the Request Builder in the [!DNL Privacy Service] UI. Weiterführende Informationen dazu finden Sie im [Benutzerhandbuch](../../privacy-service/ui/user-guide.md). |
| Einstellung des alten Endpunkts | Der alte API-Endpunkt (`data/privacy/gdpr`) wird nicht mehr unterstützt. |

Bekannte Probleme

* Keine

For more information about [!DNL Privacy Service], please start by reading the [Privacy Service overview](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten lassen sich aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, damit Sie für verschiedene Datenanbieter bequem Quellverbindungen einrichten können. Diese Quellverbindungen ermöglichen Ihnen das Authentifizieren und Verbinden mit externen Speichersystemen und CRM-Diensten, das Festlegen von Zeiten für Erfassungsläufe und das Verwalten des Datendurchsatzes bei der Erfassung.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| API- und UI-Unterstützung für Datenbanken | Neue Quellanschlüsse für [!DNL Apache Spark] (auf HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (auf HDInsights) und [!DNL Phoenix]. |
| API- und UI-Unterstützung für zahlungsbasierte Anwendungen | Neue Quell-Connectoren für [!DNL PayPal]. |
| API- und UI-Unterstützung für protokollbasierte Anwendungen | Neue Quell-Connectoren für [!DNL Generic OData]. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
