---
title: Adobe Experience Platform – Versionshinweise, September 2019
description: Versionshinweise September 2019 zu Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
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

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] bietet mehrere Alternativen zum Erfassen von Daten, einschließlich Batch-APIs, Streaming-APIs, nativen Adobe-Connectoren, Datenintegrationspartnern oder der Adobe Experience Platform-Benutzeroberfläche.

**Neue Funktionen**

| Funktion | Beschreibung |
| ----------- | ---------- |
| Neue Domäne für Streaming-Erfassung | Die Domäne `dcs.data.adobe.net` wurde in die neue gemeinsame Datenerfassungsdomäne `dcs.adobedc.net` verschoben. Benutzer müssen ihre Implementierungen entsprechend der überarbeiteten Dokumentation zur Streaming-Erfassung in Adobe Experience Platform aktualisieren. Die gesamte Dokumentation zur Streaming-Erfassung in Adobe Experience Platform wurde aktualisiert und verwendet nun die neue Domäne. |

Weitere Informationen finden Sie in der Dokumentation zur [Datenerfassung](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] ist ein vollständig verwalteter Dienst in [!DNL Experience Platform], der es Datenwissenschaftlern ermöglicht, nahtlos Einblicke aus Daten und Inhalten aus Adobe-Lösungen und Drittanbietersystemen zu generieren, indem sie Modelle für maschinelles Lernen erstellen und umsetzen. [!DNL Data Science Workspace] ist eng in [!DNL Platform] integriert und ermöglicht den End-to-End-Lebenszyklus der Datenwissenschaft, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Inbetriebnahme von Modellen, um [!DNL Real-Time Customer Profile] automatisch mit Einblicken aus maschinellem Lernen anzureichern.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Planung von Diensten über die Benutzeroberfläche | Mit [!DNL Platform] Orchestration Service integriert, um Modellschulung und -bewertung mit benutzerdefinierten Zeitplänen mithilfe der Benutzeroberfläche zu automatisieren. |
| [!DNL Service Gallery] | Durchsuchen, überwachen und greifen Sie auf maschinelle Lerndienste zu, mit der Möglichkeit, automatisierte Trainings- und Scoring-Aufträge zu planen - alles innerhalb des neu gestalteten [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Verbesserungen der Benutzeroberfläche. |

**Bekannte Probleme**

* In der [!DNL Service Gallery] gibt es derzeit keine barrierefreie Möglichkeit, einen vorhandenen Dienst zu löschen. In der Zwischenzeit lesen Sie die [Sensei Machine Learning API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) , um einen vorhandenen Dienst über API-Aufrufe zu löschen.
* Die [!DNL Service Gallery] unterstützt keine Paginierung, um die Trainings- und Scoring-Läufe eines Dienstes zu filtern.
* Beim Konfigurieren geplanter Schulungen oder Scoring-Läufe über die [!DNL Service Gallery] hinweg verhindert das Festlegen der Häufigkeit auf stündlich , dass der Zeitplan angewendet wird.

Weitere Informationen finden Sie unter [Data Science Workspace – Überblick](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] bietet die Möglichkeit, SQL-Standarddaten zur Abfrage in Adobe Experience Platform zu verwenden, um eine Vielzahl von Anwendungsfällen für Analysen und Daten-Management zu unterstützen. Es handelt sich dabei um ein Server-loses Tool, mit dem Sie Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz erfassen können, der in Berichten, [!DNL Data Science Workspace] oder zur Aufnahme in [!DNL Real-Time Customer Profile] verwendet werden kann.

Mit [!DNL Query Service] können Sie Ökosysteme für die Datenanalyse erstellen und ein Bild von Kunden über ihre verschiedenen Interaktionskanäle hinweg erstellen. Diese Kanäle können Point-of-Sale-Systeme, Web-, Mobile- oder CRM-Systeme umfassen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen an [!DNL Query Editor] | Es wurde eine Speicherfunktion hinzugefügt, mit der Sie eine Abfrage speichern und später daran arbeiten können. Der Benutzeroberfläche von Adobe Experience Platform wurde die Registerkarte &quot;Durchsuchen&quot;hinzugefügt, auf der die von Benutzern in Ihrer Organisation gespeicherten Abfragen angezeigt werden. [!DNL Query Service] Es wurde ein Bedienfeld &quot;Abfragedetails&quot;implementiert, das nützliche Metadaten zur angezeigten Abfrage anzeigt. |
| Neue Attributionsfunktionen | Adobe-definierte Funktionen in [!DNL Query Service] , um die Kanalzuordnung mit Ablaufparametern abzufragen. |
| Verbesserungen der SQL-Syntax | Unterstützung der iLike-Syntax. |
| Generieren von Datensätzen mit einem definierten XDM-Schema | Es wurde eine neue Klausel in Tabelle als Select (CTAS)-Abfragen erstellen hinzugefügt, mit der Sie ein Zielschema angeben können. |

Weitere Informationen finden Sie in der [Dokumentation zu Query Service](../../query-service/home.md).
