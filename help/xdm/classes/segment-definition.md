---
solution: Experience Platform
title: Segmentdefinitionsklasse
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über die Segmentdefinitionsklasse im Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# [!UICONTROL Segment-] Definitionsklasse

&quot;[!UICONTROL Segmentdefinition]&quot;ist eine XDM-Standardklasse (Experience Data Model), die die Details einer Segmentdefinition erfasst. Die Klasse enthält erforderliche Felder wie die ID und den Namen eines Segments sowie andere optionale Attribute. Diese Klasse sollte verwendet werden, wenn Sie Segmentdefinitionen von externen Systemen in Adobe Experience Platform einbinden.

>[!NOTE]
>
>Diese Klasse sollte nur zur Erfassung von Informationen über Segmentdefinitionen selbst verwendet werden. Um Informationen zur Segmentmitgliedschaft in Ihren Profil-Daten zu erfassen, sollten Sie das [Segment-Mitgliedschaftsdetails-Gemisch](../mixins/profile/segmentation.md) in Ihrem [!UICONTROL XDM-Profil]-Schema verwenden.

![](../images/classes/segment-definition.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| `_repo` | Ein Objekt, das die folgenden [!UICONTROL DateTime]-Felder enthält: <ul><li>`createDate`: Datum und Uhrzeit der Erstellung der Ressource im Datenspeicher, z. B. wann die Daten zum ersten Mal erfasst wurden.</li><li>`modifyDate`: Datum und Uhrzeit der letzten Änderung der Ressource.</li></ul> |
| `_id` | Ein eindeutiger, vom System generierter Zeichenfolgenbezeichner für den Datensatz. Dieses Feld dient zur Verfolgung der Einzigartigkeit eines einzelnen Datensatzes, zur Vermeidung von Datenduplizierungen und zur Nachforschung dieses Datensatzes in nachgelagerten Diensten.<br><br>Da dieses Feld vom System generiert wird, wird bei der Datenerfassung kein expliziter Wert angegeben. Sie können jedoch auch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten.<br><br>Es ist wichtig zu unterscheiden, dass dieses Feld  **keine Identität** darstellt, die sich auf eine Person bezieht, sondern vielmehr die Aufzeichnung der Daten selbst. Identitätsdaten, die sich auf eine Person beziehen, sollten stattdessen in [Identitätsfelder](../schema/composition.md#identity) umbenannt werden. |
| `createdByBatchID` | Die ID des erfassten Stapels, die zur Erstellung des Datensatzes geführt hat. |
| `description` | Eine Beschreibung der Segmentdefinition. |
| `identityMap` | Ein Zuordnungsfeld, das eine Reihe von benannten Identitäten für die Personen enthält, für die das Segment gilt. Dieses Feld wird vom System automatisch aktualisiert, wenn Identitätsdaten erfasst werden.<br /><br />Weitere Informationen zum Anwendungsfall finden Sie im Abschnitt zu Identitätskarten in den  [Grundlagen der ](../schema/composition.md#identityMap) Schema-Komposition. |
| `modifiedByBatchID` | Die ID des letzten erfassten Stapels, der zur Aktualisierung des Datensatzes geführt hat. |
| `repositoryCreatedBy` | Die ID des Benutzers, der den Datensatz erstellt hat. |
| `repositoryLastModifiedBy` | Die ID des Benutzers, der den Datensatz zuletzt geändert hat. |
| `segmentName` | **(Erforderlich)** Ein Name für die Segmentdefinition. |
| `segmentStatus` | Der Status des Segments vom externen System. Die folgenden Werte werden akzeptiert: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Die aktuelle Versionsnummer der Segmentdefinition. |
