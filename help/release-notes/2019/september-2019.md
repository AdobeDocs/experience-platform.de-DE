---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform, 10. September 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 11%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 10. September 2019**

Aktualisierungen vorhandener Funktionen in der Adobe Experience Platform:

* [!DNL Data Ingestion](#ingestion)
* [!DNL Data Science Workspace](#dsw)
* [!DNL Query Service](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] provides multiple alternatives for ingesting data including Batch APIs, Streaming APIs, native Adobe connectors, data integration partners, or the Adobe Experience Platform UI.

**Neue Funktionen**

| Funktion | Beschreibung |
| ----------- | ---------- |
| Neue Domäne für Streaming-Erfassung | Die `dcs.data.adobe.net` Domäne wurde in die neue gemeinsame Datenerfassungsdomäne verschoben `dcs.adobedc.net`. Benutzer müssen ihre Implementierungen entsprechend der überarbeiteten Dokumentation zur Streaming-Erfassung von Adobe Experience Platformen aktualisieren. Die Dokumentation zur Adobe Experience Platform-Streaming-Erfassung wurde aktualisiert und verwendet nun die neue Domäne. |

Weitere Informationen finden Sie in der [Datenaufnahmendokumentation](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] is a fully managed service within [!DNL Experience Platform] that enables data scientists to seamlessly generate insights from data and content across Adobe solutions and third-party systems by building and operationalizing Machine Learning Models. [!DNL Data Science Workspace] ist eng in den End-to-End-Datenwissenschaftslebenszyklus integriert [!DNL Platform] [!DNL Real-time Customer Profile] und ermöglicht diese, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Inbetriebnahme von Modellen, um automatisch mit Machine Learning Insights zu bereichern.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Einplanen von Diensten über die Benutzeroberfläche | In [!DNL Platform] Orchestration Service integriert, um Modellschulungen und das Punktieren mit benutzerdefinierten Zeitplänen mithilfe der Benutzeroberfläche zu automatisieren. |
| [!DNL Service Gallery] | Durchsuchen, Überwachen und Zugreifen auf Services für maschinelles Lernen mit der Möglichkeit, automatisierte Schulungs- und Bewertungsaufträge zu planen, alles innerhalb der neu gestalteten [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Verbesserungen der Benutzeroberfläche. |

**Bekannte Probleme**

* Es gibt derzeit keine barrierefreie Möglichkeit, einen vorhandenen Dienst [!DNL Service Gallery] zu löschen. In der Zwischenzeit lesen Sie die [Sensei Machine Learning API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) , um einen vorhandenen Dienst über API-Aufrufe zu löschen.
* Der Dienst unterstützt [!DNL Service Gallery] keine Paginierung, um die Schulungs- und Bewertungsläufe eines Dienstes zu filtern.
* Wenn die Konfiguration einer geplanten Schulung oder Bewertung durch die [!DNL Service Gallery]Variable erfolgt, verhindert das Festlegen der Häufigkeit auf stündlich die Anwendung des Zeitplans.

Weitere Informationen finden Sie unter [Data Science Workspace – Überblick](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] bietet die Möglichkeit, Standarddaten von SQL zur Abfrage in Adobe Experience Platform zu verwenden, um eine Vielzahl von Analysen- und Data Management-Anwendungsfällen zu unterstützen. It is a serverless tool that allows you to join datasets from the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, [!DNL Data Science Workspace], or for ingestion into [!DNL Real-time Customer Profile].

You can use [!DNL Query Service] to build data analysis ecosystems, creating a picture of customers across their various interaction channels. Zu diesen Kanälen zählen u. a. Verkaufssysteme, Web-, Mobil- oder CRM-Systeme.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen bei [!DNL Query Editor] | Es wurde eine Speicherfunktion hinzugefügt, mit der Sie eine Abfrage speichern und später daran arbeiten können. Es wurde eine Registerkarte &quot;Durchsuchen&quot;zur [!DNL Query Service] Benutzeroberfläche auf Adobe Experience Platform hinzugefügt, die Abfragen anzeigt, die von Benutzern in Ihrem Unternehmen gespeichert wurden. Es wurde ein Bedienfeld mit Details zur Abfrage implementiert, in dem nützliche Metadaten zur angezeigten Abfrage angezeigt werden. |
| Neue Zuordnungsfunktionen | Von Adobe definierte Funktionen in [!DNL Query Service] der Abfrage für die Zuordnung von Kanälen mit Ablaufparametern. |
| Verbesserungen der SQL-Syntax | Unterstützung der &quot;Gefällt mir&quot;-Syntax. |
| Generieren von Datensätzen mit einem definierten XDM-Schema | Es wurde eine neue Klausel in &quot;Tabelle erstellen&quot;zu den Abfragen &quot;Auswählen&quot;(CTAS) hinzugefügt, mit der Sie ein Zielgruppe-Schema angeben können. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).