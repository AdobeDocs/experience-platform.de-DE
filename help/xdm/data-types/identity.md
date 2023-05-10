---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Identität; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Identitätsdatentyp
description: Dieses Dokument bietet einen Überblick über den Identitäts-XDM-Datentyp.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 15%

---

# [!UICONTROL Identität] Datentyp

[!UICONTROL Identität] ist ein standardmäßiger XDM-Datentyp, mit dem Personen, die mit digitalen Erlebnissen interagieren, klar unterschieden werden. Die Identität wird von einem Identitäts-Provider festgelegt, der selbst in einem `namespace` -Attribut. Innerhalb von `namespace`, ist die Identität eindeutig.

<img src="../images/data-types/identity.png" width="550" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `namespace` | Objekt | Ein Objekt, das ein einzelnes Zeichenfolgenfeld enthält (`code`), der den Namespace angibt, der mit der angegebenen verknüpft ist `id` -Attribut. |
| `authenticatedState` | Zeichenfolge | Der authentifizierte Status für diese Identität zum Zeitpunkt des beobachteten Erlebnisereignisses. Siehe [Anhang](#authenticatedState) für akzeptierte Werte und Definitionen. |
| `id` | Zeichenfolge | Die Identität des Verbrauchers im zugehörigen Namespace. |
| `primary` | Boolesch | Gibt an, ob dies die primäre Identität der Person ist. Jede Person kann nur eine primäre Identität haben. |
| `xid` | Zeichenfolge | Falls vorhanden, stellt dieser Wert eine Namespace-übergreifenden Kennung dar, die über alle Kennungen in allen Namespaces eindeutig ist. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Anhang

Im folgenden Abschnitt finden Sie weitere Informationen zum [!UICONTROL Identität] Datentyp.

## Akzeptierte Werte für authenticatedState {#authenticatedState}

In der folgenden Tabelle sind die für `authenticatedState` und ihre zugehörige Bedeutung:

| Wert | Beschreibung |
| --- | --- |
| `ambiguous` | Der authentifizierte Status ist mehrdeutig. |
| `authenticated` | Der Benutzer wurde durch eine Anmeldung oder eine ähnliche Aktion identifiziert, die zum Zeitpunkt der Ereignisbeobachtung gültig war. |
| `loggedOut` | Der Benutzer wurde zu einem früheren Zeitpunkt durch eine Anmeldeaktion identifiziert, war aber zum Zeitpunkt der Ereignisbeobachtung nicht angemeldet. |
