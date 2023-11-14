---
keywords: Experience Platform;Home;beliebte Themen;Query Service;Query Service;Abfrage
solution: Experience Platform
title: Query Service – Übersicht
description: Dieses Dokument gibt einen Überblick über die Rolle von Query Service in Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 100%

---

# [!DNL Query Service] – Übersicht

Adobe Experience Platform nimmt Daten aus einer Vielzahl von Quellen auf. Eine große Herausforderung für Marketing-Experten besteht darin, diese Daten zu nutzen, um Einblicke in ihre Kunden zu gewinnen. Adobe Experience Platform [!DNL Query Service] erleichtert dies, indem er die Verwendung von Standard-SQL zur Abfrage von Daten in [!DNL Platform] ermöglicht. Mit [!DNL Query Service] können Sie beliebige Datensätze im [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz erfassen, der bei Reporting und maschinellem Lernen oder zur Aufnahme in das [!DNL Real-Time Customer Profile] verwendet werden kann. Dieses Dokument gibt einen Überblick über die Rolle von [!DNL Query Service] in [!DNL Experience Platform].

[!DNL Query Service] ermöglicht es Marken, die Customer Journey online und offline zu verbinden und kanalübergreifende Attribution vorzunehmen. Das folgende Video zeigt, wie ein Experience-Unternehmen [!DNL Query Service] für gängige Anwendungsfälle nutzen kann und wie [!DNL Query Service] funktioniert.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Verwenden [!DNL Query Service]

[!DNL Query Service] bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie SQL-Abfragen erstellen können, um Ihre Daten besser zu analysieren. Über die Benutzeroberfläche können Sie Abfragen schreiben und ausführen, zuvor ausgeführte Abfragen anzeigen und auf Abfragen zugreifen, die von Benutzenden in Ihrer Organisation gespeichert wurden. Die Benutzeroberfläche soll als Sandbox zum Testen Ihrer Abfragen verwendet werden, bevor Sie sie auf Ihren größeren Datensatz anwenden. Weitere Informationen zur Verwendung des interaktiven Diensts innerhalb von [!DNL Platform] finden Sie im [Handbuch zur Query Service-Benutzeroberfläche](ui/overview.md). Die RESTful-API bietet ein ähnliches Erlebnis, mit dem Sie programmatisch Abfragen schreiben und ausführen, Abfragen für die spätere Verwendung und Wiederholung planen und Vorlagen für Abfragen erstellen können, die Sie schreiben möchten. Weitere Informationen zur Verwendung der [!DNL Query Service]-API finden Sie im [Query Service-Entwicklerhandbuch](api/getting-started.md).

## [!DNL Query Service] und [!DNL Experience Platform]-Services

[!DNL Query Service] kann mit mehreren [!DNL Experience Platform]-Services verwendet werden. Um die Funktionen von [!DNL Query Service's] optimal zu nutzen, sollten Sie sich mit diesen Diensten und ihrer Interaktion mit [!DNL Query Service] vertraut machen.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in [!DNL Experience Platform] gespeicherten Daten zu gewinnen. [!DNL Data Science Workspace] ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf Daten zu Kunden und deren Aktivitäten aus Aufzeichnungen und Zeitreihen basieren. Dies erleichtert Prognosen z. B. zu Kaufneigung und empfohlenen Angeboten, die von Einzelpersonen geschätzt und verwendet werden. Sie können SQL in [!DNL Data Science Workspace] verwenden, indem Sie [!DNL Query Service] in [!DNL JupyterLab] integrieren, um Adobe Analytics-Daten untersuchen, umwandeln und analysieren zu können. Lesen Sie den Überblick über [!DNL Data Science Workspace] für weitere Informationen über [!DNL Data Science Workspace] sowie das Handbuch zur Integration von [!DNL Query Service] für weitere Informationen dazu, wie [!DNL Data Science Workspace] mit [!DNL Query Service] interagiert.

### [!DNL Segmentation Service]

Mit in Adobe Experience Platform [!DNL Segmentation Service] können Benutzer ihre Kunden in kleinere Gruppen mit ähnlichen Eigenschaften unterteilen. Diese Zielgruppen können anschließend ausgewertet werden, um eine bessere Analyse der Daten des [!DNL Real-Time Customer Profile] zu erhalten. Mit [!DNL Query Service] können Sie diese Analyse bereitstellen, indem Sie Abfragen zu diesen Segmentdaten im [!DNL Data Lake] ausführen. Weitere Informationen zur Segmentierung finden Sie im Überblick über [!DNL Segmentation Service], und Informationen zur Analyse von Zielgruppen finden Sie im Handbuch zu [!DNL Profile Query Language] (PQL).

## Anwendungsfälle

[!DNL Query Service] bietet einen flexiblen Ansatz für Ihre Datenverarbeitung, der vielen Zwecken dient. So kann unter anderem die Segmentierung durch Marketing-Fachleute erleichtert und dazu beigetragen werden, nachvollziehbare Zielgruppen und aussagekräftige geschäftliche Insights zu generieren. Die folgenden Anwendungsfälle bieten detailliertere Beispiele für die Leistungsfähigkeit von [!DNL Query Service].

### Abbruch von Durchsuchen-Vorgängen in Adobe Analytics

Dieses [Beispiel für den Abbruch von Durchsuchen-Vorgängen konzentriert sich auf die Verwendung von Adobe-Daten [!DNL Analytics]](./use-cases/abandoned-browse.md), um eine bestimmte nachvollziehbare Zielgruppe zu erstellen. [!DNL Query Service] berücksichtigt komplexe Logik für die Segmentierung, um verschiedene personalisierte Attribute zur nachgelagerten Verwendung zu berechnen oder die Erstellung Ihrer Zielgruppen erheblich zu vereinfachen.

### Looker BI-Dashboards

Mit Adobe Experience Platform können Sie alle gespeicherten Datensätze aufnehmen, speichern, strukturieren und abrufen — einschließlich Verhaltensdaten, CRM-Daten und Verkaufsdaten. Mithilfe von [!DNL Experience Platform's Query Service] können Sie Abfragen zu diesen Datensätzen durchführen, spezifische Fragen zur Geschäftstätigkeit beantworten und dann nützliche Einblicke gewinnen. Das folgende Video zeigt die Vorteile, die das Erstellen von Dashboards in Business Intelligence-Tools mit [!DNL Query Service] hat.

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Nächste Schritte und zusätzliche Ressourcen

In diesem Dokument wurden Ihnen [!DNL Query Service] und seine Funktionsweise im Zusammenhang mit [!DNL Experience Platform] vorgestellt. Weitere Informationen zur Interaktion mit verschiedenen Endpunkten in der [!DNL Query Service]-API finden Sie im [Query Service-Entwicklerhandbuch](api/getting-started.md). Weitere Informationen zur Verwendung des interaktiven Diensts innerhalb von [!DNL Platform] finden Sie im [Handbuch zur Query Service-Benutzeroberfläche](ui/overview.md). Für eine umfassende Liste zur Verbindung von externen Clients mit [!DNL Query Service] lesen Sie [Query Service-Clients – Überblick](clients/overview.md).

Sehen Sie sich das folgende Video an, um zu verstehen, wie Abfragen ausgeführt werden. In diesem Video werden Tipps und Best Practices für die Ausführung von Abfragen in der Benutzeroberfläche des Abfrage-Editors, PSQL-Clients, Business Intelligence-Lösungen (BI) und der HTTP-API vorgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
