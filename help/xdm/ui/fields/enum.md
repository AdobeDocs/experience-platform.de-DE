---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Enum; Feld;
solution: Experience Platform
title: Definieren von Enum-Feldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche ein Enum-Feld definieren.
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---

# Definieren von Aufzählungsfeldern in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) stellt ein Enum-Feld ein Feld dar, das auf eine vordefinierte Liste zulässiger Werte beschränkt ist.

Wenn Sie [ein neues Feld](./overview.md#define) in der Adobe Experience Platform-Benutzeroberfläche definieren, können Sie es als Enum-Feld festlegen, indem Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Enum]** aktivieren.

![](../../images/ui/fields/special/enum.png)

Nach Auswahl des Kontrollkästchens werden zusätzliche Steuerelemente angezeigt, mit denen Sie die Wertbegrenzungen für die Aufzählung festlegen können. Unter der Spalte **[!UICONTROL Wert]** müssen Sie den genauen Wert angeben, auf den Sie das Feld beschränken möchten. Dieser Wert muss dem [!UICONTROL Typ] entsprechen, den Sie für das Enum-Feld ausgewählt haben. Sie können optional auch eine benutzerfreundliche **[!UICONTROL Beschriftung]** für die Beschränkung angeben.

Um dem Enum zusätzliche Einschränkungen hinzuzufügen, wählen Sie **[!UICONTROL Zeile hinzufügen]** aus.

![](../../images/ui/fields/special/enum-add-row.png)

Fügen Sie der Enum weiterhin die gewünschten Einschränkungen und optionalen Beschriftungen hinzu. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus, um die Änderungen auf das Schema anzuwenden.

![](../../images/ui/fields/special/enum-configured.png)

Die Arbeitsfläche wird entsprechend den Änderungen aktualisiert. Wenn Sie dieses Schema zukünftig untersuchen, können Sie die Begrenzungen für das Enum-Feld in der rechten Leiste anzeigen und bearbeiten.

![](../../images/ui/fields/special/enum-applied.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie in der Benutzeroberfläche ein Enum-Feld definieren. Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor] finden Sie in der Übersicht zu [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special).
