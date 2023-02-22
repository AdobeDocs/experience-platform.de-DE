---
title: Veraltetes XDM-Feld in der Benutzeroberfläche
description: Erfahren Sie, wie Sie Experience-Datenmodell (XDM)-Felder mit dem Schema Editor in Experience Platform verwerfen.
source-git-commit: f791d32ae38dffe82723800aa9fb5b44bb4f0109
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Veraltetes XDM-Feld in der Benutzeroberfläche

Das Experience-Datenmodell (XDM) bietet Ihnen die Flexibilität, Ihr Datenmodell zu verwalten, da sich Ihre geschäftlichen Anforderungen ändern, indem Schemafelder nach der Erfassung von Daten eingestellt werden. Unerwünschte Felder können nicht mehr unterstützt werden, um sie aus der UI-Ansicht zu entfernen und sie auch von den nachgelagerten Benutzeroberflächen auszublenden. Praktisch können Sie mit einem Kontrollkästchen im Schema Editor veraltete Felder anzeigen und bei Bedarf auch deren Veraltung aufheben.

Da veraltete Felder standardmäßig in der Benutzeroberfläche ausgeblendet werden, wird Ihr Schema im Schema-Editor optimiert und verhindert, dass unerwünschte Felder zu nachgelagerten Abhängigkeiten wie Segment-Builder, Journey-Designer usw. hinzugefügt werden. Die Einstellung von Feldern ist ebenfalls abwärtskompatibel. Andere Systeme, die veraltete Felder wie Segmente und Abfragen verwenden, werden diese weiterhin wie gewünscht auswerten. Wenn ein veraltetes Feld in einem vorhandenen Segment verwendet wird, wird es normal behandelt. Das bedeutet, dass das Feld wie erwartet auf der Arbeitsfläche des Segmentaufbaus angezeigt oder basierend auf Daten ausgewertet wird, die in den veralteten Feldern verfügbar sind. Hierbei handelt es sich um eine grundlegende Änderung, die keine negativen Auswirkungen auf bestehende Datenflüsse hat.

>[!NOTE]
>
>Bevor Daten in ein Schema aufgenommen werden, können Sie unnötige Feldergruppen entfernen. Weitere Informationen finden Sie in der Dokumentation unter [Entfernen einer Feldergruppe aus einem Schema](../ui/resources/schemas.md#remove-fields) für weitere Informationen.

Sobald Daten in Ihr Schema aufgenommen wurden, können Sie keine Felder mehr aus dem Schema entfernen, ohne die Änderungen zu verändern. In diesem Fall können Sie ein unerwünschtes Feld innerhalb eines Schemas oder einer benutzerdefinierten Ressource mit dem [Schema Editor](./create-schema-ui.md) oder [Schema Registry-API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

In diesem Dokument wird beschrieben, wie Sie Felder für verschiedene XDM-Ressourcen mithilfe des Schema-Editors in der Experience Platform-Benutzeroberfläche nicht mehr unterstützen. Anweisungen zur Einstellung eines XDM-Felds mithilfe der API finden Sie im Tutorial zu [Veraltung eines XDM-Felds mithilfe der Schema Registry-API](./field-deprecation-api.md).

## Veraltetes Feld {#deprecate}

Um ein benutzerdefiniertes Feld abzuschaffen, navigieren Sie zum Schema-Editor für das Schema, das Sie bearbeiten möchten. Wählen Sie das Feld aus, das Sie als veraltet festlegen möchten. [!UICONTROL Struktur] Abschnitt der Arbeitsfläche, gefolgt von **[!UICONTROL Veraltet]** von [!UICONTROL Feldeigenschaften].

![Der Schema-Editor mit einem ausgewählten Feld und Veralteter hervorgehoben.](../images/tutorials/field-deprecation/deprecate-single-field.png)

Es wird ein Dialogfeld angezeigt, in dem Sie Ihre Auswahl bestätigen und Sie darüber informieren, dass das Feld aus der UI-Ansicht des Vereinigungsschemas entfernt und von den nachgelagerten Benutzeroberflächen ausgeblendet wird. Um die Aktion abzuschließen, wählen Sie **[!UICONTROL Bestätigen]**.

![Das Dialogfeld Veraltetes Feld mit hervorgehobener Bestätigung.](../images/tutorials/field-deprecation/deprecate-field-dialog.png)

Das Feld wird jetzt aus der UI-Ansicht entfernt.

>[!NOTE]
>
>Nach der Einstellung werden in nachgelagerten Benutzeroberflächen wie Segmentierungs-Dashboards, Customer Journey Analytics und Adobe Journey Optimizer nicht mehr veraltete Felder als Teil ihres Workflows angezeigt. Die nachgelagerten Benutzeroberflächen haben jedoch die Möglichkeit, bei Bedarf veraltete Felder anzuzeigen und das veraltete Feld weiterhin normal zu behandeln. Weitere Informationen finden Sie in der entsprechenden Dokumentation . Abfragen und Segmente, die das veraltete Feld verwenden, werden wie erwartet ausgeführt.

## Veraltete Felder anzeigen {#show-deprecated}

Um zuvor veraltete Felder anzuzeigen, navigieren Sie im Schema Editor zum entsprechenden Schema. Wählen Sie die **[!UICONTROL Veraltete Felder anzeigen]** im [!UICONTROL Komposition] -Abschnitt der Arbeitsfläche.

Das veraltete Feld wird jetzt in der UI-Ansicht angezeigt. Auswählen **[!UICONTROL Speichern]** um Ihre Einstellungen zu bestätigen.

![Der Schema Editor mit einem ausgewählten Feld, veraltete Felder anzeigen und Speichern hervorgehoben.](../images/tutorials/field-deprecation/show-deprecated-fields.png)

## Nicht veraltete Felder {#undeprecate-fields}

Um ein veraltetes Feld rückgängig zu machen, müssen Sie zunächst [Anzeigen des veralteten Felds](#show-deprecated) wie oben beschrieben, wählen Sie dann das veraltete Feld aus der [!UICONTROL Struktur] Abschnitt. Wählen Sie als Nächstes **[!UICONTROL Undeprecate]** von [!UICONTROL Feldeigenschaften] Seitenleiste, gefolgt von **[!UICONTROL Speichern]**.

![Der Schema Editor mit dem veralteten Feld, Nicht mehr unterstützt und Speichern hervorgehoben.](../images/tutorials/field-deprecation/undeprecate-single-field.png)

Die [!UICONTROL Nicht veraltetes Feld] angezeigt. Um Ihre Änderungen zu bestätigen, wählen Sie **[!UICONTROL Bestätigen]**.

![Die [!UICONTROL Nicht veraltetes Feld] Dialogfeld mit hervorgehobener Bestätigung.](../images/tutorials/field-deprecation/undeprecate-field-dialog.png)

Das Feld wird jetzt standardmäßig in der UI-Ansicht und auch in den nachgelagerten Benutzeroberflächen angezeigt. Auch hier haben Sie die Möglichkeit, das Feld zu verwerfen.

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie XDM-Felder mithilfe der Schema Editor-Benutzeroberfläche veraltet werden. Weitere Informationen zum Konfigurieren von Feldern für benutzerdefinierte Ressourcen finden Sie im Handbuch unter [Definieren von XDM-Feldern in der API](./custom-fields-api.md). Weitere Informationen zum Verwalten von Deskriptoren finden Sie unter [Endpunktleitfaden für Deskriptoren](../api/descriptors.md).
