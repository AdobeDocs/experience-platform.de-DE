---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Identität; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Identitätsdatentyp
topic-legacy: overview
description: Dieses Dokument bietet einen Überblick über den Identitäts-XDM-Datentyp.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 11%

---

#  Identitydata type

 Die Identifizierung ist ein standardmäßiger XDM-Datentyp, mit dem Personen, die mit digitalen Erlebnissen interagieren, klar unterschieden werden. Die Identität wird von einem Identitäts-Provider festgelegt, der selbst in einem `namespace` -Attribut referenziert wird. Innerhalb jedes `namespace` ist die Identität eindeutig.

<img src="../images/data-types/identity.png" width="550" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `namespace` | Objekt | Ein Objekt, das ein einzelnes Zeichenfolgenfeld (`code`) enthält, das den Namespace angibt, der mit dem bereitgestellten `id`-Attribut verknüpft ist. |
| `authenticatedState` | Zeichenfolge | Der authentifizierte Status für diese Identität zum Zeitpunkt des beobachteten Erlebnisereignisses. Akzeptierte Werte und Definitionen finden Sie im [Anhang](#authenticatedState) . |
| `id` | Zeichenfolge | Die Identität des Verbrauchers im zugehörigen Namespace. |
| `primary` | Boolesch | Gibt an, ob dies die primäre Identität der Person ist. Jede Person kann nur eine primäre Identität haben. |
| `xid` | Zeichenfolge | Falls vorhanden, stellt dieser Wert eine Namespace-übergreifenden Kennung dar, die über alle Kennungen in allen Namespaces eindeutig ist. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Datentyp [!UICONTROL Identität].

## Akzeptierte Werte für authenticatedState {#authenticatedState}

In der folgenden Tabelle sind die zulässigen Werte für `authenticatedState` und die zugehörige Bedeutung aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `ambiguous` | Der authentifizierte Status ist mehrdeutig. |
| `authenticated` | Der Benutzer wurde durch eine Anmeldung oder eine ähnliche Aktion identifiziert, die zum Zeitpunkt der Ereignisbeobachtung gültig war. |
| `loggedOut` | Der Benutzer wurde zu einem früheren Zeitpunkt durch eine Anmeldeaktion identifiziert, war aber zum Zeitpunkt der Ereignisbeobachtung nicht angemeldet. |
