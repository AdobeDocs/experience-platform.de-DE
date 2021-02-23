---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform vom 24. Februar 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 9f7d7ae9c721d1ce7abf0dc7d3eaff18eed09d6f
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 39%

---


# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 24. Februar 2021**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenflüsse](#dataflows)
- [Experience-Datenmodell (XDM)-System](#xdm)
- [Identity Service](#identity)
- [Quellen](#sources)

## Datenflüsse {#dataflows}

In Adobe Experience Platform werden Daten aus einer Vielzahl von Quellen erfasst, innerhalb der Experience Platform analysiert und zu einer Vielzahl von Zielen aktiviert. Plattform erleichtert die Verfolgung dieses potenziell nicht-linearen Datenflusses durch Transparenz mit Datenflüssen.

Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Diese Datenflüsse werden über verschiedene Dienste konfiguriert und unterstützen Sie dabei, Daten von den Quell-Connectors in Zielgruppen-Datasets zu verschieben, wo sie dann von [!DNL Identity Service] und [!DNL Real-time Customer Profile] verwendet werden, bevor sie schließlich nach [!DNL Destinations] aktiviert werden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neues Überwachungs-Dashboard | Sie können jetzt das Monitoring-Dashboard für dienstübergreifende Transparenz und umsetzbare Einblicke in die Erfassung von Quelldaten verwenden. Das neue Überwachungs-Dashboard bietet eine umfassende Ansicht von Daten, die von [!DNL Data Lake] bis [!DNL Identity Service] und [!DNL Profile] verarbeitet werden, und ermöglicht Ihnen gleichzeitig die Überwachung von Erfassungsraten, Erfolgen und Fehlern. Weitere Informationen finden Sie im Tutorial zu [Überwachungsquellen-Datenaflows in der Benutzeroberfläche](../../dataflows/ui/monitor-sources.md). |

Weitere allgemeine Informationen zu Datenflüssen finden Sie im [Datenaflows-Überblick](../../dataflows/home.md).

## Experience-Datenmodell (XDM)-System {#xdm}

Normung und Interoperabilität sind Schlüsselkonzepte hinter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), angetrieben von der Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierte Suchoberfläche | Verbesserte Suchfunktionen sind jetzt auf der Registerkarte [!UICONTROL Durchsuchen] im Arbeitsbereich [!UICONTROL Schema] und im Dialogfeld &quot;Mixin-Auswahl&quot;unter [!DNL Schema Editor] verfügbar.<br><br>Bei der Suche nach einem Begriff zuvor wurden nur XDM-Ressourcen berücksichtigt, deren Name mit der Abfrage übereinstimmt. Zusätzlich zu den Ressourcen, deren Name mit der Abfrage übereinstimmt, werden auch die Ressourcen mit den einzelnen Attributen, die mit dem Begriff übereinstimmen, einbezogen. Auf diese Weise können Sie nach XDM-Ressourcen basierend auf den Attributen suchen, die sie enthalten, und nicht nach dem Namen der Ressource.<br><br>Weitere Informationen finden Sie in den Dokumenten zur  [Erforschung von XDM-](../../xdm/ui/explore.md) Ressourcen und zum  [Verwalten von ](../../xdm/ui/resources/schemas.md) Schemata in der Benutzeroberfläche. |

Weitere allgemeine Informationen zu XDM finden Sie unter [XDM-Systemübersicht](../../xdm/home.md).

## Identity Service {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, eine bessere Ansicht Ihres Kundenverhaltens zu erzielen, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit wirkungsvolle persönliche digitale Erlebnisse bereitstellen können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Identitätsdiagramm Viewer | Mit dem Identitätsdiagramm-Viewer können Sie Identitäten, die in der Benutzeroberfläche zusammengefügt sind, überprüfen und visualisieren, sodass Debugging und Transparenz verbessert werden können. Weitere Informationen finden Sie im Dokument [Identitätsdiagramm-Viewer](../../identity-service/ui/identity-graph-viewer.md). |

Weitere allgemeine Informationen zu [!DNL Identity Service] finden Sie unter [Übersicht über den Identitätsdienst](../../identity-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Quellen**

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Google PubSub] | Sie können [!DNL Google PubSub] jetzt mit [!DNL Experience Platform] über die [!DNL Flow Service]-API oder die Benutzeroberfläche verbinden. Weitere Informationen finden Sie unter [[!DNL Google PubSub] Connector overview](../../sources/connectors/cloud-storage/google-pubsub.md). |
| [!DNL Oracle Object Storage] | Sie können [!DNL Oracle Object Storage] jetzt mit [!DNL Experience Platform] über die [!DNL Flow Service]-API oder die Benutzeroberfläche verbinden. Weitere Informationen finden Sie unter [[!DNL Oracle Object Storage] Connector overview](../../sources/connectors/cloud-storage/oracle-object-storage.md). |

Weitere allgemeine Informationen zu Quellen finden Sie im [Sources-Überblick](../../sources/home.md).
