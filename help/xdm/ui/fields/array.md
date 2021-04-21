---
keywords: Experience Platform;Home;beliebte Themen;API;XDM;XDM-System;Erlebnisdatenmodell;Datenmodell;ui;Arbeitsbereich;Array;Feld;
solution: Experience Platform
title: Definieren von Array-Feldern in der Benutzeroberfläche
description: Erfahren Sie, wie Sie ein Array-Feld in der Benutzeroberfläche "Experience Platform"definieren.
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Definieren von Array-Feldern in der Benutzeroberfläche

Beim Definieren eines XDM-Felds (Experience Data Model) in der Adobe Experience Platform-Benutzeroberfläche können Sie dieses Feld als Array definieren.

Der Inhalt des Arrays hängt von dem für dieses Feld ausgewählten [!UICONTROL Typ] ab. Wenn beispielsweise [!UICONTROL Type] eines Felds auf &quot;[!UICONTROL String]&quot;festgelegt ist, wird das Feld durch Festlegen als Array als Zeichenfolgenarray gekennzeichnet. Ist [!UICONTROL Type] des Felds auf einen Datentyp mit mehreren Feldern wie &quot;[!UICONTROL Postanschrift]&quot;eingestellt, wird daraus ein Array von Objekten mit Postadresse, die dem Datentyp entsprechen.

Nachdem Sie in der Benutzeroberfläche [ein neues Feld definiert haben, können Sie es als Array-Feld festlegen, indem Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Array]** aktivieren.](./overview.md#define)

![](../../images/ui/fields/special/array.png)

Sobald das Kontrollkästchen aktiviert ist, werden zusätzliche Steuerelemente in der rechten Leiste angezeigt, mit denen Sie optional das Array weiter einschränken können. Wenn Sie keine bestimmte Einschränkung erzwingen möchten, lassen Sie das Feld leer.

Die zusätzlichen Konfigurationssteuerelemente für Arrays lauten wie folgt:

| Feldeigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Mindestlänge] | Die Mindestanzahl von Elementen, die das Array enthalten muss, damit die Aufnahme erfolgreich ist. |
| [!UICONTROL Maximale Länge] | Die maximale Anzahl von Elementen, die das Array enthalten muss, damit die Aufnahme erfolgreich ist. |
| [!UICONTROL Nur eindeutige Elemente] | Wenn der Wert auf &quot;[!UICONTROL True]&quot;gesetzt ist, muss jedes Element im Array eindeutig sein, damit die Aufnahme erfolgreich ist. |

Nachdem Sie das Feld konfiguriert haben, wählen Sie **[!UICONTROL Apply]**, um die Änderung auf das Schema anzuwenden.

![](../../images/ui/fields/special/array-config.png)

Die Arbeitsfläche wird aktualisiert, um die am Feld vorgenommenen Änderungen widerzuspiegeln. Beachten Sie, dass dem Datentyp, der neben dem Feldnamen auf der Arbeitsfläche angezeigt wird, ein Paar eckiger Klammern (`[]`) angehängt wird, was angibt, dass das Feld ein Array dieses Datentyps darstellt.

![](../../images/ui/fields/special/array-applied.png)

## Nächste Schritte

In diesem Handbuch wird beschrieben, wie Sie ein Array-Feld in der Benutzeroberfläche definieren. Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor] finden Sie in der Übersicht unter [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special).
