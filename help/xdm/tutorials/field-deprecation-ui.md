---
title: Verwerfen eines XDM-Felds in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Experience-Datenmodell (XDM)-Felder mit dem Schema-Editor in Experience Platform verwerfen können.
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: ht
source-wordcount: '699'
ht-degree: 100%

---

# Verwerfen eines XDM-Felds in der Benutzeroberfläche

Das Experience-Datenmodell (XDM) bietet Ihnen die Flexibilität, Ihr Datenmodell zu verwalten, wenn sich Ihre geschäftlichen Anforderungen ändern, indem Sie Schemafelder nach der Aufnahme von Daten verwerfen können. Unerwünschte Felder können verworfen werden, um sie aus der Ansicht der Benutzeroberfläche zu entfernen und sie auch in den nachgelagerten Benutzeroberflächen auszublenden. Praktischerweise können Sie mit einem Kontrollkästchen im Schema-Editor verworfene Felder anzeigen lassen und die Verwerfung bei Bedarf auch wieder aufheben.

Da verworfene Felder in der Benutzeroberfläche standardmäßig ausgeblendet werden, wird Ihr Schema im Schema-Editor optimiert und es wird verhindert, dass unerwünschte Felder zu nachgelagerten Abhängigkeiten wie Segment Builder, Journey Designer usw. hinzugefügt werden. Das Verwerfen von Feldern ist außerdem abwärtskompatibel. Andere Systeme, die verworfene Felder verwenden, wie etwa Segmente und Abfragen, werden weiterhin davon ausgehen, dass diese Verwendung erwünscht ist. Wenn ein verworfenes Feld in einem vorhandenen Segment verwendet wird, wird es wie normal behandelt. Das bedeutet, dass das Feld wie erwartet auf der Arbeitsfläche des Segmentaufbaus angezeigt oder basierend auf Daten ausgewertet wird, die in den verworfenen Feldern vorhanden sind. Dies ist keine grundlegende Änderung und hat keine negativen Auswirkungen auf bestehende Datenflüsse.

>[!NOTE]
>
>Bevor Daten in ein Schema aufgenommen werden, können Sie nicht benötigte Feldergruppen entfernen. Weitere Informationen finden Sie in der Dokumentation [Entfernen einer Feldergruppe aus einem Schema](../ui/resources/schemas.md#remove-fields).

Sobald Daten in Ihr Schema aufgenommen wurden, können Sie keine Felder mehr aus dem Schema entfernen, ohne grundlegende Änderungen vorzunehmen. In diesem Fall können Sie ein unerwünschtes Feld innerhalb eines Schemas oder einer benutzerdefinierten Ressource mit dem [Schema-Editor](./create-schema-ui.md) oder der [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/) verwerfen.

In diesem Dokument wird beschrieben, wie Sie Felder für verschiedene XDM-Ressourcen mithilfe des Schema-Editors in der Experience Platform-Benutzeroberfläche verwerfen können. Anweisungen zur Verwerfung eines XDM-Felds mithilfe der API finden Sie im Tutorial zum [Verwerfen eines XDM-Felds mithilfe der Schema Registry-API](./field-deprecation-api.md).

## Verwerfen eines Felds {#deprecate}

Um ein benutzerdefiniertes Feld zu verwerfen, navigieren Sie zum Schema-Editor für das Schema, das Sie bearbeiten möchten. Wählen Sie das Feld, das Sie verwerfen möchten, aus dem Abschnitt [!UICONTROL Struktur] der Arbeitsfläche aus und klicken Sie danach in den [!UICONTROL Feldeigenschaften] auf **[!UICONTROL Verwerfen]**.

![Der Schema-Editor mit einem ausgewählten Feld und der hervorgehobenen Option „Verwerfen“.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Es wird ein Dialogfeld angezeigt, mit dem Sie Ihre Auswahl bestätigen können und informiert werden, dass das Feld aus der Ansicht der Benutzeroberfläche des Vereinigungsschemas entfernt wurde und in den nachgelagerten Benutzeroberflächen ausgeblendet wird. Um die Aktion abzuschließen, klicken Sie auf **[!UICONTROL Bestätigen]**.

![Das Dialogfeld „Verwerfen“ mit hervorgehobener Option „Bestätigen“.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

Das Feld wird jetzt aus der Ansicht der Benutzeroberfläche entfernt.

>[!NOTE]
>
>Nach dem Verwerfen werden verworfene Felder in nachgelagerten Benutzeroberflächen wie Segmentierungs-Dashboards, Customer Journey Analytics und Adobe Journey Optimizer nicht mehr als Teil des Workflows angezeigt. Für nachgelagerten Benutzeroberflächen besteht jedoch die Möglichkeit, verworfene Felder bei Bedarf anzuzeigen und weiterhin wie normal zu behandeln. Weitere Informationen finden Sie in der entsprechenden Dokumentation. Abfragen und Segmente, die das verworfene Feld verwenden, werden wie erwartet ausgeführt.

## Anzeigen verworfener Felder {#show-deprecated}

Um zuvor verworfene Felder anzuzeigen, navigieren Sie im Schema-Editor zum entsprechenden Schema. Markieren Sie das Kästchen **[!UICONTROL Verworfene Felder anzeigen]** im Abschnitt [!UICONTROL Komposition] der Arbeitsfläche.

Das verworfene Feld wird jetzt in der Ansicht der Benutzeroberfläche angezeigt. Klicken Sie auf **[!UICONTROL Speichern]**, um Ihre Einstellungen zu bestätigen.

![Der Schema-Editor mit einem ausgewählten Feld und den hervorgehobenen Optionen „Verworfene Felder anzeigen“ und „Speichern“.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Aufheben der Verwerfung von Feldern {#undeprecate-fields}

Um das Verwerfen eines Feldes rückgängig zu machen, müssen Sie zunächst wie oben beschrieben [das verworfene Feld anzeigen](#show-deprecated) und es dann aus dem Abschnitt [!UICONTROL Struktur] des Editors auswählen. Wählen Sie als Nächstes **[!UICONTROL Verwerfung aufheben]** in der Seitenleiste [!UICONTROL Feldeigenschaften] aus und klicken Sie dann auf **[!UICONTROL Speichern]**.

![Der Schema-Editor mit dem verworfenen Feld und den hervorgehobenen Optionen „Verwerfung aufheben“ und „Speichern“.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

Das Dialogfeld [!UICONTROL Verwerfung aufheben] wird angezeigt. Um Ihre Änderungen zu bestätigen, klicken Sie auf **[!UICONTROL Bestätigen]**.

![Das Dialogfeld [!UICONTROL Verwerfung aufheben] mit hervorgehobener Option „Bestätigen“.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

Das Feld wird jetzt standardmäßig in der Ansicht der Benutzeroberfläche und auch in den nachgelagerten Benutzeroberflächen angezeigt. Sie haben erneut die Möglichkeit, das Feld zu verwerfen.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie XDM-Felder mithilfe der Benutzeroberfläche des Schema-Editors verworfen werden können. Weitere Informationen zum Konfigurieren von Feldern für benutzerdefinierte Ressourcen finden Sie im Handbuch unter [Definieren von XDM-Feldern in der API](./custom-fields-api.md). Weitere Informationen zum Verwalten von Deskriptoren finden Sie unter [Handbuch für Deskriptoren-Endpunkte](../api/descriptors.md).
