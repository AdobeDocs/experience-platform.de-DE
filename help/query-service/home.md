---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abfrage-Service von Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: cfd767a05ad4c1dd43ac2bdde1966f9c89f5d219
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 81%

---


# Überblick über den Abfrage-Service

Adobe Experience Platform nimmt Daten aus einer Vielzahl von Quellen auf. Eine große Herausforderung für Marketing-Experten besteht darin, diese Daten zu nutzen, um Einblicke in ihre Kunden zu gewinnen. Der Abfrage-Service von Adobe Experience Platform erleichtert dies, indem er Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Platform erlaubt. Mit dem Abfrage-Service können Sie beliebige Datensätze in den Daten-Pool einbinden und die Abfragen als neuen Datensatz erfassen, der bei Reporting und maschinellem Lernen oder zur Aufnahme in das Echtzeit-Kundenprofil verwendet werden kann. Dieses Dokument gibt einen Überblick über die Rolle des Abfrage-Service in Experience Platform.

Abfrage Service ermöglicht es Marken, die Online-Customer Journey mit der Offline-Customer Journey zu verbinden und die Zuordnung von Kanälen zu verstehen. Das folgende Video zeigt, wie ein Erlebnisunternehmen Abfrage Service nutzen kann, um wichtige Anwendungsfälle zu behandeln, und wie Abfrage Service funktioniert.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Verwenden des Abfrage-Service

Der Abfrage-Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie SQL-Abfragen erstellen können, um Ihre Daten besser zu analysieren. Über die Benutzeroberfläche können Sie Abfragen schreiben und ausführen, zuvor ausgeführte Abfragen anzeigen und auf Abfragen zugreifen, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden. Die Benutzeroberfläche soll als Sandbox zum Testen Ihrer Abfragen verwendet werden, bevor Sie sie auf Ihren größeren Datensatz anwenden. Weitere Informationen zur Verwendung des interaktiven Diensts innerhalb von Platform finden Sie in der [Anleitung zur Abfrage-Service-Benutzeroberfläche](ui/overview.md). Die RESTful-API bietet ein ähnliches Erlebnis, mit dem Sie programmatisch Abfragen schreiben und ausführen, Abfragen für die spätere Verwendung und Wiederholung planen und Vorlagen für Abfragen erstellen können, die Sie schreiben möchten. Weitere Informationen zur Verwendung der Abfrage-Service-API finden Sie im [Entwicklungshandbuch für den Abfrage-Service](api/getting-started.md).

## Abfrage-Service und Experience Platform-Dienste

Der Abfrage-Service kann mit mehreren Experience Platform-Diensten verwendet werden. Um die Funktionen des Abfrage-Service optimal zu nutzen, sollten Sie sich mit diesen Diensten und ihrer Interaktion mit dem Abfrage-Service vertraut machen.

### Data Science Workspace

Data Science Workspace in Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Data Science Workspace ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf Daten zu Kunden und deren Aktivitäten aus Aufzeichnungen und Zeitreihen basieren. Dies erleichtert Prognosen z. B. zu Kaufneigung und empfohlenen Angeboten, die von Einzelpersonen geschätzt und verwendet werden. Sie können SQL in Data Science Workspace verwenden, indem Sie den Abfrage-Service in JupyterLab integrieren, um Adobe Analytics-Daten zu untersuchen, umzuwandeln und zu analysieren. Lesen Sie den Überblick über Data Science Workspace für weitere Informationen über Data Science Workspace, sowie den Integrationsleitfaden des Abfrage-Service für weitere Informationen dazu, wie Data Science Workspace mit dem Abfrage-Service interagiert.

### Segmentierungsdienst

Mit dem Segmentierungsdienst in Adobe Experience Platform können Benutzer ihre Kunden in kleinere Gruppen mit ähnlichen Eigenschaften unterteilen. Diese Segmente können anschließend ausgewertet werden, um eine bessere Analyse der Daten des Echtzeit-Kundenprofils zu erhalten. Mit dem Abfrage-Service können Sie diese Analyse bereitstellen, indem Sie Abfragen zu diesen Segmentdaten im Daten-Pool ausführen. Weitere Informationen zur Segmentierung finden Sie im Überblick über den Segmentierungsdienst, Informationen zur Analyse von Segmenten finden Sie in der Anleitung für Profile Query Language (PQL).

### Looker BI-Anwendungsfall

Mit Adobe Experience Platform können Sie alle gespeicherten Datensätze erfassen, speichern, strukturieren und abrufen — einschließlich Verhaltensdaten, CRM-Daten und Verkaufsdaten. Mithilfe [!DNL Experience Platform's Query Service]dieser Daten können Sie Abfragen zu diesen Datensätzen durchführen und spezifische Fragen zum Geschäft beantworten und dann Beginn zu wirkungsvollen Einblicken führen. Das folgende Video zeigt, wie wichtig es ist, mithilfe von BI-Tools (Business Intelligence) Dashboard zu erstellen [!DNL Query Service].

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Nächste Schritte und zusätzliche Ressourcen

In diesem Dokument wurden Ihnen der Abfrage-Service und seine Funktionsweise im größeren Umfang von Experience Platform vorgestellt. Weitere Informationen zur Interaktion mit verschiedenen Endpunkten in der Abfrage-Service-API finden Sie im [Entwicklerhandbuch für den Abfrage-Service](api/getting-started.md). Weitere Informationen zur Verwendung des interaktiven Diensts innerhalb von Platform finden Sie in der [Anleitung für die Abfrage-Service-Benutzeroberfläche](ui/overview.md). Für eine umfassende Liste zur Verbindung von externen Clients mit dem Abfrage-Service lesen Sie [Abfrage-Service-Clients – Überblick](clients/overview.md).

Sehen Sie sich das folgende Video an, um sich besser darauf vorzubereiten, Abfragen auszuführen. In diesem Video werden Tipps und Best Practices für die Ausführung von Abfragen in der Benutzeroberfläche des Abfrage-Editors, PSQL-Clients, Business Intelligence-Lösungen (BI) und der HTTP-API vorgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
