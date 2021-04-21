---
keywords: Experience Platform;Home;beliebte Themen;Abfrage-Dienst;Abfrage-Dienst;Abfrage
solution: Experience Platform
title: Übersicht über den Abfrage Service
topic-legacy: overview
description: Dieses Dokument gibt einen Überblick über die Rolle von Query Service in Experience Platform.
exl-id: fdaefc12-a97d-4e4e-9aed-d3dbd0f43ea0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 28%

---

# [!DNL Query Service]Übersicht

Adobe Experience Platform nimmt Daten aus einer Vielzahl von Quellen auf. Eine große Herausforderung für Marketing-Experten besteht darin, diese Daten zu nutzen, um Einblicke in ihre Kunden zu gewinnen. Adobe Experience Platform [!DNL Query Service] erleichtert dies, indem Sie die Verwendung von SQL-Standarddaten zur Abfrage in [!DNL Platform] zulassen. Mit [!DNL Query Service] können Sie beliebige Datensätze in [!DNL Data Lake] einbinden und die Abfragen als neuen Datensatz erfassen, der im Berichte, maschinellem Lernen oder zur Aufnahme in [!DNL Real-time Customer Profile] verwendet werden kann. Dieses Dokument bietet einen Überblick über die Rolle von [!DNL Query Service] innerhalb von [!DNL Experience Platform].

[!DNL Query Service] ermöglicht es Marken, die Journey von Online- zu Offline-Kanälen zu verbinden und die Zuordnung von Omniture-Kunden zu verstehen. Das folgende Video zeigt, wie ein Erlebnisunternehmen [!DNL Query Service] nutzen kann, um wichtige Anwendungsfälle zu behandeln, und wie [!DNL Query Service] funktioniert.

>[!VIDEO](https://video.tv.adobe.com/v/29795?quality=12&learn=on)

## Verwenden [!DNL Query Service]

[!DNL Query Service] bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie SQL-Abfragen erstellen können, um Ihre Daten besser zu analysieren. Über die Benutzeroberfläche können Sie Abfragen schreiben und ausführen, zuvor ausgeführte Abfragen anzeigen und auf Abfragen zugreifen, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden. Die Benutzeroberfläche soll als Sandbox zum Testen Ihrer Abfragen verwendet werden, bevor Sie sie auf Ihren größeren Datensatz anwenden. Weitere Informationen zur Verwendung des interaktiven Dienstes innerhalb von [!DNL Platform] finden Sie im [Abfrage Service-Benutzerhandbuch](ui/overview.md). Die RESTful-API bietet ein ähnliches Erlebnis, mit dem Sie programmatisch Abfragen schreiben und ausführen, Abfragen für die spätere Verwendung und Wiederholung planen und Vorlagen für Abfragen erstellen können, die Sie schreiben möchten. Weitere Informationen zur Verwendung der API finden Sie im [Abfrage Service Developer Guide](api/getting-started.md).[!DNL Query Service]

## [!DNL Query Service] und  [!DNL Experience Platform] Dienstleistungen

[!DNL Query Service] interagiert und kann in Verbindung mit mehreren  [!DNL Experience Platform] Diensten verwendet werden. Um die Funktionen von [!DNL Query Service's] optimal nutzen zu können, sollten Sie sich mit diesen Diensten und ihrer Interaktion mit [!DNL Query Service] vertraut machen.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] verwendet maschinelles Lernen und künstliche Intelligenz, um Einblicke aus Daten zu gewinnen, die innerhalb von [!DNL Experience Platform] gespeichert werden. [!DNL Data Science Workspace] ermöglicht es Datenwissenschaftlern, Rezepte zu erstellen, die auf Daten zu Kunden und deren Aktivitäten aus Aufzeichnungen und Zeitreihen basieren. Dies erleichtert Prognosen z. B. zu Kaufneigung und empfohlenen Angeboten, die von Einzelpersonen geschätzt und verwendet werden. Sie können SQL in [!DNL Data Science Workspace] verwenden, indem Sie [!DNL Query Service] in [!DNL JupyterLab] integrieren, sodass Sie Adobe Analytics-Daten untersuchen, transformieren und analysieren können. Lesen Sie die [!DNL Data Science Workspace]-Übersicht für weitere Informationen über [!DNL Data Science Workspace] und das [!DNL Query Service] Integrationsleitfaden für weitere Informationen zur Interaktion von [!DNL Data Science Workspace] mit [!DNL Query Service].

### [!DNL Segmentation Service]

Mit Adobe Experience Platform [!DNL Segmentation Service] können Benutzer ihre Kunden in kleinere Gruppen mit ähnlichen Eigenschaften unterteilen. Diese Segmente können anschließend ausgewertet werden, um eine bessere Analyse Ihrer [!DNL Real-time Customer Profile]-Daten zu gewährleisten. [!DNL Query Service] kann verwendet werden, um diese Analyse bereitzustellen, indem Abfragen für diese Segmentdaten in der  [!DNL Data Lake] ausgeführt werden. Weitere Informationen zur Segmentierung finden Sie in der [!DNL Segmentation Service]-Übersicht und im [!DNL Profile Query Language] (PQL)-Handbuch für weitere Informationen zur Segmentanalyse.

### Looker BI-Anwendungsfall

Mit Adobe Experience Platform können Sie alle gespeicherten Datensätze erfassen, speichern, strukturieren und abrufen — einschließlich Verhaltensdaten, CRM-Daten und Verkaufsdaten. Mithilfe von [!DNL Experience Platform's Query Service] können Sie Abfragen zu diesen Datensätzen durchführen und spezifische Fragen zum Geschäft beantworten und dann Beginn zu wirkungsvollen Einblicken führen. Das folgende Video zeigt den Wert, den das Erstellen von Dashboards in Business Intelligence-Werkzeugen mit [!DNL Query Service] hat.

>[!VIDEO](https://video.tv.adobe.com/v/28981?quality=12&learn=on)

## Nächste Schritte und zusätzliche Ressourcen

Durch das Lesen dieses Dokuments wurden Sie mit [!DNL Query Service] eingeführt und wie es im größeren Bereich von [!DNL Experience Platform] funktioniert. Weitere Informationen zur Interaktion mit verschiedenen Endpunkten in der [!DNL Query Service]-API finden Sie im [Abfrage Service Developer Guide](api/getting-started.md). Weitere Informationen zur Verwendung des interaktiven Dienstes innerhalb von [!DNL Platform] finden Sie im Benutzerhandbuch [Abfrage Service](ui/overview.md). Eine umfassende Liste zur Verbindung externer Clients mit [!DNL Query Service] finden Sie unter [Abfrage Service Clients overview](clients/overview.md).

Sehen Sie sich das folgende Video an, um sich besser darauf vorzubereiten, Abfragen auszuführen. In diesem Video werden Tipps und Best Practices für die Ausführung von Abfragen in der Benutzeroberfläche des Abfrage-Editors, PSQL-Clients, Business Intelligence-Lösungen (BI) und der HTTP-API vorgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/29811?quality=12&learn=on)
