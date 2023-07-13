---
solution: Experience Platform
title: PQL Map-Funktionen
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Zuordnungen erleichtern.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 90%

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
