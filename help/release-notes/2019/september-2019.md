---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 10. September 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: e5fa12b92f7006f2c5c428b25f81dade57733498
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 4%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 10. September 2019**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [Dateneinbindung](#ingestion)
* [Data Science-Arbeitsbereich](#dsw)
* [Abfrage](#query)

## Dateneinbindung {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform Data Ingestion bietet mehrere Alternativen zum Erfassen von Daten, einschließlich Batch-APIs, Streaming-APIs, nativen Adobe-Connectors, Data Integration-Partnern oder der Benutzeroberfläche der Adobe Experience Platform.

**Neue Funktionen**

| Funktion | Beschreibung |
| ----------- | ---------- |
| Neue Domäne für Streaming-Erfassung | Die `dcs.data.adobe.net` Domäne wurde in die neue gemeinsame Datenerfassungsdomäne verschoben `dcs.adobedc.net`. Benutzer müssen ihre Implementierungen entsprechend der überarbeiteten Dokumentation zur Erfassung von Adobe Experience Platform-Streaming aktualisieren. Die gesamte Dokumentation zur Adobe Experience Platform-Streaming-Erfassung wurde aktualisiert und verwendet nun die neue Domäne. |

Weitere Informationen finden Sie in der [Datenaufnahmendokumentation](../../ingestion/home.md).

## Data Science-Arbeitsbereich {#dsw}

Adobe Experience Platform Data Science Workspace ist ein vollständig verwalteter Dienst innerhalb der Experience Platform, mit dem Datenwissenschaftler nahtlos Einblicke aus Daten und Inhalten in Adobe-Lösungen und Drittanbietersystemen generieren können, indem sie maschinelle Lernmodelle erstellen und operationalisieren. Data Science Workspace ist eng mit der Plattform integriert und ermöglicht den End-to-End-Data Science-Lebenszyklus, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Inbetriebnahme von Modellen, um das Echtzeit-Profil von Kunden automatisch mit Machine Learning Insights zu bereichern.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Einplanen von Diensten über die Benutzeroberfläche | In die Benutzeroberfläche integriert mit Platform Orchestration Service zur Automatisierung der Modellschulung und der Auswertung mit benutzerdefinierten Zeitplänen. |
| Servicegalerie | Durchsuchen, überwachen und auf die Services für maschinelles Lernen zugreifen mit der Möglichkeit, automatisierte Schulungs- und Bewertungsaufträge zu planen, alles innerhalb der neu gestalteten Service Gallery. |
| JupyterLab 5.0.0 | Verbesserungen der Benutzeroberfläche von JupyterLab. |

**Bekannte Probleme**

* Es gibt derzeit keine barrierefreie Möglichkeit in der Dienstgalerie, einen vorhandenen Dienst zu löschen. In der Zwischenzeit lesen Sie die [Sensei Machine Learning API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) , um einen vorhandenen Dienst über API-Aufrufe zu löschen.
* Die Service Gallery unterstützt keine Paginierung zum Filtern der Trainings- und Bewertungsläufe eines Dienstes.
* Wenn die Konfiguration einer geplanten Schulung oder Bewertung in der Service Gallery ausgeführt wird, verhindert das Festlegen der Häufigkeit auf stündlich die Anwendung des Zeitplans.

Weitere Informationen finden Sie unter Übersicht über den [Data Science Workspace](../../data-science-workspace/home.md).

## Abfrage {#query}

Abfrage Service bietet die Möglichkeit, Standarddaten aus SQL zur Abfrage in Adobe Experience Platform zu verwenden, um eine Vielzahl von Anwendungsfällen für Analyse und Data Management zu unterstützen. Es ist ein serverloses Tool, mit dem Sie Datasets aus dem Data Lake zusammenführen und die Abfragen als neuer Datensatz erfassen können, der in Berichte, Data Science Workspace oder zur Erfassung in Echtzeit-Kundendaten verwendet werden kann.

Mit dem Abfrage Service können Sie Ökosysteme zur Analyse von Daten erstellen und so ein Bild von Kunden über ihre verschiedenen Interaktionskunden hinweg erstellen. Zu diesen Kanälen zählen u. a. Verkaufssysteme, Web-, Mobil- oder CRM-Systeme.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen am Abfragen-Editor | Es wurde eine Speicherfunktion hinzugefügt, mit der Sie eine Abfrage speichern und später daran arbeiten können. Der Benutzeroberfläche des Abfrage Service auf der Adobe Experience Platform wurde die Registerkarte &quot;Durchsuchen&quot;hinzugefügt, auf der die von den Benutzern in Ihrem Unternehmen gespeicherten Abfragen angezeigt werden. Es wurde ein Bedienfeld mit Details zur Abfrage implementiert, in dem nützliche Metadaten zur angezeigten Abfrage angezeigt werden. |
| Neue Zuordnungsfunktionen | Von Adobe definierte Funktionen im Abfrage Service to Abfrage für die Zuweisung von Kanälen mit Ablaufparametern. |
| Verbesserungen der SQL-Syntax | Unterstützung der &quot;Gefällt mir&quot;-Syntax. |
| Generieren von Datensätzen mit einem definierten XDM-Schema | Es wurde eine neue Klausel in &quot;Tabelle erstellen&quot;zu den Abfragen &quot;Auswählen&quot;(CTAS) hinzugefügt, mit der Sie ein Zielgruppe-Schema angeben können. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).