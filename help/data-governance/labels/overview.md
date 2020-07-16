---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datennutzungsbezeichnungen – Übersicht
topic: labels
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 23%

---


# Datennutzungsbezeichnungen – Übersicht

Data Usage Labeling and Enforcement (DULE) ist der Kernmechanismus von Adobe Experience Platform [!DNL Data Governance]. Mit den im Rahmen von DULE bereitgestellten Funktionen lassen sich Datensätze und Felder anhand von Beschriftungen für die Datennutzung entsprechend den für sie geltenden Nutzungsrichtlinien kategorisieren.

Dieses Dokument bietet eine Übersicht über die Datenverwendungsbeschriftungen in [!DNL Experience Platform]. Bevor Sie dieses Handbuch lesen, lesen Sie sich die Übersicht über die [Datenverwaltung](../home.md) durch, um eine solidere Einführung in das DUL-Framework zu erhalten.

## Informationen zu den Datenverwendungsbeschreibungen

Mit Datennutzungsbeschriftungen können Sie Daten anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Beschriftungen können jederzeit angewendet werden, was eine flexible Handhabung der Daten ermöglicht. Best practices encourage labeling data as soon as it is ingested into [!DNL Experience Platform], or as soon as data becomes available for use in [!DNL Platform].

Datennutzungsbeschriftungen, die auf Datensatzebene angewendet werden, werden für alle Felder des Datensatzes übernommen. Außerdem können Beschriftungen direkt auf einzelne Felder (Spaltenüberschriften) in einem Datensatz angewendet werden, ohne dass eine Übernahme erfolgt.

[!DNL Platform] bietet mehrere standardmäßige &quot;Kern&quot;-Datenverwendungsbezeichnungen, die eine Vielzahl von allgemeinen Einschränkungen für die Datenverwaltung abdecken. Weitere Informationen zu diesen Beschriftungen und den von ihnen dargestellten Nutzungsrichtlinien finden Sie im Handbuch zu den [Gebrauchsbeschriftungen](reference.md)der Kerndaten.

Zusätzlich zu den von Adobe bereitgestellten Beschriftungen können Sie auch eigene benutzerdefinierte Beschriftungen definieren. Anweisungen dazu finden Sie im Benutzerhandbuch [zu den](./user-guide.md)Datenverwendungsbeschriftungen. Anweisungen dazu, wie Sie dies mithilfe von API-Aufrufen durchführen, finden Sie im API-Handbuch [für die](./api.md)Datenverwendung.

## Beschriftungsvererbung für Audiencen

Alle vom [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) erstellten Segmentsegmente übernehmen die Gebrauchsbeschriftungen der zugehörigen Datensätze. Dies ermöglicht Anwendungen, die auf [!DNL Experience Platform] (z. B. [!DNL Real-time Customer Data Platform]) aufbauen, eine automatische Durchsetzung der Datenverwendungsrichtlinien bei der Aktivierung von Segmenten an Ziele zu ermöglichen.

Neben der Vererbung von Bezeichnungen auf Datensatzebene übernehmen Segmente standardmäßig alle Bezeichnungen auf Feldebene aus den zugehörigen Datensätzen. Je nachdem, wie Ihre [!DNL Platform]basierte Anwendung Segmente verbraucht, können Sie potenziell angeben, welche Felder verwendet werden, wodurch verhindert wird, dass das Segment Beschriftungen aus ausgeschlossenen Feldern erbt.

Weitere Informationen zur Funktionsweise der automatischen Datendurchsetzung in Echtzeit-CDP finden Sie in der Übersicht [zur](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe Echtzeit-Datenverwaltung.

### Vererbung von Adobe Audience Manager Data Export Controls

[!DNL Experience Platform] hat die Möglichkeit, Segmente für Adobe Audience Manager freizugeben. Alle Datenexportsteuerelemente, die auf Audience Manager angewendet wurden, werden in entsprechende Beschriftungen und Marketingaktionen übersetzt, die von [!DNL Experience Platform][!DNL Data Governance]erkannt werden.

Eine Referenz dazu, wie bestimmte Datenexportsteuerelemente den Datenverwendungsbeschriftungen in zugeordnet werden, [!DNL Platform]finden Sie in der Dokumentation zum [Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).


## Nächste Schritte

Nachdem Sie die Bezeichnungen für die Datenverwendung eingeführt haben, können Sie das [Benutzerhandbuch](user-guide.md) lesen, um zu erfahren, wie Bezeichnungen in der [!DNL Experience Platform] Benutzeroberfläche verwaltet werden. Anweisungen zum Verwalten von Bezeichnungen mithilfe von APIs finden Sie im API-Handbuch [zu Nutzungsbezeichnungen](./api.md).