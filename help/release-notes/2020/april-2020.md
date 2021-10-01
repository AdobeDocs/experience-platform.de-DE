---
title: Versionshinweise zu Adobe Experience Platform
description: Versionshinweise zu Experience Platform vom 8. April 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: Versionshinweise;
exl-id: 0f68c71e-3c9d-453b-a953-1cd1b6ca2e35
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 68%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 8. April 2020**

Neue Funktionen in Adobe Experience Platform:
* [[!DNL Intelligent Services]](#intelligent)

Aktualisierungen vorhandener Funktionen:
* [[!DNL Experience Data Model (XDM)]](#xdm)
* [[!DNL Data Governance]](#governance)
* [[!DNL Destinations]](#destinations)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)

## [!DNL Intelligent Services] {#intelligent}

[!DNL Intelligent Services]Mit können Marketing-Analysten und -Experten die Vorteile von künstlicher Intelligenz und maschinellem Lernen in Anwendungsfällen mit Kundenerlebnissen nutzen. So können Marketing-Analysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen der Firma erstellen, ohne dass hierfür Kenntnisse aus der Datenwissenschaft erforderlich ist. Darüber hinaus können Marketing-Experten Prognosen in Adobe Experience Cloud, Adobe Experience Platform und Anwendungen anderer Anbieter aktivieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| [!DNL Customer AI] | [!DNL Customer AI] bietet Marketing-Experten die Möglichkeit, Kundenprognosen auf individueller Ebene inklusive Erläuterungen zu generieren. Mithilfe von Einflussfaktoren kann [!DNL Customer AI] Ihnen mitteilen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Marketing-Experten von den Prognosen und Einblicken von [!DNL Customer AI] profitieren, um Kundenerlebnisse durch Bereitstellung der am besten geeigneten Angebote und Botschaften zu personalisieren. |
| [!DNL Attribution AI] | [!DNL Attribution AI] ist ein algorithmischer Attributionsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. Mit [!DNL Attribution AI] können Marketing-Experten die Ausgaben für Marketing und Werbung messen und optimieren, indem sie die Auswirkungen einzelner Kundeninteraktionen in einzelnen Phasen der Customer Journey untersuchen. |

**Bekannte Probleme**

* Derzeit gibt es keine bekannten Probleme.

Weitere Informationen zu [!DNL Intelligent Services] und dessen Angeboten finden Sie in der [Übersicht über intelligente Dienste](../../intelligent-services/home.md).

## [!DNL Experience Data Model] (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Automatische alternative Anzeigeinformationen | Der [!DNL Schema Registry] wendet automatisch die benutzerdefinierten Titel- und Beschreibungswerte an, die im `alternateDisplayInfo` -Deskriptor konfiguriert sind. |
| Skalare Feldbeschränkungen | [!DNL Schema Registry] lässt nicht mehr als 6000 skalare Felder in einem Schema zu. |
| Leistungsüberholung | Das [!DNL Schema Registry] wurde überarbeitet, um die Anforderungen von [!DNL Experience Platform] besser zu erfüllen. |

**Fehlerkorrekturen**

* Aktualisiertes XDM in XED umgewandelt, um ein saubereres XED-Format für verschachtelte URI-Felder in Standard-XDM zu unterstützen.

**Bekannte Probleme**

* Bekannt

## [!DNL Data Governance] {#governance}

Adobe Experience Platform [!DNL Data Governance] ist eine Reihe von Strategien und Technologien, mit denen Kundendaten verwaltet und die Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datennutzung sichergestellt wird. Er spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine Schlüsselrolle, darunter Katalogisierung, Datenherkunft, Datennutzungsbeschriftung, Datenzugriffsrichtlinien und Zugriffskontrolle auf Daten für Marketing-Aktionen.

Das Thema Data Governance erfordert ein tiefgehendes Verständnis aller für Ihre Kundendaten geltenden gesetzlichen Bestimmungen, vertraglichen Pflichten und Unternehmensrichtlinien. Anschließend lassen sich Daten mithilfe der entsprechenden Datennutzungsbezeichnungen klassifizieren und ihre Verwendung durch Definition von Datennutzungsrichtlinien steuern.

Das [!DNL Data Governance]-Framework vereinfacht und optimiert die Kategorisierung von Daten und Erstellung von Datennutzungsrichtlinien über die [!DNL Experience Platform]-Benutzeroberfläche und die [!DNL Policy Service]-API.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Datennutzungsrichtlinien in der Benutzeroberfläche verwalten | Datennutzungsrichtlinien können jetzt im Arbeitsbereich **Richtlinien** der Benutzeroberfläche von verwaltet werden.[!DNL Experience Platform] Weiterführende Informationen finden Sie im [Benutzerhandbuch zu Richtlinien](../../data-governance/policies/user-guide.md). |

**Bekannte Probleme**

* Keine.

Weiterführende Informationen finden Sie in der [Übersicht zu Data Governance](../../data-governance/home.md).


## Ziele {#destinations}

In der [ Echtzeit-Kundendatenplattform](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner auf nahtlose Weise aktivieren.

**Neue Ziele**

Die Echtzeit-Kundendatenplattform unterstützt jetzt die Aktivierung von Daten für mehr als fünfzig [!DNL Experience Cloud Launch]-Erweiterungen, wodurch Analysen, Personalisierung und andere Anwendungsfälle möglich sind. Weitere Informationen finden Sie hier:

| Dokumentation | Beschreibung |
|--- | ---|
| [Zieltypen und Kategorien](../../destinations/destination-types.md) | In diesem Artikel wird der Unterschied zwischen Verbindungen und Erweiterungen in der Benutzeroberfläche der Echtzeit-Kundendatenplattform von erläutert und empfohlen, wann die Ziele verwendet werden sollten. |
| [Experience Platform Launch-Erweiterungen](../../destinations/catalog/launch-extensions/overview.md) | Auf dieser Seite werden die [!DNL Launch]-Erweiterungen erläutert, Anwendungsfälle für ihre Verwendung aufgelistet und Links zur Dokumentation für jede [!DNL Launch]-Erweiterung in der Echtzeit-Kundendatenplattform beschrieben. |

Weiterführende Informationen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## [!DNL Privacy Service] {#privacy}

Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie diese Datenanforderungen Ihrer Kunden verwalten können. Mit [!DNL Privacy Service] können Sie Anfragen zum Zugreifen auf und Löschen von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, was die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen erleichtert.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für PDPA | Datenschutzanfragen können jetzt mit Blick auf das Datenschutzgesetz (PDPA) in Thailand erstellt und verfolgt werden. Bei Datenschutzanfragen in der API akzeptiert das `regulation`-Array nun den Wert „pdpa_tha“. |
| Namespace-Typen in der Benutzeroberfläche | Sie können jetzt im Request Builder in der [!DNL Privacy Service] -Benutzeroberfläche verschiedene Namespace-Typen angeben. Weiterführende Informationen dazu finden Sie im [Benutzerhandbuch](../../privacy-service/ui/user-guide.md). |
| Einstellung des alten Endpunkts | Der alte API-Endpunkt (`data/privacy/gdpr`) wird nicht mehr unterstützt. |

Bekannte Probleme

* Keine

Weitere Informationen zu [!DNL Privacy Service] finden Sie in der [Übersicht über Privacy Service](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von [!DNL Platform]-Diensten strukturieren, beschriften und erweitern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| API- und UI-Unterstützung für Datenbanken | Neue Quell-Connectoren für [!DNL Apache Spark] (in HDInsights), [!DNL Azure Synapse Analytics], [!DNL Azure Table Storage], [!DNL Hive] (in HDInsights) und [!DNL Phoenix]. |
| API- und UI-Unterstützung für zahlungsbasierte Anwendungen | Neue Quell-Connectoren für [!DNL PayPal]. |
| API- und UI-Unterstützung für protokollbasierte Anwendungen | Neue Quell-Connectoren für [!DNL Generic OData]. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
