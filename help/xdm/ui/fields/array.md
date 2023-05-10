---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; Array; Feld;
solution: Experience Platform
title: Definieren von Array-Feldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie ein Array-Feld in der Benutzeroberfläche "Experience Platform"definieren.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Definieren von Array-Feldern in der Benutzeroberfläche

Beim Definieren eines XDM-Felds (Experience-Datenmodell) in der Benutzeroberfläche von Adobe Experience Platform können Sie dieses Feld als Array festlegen.

Der Inhalt des Arrays hängt von der [!UICONTROL Typ] für dieses Feld ausgewählt wurde. Wenn beispielsweise die Variable [!UICONTROL Typ] auf &quot;[!UICONTROL Zeichenfolge]&quot;, wird das Feld durch Festlegen dieses Felds als Array als Zeichenfolgen-Array gekennzeichnet. Wenn das Feld [!UICONTROL Typ] auf einen Datentyp mit mehreren Feldern festgelegt ist, z. B. &quot;[!UICONTROL Postanschrift]&quot;, würde es sich zu einem Array von Postadresse-Objekten entwickeln, die dem Datentyp entsprechen.

Nachdem Sie [ein neues Feld in der Benutzeroberfläche definiert hat](./overview.md#define), können Sie es als Array-Feld festlegen, indem Sie die **[!UICONTROL Array]** in der rechten Leiste.

![](../../images/ui/fields/special/array.png)

Sobald das Kontrollkästchen aktiviert ist, werden in der rechten Leiste zusätzliche Steuerelemente angezeigt, mit denen Sie das Array optional weiter einschränken können. Wenn Sie eine bestimmte Einschränkung nicht erzwingen möchten, lassen Sie das Feld leer.

Die zusätzlichen Konfigurationssteuerelemente für Arrays lauten wie folgt:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Mindestlänge] | Die Mindestanzahl von Elementen, die das Array enthalten muss, damit die Aufnahme erfolgreich ist. |
| [!UICONTROL Maximale Länge] | Die maximale Anzahl von Elementen, die das Array enthalten muss, damit die Aufnahme erfolgreich ist. |
| [!UICONTROL Nur eindeutige Elemente] | Wenn auf &quot;[!UICONTROL True]&quot;, muss jedes Element im Array eindeutig sein, damit die Aufnahme erfolgreich ist. |

{style="table-layout:auto"}

Nachdem Sie die Konfiguration des Felds abgeschlossen haben, wählen Sie **[!UICONTROL Anwenden]** , um die Änderung auf das Schema anzuwenden.

![](../../images/ui/fields/special/array-config.png)

Die Arbeitsfläche wird aktualisiert, um die am Feld vorgenommenen Änderungen widerzuspiegeln. Beachten Sie, dass der Datentyp, der neben dem Feldnamen auf der Arbeitsfläche angezeigt wird, mit einem Paar eckiger Klammern (`[]`), was angibt, dass das Feld ein Array dieses Datentyps darstellt.

![](../../images/ui/fields/special/array-applied.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein Array-Feld in der Benutzeroberfläche definieren. Siehe Übersicht unter [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) , um zu erfahren, wie Sie andere XDM-Feldtypen im [!DNL Schema Editor].
