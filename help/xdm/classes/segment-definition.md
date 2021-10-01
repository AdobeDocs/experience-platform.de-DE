---
solution: Experience Platform
title: Segmentdefinitionsklasse
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über die Segmentdefinitionsklasse im Experience-Datenmodell (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 632ea4e2a94bfcad098a5fc5a5ed8985c0f41e0e
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 1%

---

# [!UICONTROL Segment ] definitionclass

&quot;[!UICONTROL Segmentdefinition]&quot;ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die Details einer Segmentdefinition erfasst. Die Klasse enthält erforderliche Felder wie die ID und den Namen eines Segments sowie andere optionale Attribute. Diese Klasse sollte verwendet werden, wenn Sie Segmentdefinitionen aus externen Systemen in Adobe Experience Platform einbinden.

>[!NOTE]
>
>Diese Klasse sollte nur zum Erfassen von Informationen zu Segmentdefinitionen selbst verwendet werden. Um Segmentmitgliedschaftsinformationen in Ihren Profildaten zu erfassen, sollten Sie die Feldergruppe [Segmentzugehörigkeitsdetails](../field-groups/profile/segmentation.md) in Ihrem Schema [!UICONTROL XDM Individual Profile] verwenden.

![](../images/classes/segment-definition.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das die folgenden [!UICONTROL DateTime]-Felder enthält: <ul><li>`createDate`: Datum und Uhrzeit der Erstellung der Ressource im Datenspeicher, z. B. Zeitpunkt der ersten Datenerfassung.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten.<br><br>Es ist wichtig zu unterscheiden, dass dieses Feld  **keine Identität** darstellt, die sich auf eine Person bezieht, sondern vielmehr den Datensatz selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder](../schema/composition.md#identity) umgeleitet werden. |
| `createdByBatchID` | Die ID des erfassten Batches, der zur Erstellung des Datensatzes geführt hat. |
| `description` | Eine Beschreibung für die Segmentdefinition. |
| `identityMap` | Ein map -Feld, das eine Reihe von Namespaced-Identitäten für die Einzelanwender enthält, für die das Segment gilt. Weitere Informationen zu ihrem Anwendungsfall finden Sie im Abschnitt zu Identitätskarten in den [Grundlagen der Schemakomposition](../schema/composition.md#identityMap) . |
| `modifiedByBatchID` | Die ID des letzten erfassten Batches, der zur Aktualisierung des Datensatzes geführt hat. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |
| `segmentName` | **(Erforderlich)** Ein Name für die Segmentdefinition. |
| `segmentStatus` | Der Status des Segments vom externen System. Folgende Werte werden akzeptiert: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Die aktuelle Versionsnummer der Segmentdefinition. |
