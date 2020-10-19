---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;identity;datatype;data-type;data type;
solution: Experience Platform
title: Identitätsdatentyp
topic: overview
description: Dieses Dokument bietet eine Übersicht über den Identitäts-XDM-Datentyp.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 11%

---


# [!UICONTROL Identitätsdatentyp]

[!UICONTROL Identity] ist ein standardmäßiger XDM-Datentyp, der verwendet wird, um Personen, die mit digitalen Erlebnissen interagieren, klar zu unterscheiden. Identität wird von einem Identitäts-Provider festgelegt, der selbst in einem `namespace` Attribut referenziert wird. Innerhalb jeder `namespace`ist die Identität eindeutig.

<img src="../images/data-types/identity.png" width="550" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `namespace` | Objekt | Ein Objekt, das ein einzelnes Zeichenfolgenfeld enthält (`code`), das den mit dem bereitgestellten `id` Attribut verknüpften Namensraum angibt. |
| `authenticatedState` | Zeichenfolge | Der authentifizierte Status für diese Identität zum Zeitpunkt des beobachteten Experience Ereignisses. Zulässige Werte und Definitionen finden Sie im [Anhang](#authenticatedState) . |
| `id` | Zeichenfolge | Die Identität des Verbrauchers im entsprechenden Namensraum. |
| `primary` | Boolesch | Gibt an, ob dies die primäre Identität der Person ist. Jede Person kann nur eine primäre Identität haben. |
| `xid` | Zeichenfolge | Falls vorhanden, stellt dieser Wert eine Namespace-übergreifenden Kennung dar, die über alle Kennungen in allen Namespaces eindeutig ist. |

Weitere Informationen zum Mixin finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Anhang

Der folgende Abschnitt enthält weitere Informationen zum Datentyp [!UICONTROL Identity] .

## Akzeptierte Werte für authenticationState {#authenticatedState}

In der folgenden Tabelle sind die zulässigen Werte für `authenticatedState` und die damit verbundene Bedeutung aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `ambiguous` | Der authentifizierte Status ist nicht eindeutig. |
| `authenticated` | Der Benutzer wurde durch eine Anmeldung oder eine ähnliche Aktion identifiziert, die zum Zeitpunkt der Ereignis-Beobachtung gültig war. |
| `loggedOut` | Der Benutzer wurde zu einem früheren Zeitpunkt durch eine Anmeldeaktion identifiziert, war aber zum Zeitpunkt der Ereignis-Beobachtung nicht angemeldet. |