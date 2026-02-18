---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Service;Abfrage Service;Abfrage
solution: Experience Platform
title: Abfrage-Service – Überblick
description: Erfahren Sie mehr über die Rolle des Abfrage-Service in Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: 161de7f9692cdd219d73a1a301f891cf9636a2e9
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 16%

---

# Abfrage-Service – Überblick

Adobe Experience Platform nimmt Daten aus einer Vielzahl von Quellen auf. Eine große Herausforderung für Marketing-Experten besteht darin, diese Daten zu nutzen, um Einblicke in ihre Kunden zu gewinnen. Um Daten in Experience Platform abzufragen, können Sie standardmäßige SQL- und Adobe Experience Platform-Abfrage-Services verwenden. Sie können den Abfrage-Service verwenden, um einen beliebigen Datensatz im Data Lake zu verbinden und die Abfrageergebnisse als neuen Datensatz zu erfassen, der bei Reporting und maschinellem Lernen oder zur Aufnahme in [!DNL Real-Time Customer Profile] verwendet werden kann. Dieses Dokument gibt einen Überblick über die Rolle des Abfrage-Service in Experience Platform.

Sie können Query Service verwenden, um die Kunden-Journey online und offline zu verbinden und die Omni-Channel-Attribution für Ihre Marke zu verstehen. Das folgende Video zeigt, wie ein Experience-Unternehmen den Abfrage-Service verwenden kann, um wichtige Anwendungsfälle zu beheben, und erläutert, wie der Abfrage-Service funktioniert.

