---
keywords: Experience Platform;Startseite;beliebte Themen;API;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Workspace;enum;Feld;
solution: Experience Platform
title: Enum-Felder in der Benutzeroberfläche definieren
description: Erfahren Sie, wie Sie ein Enum-Feld in der Benutzeroberfläche "Experience Platform"definieren.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Definieren von Enum-Feldern in der Benutzeroberfläche

Im Erlebnis-Datenmodell (XDM) stellt ein Enum-Feld ein Feld dar, das auf eine vordefinierte Liste zulässiger Werte beschränkt ist.

Wenn Sie [ein neues Feld](./overview.md#define) in der Adobe Experience Platform-Benutzeroberfläche definieren, können Sie es als Enum-Feld festlegen, indem Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Enum]** aktivieren.

![](../../images/ui/fields/special/enum.png)

Nach dem Aktivieren des Kontrollkästchens werden weitere Steuerelemente angezeigt, mit denen Sie die Werteinschränkungen für die Enum festlegen können. Unter der Spalte **[!UICONTROL Wert]** müssen Sie den genauen Wert angeben, auf den Sie das Feld beschränken möchten. Dieser Wert muss mit dem für das Enum-Feld ausgewählten Wert übereinstimmen.  Sie können optional auch eine benutzerfreundliche **[!UICONTROL Beschriftung]** für die Beschränkung angeben.

Um der Enum weitere Einschränkungen hinzuzufügen, wählen Sie **[!UICONTROL Hinzufügen Zeile]**.

![](../../images/ui/fields/special/enum-add-row.png)

Fügen Sie der Enum weiterhin die gewünschten Einschränkungen und optionalen Beschriftungen hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]**, um die Änderungen auf das Schema anzuwenden.

![](../../images/ui/fields/special/enum-configured.png)

Die Arbeitsfläche wird aktualisiert, um die Änderungen widerzuspiegeln. Wenn Sie dieses Schema in der Zukunft erkunden, können Sie die Einschränkungen für das Enum-Feld in der rechten Leiste Ansicht und bearbeiten.

![](../../images/ui/fields/special/enum-applied.png)

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Sie ein Enum-Feld in der Benutzeroberfläche definieren. Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor] finden Sie in der Übersicht unter [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special).
