---
keywords: Experience Platform;Startseite;beliebte Themen;API;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Array;Feld;
solution: Experience Platform
title: Definieren von Array-Feldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie ein Array-Feld in der Experience Platform-Benutzeroberfläche definieren.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definieren von Array-Feldern in der Benutzeroberfläche

Beim Definieren eines Experience-Datenmodell (XDM)-Felds in der Adobe Experience Platform-Benutzeroberfläche können Sie dieses Feld als Array festlegen.

Der Inhalt des Arrays hängt von dem für [!UICONTROL &#x200B; Feld &#x200B;]Typ“ ab. Wenn beispielsweise der „Typ eines Felds auf &quot;[!UICONTROL Zeichenfolge]&quot; festgelegt ist, wird das Feld durch Festlegen dieses Felds als Array als Array von Zeichenfolgen gekennzeichnet. Wenn der [!UICONTROL Typ] des Felds auf einen Mehrfeld-Datentyp wie &quot;[!UICONTROL Postanschrift]&quot; festgelegt ist, wird es zu einem Array von Postanschrift-Objekten, die dem Datentyp entsprechen.

Nachdem Sie [&#x200B; neues Feld in der Benutzeroberfläche definiert haben](./overview.md#define) können Sie es als Array-Feld festlegen, indem Sie das Kontrollkästchen **[!UICONTROL Array]** in der rechten Leiste aktivieren.

![](../../images/ui/fields/special/array.png)

Sobald das Kontrollkästchen aktiviert ist, werden zusätzliche Steuerelemente in der rechten Leiste angezeigt, mit denen Sie das Array optional weiter einschränken können. Wenn Sie eine bestimmte Einschränkung nicht erzwingen möchten, lassen Sie das Feld leer.

Die zusätzlichen Konfigurationssteuerelemente für Arrays lauten wie folgt:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Mindestlänge] | Die Mindestanzahl von Elementen, die das Array enthalten muss, damit die Aufnahme erfolgreich ist. |
| [!UICONTROL Maximale Länge] | Die maximale Anzahl von Elementen, die das Array enthalten muss, damit die Aufnahme erfolgreich ist. |
| [!UICONTROL Nur eindeutige Elemente] | Wenn auf &quot;[!UICONTROL True]&quot; festgelegt, muss jedes Element im Array eindeutig sein, damit die Aufnahme erfolgreich ist. |

{style="table-layout:auto"}

Nachdem Sie mit der Konfiguration des Felds fertig sind, wählen Sie **[!UICONTROL Anwenden]** aus, um die Änderung auf das Schema anzuwenden.

![](../../images/ui/fields/special/array-config.png)

Die Arbeitsfläche wird aktualisiert, um die am Feld vorgenommenen Änderungen widerzuspiegeln. Beachten Sie, dass an den neben dem Feldnamen auf der Arbeitsfläche angezeigten Datentyp ein Paar eckiger Klammern (`[]`) angehängt ist, was angibt, dass das Feld ein Array dieses Datentyps darstellt.

![](../../images/ui/fields/special/array-applied.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein Array-Feld in der Benutzeroberfläche definieren. In der Übersicht über [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) erfahren Sie, wie Sie andere XDM-Feldtypen in der [!DNL Schema Editor] definieren.
