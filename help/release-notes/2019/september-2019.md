---
title: Adobe Experience Platform – Versionshinweise, September 2019
description: Versionshinweise September 2019 zu Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 15%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Mittwoch, 10. September 2019**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] bietet mehrere Alternativen für die Aufnahme von Daten, einschließlich Batch-APIs, Streaming-APIs, nativer Adobe-Connectoren, Datenintegrationspartnern oder der Adobe Experience Platform-Benutzeroberfläche.

**Neue Funktionen**

| Funktion | Beschreibung |
| ----------- | ---------- |
| Neue Domain für die Streaming-Aufnahme | Die `dcs.data.adobe.net` Domain wurde in die neue gemeinsame Datenerfassungsdomäne `dcs.adobedc.net` verschoben. Benutzende müssen ihre Implementierungen entsprechend der überarbeiteten Dokumentation zur Streaming-Aufnahme in Adobe Experience Platform aktualisieren. Die gesamte Dokumentation zur Aufnahme von Adobe Experience Platform-Streaming wurde aktualisiert, um die neue Domain zu verwenden. |

Weitere Informationen finden Sie in der [Dokumentation zur Datenaufnahme](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] ist ein vollständig verwalteter Service innerhalb von [!DNL Experience Platform], mit dem Datenwissenschaftler nahtlos Einblicke aus Daten und Inhalten in Adobe-Lösungen und Drittanbietersystemen generieren können, indem sie Modelle für maschinelles Lernen erstellen und umsetzen. [!DNL Data Science Workspace] ist eng in [!DNL Experience Platform] integriert und unterstützt den gesamten Datenwissenschafts-Lebenszyklus, einschließlich der Untersuchung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Operationalisierung von Modellen zur automatischen Anreicherung von [!DNL Real-Time Customer Profile] mit Einblicken aus maschinellem Lernen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Planung von Services über die Benutzeroberfläche | Integriert mit [!DNL Experience Platform] Orchestration Service zur Automatisierung des Modell-Trainings und der Bewertung mit benutzerdefinierten Zeitplänen über die Benutzeroberfläche. |
| [!DNL Service Gallery] | Durchsuchen, Überwachen und Zugreifen auf Services für maschinelles Lernen mit der Möglichkeit, automatisierte Schulungs- und Bewertungsaufträge zu planen, und das alles innerhalb der neu gestalteten [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | Verbesserungen der [!DNL JupyterLab]-Benutzeroberfläche. |

**Bekannte Probleme**

* In der [!DNL Service Gallery] gibt es derzeit keine barrierefreie Möglichkeit, einen vorhandenen Service zu löschen. In der Zwischenzeit verwenden Sie die [API-Referenz für maschinelles Lernen von Sensei](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) um einen vorhandenen Service über API-Aufrufe zu löschen.
* Der [!DNL Service Gallery] verfügt nicht über Paginierungsunterstützung, um die Trainings- und Bewertungsdurchgänge eines Services zu filtern.
* Bei der Konfiguration geplanter Trainings- oder Scoring-Läufe durch den [!DNL Service Gallery] verhindert das Festlegen der Häufigkeit auf Stündlich, dass der Zeitplan angewendet wird.

Weitere Informationen finden Sie unter [Data Science Workspace – Überblick](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] bietet die Möglichkeit, in Adobe Experience Platform standardmäßige SQL zur Abfrage von Daten zu verwenden, um eine Vielzahl von Anwendungsfällen für Analyse und Daten-Management zu unterstützen. Es handelt sich dabei um ein Server-loses Tool, mit dem Sie Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz erfassen können, der bei Reporting- und [!DNL Data Science Workspace] oder zur Aufnahme in [!DNL Real-Time Customer Profile] verwendet werden kann.

Sie können [!DNL Query Service] verwenden, um Ökosysteme für die Datenanalyse zu erstellen und sich ein Bild über die Kunden über ihre verschiedenen Interaktionskanäle hinweg zu machen. Zu diesen Kanälen können Point-of-Sale-Systeme, Web-, Mobile- oder CRM-Systeme gehören.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen an [!DNL Query Editor] | Es wurde eine Speicherfunktion hinzugefügt, mit der Sie eine Abfrage speichern und später daran arbeiten können. Der [!DNL Query Service]-Benutzeroberfläche in Adobe Experience Platform wurde eine Registerkarte „Durchsuchen“ hinzugefügt, auf der Abfragen angezeigt werden, die von Benutzenden in Ihrem Unternehmen gespeichert wurden. Es wurde ein Bedienfeld „Abfragedetails“ implementiert, das nützliche Metadaten zur angezeigten Abfrage anzeigt. |
| Neue Attributionsfunktionen | Adobe-definierte Funktionen in , [!DNL Query Service] die Kanalzuordnung mit Ablaufparametern abzufragen. |
| Verbesserungen der SQL-Syntax | Unterstützung für iLike-Syntax. |
| Generieren von Datensätzen mit einem definierten XDM-Schema | Es wurde eine neue -Klausel in CTAS-Abfragen (Create Table As Select) hinzugefügt, mit der Sie ein Zielschema angeben können. |

Weitere Informationen finden Sie in der [Dokumentation zu Query Service](../../query-service/home.md).
