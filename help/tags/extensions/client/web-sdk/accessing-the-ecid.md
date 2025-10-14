---
title: Zugreifen auf die ECID
description: Erfahren Sie, wie Sie über die Datenvorbereitung oder Tags auf die Experience Cloud-ID zugreifen können
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e53ae6053a4b00e7e75242b95496c6795953005a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 3%

---


# Zugreifen auf die ECID

Die [!DNL Experience Cloud Identity (ECID)] ist eine persistente Kennung, die einem Benutzer beim Besuch einer Website zugewiesen wird. Unter bestimmten Umständen möchten Sie vielleicht lieber auf die [!DNL ECID] zugreifen (um sie beispielsweise an einen Drittanbieter zu senden). Ein weiterer Anwendungsfall besteht darin, die [!DNL ECID] in einem benutzerdefinierten XDM-Feld festzulegen, zusätzlich zu ihrer Verwendung in der Identitätszuordnung.

Sie können auf die ECID entweder über [Datenvorbereitung für die Datenerfassung](../../../../datastreams/data-prep.md) (empfohlen) oder über Tags zugreifen.

## Zugriff auf die ECID über die Datenvorbereitung (bevorzugte Methode) {#accessing-ecid-data-prep}

Diese Methode verwendet [Datenvorbereitung für die Datenerfassung](../../../../datastreams/data-prep.md) um eine benutzerdefinierte Zuordnung für die `ECID` zu konfigurieren.

Weitere Informationen zur Verwendung [&#x200B; Funktion finden Sie in der &#x200B;](../../../../datastreams/data-prep.md) zur Datenvorbereitung für die Datenerfassung .

Wenn Sie die ECID nicht nur in der Identitätszuordnung haben, sondern auch in einem benutzerdefinierten XDM-Feld festlegen möchten, können Sie dies tun, indem Sie die `source` auf den folgenden Pfad festlegen:

```js
xdm.identityMap.ECID[0].id
```

Legen Sie dann das Ziel auf einen XDM-Pfad fest, in dem das Feld vom Typ `string` ist.

![](./assets/access-ecid-data-prep.png)

## Tags

Wenn Sie Client-seitig auf die [!DNL ECID] zugreifen müssen, verwenden Sie den Tag-Ansatz wie unten beschrieben.

1. Stellen Sie sicher, dass die Eigenschaft mit [Regelkomponentensequenzierung](../../../ui/managing-resources/rules.md#sequencing) konfiguriert ist.
1. Erstellen Sie eine neue Regel. Diese Regel sollte ausschließlich zur Erfassung der [!DNL ECID] ohne andere wichtige Aktionen verwendet werden.
1. Fügen Sie [!UICONTROL &#x200B; Regel ein Ereignis &#x200B;]Bibliothek geladen“ hinzu.
1. Fügen Sie [!UICONTROL &#x200B; Regel eine Aktion &#x200B;]Benutzerdefinierter Code“ mit dem folgenden Code hinzu (vorausgesetzt, der für die SDK-Instanz konfigurierte Name ist `alloy` und es gibt noch kein Datenelement mit demselben Namen):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Speichern Sie die Regel.

Anschließend sollten Sie in der Lage sein, in nachfolgenden Regeln mithilfe von `%ECID%` oder `_satellite.getVar("ECID")` auf die [!DNL ECID] zuzugreifen, wie Sie auch auf jedes andere Datenelement zugreifen würden.
