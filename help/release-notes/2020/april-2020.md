---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 8. April 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 5%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 8. April 2020**

Neue Funktionen in Adobe Experience Platform:
* [Intelligente Dienste](#intelligent)

Aktualisierungen vorhandener Funktionen:
* [Erlebnisdatenmodell (XDM)](#xdm)
* [Data Governance](#governance)
* [Ziele](#destinations)
* [Privacy Service](#privacy)
* [Quellen](#sources)

## Intelligente Dienste {#intelligent}

Intelligente Dienste ermöglichen es Marketinganalysten und Praktikern, die Leistungsfähigkeit künstlicher Intelligenz und maschinelles Lernen in Anwendungsfällen mit Kundenerlebnissen zu nutzen. Auf diese Weise können Marketinganalysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen einer Firma erstellen, ohne dass hierfür Fachwissen in der Datenwissenschaft erforderlich ist. Darüber hinaus können Marketingfachleute Prognosen in Adobe Experience Cloud-, Adobe Experience Platform- und Drittanbieteranwendungen aktivieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| Kunden-AI | Die Kundentechnik bietet Marketingexperten die Möglichkeit, Kundenprognosen auf individueller Ebene mit Erläuterungen zu generieren. Mithilfe von einflussreichen Faktoren kann Ihnen die Kundentraining mitteilen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Marketingexperten von den Prognosen und Einblicken der Kundenaktivität profitieren, um Kundenerlebnisse durch die Bereitstellung der am besten geeigneten Angebot und Botschaften zu personalisieren. |
| Zuordnung AI | Attribution AI ist ein algorithmischer Zuordnungsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. Mit Attribution AI können Marketingfachleute die Ausgaben für Marketing und Werbung messen und optimieren, indem sie die Auswirkungen jeder einzelnen Kundeninteraktion auf die einzelnen Phasen der Customer Journey verstehen. |

**Bekannte Probleme**

* Derzeit sind keine bekannten Probleme aufgetreten.

Weitere Informationen zu intelligenten Diensten und deren Angebot finden Sie in der Übersicht über [intelligente Dienste](../../intelligent-services/home.md).

## Erlebnis-Datenmodell (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte der Experience Platform. Das von Adobe unterstützte Experience Data Model (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten auf der Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Audiencen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Automatische alternative Anzeigeinformationen | Die Schema-Registrierung wendet automatisch die im `alternateDisplayInfo` Deskriptor konfigurierten benutzerdefinierten Titel- und Beschreibungswerte an. |
| Feldbeschränkungen skalieren | Die Schema-Registrierung erlaubt nicht mehr als 6000 skalare Felder in einem Schema. |
| Leistungsüberholung | Das Schema Registry wurde überarbeitet, um die Anforderungen der Experience Platform besser zu erfüllen. |

**Fehlerkorrekturen**

* XDM in XED umgewandelt, um ein saubereres XED-Format für verschachtelte URI-Felder in Standard-XDM zu unterstützen.

**Bekannte Probleme**

* bekannt

## Data Governance {#governance}

Adobe Experience Platform Data Governance ist eine Reihe von Strategien und Technologien zur Verwaltung von Kundendaten und zur Gewährleistung der Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung. Es spielt eine Schlüsselrolle in der Experience Platform auf verschiedenen Ebenen, wie z.B. Katalogisierung, Datennutzungsbeschriftung, Datenzugriffsrichtlinien und Zugriffskontrolle von Daten für Marketingaktionen.

Der Einstieg in die Datenverwaltung erfordert ein grundlegendes Verständnis der Vorschriften, vertraglichen Pflichten und Unternehmensrichtlinien, die für Ihre Kundendaten gelten. Von dort aus können Daten mithilfe der entsprechenden Datenverwendungsbeschriftungen klassifiziert und ihre Verwendung durch die Definition von Datenverwendungsrichtlinien gesteuert werden.

Das DULE-Framework vereinfacht und optimiert den Prozess der Kategorisierung von Daten und der Erstellung von Datenverwendungsrichtlinien über die Experience Platform-Benutzeroberfläche und die DULE Policy Service API.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Richtlinien zur Datenverwendung in der Benutzeroberfläche verwalten | Datenverwendungsrichtlinien können jetzt im Arbeitsbereich &quot; _Richtlinien_ &quot;der Experience Platform-Benutzeroberfläche verwaltet werden. Weitere Informationen finden Sie im [Richtlinien-Benutzerhandbuch](../../data-governance/policies/user-guide.md) . |

**Bekannte Probleme**

* Keine.

Weitere Informationen finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md).


## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md)sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten nahtlos an diese Partner aktivieren.

**Neue Ziele**

Adobe Echtzeit-CDP unterstützt jetzt die Aktivierung von Daten auf mehr als fünfzig Experience Cloud-Starterweiterungen, wodurch Analysen, Personalisierung und andere Anwendungsfälle ermöglicht werden. Weitere Informationen finden Sie unter:

| Dokumentation | Beschreibung |
|--- | ---|
| [Zieltypen und Kategorien](/help/rtcdp/destinations/destination-types.md) | In diesem Artikel wird der Unterschied zwischen Verbindungen und Erweiterungen in der Adobe Echtzeit-CDP-Oberfläche erläutert und empfohlen, wann diese Ziele verwendet werden. |
| [Erlebnis-Plattform-Starterweiterungen](/help/rtcdp/destinations/experience-platform-launch-extensions.md) | Auf dieser Seite werden die Funktionen von Launch-Erweiterungen, Anwendungsfälle für Listen und Links zur Dokumentation für jede Launch-Erweiterung in Adobe Echtzeit-CDP erläutert. |

Weitere Informationen finden Sie in der Übersicht über die [Ziele](/help/rtcdp/destinations/destinations-overview.md).

## Privacy Service {#privacy}

Die neuen gesetzlichen und organisatorischen Vorschriften geben den Nutzern das Recht, auf ihre personenbezogenen Daten auf Anfrage aus Ihren Datenspeichern zuzugreifen oder sie zu löschen. Der Datenschutzdienst für Adobe Experience Platform stellt eine RESTful-API und eine Benutzeroberfläche bereit, mit der Sie diese Datenanforderungen Ihrer Kunden verwalten können. Mit dem Datenschutzdienst können Sie Anfragen zum Zugriff auf und Löschen von persönlichen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| PDPA-Unterstützung | Datenschutzanforderungen können nun im Rahmen des Datenschutzgesetzes (PDPA) in Thailand erstellt und nachverfolgt werden. Bei Datenschutzanforderungen in der API akzeptiert das `regulation` Array den Wert &quot;pdpa_tha&quot;. |
| Namensraum-Typen in der Benutzeroberfläche | Sie können jetzt im Anforderungs-Builder in der Benutzeroberfläche des Datenschutzdienstes verschiedene Namensraum angeben. Weitere Informationen finden Sie im [Benutzerhandbuch](../../privacy-service/ui/user-guide.md) . |
| Alter Endpunktverfall | Der alte API-Endpunkt (`data/privacy/gdpr`) wurde nicht mehr unterstützt. |

Bekannte Probleme

* Keine

Weitere Informationen zum Datenschutzdienst finden Sie in der Übersicht über den [Datenschutzdienst](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe von Plattformdiensten strukturieren, beschriften und verbessern können. Sie können Daten aus verschiedenen Quellen erfassen, z. B. Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Drittanbieter-Software und Ihr CRM-System.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen für verschiedene Datenanbieter einfach einrichten können. Diese Quellverbindungen ermöglichen Ihnen die Authentifizierung und Verbindung zu externen Datenspeicherung- und CRM-Diensten, die Festlegung von Zeiten für die Erfassungsausführung und die Verwaltung des Datenaufkommens.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| API- und UI-Unterstützung für Datenbanken | Neue Quellanschlüsse für Apache Spark (auf HDInsights), Azurblaus Synapse Analytics, Azurblase Table Datenspeicherung, Hive (auf HDInsights) und Phoenix. |
| API- und UI-Unterstützung für zahlungsbasierte Anwendungen | Neue Quellanschlüsse für PayPal. |
| API- und UI-Unterstützung für protokollbasierte Anwendungen | Neue Quellschnittstellen für generische OData. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).
