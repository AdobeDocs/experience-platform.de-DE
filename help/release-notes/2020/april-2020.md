---
title: Adobe Experience Platform – Versionshinweise April 2020
description: Versionshinweise April 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: Versionshinweise;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 58%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Donnerstag, 8. April 2020**

Neue Funktionen in Adobe Experience Platform:

* [[!DNL Intelligent Services]](#intelligent)

Aktualisierungen vorhandener Funktionen:

* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Data Governance](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services] ermöglichen es Marketing-Analysten und -Praktikern, die Leistungsfähigkeit von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen zu nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich ist. Darüber hinaus können Marketing-Experten Prognosen in Adobe Experience Cloud, Adobe Experience Platform und Anwendungen anderer Anbieter aktivieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] bietet Marketing-Experten die Möglichkeit, Kundenprognosen auf individueller Ebene mit Erläuterungen zu generieren. Mithilfe von Einflussfaktoren können [!DNL Customer AI] Ihnen sagen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Marketing-Fachleute von [!DNL Customer AI] Prognosen und Einblicken profitieren, um Kundenerlebnisse durch Bereitstellung der am besten geeigneten Angebote und Botschaften zu personalisieren. |
| [!DNL Attribution AI] | [!DNL Attribution AI] ist ein mehrere Kanäle umfassender algorithmischer Attributions-Service, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. Mit [!DNL Attribution AI] können Marketing-Fachleute die Ausgaben für Marketing und Werbung messen und optimieren, indem sie die Auswirkungen jeder individuellen Kundeninteraktion in jeder Phase der Journey des Kunden verstehen. |

**Bekannte Probleme**

* Derzeit gibt es keine bekannten Probleme.

Weitere Informationen zu [!DNL Intelligent Services] und dessen Funktionen finden Sie in der [Intelligent Services - Übersicht](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemata für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Automatische alternative Anzeigeinformationen | Der [!DNL Schema Registry] wendet automatisch die benutzerdefinierten Titel- und Beschreibungswerte an, die im `alternateDisplayInfo`-Deskriptor konfiguriert sind. |
| Skalare Feldbeschränkungen | Die [!DNL Schema Registry] lässt nicht mehr als 6.000 Skalarfelder in einem einzelnen Schema zu. |
| Performance-Überholung | Die [!DNL Schema Registry] wurde überarbeitet, um die Anforderungen der [!DNL Experience Platform] besser zu erfüllen. |

**Fehlerkorrekturen**

* Aktualisiertes XDM in XED umgewandelt, um ein saubereres XED-Format für verschachtelte URI-Felder in Standard-XDM zu unterstützen.

**Bekannte Probleme**

* Bekannt

## Data Governance {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffssteuerung für Daten bei Marketing-Aktionen.

Das Thema Data Governance erfordert ein tiefgehendes Verständnis aller für Ihre Kundendaten geltenden gesetzlichen Bestimmungen, vertraglichen Pflichten und Unternehmensrichtlinien. Anschließend lassen sich Daten mithilfe der entsprechenden Datennutzungs-Labels klassifizieren und ihre Verwendung durch Definition von Datennutzungsrichtlinien steuern.

Das Data Governance-Framework vereinfacht und optimiert die Kategorisierung von Daten und die Erstellung von Datennutzungsrichtlinien über die [!DNL Experience Platform]-Benutzeroberfläche und die [!DNL Policy Service]-API.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datennutzungsrichtlinien in der Benutzeroberfläche verwalten | Datennutzungsrichtlinien können jetzt im Arbeitsbereich **Richtlinien“ in** Benutzeroberfläche von [!DNL Experience Platform] verwaltet werden. Weiterführende Informationen finden Sie im [Benutzerhandbuch zu Richtlinien](../../data-governance/policies/user-guide.md). |

**Bekannte Probleme**

* Keine.

Weiterführende Informationen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).


## Ziele {#destinations}

In [Real-Time Customer Data Platform](../../rtcdp/overview.md) sind Ziele vorgefertigte Integrationen mit Zielplattformen, die Daten nahtlos für diese Partner aktivieren.

**Neue Ziele**

Real-Time CDP unterstützt jetzt die Datenaktivierung für über fünfzig [!DNL Experience Cloud Launch] Erweiterungen und ermöglicht so Analysen, Personalisierung und andere Anwendungsfälle. Weitere Informationen finden Sie hier:

| Dokumentation | Beschreibung |
|--- | ---|
| [Zieltypen und Kategorien](../../destinations/destination-types.md) | In diesem Artikel wird der Unterschied zwischen Verbindungen und Erweiterungen in der Real-Time CDP-Benutzeroberfläche erläutert und empfohlen, wann die einzelnen Ziele verwendet werden sollten. |
| [Experience Platform Launch-Erweiterungen](../../destinations/catalog/launch-extensions/overview.md) | Auf dieser Seite wird erläutert, was [!DNL Launch] Erweiterungen sind, es werden Anwendungsfälle für ihre Verwendung aufgelistet und Links zur Dokumentation für jede [!DNL Launch] in Real-Time CDP bereitgestellt. |

Weiterführende Informationen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung dieser Datenanfragen Ihrer Kunden unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen für den Zugriff auf und die Löschung von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Programmen stellen, was die automatische Einhaltung gesetzlicher und unternehmensinterner Datenschutzbestimmungen erleichtert.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für PDPA | Datenschutzanfragen können jetzt mit Blick auf das Datenschutzgesetz (PDPA) in Thailand erstellt und verfolgt werden. Bei Datenschutzanfragen in der API akzeptiert das `regulation`-Array nun den Wert „pdpa_tha“. |
| Namespace-Typen in der Benutzeroberfläche | Sie können jetzt im Request Builder in der [!DNL Privacy Service]-Benutzeroberfläche verschiedene Namespace-Typen angeben. Weiterführende Informationen dazu finden Sie im [Benutzerhandbuch](../../privacy-service/ui/user-guide.md). |
| Einstellung des alten Endpunkts | Der alte API-Endpunkt (`data/privacy/gdpr`) wird nicht mehr unterstützt. |

Bekannte Probleme

* Keine

Für weitere Informationen zu [!DNL Privacy Service] lesen Sie zunächst die [Übersicht über Privacy Service](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| API- und UI-Unterstützung für Datenbanken | Neue Quell-Connectoren für [!DNL Apache Spark] (in HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage] und [!DNL Hive]. |
| API- und UI-Unterstützung für protokollbasierte Anwendungen | Neue Quell-Connectoren für [!DNL Generic OData]. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
