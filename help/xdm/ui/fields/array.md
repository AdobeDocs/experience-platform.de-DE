---
keywords: Experience Platform; home; beliebte Themen; API; XDM; XDM; XDM-System; Erlebnisdatenmodell; Datenmodell; ui; workspace; Array; field;
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

Beim Definieren eines XDM-Felds (Experience-Datenmodell) in der Benutzeroberfläche von Adobe Experience Platform können Sie dieses Feld als Array festlegen.

Der Inhalt des Arrays hängt vom für dieses Feld ausgewählten [!UICONTROL Typ] ab. Wenn beispielsweise der [!UICONTROL Typ] eines Felds auf &quot;[!UICONTROL String]&quot; gesetzt ist, wird das Feld durch Festlegen dieses Felds als Array als Zeichenfolgen-Array gekennzeichnet. Wenn der [!UICONTROL Typ] des Felds auf einen Datentyp mit mehreren Feldern festgelegt ist, z. B. &quot;[!UICONTROL Postanschrift]&quot;, würde dies zu einem Array von Postadressobjekten werden, die dem Datentyp entsprechen.

Nachdem Sie [ein neues Feld in der Benutzeroberfläche](./overview.md#define) definiert haben, können Sie es als Array-Feld festlegen, indem Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Array]** aktivieren.

![](../../images/ui/fields/special/array.png)

Sobald das Kontrollkästchen aktiviert ist, werden in der rechten Leiste zusätzliche Steuerelemente angezeigt, mit denen Sie das Array optional weiter einschränken können. Wenn Sie eine bestimmte Einschränkung nicht erzwingen möchten, lassen Sie das Feld leer.

Die zusätzlichen Konfigurationssteuerelemente für Arrays lauten wie folgt:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Mindestlänge] | Die Mindestanzahl von Elementen, die das Array enthalten muss, damit die Aufnahme erfolgreich ist. |
| [!UICONTROL Maximale Länge] | Die maximale Anzahl von Elementen, die das Array enthalten muss, damit die Aufnahme erfolgreich ist. |
| [!UICONTROL Nur eindeutige Elemente] | Wenn der Wert auf &quot;[!UICONTROL True]&quot; gesetzt ist, muss jedes Element im Array eindeutig sein, damit die Aufnahme erfolgreich ist. |

{style="table-layout:auto"}

Nachdem Sie die Konfiguration des Felds abgeschlossen haben, wählen Sie **[!UICONTROL Anwenden]** aus, um die Änderung auf das Schema anzuwenden.

![](../../images/ui/fields/special/array-config.png)

Die Arbeitsfläche wird aktualisiert, um die am Feld vorgenommenen Änderungen widerzuspiegeln. Beachten Sie, dass der Datentyp, der neben dem Feldnamen auf der Arbeitsfläche angezeigt wird, mit einem Paar eckiger Klammern (`[]`) angehängt wird, was angibt, dass das Feld ein Array dieses Datentyps darstellt.

![](../../images/ui/fields/special/array-applied.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein Array-Feld in der Benutzeroberfläche definieren. Informationen zum Definieren anderer XDM-Feldtypen in der [!DNL Schema Editor] finden Sie in der Übersicht zu [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) .
