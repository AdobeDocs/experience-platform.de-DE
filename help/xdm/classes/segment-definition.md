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

# [!UICONTROL Segmentdefinition] Klasse

&quot;[!UICONTROL Segmentdefinition]&quot; ist eine standardmäßige Klasse des Experience-Datenmodells (XDM), die die Details einer Segmentdefinition erfasst. Die Klasse enthält erforderliche Felder wie die ID und den Namen einer Zielgruppe sowie andere optionale Attribute. Diese Klasse sollte verwendet werden, wenn Sie Segmentdefinitionen aus externen Systemen in Adobe Experience Platform importieren.

>[!NOTE]
>
>Diese Klasse sollte nur verwendet werden, um Informationen über die Segmentdefinitionen selbst zu erfassen. Um Informationen zur Zielgruppenzugehörigkeit in Ihren Profildaten zu erfassen, sollten Sie die Feldergruppe [Details zur Segmentzugehörigkeit](../field-groups/profile/segmentation.md) in Ihrem Schema [!UICONTROL XDM Individual Profile] verwenden.

![](../images/classes/segment-definition.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das die folgenden &quot;[!UICONTROL &quot;-] enthält: <ul><li>`createDate`: Datum und die Uhrzeit, zu der die Ressource im Datenspeicher erstellt wurde, z. B. zum Zeitpunkt der ersten Datenaufnahme.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes nachzuverfolgen, Doppelungen von Daten zu verhindern und diesen Datensatz in nachgelagerten Services nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, wird bei der Datenaufnahme kein expliziter Wert bereitgestellt. Sie können jedoch auch weiterhin eigene eindeutige ID-Werte angeben, wenn Sie dies wünschen.<br><br>Es ist wichtig zu erkennen, dass dieses Feld **keine** Identität repräsentiert, die mit einer einzelnen Person in Verbindung steht, sondern den Datensatz an sich. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen auf [Identitätsfelder“ ](../schema/composition.md#identity) werden. |
| `createdByBatchID` | Die ID des erfassten Batches, der zur Erstellung des Datensatzes geführt hat. |
| `description` | Eine Beschreibung für die Segmentdefinition. |
| `identityMap` | Ein Zuordnungsfeld, das einen Satz von Identitäten mit Namespace für die Einzelpersonen enthält, für die die Zielgruppe gilt. Weitere Informationen zu ihrem Anwendungsfall finden Sie im Abschnitt [Identitätszuordnungen“ in ](../schema/composition.md#identityMap)Grundlagen der Schemakomposition“. |
| `modifiedByBatchID` | Die ID des zuletzt aufgenommenen Batches, der zur Aktualisierung des Datensatzes geführt hat. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |
| `segmentName` | **(Erforderlich)** Ein Name für die Segmentdefinition. |
| `segmentStatus` | Der Status der Zielgruppe aus dem externen System. Folgende Werte werden akzeptiert: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Die neueste Versionsnummer der Segmentdefinition. |

{style="table-layout:auto"}
