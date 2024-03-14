---
title: Zugreifen auf die ECID
description: Erfahren Sie, wie Sie über die Datenvorbereitung oder Tags auf die Experience Cloud-ID zugreifen können.
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e01dfcf3cccea589083a23171f4b8d9ecad58233
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 3%

---


# Zugreifen auf die ECID

Die [!DNL Experience Cloud Identity (ECID)] ist eine persistente Kennung, die einem Benutzer beim Besuch Ihrer Website zugewiesen wird. Unter bestimmten Umständen bevorzugen Sie möglicherweise den Zugriff auf die [!DNL ECID] (um sie beispielsweise an einen Dritten zu senden). Ein weiterer Anwendungsfall ist das Festlegen der [!DNL ECID] in ein benutzerdefiniertes XDM-Feld ein, zusätzlich zu dessen Verwendung in der Identitätszuordnung.

Der Zugriff auf die ECID erfolgt über [Datenvorbereitung für die Datenerfassung](../../../../datastreams/data-prep.md) (empfohlen) oder über Tags.

## Zugriff auf die ECID über Data Prep (bevorzugte Methode) {#accessing-ecid-data-prep}

Wenn Sie die ECID in einem benutzerdefinierten XDM-Feld festlegen möchten, können Sie dies nicht nur in der Identitätszuordnung tun, sondern auch durch Festlegen der `source` zum folgenden Pfad:

```js
xdm.identityMap.ECID[0].id
```

Legen Sie dann das Ziel auf einen XDM-Pfad fest, bei dem das Feld vom Typ ist `string`.

![](./assets/access-ecid-data-prep.png)

## Tags

Wenn Sie auf die [!DNL ECID] Client-seitig verwenden Sie den Tags-Ansatz wie unten beschrieben.

1. Stellen Sie sicher, dass Ihre Eigenschaft mit [Sequenzierung von Regelkomponenten](../../../ui/managing-resources/rules.md#sequencing) aktiviert.
1. Erstellen Sie eine neue Regel. Diese Regel sollte ausschließlich zur Erfassung der [!DNL ECID] ohne sonstige wichtige Maßnahmen.
1. Hinzufügen einer [!UICONTROL Bibliothek geladen] -Ereignis der Regel hinzufügen.
1. Hinzufügen einer [!UICONTROL Benutzerspezifischer Code] -Aktion mit dem folgenden Code auf die Regel anwenden (vorausgesetzt, der für die SDK-Instanz konfigurierte Name lautet `alloy` und noch kein Datenelement mit demselben Namen vorhanden ist):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Speichern Sie die Regel.

Sie sollten dann auf die [!DNL ECID] in nachfolgenden Regeln mit `%ECID%` oder `_satellite.getVar("ECID")`, wie Sie auf jedes andere Datenelement zugreifen würden.
