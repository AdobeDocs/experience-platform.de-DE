---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Identität;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Identitätsdatentyp
description: Erfahren Sie mehr über den XDM-Datentyp Identität.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 11%

---

# [!UICONTROL Identität] Datentyp

[!UICONTROL Identity] ist ein standardmäßiger XDM-Datentyp, mit dem Personen, die mit digitalen Erlebnissen interagieren, eindeutig unterschieden werden können. Die Identität wird von einem Identitätsanbieter festgelegt, der selbst in einem `namespace` Attribut referenziert wird. Innerhalb jedes `namespace` ist die Identität eindeutig.

<img src="../images/data-types/identity.png" width="550" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `namespace` | Objekt | Ein -Objekt, das ein einzelnes Zeichenfolgenfeld (`code`) enthält, das den Namespace angibt, der mit dem bereitgestellten `id`-Attribut verknüpft ist. |
| `authenticatedState` | String | Der authentifizierte Status für diese Identität zum Zeitpunkt des beobachteten Erlebnisereignisses. Siehe [Anhang](#authenticatedState) für akzeptierte Werte und Definitionen. |
| `id` | String | Die Identität des Verbrauchers im zugehörigen Namespace. |
| `primary` | Boolesch | Gibt an, ob dies die primäre Identität für die Person ist. Jede Person kann nur eine primäre Identität haben. |
| `xid` | String | Falls vorhanden, stellt dieser Wert eine Namespace-übergreifenden Kennung dar, die über alle Kennungen in allen Namespaces eindeutig ist. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Anhang

Der folgende Abschnitt enthält zusätzliche Informationen zum Datentyp [!UICONTROL Identität].

## Akzeptierte Werte für AuthenticatedState {#authenticatedState}

In der folgenden Tabelle sind die akzeptierten Werte für `authenticatedState` und ihre zugehörigen Bedeutungen aufgeführt:

| Wert | Beschreibung |
| --- | --- |
| `ambiguous` | Der authentifizierte Status ist mehrdeutig. |
| `authenticated` | Der Benutzer wurde durch eine Anmeldung oder eine ähnliche Aktion identifiziert, die zum Zeitpunkt der Ereignisbeobachtung gültig war. |
| `loggedOut` | Der Benutzer wurde durch eine Anmeldeaktion zu einem früheren Zeitpunkt identifiziert, war jedoch zum Zeitpunkt der Ereignisbeobachtung nicht angemeldet. |
