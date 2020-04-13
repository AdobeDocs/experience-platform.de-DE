---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 8. April 2020
doc-type: release notes
last-update: April 13, 2020
author: ens71067
keywords: release notes;
translation-type: tm+mt
source-git-commit: c2495b463d713f85ba621a7bf687c5959ec13adb

---


# Adobe Experience Platform – Versionshinweise

## Veröffentlichungsdatum: 8. April 2020

## Data Governance

Adobe Experience Platform Data Governance ist eine Reihe von Strategien und Technologien zur Verwaltung von Kundendaten und zur Gewährleistung der Einhaltung von Vorschriften, Einschränkungen und Richtlinien für die Datenverwendung. Es spielt eine Schlüsselrolle in der Experience Platform auf verschiedenen Ebenen, wie z.B. Katalogisierung, Datennutzungsbeschriftung, Datenzugriffsrichtlinien und Zugriffskontrolle von Daten für Marketingaktionen.

Der Einstieg in die Datenverwaltung erfordert ein grundlegendes Verständnis der Vorschriften, vertraglichen Pflichten und Unternehmensrichtlinien, die für Ihre Kundendaten gelten. Von dort aus können Daten mithilfe der entsprechenden Datenverwendungsbeschriftungen klassifiziert und ihre Verwendung durch die Definition von Datenverwendungsrichtlinien gesteuert werden.

Das DULE-Framework vereinfacht und optimiert den Prozess der Kategorisierung von Daten und der Erstellung von Datenverwendungsrichtlinien über die Experience Platform-Benutzeroberfläche und die DULE Policy Service API.

### Neue Funktionen

| Funktion | Beschreibung |
| -----------| ---------- |
| Richtlinien zur Datenverwendung in der Benutzeroberfläche verwalten | Datenverwendungsrichtlinien können jetzt im Arbeitsbereich &quot; _Richtlinien_ &quot;der Experience Platform-Benutzeroberfläche verwaltet werden. Weitere Informationen finden Sie im [Richtlinien-Benutzerhandbuch](../../data-governance/policies/user-guide.md) . |

**Bekannte Probleme**

* Keine.

Weitere Informationen finden Sie in der Übersicht über die [Datenverwaltung](../../data-governance/home.md).

## Intelligente Dienste

Intelligente Dienste ermöglichen es Marketinganalysten und Praktikern, die Leistungsfähigkeit künstlicher Intelligenz und maschinelles Lernen in Anwendungsfällen mit Kundenerlebnissen zu nutzen. Auf diese Weise können Marketinganalysten mithilfe von Konfigurationen auf Unternehmensebene spezifische Prognosen für die Anforderungen einer Firma erstellen, ohne dass hierfür Fachwissen in der Datenwissenschaft erforderlich ist. Darüber hinaus können Marketingfachleute Prognosen in Adobe Experience Cloud-, Adobe Experience Platform- und Drittanbieteranwendungen aktivieren.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|---|---|
| Kunden-AI | Die Kundentechnik bietet Marketingexperten die Möglichkeit, Kundenprognosen auf individueller Ebene mit Erläuterungen zu generieren. Mithilfe von einflussreichen Faktoren kann Ihnen die Kundentraining mitteilen, was ein Kunde wahrscheinlich tun wird und warum. Darüber hinaus können Marketingexperten von den Prognosen und Einblicken der Kundenaktivität profitieren, um Kundenerlebnisse durch die Bereitstellung der am besten geeigneten Angebot und Botschaften zu personalisieren. |
| Zuordnung AI | Attribution AI ist ein algorithmischer Zuordnungsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. Mit Attribution AI können Marketingfachleute die Ausgaben für Marketing und Werbung messen und optimieren, indem sie die Auswirkungen jeder einzelnen Kundeninteraktion auf die einzelnen Phasen der Customer Journey verstehen. |

**Bekannte Probleme**

* Derzeit sind keine bekannten Probleme aufgetreten.

Weitere Informationen zu intelligenten Diensten und deren Angebot finden Sie in der Übersicht über [intelligente Dienste](../../intelligent-services/home.md).

## Privacy Service

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

## Quellen

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe von Plattformdiensten strukturieren, beschriften und verbessern können. Sie können Daten aus verschiedenen Quellen erfassen, z. B. Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Drittanbieter-Software und Ihr CRM-System.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen für verschiedene Datenanbieter einfach einrichten können. Diese Quellverbindungen ermöglichen Ihnen die Authentifizierung und Verbindung zu externen Datenspeicherung- und CRM-Diensten, die Festlegung von Zeiten für die Erfassungsausführung und die Verwaltung des Datenaufkommens.

### Neue Funktionen

| Funktion | Beschreibung |
| ------- | ----------- |
| API- und UI-Unterstützung für Datenbanken | Neue Quellanschlüsse für Apache Spark (auf HDInsights), Azurblaus Synapse Analytics, Azurblase Table Datenspeicherung, Hive (auf HDInsights) und Phoenix. |
| API- und UI-Unterstützung für zahlungsbasierte Anwendungen | Neue Quellanschlüsse für PayPal. |
| API- und UI-Unterstützung für protokollbasierte Anwendungen | Neue Quellschnittstellen für generische OData. |

### Bekannte Probleme

* Keine

For more information about sources, see the [sources overview](../../source-connectors/home.md).