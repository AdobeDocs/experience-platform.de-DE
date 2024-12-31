---
solution: Experience Platform
title: PQL-Zuordnungsfunktionen
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Zuordnungen erleichtern.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 46%

---

# Zuordnungsfunktionen

[!DNL Profile Query Language] (PQL) bietet Funktionen, die die Interaktion mit Zuordnungen erleichtern. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md).

## Abrufen

Die Funktion `get` wird verwendet, um den Wert einer Zuordnung für einen bestimmten Schlüssel als Objekt abzurufen.

**Format**

```sql
{MAP}.get({STRING})
```

**Beispiel**

Die folgende PQL-Abfrage ruft den Wert der dentitätszuordnung für den Schlüssel `example@example.com` ab.

```sql
identityMap.get("example@example.com")
```

## Schlüssel

Die Funktion `keys` wird verwendet, um alle Schlüssel für eine bestimmte Zuordnung als Array oder Liste abzurufen.

**Format**

```sql
{MAP}.keys()
```

**Beispiel**

Die folgende PQL-Abfrage ruft alle Schlüssel für die `identityMap`-Zuordnung ab.

```sql
identityMap.keys()
```

## Werte

Die Funktion `values` wird verwendet, um alle Werte einer bestimmten Zuordnung als Array oder Liste abzurufen.

**Format**

```sql
{MAP}.values()
```

**Beispiel**

Die folgende PQL-Abfrage ruft alle Werte für die `identityMap`-Zuordnung ab.

```sql
identityMap.values()
```

## Nächste Schritte

Nachdem Sie sich mit den Zuordnungsfunktionen vertraut gemacht haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
