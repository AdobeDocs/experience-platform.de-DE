---
title: onBeforeLinkClickSend
description: Callback, der unmittelbar vor dem Senden der Linktracking-Daten ausgeführt wird.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Dieser Callback ist veraltet. Verwenden Sie stattdessen [`clickCollection.filterClickDetails`](clickcollection.md) .

Mit dem `onBeforeLinkClickSend` Callback können Sie eine JavaScript-Funktion registrieren, die Linktracking-Daten ändern kann, die Sie unmittelbar vor dem Senden dieser Daten an Adobe senden. Damit können Sie das `xdm`- oder `data`-Objekt bearbeiten, einschließlich der Möglichkeit, Elemente hinzuzufügen, zu bearbeiten oder zu entfernen. Sie können das Senden von Daten auch ganz abbrechen, z. B. bei erkanntem Client-seitigem Bot-Traffic.

Dieser Rückruf wird nur ausgeführt, wenn [`clickCollectionEnabled`](clickcollectionenabled.md) aktiviert ist und `filterClickDetails` keine registrierte Funktion enthält.

Wenn [`onBeforeEventSend`](onbeforeeventsend.md) und `onBeforeLinkClickSend` beide registrierte Funktionen enthalten, wird `onBeforeLinkClickSend` zuerst ausgeführt.

>[!WARNING]
>
>Dieser Callback ermöglicht die Verwendung von benutzerdefiniertem Code. Wenn ein Code, den Sie in den Callback einbeziehen, eine nicht abgefangene Ausnahme auslöst, wird die Verarbeitung für das Ereignis angehalten. Daten werden nicht an Adobe gesendet.

## `onBeforeLinkClickSend` und `filterClickDetails`

Der [`clickCollection.filterClickDetails`](clickcollection.md)-Callback soll `onBeforeLinkClickSend` ersetzen. Adobe rät dringend davon ab, beiden gleichzeitig Rückruffunktionen zuzuweisen. Wenn Sie sowohl `filterClickDetails` als auch `onBeforeLinkClickSend` eine Callback-Funktion zuweisen, verwendet die Bibliothek die folgende Logik:

* Nur `filterClickDetails` wird ausgeführt, `onBeforeLinkClickSend` nicht.
* `clickCollection.eventGroupingEnabled` für die Ereignisgruppierung funktioniert nicht.
