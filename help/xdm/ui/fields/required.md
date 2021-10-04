---
keywords: Experience Platform; Startseite; beliebte Themen; API; XDM; XDM; XDM-System; Experience-Datenmodell; Datenmodell; ui; Workspace; erforderlich; Feld;
title: Definieren erforderlicher Felder in der Benutzeroberfläche
description: Erfahren Sie, wie Sie in der Experience Platform-Benutzeroberfläche ein erforderliches XDM-Feld definieren.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 1d04bf56c51506f84c5156e6d2ed6c9f58f15235
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Definieren erforderlicher Felder in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) gibt ein erforderliches Feld an, dass ein gültiger Wert angegeben werden muss, damit ein bestimmter Datensatz oder ein Zeitreihenereignis bei der Datenerfassung akzeptiert werden kann. Häufige Anwendungsfälle für erforderliche Felder umfassen Informationen zur Benutzeridentität und Zeitstempel.

Wenn Sie [ein neues Feld](./overview.md#define) in der Adobe Experience Platform-Benutzeroberfläche definieren, können Sie es als erforderliches Feld festlegen, indem Sie in der rechten Leiste das Kontrollkästchen **[!UICONTROL Erforderlich]** aktivieren. Wählen Sie **[!UICONTROL Anwenden]** aus, um die Änderung auf das Schema anzuwenden.

![Erforderliches Kontrollkästchen](../../images/ui/fields/required/root.png)

Wenn das Feld ein Attribut auf der Stammebene unter dem Mandanten-ID-Objekt ist, wird sein Pfad sofort in der linken Leiste unter **[!UICONTROL Erforderliche Felder]** angezeigt.

![Erforderliches Feld auf Stammebene](../../images/ui/fields/required/applied.png)

Wenn ein erforderliches Feld innerhalb eines Objekts verschachtelt ist, das selbst nicht als erforderlich markiert ist, wird das verschachtelte Feld in der linken Leiste nicht unter **[!UICONTROL Erforderliche Felder]** angezeigt.

Im folgenden Beispiel wird das Feld `loyaltyId` nach Bedarf festgelegt, das übergeordnete Objekt `loyalty` jedoch nicht. In diesem Fall würden keine Validierungsfehler auftreten, wenn `loyalty` bei der Datenaufnahme ausgeschlossen wurde, auch wenn das untergeordnete Feld `loyaltyId` als erforderlich markiert ist. Das heißt, `loyalty` ist optional, muss jedoch ein `loyaltyId` -Feld für das Ereignis enthalten, in dem es enthalten ist.

![Verschachteltes erforderliches Feld](../../images/ui/fields/required/nested.png)

Wenn ein verschachteltes Feld in einem Schema immer erforderlich sein soll, müssen Sie auch alle übergeordneten Felder nach Bedarf festlegen (mit Ausnahme des Mandanten-ID-Objekts).

![Übergeordnete und untergeordnete erforderliche Felder](../../images/ui/fields/required/parent-and-child.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein erforderliches Feld in der Benutzeroberfläche definieren. Informationen zum Definieren anderer XDM-Feldtypen im [!DNL Schema Editor] finden Sie in der Übersicht zu [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special).
