---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentierung; Segmentierung; Segmentierungsdienst; pql; PQL; Profile Query Language; Zuordnungsfunktionen; map;
solution: Experience Platform
title: PQL Map-Funktionen
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Zuordnungen erleichtern.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 81%

---

# Zuordnungsfunktionen

[!DNL Profile Query Language] (PQL) bietet Funktionen, die die Interaktion mit Zuordnungen erleichtern. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] Übersicht](./overview.md).

## Abrufen

Mit der `get`-Funktion wird der Wert einer Zuordnung für einen bestimmten Schlüssel abgerufen.

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

Die `keys`-Funktion wird zum Abrufen aller Schlüssel einer gegebenen Zuordnung verwendet.

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

Die `values`-Funktion wird zum Abrufen aller Werte einer gegebenen Zuordnung verwendet.

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
