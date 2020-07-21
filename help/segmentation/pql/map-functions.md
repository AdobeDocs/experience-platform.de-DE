---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Zuordnungsfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 93%

---


# Zuordnungsfunktionen

[!DNL Profile Query Language] (PQL) Angebote Funktionen, um die Interaktion mit Karten zu erleichtern. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).

## Abrufen

Mit der `get`-Funktion wird der Wert einer Zuordnung für einen bestimmten Schlüssel abgerufen.

**Format**

```sql
{MAP}.get({STRING})
```

**Beispiel**

Die folgende PQL-Abfrage ruft den Wert der Identitätskarte für den Schlüssel `example@example.com` ab.

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
