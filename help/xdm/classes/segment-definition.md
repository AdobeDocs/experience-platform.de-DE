---
solution: Experience Platform
title: Segmentdefinitionsklasse
description: Erfahren Sie mehr über die Segmentdefinitionsklasse im Experience-Datenmodell (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# [!UICONTROL Segmentdefinition] class

&quot;[!UICONTROL Segmentdefinition]&quot; ist eine standardmäßige Experience-Datenmodell (XDM)-Klasse, die die Details einer Segmentdefinition erfasst. Die Klasse enthält erforderliche Felder wie die ID und den Namen einer Zielgruppe sowie andere optionale Attribute. Diese Klasse sollte verwendet werden, wenn Sie Segmentdefinitionen aus externen Systemen in Adobe Experience Platform einbinden.

>[!NOTE]
>
>Diese Klasse sollte nur zum Erfassen von Informationen zu Segmentdefinitionen selbst verwendet werden. Um Informationen zur Zielgruppenmitgliedschaft in Ihren Profildaten zu erfassen, sollten Sie die [Feldergruppe Segmentzugehörigkeitsdetails](../field-groups/profile/segmentation.md) in [!UICONTROL Individuelles XDM-Profil] Schema.

![](../images/classes/segment-definition.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das Folgendes enthält: [!UICONTROL DateTime] -Felder: <ul><li>`createDate`: Datum und Uhrzeit der Erstellung der Ressource im Datenspeicher, z. B. Zeitpunkt der ersten Datenerfassung.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten.<br><br>Es ist wichtig zu unterscheiden, dass dieses Feld **nicht** eine Identität darstellen, die mit einer Person in Verbindung steht, sondern den Datensatz selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten [Identitätsfelder](../schema/composition.md#identity) anstatt. |
| `createdByBatchID` | Die ID des erfassten Batches, der zur Erstellung des Datensatzes geführt hat. |
| `description` | Eine Beschreibung für die Segmentdefinition. |
| `identityMap` | Ein Zuordnungsfeld mit einem Satz von Namespaced-Identitäten für die Kontakte, für die die Zielgruppe gilt. Siehe Abschnitt zu Identitätskarten im Abschnitt [Grundlagen der Schemakomposition](../schema/composition.md#identityMap) für weitere Informationen zu ihrem Anwendungsfall. |
| `modifiedByBatchID` | Die ID des letzten erfassten Batches, der zur Aktualisierung des Datensatzes geführt hat. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |
| `segmentName` | **(Erforderlich)** Ein Name für die Segmentdefinition. |
| `segmentStatus` | Der Status der Zielgruppe aus dem externen System. Folgende Werte werden akzeptiert: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Die aktuelle Versionsnummer der Segmentdefinition. |

{style="table-layout:auto"}
