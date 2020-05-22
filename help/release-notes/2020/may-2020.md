---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 13. Mai 2020
doc-type: release notes
last-update: May 13, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: db3acec75c24a0cb75d1d88e7aa2171e794abc4f
workflow-type: tm+mt
source-wordcount: '1299'
ht-degree: 7%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 13. Mai 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Aktualisierungen der Benutzeroberfläche](#ux)
- [Data Science-Arbeitsbereich](#dsw)
- [Ziele](#destinations)
- [Experience Platform Web SDK und Experience Platform Edge Network](#edge)
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

## Aktualisierungen der Benutzeroberfläche {#ux}

Adobe Experience Platform veröffentlicht Updates für die Domäne und Kopfzeilenleiste, um Ihr Erlebnis zu verbessern und die Verbindung mit anderen Experience Cloud-Anwendungen herzustellen.

- Einfacherer Wechsel zwischen Ihren Organisationen oder zu einer anderen Anwendung
- Verbesserte Hilfe für Benutzer, einschließlich Artikel und kontextbezogene Dokumentation im Hilfemenü
- Möglichkeit, Feedback über die Plattform und die Support-Tickets für Dateien zu geben

Die Einführung des neuen Erlebnisses erfolgt schrittweise. Sie können das Erlebnis unter [https://experience.adobe.com/platform](https://experience.adobe.com/platform)Ansicht haben.

## Data Science-Arbeitsbereich {#dsw}

Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Der Data Science Workspace ist in die Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen mithilfe Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen. Data Science Workspace erreicht dies unter anderem durch den Einsatz von JupyterLab. JupyterLab ist eine webbasierte Benutzeroberfläche für <a href="https://jupyter.org/" target="_blank">Project Jupyter</a> und ist eng in die Adobe Experience Platform integriert. Es bietet eine interaktive Entwicklungs-Umgebung für Datenwissenschaftler, die mit Jupyter-Notebooks, -Codes und -Daten arbeiten können.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| JupyterLab Launcher | Der JupyterLab Launcher enthält jetzt Starter für Spark 2.4 Notebooks. Spark 2.3 Notebook-Starter werden jetzt als veraltet markiert und in einer späteren Version entfernt. |
| Spark 2.4 | Neue Scala- (Spark-) und PySpark-Rezepte verwenden jetzt Spark 2.4. |
| Kernels | Scala (Spark) Notebooks werden jetzt über den Scala Kernel verfasst. PySpark Notebooks werden jetzt über den Python Kernel verfasst. Der Spark- und PySpark-Kernel sind veraltet und sollen in einer nachfolgenden Version entfernt werden. |
| Rezepte | Neue PySpark- und Spark-Rezepte folgen jetzt dem Docker-Arbeitsablauf ähnlich Python- und R-Rezepten. |

Weitere Informationen zur Migration Ihrer Notebooks und Rezepte auf Spark 2.4 finden Sie im Handbuch zur Migration von [Notebooks](../../data-science-workspace/recipe-notebook-migration.md). Weitere allgemeine Informationen zum Data Science Workspace finden Sie in der [Übersichtsdokumentation](../../data-science-workspace/home.md).

## Ziele {#destinations}

In der [Adobe Echtzeit-Kundendatenplattform](../../rtcdp/overview.md)sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten nahtlos an diese Partner aktivieren.

**Facebook**

Adobe Echtzeit-CDP unterstützt jetzt die Aktivierung von Daten auf Facebook, sodass Sie Profil für Ihre Facebook-Kampagnen aktivieren können, um Audiencen-Targeting, Personalisierung und Unterdrückung auf Basis von Hash-E-Mails zu ermöglichen.

Weitere Informationen zu den neuen Funktionen finden Sie auf der [Facebook-Zielseite](/help/rtcdp/destinations/facebook-destination.md) .

<br> 

**Amazon Kinesis und Azurblase Ereignis Hubs Streaming Cloud Datenspeicherung Ziele**

Adobe Echtzeit-CDP unterstützt jetzt die Aktivierung von Daten in Streaming-Cloud-Datenspeicherung-Ziele, sodass Sie Audiencen- und Ereignisse im JSON-Format an diese Ziele exportieren können. Anschließend können Sie die Geschäftslogik über diesen Ereignissen in Ihren Zielen beschreiben. Weitere Informationen finden Sie unter:

>[!NOTE]
>
>Die CDP-Dateien [!DNL Amazon Kinesis] und die [!DNL Azure Event Hubs] Ziele in Adobe Echtzeit sind derzeit in der Betaphase. Dokumentation und Funktionalität können sich ändern.

| Dokumentation | Beschreibung |
|--- | ---|
| [(Beta) Amazon Kinesis-Ziel](/help/rtcdp/destinations/amazon-kinesis-destination.md) | In diesem Artikel wird beschrieben, wie Sie eine ausgehende Echtzeitverbindung zu Ihrer [!DNL Amazon Kinesis] Datenspeicherung erstellen, um Daten von Adobe Experience Platform zu streamen. |
| [(Beta) Azurblauer Ereignis Hubs-Ziel](/help/rtcdp/destinations/azure-event-hubs-destination.md) | In diesem Artikel wird beschrieben, wie Sie eine ausgehende Echtzeitverbindung zu Ihrer [!DNL Azure Event Hubs] Datenspeicherung erstellen, um Daten von Adobe Experience Platform zu streamen. |
| [API-Lernprogramm - Verbindungen zu Streaming-Zielen herstellen und Daten aktivieren](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md) | In diesem Lernprogramm wird gezeigt, wie Sie mit API-Aufrufen eine Verbindung zu Ihren Adobe Experience Platform-Daten herstellen, eine Verbindung zu einem Streaming Cloud-Datenspeicherung-Ziel herstellen (Amazon Kinesis oder Azurblauer Ereignis-Hubs), einen Datenfluss zu Ihrem neu erstellten Ziel erstellen und Daten an Ihr neu erstelltes Ziel aktivieren können. |

Weitere Informationen finden Sie in der Übersicht über die [Ziele](/help/rtcdp/destinations/destinations-overview.md).

## Experience Platform Web SDK und Experience Platform Edge Network {#edge}

Das Experience Platform Web SDK und Experience Platform Edge Network ermöglichen es Benutzern, Daten für Endbenutzer und Browser an die Adobe Experience Platform und andere Adobe-Lösungen in Echtzeit zu senden. Die aktuellste Liste der Anwendungsfälle finden Sie in unserem häufig aktualisierten [Fahrplan](https://github.com/adobe/alloy/projects/5) .

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| ECID-Unterstützung | Das SDK unterstützt standardmäßig ECID ohne zusätzliche Bibliotheken oder Informationen zur Installation |
| Konfigurationsoberfläche | Verwalten Sie Ihre Konfigurations-ID-Einstellungen mit der neuen Benutzeroberfläche für die Edge-Konfiguration in Launch, muss auf die Positivliste gesetzt sein, um Zugriff zu erhalten |
| Adobe Experience Platform Web SDK Mixin | Eine Mischung zur Verwendung mit dem Experience Platform Web SDK, die alle unterstützten Felder umfasst. |
| Einwilligungseinstellungen des Kurses | Bietet Firmen die Kontrolle über die Teilnahme am Experience Platform Web SDK |
| Clientseitige Debugging-Unterstützung in der neuen Experience Cloud Debugger-Erweiterung | Sehen Sie sich Anforderungen des Experience Platform Web SDK sowie Edge Traces an, um zu sehen, wie Daten durch das System fließen. |
| Adobe Analytics | Senden von Daten über die Edge-Konfiguration an Analytics-Report Suites XDM wird in Kontextdaten reduziert, unterstützt Multi-Suite-Tagging |
| Adobe Target | Support für Adobe Zielgruppe. Einschließlich VEC, Form-Based Composer, A/B, XT, Automatisierte Personalisierung, MVT |
| Adobe Audience Manager-Support | Unterstützung für Audience Manager-ID-Syncs, URL-Ziele und Cookie-Ziele |
| Identitätssynchronisierung | Umbenannt `setCustomersIds` in `syncIdentity` klarer |
| XDM Object Builder | In der Starterweiterung können Sie jetzt XDM-Objekte als Datenelemente erstellen |

Weitere Informationen zu Platform Web SDK und Edge Network finden Sie in der [Dokumentation](../../edge/home.md).

## Echtzeit-Kundenprofil {#profile}

Mit der Adobe Experience Platform können Sie koordinierte, konsistente und relevante Erlebnisse für Ihre Kunden bereitstellen, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Mit Echtzeit-Kundendaten können Sie eine ganzheitliche Ansicht jedes einzelnen Profils anzeigen, die Daten aus mehreren Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieterdaten, kombiniert. Mit dem Profil können Sie Ihre unterschiedlichen Kundendaten in einer einheitlichen Sicht zusammenfassen, die ein umsetzbares Konto mit Zeitstempel für jede Kundeninteraktion bietet.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Neue Profil-Exportmetriken | Es wurden Metriken zu Exportaufträgen für Profile hinzugefügt, die die Gesamtzahl der exportierten Profil und die Anzahl der Profil in jedem Namensraum anzeigen. |
| Neue Metriken zur Beobachtbarkeit | Die Insight-API für die Observability Insights-Funktion verfügt jetzt über die folgenden Metriken für die Streaming-Erfassung in Profil: Eingehende Anforderungsrate, Erfolgreiche Ingestion-Rate, Aufgenommene Datensatzgröße. |
| Massen-GET-Endpunkt | Es wurde ein Massen-GET-Endpunkt zur Echtzeit-Kunden-Profil-API hinzugefügt, um das Abrufen mehrerer Ergebnisse in einem einzigen API-Aufruf zu ermöglichen. Für Segmentdefinitionen, Segmentaufträge und Zusammenführungsrichtlinien können Sie jetzt eine Massen-GET-Datei mit bis zu 100 IDs erstellen. |
| Profil nach Identität durchsuchen | In der Plattform-Benutzeroberfläche können Sie jetzt einen Identitäts-Namensraum auswählen und einen Identitätswert angeben, um ein Profil zu durchsuchen. |

**Fehlerkorrekturen**

- Keine.

**Bekannte Probleme**

- Keine.

Weitere Informationen zum Echtzeit-Profil von Kunden, einschließlich Übungen und Best Practices für die Arbeit mit Profil-Daten, finden Sie in der Übersicht über das [Echtzeit-Kundenerlebnis](../../profile/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe von Plattformdiensten strukturieren, beschriften und verbessern können. Sie können Daten aus verschiedenen Quellen erfassen, z. B. Adobe-Anwendungen, Cloud-basierte Datenspeicherung, Drittanbieter-Software und Ihr CRM-System.

Experience Platform bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie Quellverbindungen für verschiedene Datenanbieter einfach einrichten können. Diese Quellverbindungen ermöglichen Ihnen die Authentifizierung und Verbindung zu externen Datenspeicherung- und CRM-Diensten, die Festlegung von Zeiten für die Erfassungsausführung und die Verwaltung des Datenaufkommens.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Zusätzliche API- und UI-Unterstützung für Cloud-Datenspeicherung | Neue Quellanschlüsse für die Datenspeicherung von Azurblauen Dateien. |
| Zusätzliche API- und UI-Unterstützung für Datenbanken | Neue Quellschnittstellen für Azurblase Data Explorer, IBM DB2 und Oracle DB. |
| Datenfreigabe mit Adobe Audience Manager für Experience Platform | Der Bereitstellungsprozess für den Audience Manager Connector wurde aktualisiert. Audience Manager-Datensätze für Echtzeit-Kundendaten sind jetzt standardmäßig deaktiviert. Sie können manuell festlegen, welche Datensätze für Profil bewerben sollen. Die neuen Standardeinstellungen sind nicht rückwirkend und wirken sich nur auf die Bereitstellung für neue Audience Manager-Connectors aus. Weitere Informationen finden Sie im [Benutzerhandbuch](../../catalog/datasets/user-guide.md)für Datasets. |

**Bekannte Probleme**

- Keine.

Weitere Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md).