>[!VIDEO](https://video.tv.adobe.com/v/3464268?captions=ger&quality=12&learn=on)

## Verwenden des Abfrage-Service {#usage}

Um Ihre Daten zu analysieren, erstellen und führen Sie SQL-Abfragen entweder mit der Query Service-Benutzeroberfläche oder der RESTful-API aus.
Mit der Benutzeroberfläche von Query Service können Sie Abfragen schreiben, ausführen und planen, zuvor ausgeführte Abfragen anzeigen und auf Abfragen zugreifen, die von Benutzern in Ihrer Organisation gespeichert wurden. Sie können Ihre Abfragen auch testen, bevor Sie sie mit dem Abfrage-Editor für einen größeren Datensatz ausführen. Eine Übersicht über [ Benutzeroberflächenfunktionalität finden Sie im Handbuch zur ]-Service-Benutzeroberfläche (ui/overview.md).

Die RESTful-API bietet ein ähnliches Erlebnis. Sie können die Abfrage-Service-API verwenden, um Abfragen programmgesteuert zu schreiben und auszuführen, Vorlagen für Abfragen zu erstellen und zu speichern, die Sie anpassen möchten, oder Abfragen für die automatisierte Ausführung zu planen. Weitere Informationen zur Verwendung [&#x200B; Abfrage-Service-API finden &#x200B;](api/getting-started.md) im Query Service-Entwicklerhandbuch .

Um schnell mit den Funktionen von Query Service zu beginnen, sollten Sie die folgenden Dokumente lesen:

- [Allgemeine Leitlinien für die Ausführung von Abfragen](./best-practices/writing-queries.md)
- [SQL-Syntax in Query Service](./sql/syntax.md)
- [Erstellen abgeleiteter Datensätze mit SQL](./data-distiller/derived-datasets/create-derived-datasets-with-sql.md)

## Abfrage-Service und Experience Platform-Dienste {#experience-platform-services}

Query Service interagiert mit mehreren Experience Platform-Services und kann mit diesen verwendet werden. Um die Funktionen des Abfrage-Service optimal zu nutzen, sollten Sie sich mit diesen Services vertraut machen und auch damit, wie sie mit dem Abfrage-Service interagieren. Die Landingpage der [Experience Platform]Dokumentation (https://experienceleague.adobe.com/docs/experience-platform.html?lang=de) enthält Zusammenfassungen und Links zu den Funktionen der Plattform.

### [!DNL Data Science Workspace] {#data-science-workspace}

Adobe Experience Platform [!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Datenwissenschaftler können die [!DNL I Data Science Workspace] verwenden, um Rezepte zu erstellen, die auf Datensatz- und Zeitreihendaten über Kunden und ihre Aktivitäten basieren. Diese Rezepte erleichtern Prognosen wie Kaufneigung und empfohlene Angebote, die von Einzelpersonen geschätzt und verwendet werden. Sie können SQL in [!DNL Data Science Workspace] verwenden, indem Sie den Abfrage-Service in [!DNL JupyterLab] integrieren, um Adobe Analytics-Daten zu untersuchen, umzuwandeln und zu analysieren. Weitere Informationen [[!DNL Data Science Workspace]  Interaktion von &#x200B;](../data-science-workspace/home.md) mit dem Abfrage[&#128279;](./clients/jupyter-notebook.md) Service finden Sie im Jupyter[!DNL Data Science Workspace]Notebook-Verbindungshandbuch .

### [!DNL Segmentation Service] {#segmentation}

Verwenden Sie den Segmentierungs-Service von Adobe Experience Platform, um Ihre Kunden in kleinere Gruppen mit ähnlichen Eigenschaften zu unterteilen. Diese Zielgruppen können dann ausgewertet werden, um eine bessere Analyse der Daten Ihres Echtzeit-Kundenprofils zu ermöglichen. Sie können Query Service verwenden, um Abfragen zu diesen Zielgruppendaten im Data Lake auszuführen und die Analyse bereitzustellen. PQL Weitere Informationen [&#x200B; Analyse von Zielgruppen finden Sie &#x200B;](../segmentation/home.md) der Übersicht zum Segmentierungs Service und im Handbuch zu [[!DNL Profile Query Language] (](../segmentation/pql/overview.md)) .

## Anwendungsfälle {#use-cases}

Query Service bietet einen flexiblen Ansatz für Ihre Datenverarbeitung, der vielen Zwecken dient. Sie kann unter anderem die Segmentierung durch Marketing-Experten erleichtern und dazu beitragen, nachvollziehbare Zielgruppen und aussagekräftige geschäftliche Einblicke zu generieren. Die folgenden Anwendungsfälle bieten detailliertere Beispiele für die Leistungsfähigkeit des Abfrage-Service.

### Abbruch von Durchsuchen-Vorgängen in Adobe Analytics {#abandon-browse}

Dieses [Beispiel für den Abbruch von Durchsuchen-Vorgängen konzentriert sich auf die Verwendung von Adobe-Daten [!DNL Analytics]](./use-cases/abandoned-browse.md), um eine bestimmte nachvollziehbare Zielgruppe zu erstellen. Der Abfrage-Service berücksichtigt komplexe Logik für die Segmentierung, um verschiedene personalisierte Attribute zur nachgelagerten Verwendung zu berechnen oder die Erstellung Ihrer Zielgruppen erheblich zu vereinfachen.

## Generieren von Insights mit benutzerdefinierten Dashboards {#custom-dashboards}

Mit Adobe Experience Platform können Sie alle gespeicherten Datensätze aufnehmen, speichern, strukturieren und abrufen, einschließlich Verhaltens-, CRM- und Verkaufsdaten. Mit Query Service können Sie diese Datensätze abfragen und spezifische geschäftliche Fragen beantworten und so wirkungsvolle Einblicke gewinnen. Erfahren Sie, wie Sie benutzerdefinierte Dashboards erstellen und verwalten, in denen Sie maßgeschneiderte Widgets erstellen, hinzufügen und bearbeiten können, um Schlüsselmetriken mit [benutzerdefinierten Dashboards“ &#x200B;](../dashboards/standard-dashboards.md) visualisieren. Sie können auch [Ihre eigenen Real-Time CDP-Berichte](../dashboards/data-models/cdp-insights-data-model-b2c.md) für Ihre Marketing- und KPI-Anwendungsfälle anpassen, indem Sie SQL-Abfragen mit Real-Time Customer Data Platform Insights-Datenmodellen verwenden.

## Nächste Schritte und zusätzliche Ressourcen

In diesem Dokument wurden Ihnen der Abfrage-Service und seine Funktionsweise im größeren Umfang von Experience Platform vorgestellt. Um weiter über die Funktionen von Query Service zu lernen, sollten Sie die folgenden Dokumente lesen:

- Das [Query Service-Entwicklerhandbuch](api/getting-started.md): Weitere Informationen zur Interaktion mit verschiedenen Endpunkten in der Query Service-API.
- Das [Handbuch zur Query Service-Benutzeroberfläche](ui/overview.md): Weitere Informationen zur Verwendung des Abfrage-Editors und der Benutzeroberfläche.
- Die [Query Service-Clients - Übersicht](clients/overview.md): Eine umfassende Liste der externen Clients, die mit dem Query Service verbunden werden sollen.

Sehen Sie sich das folgende Video an, um zu verstehen, wie Abfragen ausgeführt werden. In diesem Video werden Tipps und Best Practices für die Ausführung von Abfragen in der Benutzeroberfläche des Abfrage-Editors, PSQL-Clients, Business Intelligence-Lösungen (BI) und der HTTP-API vorgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/32951?captions=ger&quality=12&learn=on)
