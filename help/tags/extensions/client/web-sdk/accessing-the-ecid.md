---
title: Zugreifen auf die ECID
description: Erfahren Sie, wie Sie über die Datenvorbereitung oder Tags auf die Experience Cloud-ID zugreifen können.
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: e53ae6053a4b00e7e75242b95496c6795953005a
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 3%

---


# Zugreifen auf die ECID

Die [!DNL Experience Cloud Identity (ECID)] ist eine beständige Kennung, die einem Benutzer beim Besuch Ihrer Website zugewiesen wird. Unter bestimmten Umständen bevorzugen Sie möglicherweise den Zugriff auf den [!DNL ECID] (um ihn beispielsweise an einen Drittanbieter zu senden). Ein weiterer Anwendungsfall ist das Festlegen von [!DNL ECID] in einem benutzerdefinierten XDM-Feld, zusätzlich zu dessen Verwendung in der Identitätszuordnung.

Sie können auf die ECID entweder über [Datenvorbereitung für die Datenerfassung](../../../../datastreams/data-prep.md) (empfohlen) oder über Tags zugreifen.

## Zugriff auf die ECID über Data Prep (bevorzugte Methode) {#accessing-ecid-data-prep}

Diese Methode verwendet [Datenvorbereitung für die Datenerfassung](../../../../datastreams/data-prep.md) , um eine benutzerdefinierte Zuordnung für die `ECID` zu konfigurieren.

Informationen zur Verwendung dieser Funktion finden Sie in der Dokumentation [Datenvorbereitung für die Datenerfassung](../../../../datastreams/data-prep.md) .

Wenn Sie die ECID in einem benutzerdefinierten XDM-Feld festlegen möchten, müssen Sie sie nicht nur in der Identitätszuordnung enthalten, sondern können dies auch tun, indem Sie die `source` auf den folgenden Pfad setzen:

```js
xdm.identityMap.ECID[0].id
```

Legen Sie dann das Ziel auf einen XDM-Pfad fest, bei dem das Feld vom Typ `string` ist.

![](./assets/access-ecid-data-prep.png)

## Tags

Wenn Sie clientseitig auf den [!DNL ECID] zugreifen müssen, verwenden Sie den Tagansatz wie unten beschrieben.

1. Stellen Sie sicher, dass Ihre Eigenschaft mit aktivierter [Sequenzierung der Regelkomponenten](../../../ui/managing-resources/rules.md#sequencing) konfiguriert ist.
1. Erstellen Sie eine neue Regel. Diese Regel sollte ausschließlich zur Erfassung der [!DNL ECID] ohne andere wichtige Aktionen verwendet werden.
1. Fügen Sie der Regel das Ereignis [!UICONTROL Bibliothek geladen] hinzu.
1. Fügen Sie der Regel eine Aktion vom Typ [!UICONTROL Benutzerdefinierter Code] mit folgendem Code hinzu (vorausgesetzt, der für die SDK-Instanz konfigurierte Name ist `alloy` und es gibt noch kein Datenelement mit demselben Namen):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Speichern Sie die Regel.

Sie sollten dann in den nachfolgenden Regeln mit `%ECID%` oder `_satellite.getVar("ECID")` auf die [!DNL ECID] zugreifen können, wie Sie auf jedes andere Datenelement zugreifen würden.
