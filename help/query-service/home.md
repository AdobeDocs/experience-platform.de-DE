---
keywords: Experience Platform;Home;beliebte Themen;Query Service;Query Service;Abfrage
solution: Experience Platform
title: Query Service – Übersicht
description: Erfahren Sie mehr über die Rolle von Query Service im Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e06519978ed9c6128be53a15cef3046a0dbc2a16
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 25%

---

# Query Service – Übersicht

Adobe Experience Platform nimmt Daten aus einer Vielzahl von Quellen auf. Eine große Herausforderung für Marketing-Experten besteht darin, diese Daten zu nutzen, um Einblicke in ihre Kunden zu gewinnen. Zur Abfrage von Daten in Platform können Sie SQL- und Adobe Experience Platform Query Service verwenden. Sie können Query Service verwenden, um einen beliebigen Datensatz im Data Lake zu verbinden und die Abfrageergebnisse als neuen Datensatz zu erfassen, der für Berichte, maschinelles Lernen oder für die Aufnahme in [!DNL Real-Time Customer Profile]. Dieses Dokument gibt einen Überblick über die Rolle von Query Service in Experience Platform.

Sie können Query Service verwenden, um die Online- und Offline-Journey von Kunden zu verbinden und die kanalübergreifende Attribution für Ihre Marke zu verstehen. Das folgende Video zeigt, wie ein Erlebnisunternehmen Query Service verwenden kann, um wichtige Anwendungsfälle zu beheben, und wie Query Service funktioniert.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Verwenden von Query Service {#usage}

Zur Analyse Ihrer Daten können Sie die Query Service-Benutzeroberfläche und eine RESTful-API verwenden, über die Sie SQL-Abfragen erstellen können. Über die Benutzeroberfläche können Sie Abfragen schreiben und ausführen, zuvor ausgeführte Abfragen anzeigen und auf Abfragen zugreifen, die von Benutzenden in Ihrer Organisation gespeichert wurden. Sie können den Abfrage-Editor wie eine Sandbox verwenden, um Ihre Abfragen zu testen, bevor Sie sie in Ihrem größeren Datensatz ausführen. Siehe [Benutzerhandbuch zum Query Service](ui/overview.md) für weitere Informationen zur Verwendung der Benutzeroberfläche. Die RESTful-API bietet ein ähnliches Erlebnis. Mit der Query Service-API können Sie Abfragen programmgesteuert schreiben und ausführen, Abfragen für die zukünftige Verwendung und Wiederholung planen sowie Vorlagen für Abfragen erstellen, die Sie schreiben möchten. Weitere Informationen zur Verwendung der Query Service-API finden Sie im [Entwicklerhandbuch für Query Service](api/getting-started.md).

## Query Service und Experience Platform-Dienste {#experience-platform-services}

Query Service interagiert und kann mit mehreren Experience Platform-Services verwendet werden. Um die Funktionen von Query Service optimal zu nutzen, sollten Sie sich mit diesen Diensten und ihrer Interaktion mit Query Service vertraut machen. Die [Landingpage zur Experience Platform-Dokumentation](https://experienceleague.adobe.com/docs/experience-platform.html?lang=de) bietet Zusammenfassungen und Links zu den Funktionen der Plattform.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus in Experience Platform gespeicherten Daten zu gewinnen. Datenwissenschaftler können [!DNL Data Science Workspace] , um Rezepte zu erstellen, die auf Datensatz- und Zeitreihendaten zu Kunden und deren Aktivitäten basieren. Diese Rezepte erleichtern Vorhersagen wie Kaufneigung und empfohlene Angebote, die der Kontakt schätzen und nutzen kann. Sie können SQL in [!DNL Data Science Workspace] durch Integration von Query Service in [!DNL JupyterLab] zur Untersuchung, Transformation und Analyse von Adobe Analytics-Daten. Lesen Sie die [[!DNL Data Science Workspace] Übersicht](../data-science-workspace/home.md) und [Jypiter Notebook-Verbindungshandbuch](./clients/jupyter-notebook.md) für weitere Informationen zur [!DNL Data Science Workspace] interagiert mit Query Service.

### [!DNL Segmentation Service] {#segmentation}

Verwenden Sie den Segmentierungsdienst von Adobe Experience Platform , um Ihre Kunden in kleinere Gruppen mit ähnlichen Eigenschaften zu unterteilen. Diese Zielgruppen können dann ausgewertet werden, um eine bessere Analyse Ihrer Echtzeit-Kundenprofildaten zu ermöglichen. Sie können Query Service verwenden, um Abfragen zu diesen Zielgruppendaten im Data Lake auszuführen und die Analyse bereitzustellen. Lesen Sie die [Übersicht über den Segmentierungsdienst](../segmentation/home.md) und [[!DNL Profile Query Language] Handbuch (PQL)](../segmentation/pql/overview.md) für weitere Informationen zur Analyse von Zielgruppen.

## Anwendungsfälle {#use-cases}

Query Service bietet einen flexiblen Ansatz für Ihre Datenverarbeitung, der vielen Zwecken dient. Unter anderem kann es die Last der Segmentierung durch Marketing-Experten verringern und dazu beitragen, umsetzbare Zielgruppen und aussagekräftige geschäftliche Einblicke zu generieren. Die folgenden Anwendungsbeispiele bieten detailliertere Beispiele für die Leistungsfähigkeit von Query Service.

### Abbruch von Durchsuchen-Vorgängen in Adobe Analytics {#abandon-browse}

Dieses [Beispiel für den Abbruch von Durchsuchen-Vorgängen konzentriert sich auf die Verwendung von Adobe-Daten [!DNL Analytics]](./use-cases/abandoned-browse.md), um eine bestimmte nachvollziehbare Zielgruppe zu erstellen. Query Service unterstützt eine komplexe Logik für die Segmentierung, um verschiedene personalisierte Attribute zur nachgelagerten Verwendung zu berechnen oder die Erstellung Ihrer Zielgruppen deutlich zu vereinfachen.

## Erstellen von Einblicken mit benutzerdefinierten Dashboards {#custom-dashboards}

Mit Adobe Experience Platform können Sie alle gespeicherten Datensätze aufnehmen, speichern, strukturieren und abrufen — einschließlich Verhaltensdaten, CRM-Daten und Verkaufsdaten. Mithilfe von [!DNL Experience Platform's Query Service] können Sie Abfragen zu diesen Datensätzen durchführen, spezifische Fragen zur Geschäftstätigkeit beantworten und dann nützliche Einblicke gewinnen. Erfahren Sie, wie Sie benutzerdefinierte Dashboards erstellen und verwalten, in denen Sie benutzerspezifische Widgets erstellen, hinzufügen und bearbeiten können, um Schlüsselmetriken mit [Benutzerdefinierte Dashboards](../dashboards/user-defined-dashboards.md). Sie können sogar [Anpassen eigener Real-Time CDP-Berichte](../dashboards/cdp-insights-data-model.md) für Ihre Marketing- und KPI-Anwendungsfälle durch Verwendung von SQL-Abfragen mit den Real-time Customer Data Platform Insights-Datenmodellen.

## Nächste Schritte und zusätzliche Ressourcen

In diesem Dokument wurden Ihnen Query Service und seine Funktionsweise im größeren Umfang von Experience Platform vorgestellt. Um mit den Funktionen von Query Service fortzufahren, sollten Sie die folgenden Dokumente lesen:

- Die [Entwicklerhandbuch für Query Service](api/getting-started.md): Weitere Informationen zur Interaktion mit verschiedenen Endpunkten in der Query Service-API.
- Die [Benutzerhandbuch zum Query Service](ui/overview.md): Weitere Informationen zur Verwendung des Abfrage-Editors und der Benutzeroberfläche.
- Die [Übersicht über Query Service Clients](clients/overview.md): Für eine umfassende Liste externer Clients zur Verbindung mit Query Service.

Sehen Sie sich das folgende Video an, um zu verstehen, wie Abfragen ausgeführt werden. In diesem Video werden Tipps und Best Practices für die Ausführung von Abfragen in der Benutzeroberfläche des Abfrage-Editors, PSQL-Clients, Business Intelligence-Lösungen (BI) und der HTTP-API vorgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
