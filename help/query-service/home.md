---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Abfrage Service
topic: overview
translation-type: tm+mt
source-git-commit: 45da024d45b5eebdfc393ee14890e24aed6021ce
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---


# Übersicht über den Abfrage Service

Adobe Experience Platform erfasst Daten aus einer Vielzahl von Quellen. Eine große Herausforderung für Marketingexperten besteht darin, diese Daten zu nutzen, um Einblicke über ihre Kunden zu gewinnen. Adobe Experience Platform Abfrage Service erleichtert dies, indem Sie die Verwendung von SQL-Standarddaten zur Abfrage in Platform zulassen. Mit dem Abfrage Service können Sie beliebige Datensätze in den Data Lake einbinden und die Abfragen als neuen Datensatz erfassen, der im Berichte, maschinellem Lernen oder zur Erfassung in Echtzeit-Kundendaten verwendet werden kann. Dieses Dokument gibt einen Überblick über die Rolle des Abfrage Service in Experience Platform.

## Verwenden des Abfrage-Dienstes

Abfrage Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie SQL-Abfragen erstellen können, um Ihre Daten besser zu analysieren. Über die Benutzeroberfläche können Sie Abfragen, Ansichten, die zuvor ausgeführt wurden, schreiben und ausführen sowie auf Abfragen zugreifen, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden. Die Benutzeroberfläche soll als Sandbox zum Testen Ihrer Abfragen verwendet werden, bevor Sie sie in Ihrem größeren Datensatz ausführen. Weitere Informationen zur Verwendung des interaktiven Diensts innerhalb der Plattform finden Sie im Benutzerhandbuch [der Benutzeroberfläche des](ui/overview.md)Abfrage-Diensts. Die RESTful-API bietet ein ähnliches Erlebnis, mit dem Sie programmatisch Abfragen schreiben und ausführen, Abfragen für die spätere Verwendung und Wiederholung planen und Vorlagen für Abfragen erstellen können, die Sie schreiben möchten. Weitere Informationen zur Verwendung der Abfrage Service API finden Sie im Entwicklerhandbuch für [Abfrage Service](api/getting-started.md).

## Abfrage Service und Experience Platform-Dienste

Abfrage Service interagiert und kann mit mehreren Experience Platform-Diensten verwendet werden. Um die Funktionen von Abfrage Service optimal nutzen zu können, sollten Sie sich mit diesen Diensten und ihrer Interaktion mit Abfrage Service vertraut machen.

### Data Science-Arbeitsbereich

Der Data Science Workspace der Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Einblicke aus den in Experience Platform gespeicherten Daten zu gewinnen. Data Science Workspace ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf Daten zu Kunden und deren Aktivitäten aus Aufzeichnungen und Zeitreihen basieren. Dies erleichtert Prognosen wie Kaufneigung und empfohlene Angebot, die von Einzelpersonen geschätzt und verwendet werden können. Sie können SQL in Data Science Workspace verwenden, indem Sie Abfrage Service in JupyterLab integrieren, um Adobe Analytics-Daten zu untersuchen, umzuformen und zu analysieren. Weitere Informationen zum Data Science Workspace und zum Integrationsleitfaden für Abfragen finden Sie in der Übersicht über den Data Science Workspace. Weitere Informationen zur Interaktion von Data Science Workspace mit dem Abfrage Service finden Sie im Dokument Data Science Workspace.

### Segmentierungsdienst

Mit dem Segmentierungsdienst für Adobe Experience Platform können Benutzer ihre Kunden in kleinere Gruppen mit ähnlichen Eigenschaften unterteilen. Diese Segmente können anschließend ausgewertet werden, um eine bessere Analyse der Daten Ihres Echtzeit-Profils zu erhalten. Mit dem Abfrage Service können Sie diese Analyse bereitstellen, indem Sie Abfragen zu diesen Segmentdaten im Data Lake ausführen. Weitere Informationen zur Segmentierung finden Sie in der Segmentierungsdienstübersicht und im Profil Abfrage Language (PQL)-Handbuch.

## Nächste Schritte

Durch das Lesen dieses Dokuments wurden Sie zum Abfrage Service und seiner Funktionsweise im größeren Umfang der Experience Platform hinzugefügt. Weitere Informationen zur Interaktion mit verschiedenen Endpunkten in der Abfrage Service API finden Sie im Entwicklerhandbuch für [Abfrage Service](api/getting-started.md). Weitere Informationen zur Verwendung des interaktiven Diensts innerhalb der Plattform finden Sie im Benutzerhandbuch [der](ui/overview.md)Abfrage Service-Benutzeroberfläche. Für eine umfassende Liste zur Verbindung von externen Kunden mit Abfrage Service lesen Sie bitte die Übersicht über die [Abfrage Service-Kunden](clients/overview.md).
