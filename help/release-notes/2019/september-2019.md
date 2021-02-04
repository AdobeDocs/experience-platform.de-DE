---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform vom 10. September 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 13%

---


# Adobe Experience Platform – Versionshinweise

**Release-Datum: 10. September 2019**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] bietet mehrere Alternativen zum Erfassen von Daten, einschließlich Batch-APIs, Streaming-APIs, nativen Adoben-Connectors, Data Integration-Partnern oder der Adobe Experience Platform-Benutzeroberfläche.

**Neue Funktionen**

| Funktion | Beschreibung |
| ----------- | ---------- |
| Neue Domäne für Streaming-Erfassung | Die Domäne `dcs.data.adobe.net` wurde in die neue allgemeine Datenerfassungsdomäne `dcs.adobedc.net` verschoben. Benutzer müssen ihre Implementierungen entsprechend der überarbeiteten Dokumentation zur Adobe Experience Platform-Streaming-Erfassung aktualisieren. Die Dokumentation zur Adobe Experience Platform-Streaming-Erfassung wurde aktualisiert und verwendet nun die neue Domäne. |

Weitere Informationen finden Sie in der [Dateneinbettungsdokumentation](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] ist ein vollständig verwalteter Dienst innerhalb von [!DNL Experience Platform], der Datenwissenschaftlern die nahtlose Erstellung von Einblicken aus Daten und Inhalten über Adoben- und Drittanbietersysteme hinweg ermöglicht, indem sie maschinelle Lernmodelle erstellen und operationalisieren. [!DNL Data Science Workspace] ist eng in den End-to-End-Datenwissenschaftslebenszyklus integriert  [!DNL Platform] und ermöglicht diese, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Operationalisierung von Modellen, um automatisch  [!DNL Real-time Customer Profile] mit Machine Learning Insights zu bereichern.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Einplanen von Diensten über die Benutzeroberfläche | Integration mit [!DNL Platform] Orchestration Service zur Automatisierung der Modellschulung und -auswertung mit benutzerdefinierten Zeitplänen mithilfe der Benutzeroberfläche. |
| [!DNL Service Gallery] | Durchsuchen, überwachen und Zugriff auf Services für maschinelles Lernen mit der Möglichkeit, automatisierte Schulungs- und Bewertungsaufträge zu planen, alle innerhalb der neu gestalteten [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Verbesserungen der Benutzeroberfläche. |

**Bekannte Probleme**

* Es gibt derzeit keine barrierefreie Möglichkeit in [!DNL Service Gallery], einen vorhandenen Dienst zu löschen. In der Zwischenzeit lesen Sie die [Sensei Machine Learning API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml), um einen vorhandenen Dienst über API-Aufrufe zu löschen.
* Das [!DNL Service Gallery] unterstützt keine Paginierung, um die Trainings- und Scoring-Vorgänge eines Dienstes zu filtern.
* Beim Konfigurieren einer geplanten Schulung oder Bewertung wird das [!DNL Service Gallery] ausgeführt. Wenn Sie die Häufigkeit auf stündlich einstellen, wird die Anwendung des Zeitplans verhindert.

Weitere Informationen finden Sie unter [Data Science Workspace – Überblick](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] bietet die Möglichkeit, Standarddaten von SQL zur Abfrage in Adobe Experience Platform zu verwenden, um eine Vielzahl von Analysen- und Data Management-Anwendungsfällen zu unterstützen. Es ist ein serverloses Tool, mit dem Sie Datasets aus dem [!DNL Data Lake] verbinden und die Abfragen als neues Dataset erfassen können, das in Berichte, [!DNL Data Science Workspace] oder zur Aufnahme in [!DNL Real-time Customer Profile] verwendet werden kann.

Sie können [!DNL Query Service] verwenden, um Ökosysteme für die Analyse von Daten zu erstellen und so ein Bild der Kunden über ihre verschiedenen Interaktionskenntnisse zu erstellen. Zu diesen Kanälen zählen u. a. Verkaufssysteme, Web-, Mobil- oder CRM-Systeme.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen an [!DNL Query Editor] | Es wurde eine Speicherfunktion hinzugefügt, mit der Sie eine Abfrage speichern und später daran arbeiten können. Es wurde eine Registerkarte &quot;Durchsuchen&quot;zur [!DNL Query Service]-Benutzeroberfläche auf Adobe Experience Platform hinzugefügt, die Abfragen anzeigt, die von Benutzern in Ihrem Unternehmen gespeichert wurden. Es wurde ein Bedienfeld mit Details zur Abfrage implementiert, in dem nützliche Metadaten zur angezeigten Abfrage angezeigt werden. |
| Neue Zuordnungsfunktionen | Adobe-definierte Funktionen in [!DNL Query Service] in Abfrage für die Kanal-Zuordnung mit Ablaufparametern. |
| Verbesserungen der SQL-Syntax | Unterstützung der &quot;Gefällt mir&quot;-Syntax. |
| Generieren von Datensätzen mit einem definierten XDM-Schema | Es wurde eine neue Klausel in &quot;Tabelle erstellen&quot;zu den Abfragen &quot;Auswählen&quot;(CTAS) hinzugefügt, mit der Sie ein Zielgruppe-Schema angeben können. |

Weitere Informationen finden Sie in der Dokumentation zum [Abfrage-Dienst](../../query-service/home.md).