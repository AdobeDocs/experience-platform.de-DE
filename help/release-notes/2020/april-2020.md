---
title: Adobe Experience Platform - Versionshinweise, April 2020
description: Die Versionshinweise für Adobe Experience Platform vom April 2020.
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: Versionshinweise;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 67%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 8. April 2020**

Neue Funktionen in Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Aktualisierungen vorhandener Funktionen:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [Data Governance](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services]Mit können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich ist. Darüber hinaus können Marketing-Experten Prognosen in Adobe Experience Cloud, Adobe Experience Platform und Anwendungen anderer Anbieter aktivieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] bietet Marketing-Experten die Möglichkeit, Kundenprognosen auf individueller Ebene inklusive Erläuterungen zu generieren. Mithilfe von Einflussfaktoren [!DNL Customer AI] kann Ihnen mitteilen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Marketing-Experten von [!DNL Customer AI] Prognosen und Einblicke zur Personalisierung von Kundenerlebnissen durch Bereitstellung der am besten geeigneten Angebote und Botschaften. |
| [!DNL Attribution AI] | [!DNL Attribution AI] ist ein algorithmischer Attributionsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. Mit [!DNL Attribution AI] können Marketing-Experten die Ausgaben für Marketing und Werbung messen und optimieren, indem sie die Auswirkungen einzelner Kundeninteraktionen in einzelnen Phasen der Customer Journey untersuchen. |

**Bekannte Probleme**

* Derzeit gibt es keine bekannten Probleme.

Weitere Informationen finden Sie unter [!DNL Intelligent Services] und was sie anbieten muss, siehe [Übersicht über Intelligent Services](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Automatische alternative Anzeigeinformationen | Die [!DNL Schema Registry] wendet automatisch die benutzerdefinierten Titel- und Beschreibungswerte an, die in der `alternateDisplayInfo` Deskriptor. |
| Skalare Feldbeschränkungen | Die [!DNL Schema Registry] erlaubt nicht mehr als 6000 skalare Felder in einem Schema. |
| Leistungsüberholung | Die [!DNL Schema Registry] wurde überarbeitet, um die Anforderungen von [!DNL Experience Platform] besser. |

**Fehlerkorrekturen**

* Aktualisiertes XDM in XED umgewandelt, um ein saubereres XED-Format für verschachtelte URI-Felder in Standard-XDM zu unterstützen.

**Bekannte Probleme**

* Bekannt

## Data Governance {#governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffssteuerung für Daten bei Marketing-Aktionen.

Das Thema Data Governance erfordert ein tiefgehendes Verständnis aller für Ihre Kundendaten geltenden gesetzlichen Bestimmungen, vertraglichen Pflichten und Unternehmensrichtlinien. Anschließend lassen sich Daten mithilfe der entsprechenden Datennutzungsbezeichnungen klassifizieren und ihre Verwendung durch Definition von Datennutzungsrichtlinien steuern.

Das Data Governance-Framework vereinfacht und optimiert den Prozess der Datenkategorisierung und Erstellung von Datennutzungsrichtlinien mithilfe der [!DNL Experience Platform] Benutzeroberfläche und [!DNL Policy Service] API.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datennutzungsrichtlinien in der Benutzeroberfläche verwalten | Datennutzungsrichtlinien können jetzt im Arbeitsbereich **Richtlinien** der Benutzeroberfläche von verwaltet werden.[!DNL Experience Platform] Weiterführende Informationen finden Sie im [Benutzerhandbuch zu Richtlinien](../../data-governance/policies/user-guide.md). |

**Bekannte Probleme**

* Keine.

Weiterführende Informationen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).


## Ziele {#destinations}

In [Real-time Customer Data Platform](../../rtcdp/overview.md), sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner nahtlos aktivieren.

**Neue Ziele**

Real-Time CDP unterstützt jetzt die Datenaktivierung auf über 50 [!DNL Experience Cloud Launch] Erweiterungen, die Analyse, Personalisierung und andere Anwendungsfälle ermöglichen. Weitere Informationen finden Sie hier:

| Dokumentation | Beschreibung |
|--- | ---|
| [Zieltypen und Kategorien](../../destinations/destination-types.md) | In diesem Artikel wird der Unterschied zwischen Verbindungen und Erweiterungen in der Real-Time CDP-Benutzeroberfläche erläutert und empfohlen, wann diese Ziele verwendet werden. |
| [Experience Platform Launch-Erweiterungen](../../destinations/catalog/launch-extensions/overview.md) | Auf dieser Seite erfahren Sie, was [!DNL Launch] Erweiterungen sind, listet Anwendungsfälle für die Verwendung auf und verlinkt zu jedem [!DNL Launch] -Erweiterung in Real-Time CDP. |

Weiterführende Informationen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie diese Datenanforderungen Ihrer Kunden verwalten können. Mit [!DNL Privacy Service]können Sie Anfragen zum Zugriff auf und zur Löschung von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, was die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen erleichtert.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für PDPA | Datenschutzanfragen können jetzt mit Blick auf das Datenschutzgesetz (PDPA) in Thailand erstellt und verfolgt werden. Bei Datenschutzanfragen in der API akzeptiert das `regulation`-Array nun den Wert „pdpa_tha“. |
| Namespace-Typen in der Benutzeroberfläche | Sie können jetzt verschiedene Namespace-Typen im Anforderungs-Builder im [!DNL Privacy Service] Benutzeroberfläche. Weiterführende Informationen dazu finden Sie im [Benutzerhandbuch](../../privacy-service/ui/user-guide.md). |
| Einstellung des alten Endpunkts | Der alte API-Endpunkt (`data/privacy/gdpr`) wird nicht mehr unterstützt. |

Bekannte Probleme

* Keine

Weitere Informationen finden Sie unter [!DNL Privacy Service]Bitte lesen Sie zunächst [Übersicht über Privacy Service](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten strukturieren, beschriften und erweitern, indem es [!DNL Platform] Dienste. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| API- und UI-Unterstützung für Datenbanken | Neue Quell-Connectoren für [!DNL Apache Spark] (auf HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (auf HDInsights) und [!DNL Phoenix]. |
| API- und UI-Unterstützung für zahlungsbasierte Anwendungen | Neue Quell-Connectoren für [!DNL PayPal]. |
| API- und UI-Unterstützung für protokollbasierte Anwendungen | Neue Quell-Connectoren für [!DNL Generic OData]. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
