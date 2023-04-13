---
title: Adobe Experience Platform – Versionshinweise Februar 2021
description: Die Versionshinweise für Adobe Experience Platform vom Februar 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 97%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 24. Februar 2021**

Neue Funktionen in Adobe Experience Platform:

- [(Beta) Dashboard](#dashboards)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta) Dashboard {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Informationen zu den Daten Ihres Unternehmens sehen, basierend auf täglichen Schnappschüssen der Daten.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Dashboards (Beta) für Profile, Segmente, Ziele und Lizenznutzung | **Anmerkung: Diese Funktion befindet sich derzeit in der Beta-Phase und steht nicht allen Nutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.**<br/><br/> Dashboards bieten vordefinierte Berichte zu den Daten Ihres Unternehmens und werden direkt in den Marketing-Workflow in von Platform integriert. Diese Dashboards können ohne zusätzliche IT-Unterstützung genutzt werden, und es fällt hierbei auch nicht der Zeit- und Arbeitsaufwand an, der andernfalls für den Export und die Verarbeitung von Daten mit Data Warehouse-Design und -Implementierung als Zusatz erforderlich wäre. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Data Science Workspace ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| JupyterLab EDA Notebook | Das Python-Notebook zur explorativen Datenanalyse (EDA) ist jetzt in Jupyterlab verfügbar. Dieses Notebook hilft Ihnen beim Erkennen von Datenmustern, beim Überprüfen der Datenplausibilität und beim Zusammenfassen der relevanten Daten für Prognosemodelle. Weitere Informationen finden Sie im Tutorial zum [Untersuchen von Web-basierten Daten für Prognosemodelle](../../data-science-workspace/jupyterlab/eda-notebook.md). |

Weitere allgemeine Informationen zu Data Science Workspace finden Sie im Abschnitt [Übersicht über Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

In Adobe Experience Platform werden Daten aus zahlreichen Quellen aufgenommen, analysiert und für eine Vielzahl an Zielen aktiviert. Plattform erleichtert das Tracking dieses potenziell nicht-linearen Datenflusses durch Transparenz.

Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Diese Datenflüsse werden über verschiedene Services konfiguriert und unterstützen Sie dabei, Daten von den Quell-Connektoren in Zielgruppen-Datensätze zu verschieben, wo sie dann von [!DNL Identity Service] und [!DNL Real-Time Customer Profile] verwendet werden, bevor sie schließlich für [!DNL Destinations] aktiviert werden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neues Überwachungs-Dashboard | Sie können jetzt das Überwachungs-Dashboard für Service-übergreifende Transparenz und umsetzbare Einblicke in die Erfassung von Quelldaten verwenden. Das neue Überwachungs-Dashboard bietet eine umfassende Ansicht von Daten, die von [!DNL Data Lake] zu [!DNL Identity Service] und [!DNL Profile] verarbeitet werden, und ermöglicht Ihnen gleichzeitig das Überwachen von Erfassungsraten, Erfolgen und Fehlern. Weitere Informationen finden Sie im Tutorial zum [Überwachen von Quelldatenflüssen in der Benutzeroberfläche](../../dataflows/ui/monitor-sources.md). |

Weitere allgemeine Informationen zu Datenflüssen finden Sie in der [Übersicht zu Datenflüssen](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] sind vordefinierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | Mit der [!DNL LinkedIn Matched Audiences]-Verbindung können Sie Zielgruppen auf der sozialen Plattform [!DNL LinkedIn] aktivieren. |

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierte Suchoberfläche | Verbesserte Suchfunktionen sind jetzt auf dem Tab [!UICONTROL Durchsuchen] im Arbeitsbereich [!UICONTROL Schemas] und im Dialogfeld für die Schemafeldgruppe von [!DNL Schema Editor] verfügbar.<br><br>Beim Suchen nach einem Begriff wurden bisher nur XDM-Ressourcen berücksichtigt, deren Name mit der Suchanfrage übereinstimmten. Nun werden zusätzlich zu diesen Ressourcen, deren Name mit der Suchanfrage übereinstimmt, auch die Ressourcen mit einbezogen, bei denen einzelne Attribute mit dem Begriff übereinstimmen. Auf diese Weise können Sie basierend auf den enthaltenen Attributen und nicht nur basierend auf dem Namen der Ressource nach XDM-Ressourcen suchen.<br><br>Weitere Informationen finden Sie in den Dokumenten zum [Kennenlernen von XDM-Ressourcen](../../xdm/ui/explore.md) und zum [Verwalten von Schemas](../../xdm/ui/resources/schemas.md) in der Benutzeroberfläche. |

Weitere allgemeine Informationen zu XDM finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und ihr Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für effektive und persönliche digitale Erlebnisse sorgen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Identitätsdiagramm-Viewer | Mit dem Identitätsdiagramm-Viewer können Sie Identitäten, die in der Benutzeroberfläche zusammengefügt sind, überprüfen und visualisieren, wodurch Debugging und Transparenz verbessert werden können. Weitere Informationen finden Sie im Dokument [Identitätsdiagramm-Viewer](../../identity-service/ui/identity-graph-viewer.md). |

Weitere allgemeine Informationen zu [!DNL Identity Service] finden Sie unter [Identity Service – Übersicht](../../identity-service/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit [!DNL Profile] können Sie Ihre unterschiedlichen Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige, im Zeitverlauf gezeichnete Darstellung jeder Kundeninteraktion bietet.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Berechnete Attribute (Alphaversion) | ***Hinweis: Diese Funktion befindet sich derzeit in der Alphaphase und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.*** <br/><br/>Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Anschließend können Sie die Aggregate in der Segmentierung, Aktivierung und Personalisierung verwenden. Einige Beispiele für diese Funktionen sind Anzahl, Summe, Durchschnitt, min, max, true/false. Berechnete Attribute stehen derzeit nur per API zur Verfügung. |

Weitere Informationen zum Echtzeit-Kundenprofil, einschließlich Tutorials und Best Practices für die Arbeit mit [!DNL Profile] Daten, lesen Sie bitte zunächst die [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md).

## [!DNL Sources] {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Quellen**

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Google PubSub] | Sie können [!DNL Google PubSub] jetzt mit [!DNL Experience Platform] über die [!DNL Flow Service]-API oder die Benutzeroberfläche verbinden. Weiterführende Informationen dazu finden Sie unter [[!DNL Google PubSub] Connectoren – Übersicht](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | Sie können [!DNL Oracle Object Storage] jetzt mit [!DNL Experience Platform] über die [!DNL Flow Service]-API oder die Benutzeroberfläche verbinden. Weiterführende Informationen dazu finden Sie unter [[!DNL Oracle Object Storage] Connectoren – Übersicht](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Weitere allgemeine Informationen zu Quellen finden Sie unter [Quellen – Übersicht](../../sources/home.md).
