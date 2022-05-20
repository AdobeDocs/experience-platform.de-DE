---
title: Adobe Experience Platform - Versionshinweise - September 2019
description: Die Versionshinweise für Adobe Experience Platform vom September 2019.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 13%

---

# Adobe Experience Platform – Versionshinweise

**Release-Datum: 10. September 2019**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen, mit denen Daten jeder Art und Latenzzeit erfasst werden können. Adobe Experience Platform [!DNL Data Ingestion] bietet mehrere Alternativen zum Erfassen von Daten, einschließlich Batch-APIs, Streaming-APIs, nativen Adobe-Connectoren, Datenintegrationspartnern oder der Adobe Experience Platform-Benutzeroberfläche.

**Neue Funktionen**

| Funktion | Beschreibung |
| ----------- | ---------- |
| Neue Domäne für Streaming-Erfassung | Die `dcs.data.adobe.net` Die Domäne wurde in die neue gemeinsame Datenerfassungsdomäne verschoben. `dcs.adobedc.net`. Benutzer müssen ihre Implementierungen entsprechend der überarbeiteten Dokumentation zur Streaming-Erfassung in Adobe Experience Platform aktualisieren. Die gesamte Dokumentation zur Streaming-Erfassung in Adobe Experience Platform wurde aktualisiert und verwendet nun die neue Domäne. |

Weitere Informationen finden Sie unter [Dokumentation zur Datenerfassung](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] ist ein vollständig verwalteter Dienst in [!DNL Experience Platform] ermöglicht es Datenwissenschaftlern, nahtlos Einblicke aus Daten und Inhalten über Adobe-Lösungen und Drittanbietersysteme zu generieren, indem sie Modelle für maschinelles Lernen erstellen und umsetzen. [!DNL Data Science Workspace] eng in [!DNL Platform] und ermöglicht den durchgängigen Data Science-Lebenszyklus, einschließlich der Erforschung und Vorbereitung von XDM-Daten, gefolgt von der Entwicklung und Inbetriebnahme von Modellen zur automatischen Anreicherung [!DNL Real-time Customer Profile] mit Insights für maschinelles Lernen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Planung von Diensten über die Benutzeroberfläche | Integriert mit [!DNL Platform] Orchestration Service zur Automatisierung der Modellschulung und -bewertung mit benutzerdefinierten Zeitplänen über die Benutzeroberfläche. |
| [!DNL Service Gallery] | Durchsuchen, Überwachen und Zugreifen auf maschinelle Lerndienste mit der Möglichkeit, automatisierte Trainings- und Scoring-Aufträge zu planen - alles innerhalb der neu gestalteten [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5,0,0 | [!DNL JupyterLab] Verbesserungen der Benutzeroberfläche. |

**Bekannte Probleme**

* Es gibt derzeit keine barrierefreie Methode in der [!DNL Service Gallery] , um einen vorhandenen Dienst zu löschen. In der Zwischenzeit siehe [Sensei Machine Learning API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) , um einen vorhandenen Dienst über API-Aufrufe zu löschen.
* Die [!DNL Service Gallery] unterstützt keine Paginierung, um die Trainings- und Scoring-Läufe eines Dienstes zu filtern.
* Beim Konfigurieren geplanter Schulungen oder Scoring-Läufe durch die [!DNL Service Gallery], wodurch die Häufigkeit auf stündlich gesetzt wird, verhindert wird, dass der Zeitplan angewendet wird.

Weitere Informationen finden Sie unter [Data Science Workspace – Überblick](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] bietet die Möglichkeit, SQL-Standard zur Abfrage von Daten in Adobe Experience Platform zu verwenden, um eine Vielzahl von Anwendungsfällen für Analyse und Datenverwaltung zu unterstützen. Es ist ein Server-loses Tool, mit dem Sie Datensätze aus der [!DNL Data Lake] und erfassen Sie die Abfrageergebnisse als neuen Datensatz zur Verwendung in Berichten, [!DNL Data Science Workspace]oder zur Aufnahme in [!DNL Real-time Customer Profile].

Sie können [!DNL Query Service] um Ökosysteme für Datenanalysen zu erstellen und so ein Bild der Kunden über ihre verschiedenen Interaktionskanäle hinweg zu erstellen. Diese Kanäle können Point-of-Sale-Systeme, Web-, Mobile- oder CRM-Systeme umfassen.

**Neue Funktionen**

| Funktion | Beschreibung |
| -----------| ---------- |
| Verbesserungen bei [!DNL Query Editor] | Es wurde eine Speicherfunktion hinzugefügt, mit der Sie eine Abfrage speichern und später daran arbeiten können. Die Registerkarte &quot;Durchsuchen&quot;wurde zum [!DNL Query Service] -Benutzeroberfläche in Adobe Experience Platform, die die von Benutzern in Ihrem Unternehmen gespeicherten Abfragen anzeigt. Es wurde ein Bedienfeld &quot;Abfragedetails&quot;implementiert, das nützliche Metadaten zur angezeigten Abfrage anzeigt. |
| Neue Attributionsfunktionen | Adobe-definierte Funktionen in [!DNL Query Service] , um nach der Kanalzuordnung mit Ablaufparametern zu suchen. |
| Verbesserungen der SQL-Syntax | Unterstützung der iLike-Syntax. |
| Generieren von Datensätzen mit einem definierten XDM-Schema | Es wurde eine neue Klausel in Tabelle als Select (CTAS)-Abfragen erstellen hinzugefügt, mit der Sie ein Zielschema angeben können. |

Weitere Informationen finden Sie in der [Dokumentation zu Query Service](../../query-service/home.md).
