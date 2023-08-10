---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; erforderlich; Feld;
title: Definieren erforderlicher Felder in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche ein erforderliches XDM-Feld definieren.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Definieren erforderlicher Felder in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) gibt ein erforderliches Feld an, dass ein gültiger Wert angegeben werden muss, damit ein bestimmter Datensatz oder ein Zeitreihenereignis bei der Datenerfassung akzeptiert werden kann. Häufige Anwendungsfälle für erforderliche Felder umfassen Informationen zur Benutzeridentität und Zeitstempel.

>[!IMPORTANT]
>
>Unabhängig davon, ob ein Schemafeld erforderlich ist oder nicht, akzeptiert Platform nicht `null` oder leere Werte für alle erfassten Felder. Wenn in einem Datensatz oder Ereignis kein Wert für ein bestimmtes Feld vorhanden ist, sollte der Schlüssel für dieses Feld aus der Aufnahme-Payload ausgeschlossen werden.

Wann [Definieren eines neuen Felds](./overview.md#define) In der Benutzeroberfläche von Adobe Experience Platform können Sie sie als erforderliches Feld festlegen, indem Sie die **[!UICONTROL Erforderlich]** in der rechten Leiste. Auswählen **[!UICONTROL Anwenden]** , um die Änderung auf das Schema anzuwenden.

![Erforderliches Kontrollkästchen](../../images/ui/fields/required/root.png)

Wenn das Feld ein Attribut auf der Stammebene unter dem Mandanten-ID-Objekt ist, wird sein Pfad sofort unter **[!UICONTROL Erforderliche Felder]** in der linken Leiste.

![Erforderliches Feld auf Stammebene](../../images/ui/fields/required/applied.png)

Wenn ein erforderliches Feld jedoch innerhalb eines Objekts verschachtelt ist, das selbst nicht als erforderlich markiert ist, wird das verschachtelte Feld nicht unter **[!UICONTROL Erforderliche Felder]** in der linken Leiste.

Im folgenden Beispiel wird die Variable `internalSKU` -Feld ist wie erforderlich festgelegt, aber sein übergeordnetes Objekt `SKUs` ist nicht. In diesem Fall würden keine Validierungsfehler auftreten, wenn `SKUs` wird bei der Aufnahme von Daten ausgeschlossen, auch wenn das untergeordnete Feld `internalSKU` als erforderlich markiert ist. Mit anderen Worten, während `SKUs` ist optional und muss eine `internalSKU` -Feld in das -Ereignis ein.

![Verschachteltes erforderliches Feld](../../images/ui/fields/required/nested.png)

Wenn ein verschachteltes Feld in einem Schema immer erforderlich sein soll, müssen Sie auch alle übergeordneten Felder nach Bedarf festlegen (mit Ausnahme des Mandanten-ID-Objekts).

![Übergeordnete und untergeordnete erforderliche Felder](../../images/ui/fields/required/parent-and-child.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein erforderliches Feld in der Benutzeroberfläche definieren. Siehe Übersicht unter [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor].
