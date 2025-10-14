---
keywords: Experience Platform;Startseite;beliebte Themen;api;API;XDM;XDM-System;Experience-Datenmodell;Datenmodell;UI;Arbeitsbereich;Pflichtfeld;Feld;
title: Definieren erforderlicher Felder in der Benutzeroberfläche
description: Erfahren Sie, wie Sie ein erforderliches XDM-Feld in der Benutzeroberfläche von Experience Platform definieren.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definieren erforderlicher Felder in der Benutzeroberfläche

Im Experience-Datenmodell (XDM) gibt ein erforderliches Feld an, dass ein gültiger Wert bereitgestellt werden muss, damit ein bestimmtes Datensatz- oder Zeitreihenereignis während der Datenaufnahme akzeptiert wird. Häufige Anwendungsfälle für erforderliche Felder sind Informationen zur Benutzeridentität und Zeitstempel.

>[!IMPORTANT]
>
>Unabhängig davon, ob ein Schemafeld erforderlich ist oder nicht, akzeptiert Experience Platform für kein aufgenommenes Feld `null` oder leere Werte. Wenn in einem Datensatz oder Ereignis kein Wert für ein bestimmtes Feld vorhanden ist, sollte der Schlüssel für dieses Feld aus der Aufnahme-Payload ausgeschlossen werden.

Beim [Definieren eines neuen &#x200B;](./overview.md#define) in der Benutzeroberfläche von Adobe Experience Platform können Sie es als erforderliches Feld festlegen, indem Sie das Kontrollkästchen **[!UICONTROL Erforderlich]** in der rechten Leiste aktivieren. Wählen Sie **[!UICONTROL Anwenden]** aus, um die Änderung auf das Schema anzuwenden.

![Kontrollkästchen Erforderlich](../../images/ui/fields/required/root.png)

Wenn das Feld ein Attribut auf Stammebene unter dem Mandanten-ID-Objekt ist, wird sein Pfad sofort unter **[!UICONTROL Erforderliche Felder]** in der linken Leiste angezeigt.

![Erforderliches Feld auf Stammebene](../../images/ui/fields/required/applied.png)

Wenn ein erforderliches Feld in einem Objekt verschachtelt ist, das selbst nicht als erforderlich markiert ist, wird das verschachtelte Feld jedoch nicht unter **[!UICONTROL Erforderliche Felder]** in der linken Leiste angezeigt.

Im folgenden Beispiel wird das Feld `internalSKU` wie erforderlich festgelegt, das übergeordnete -Objekt `SKUs` jedoch nicht. In diesem Fall würden keine Validierungsfehler auftreten, wenn `SKUs` bei der Datenaufnahme ausgeschlossen wird, obwohl die `internalSKU` des untergeordneten Felds als erforderlich markiert ist. Mit anderen Worten: Obwohl `SKUs` optional ist, muss es ein `internalSKU` enthalten, falls es enthalten ist.

![Verschachteltes Pflichtfeld](../../images/ui/fields/required/nested.png)

Wenn ein verschachteltes Feld immer in einem Schema erforderlich sein soll, müssen Sie auch alle übergeordneten Felder wie erforderlich festlegen (mit Ausnahme des Mandanten-ID-Objekts).

![Erforderliche Felder für übergeordnete und untergeordnete Elemente](../../images/ui/fields/required/parent-and-child.png)

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie ein erforderliches Feld in der Benutzeroberfläche definieren. In der Übersicht über [Definieren von Feldern in der Benutzeroberfläche](./overview.md#special) erfahren Sie, wie Sie andere XDM-Feldtypen in der [!DNL Schema Editor] definieren.
