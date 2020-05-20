---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funktionen für Imagemaps
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 6%

---


# Funktionen für Imagemaps

Profil Abfrage Language (PQL)-Angebote, um die Interaktion mit Karten zu erleichtern. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).

## Abrufen

Mit der `get` Funktion wird der Wert einer Zuordnung für einen bestimmten Schlüssel abgerufen.

**Format**

```sql
{MAP}.get({STRING})
```

**Beispiel**

Die folgende PQL-Abfrage ruft den Wert der Identitätskarte für den Schlüssel ab `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Schlüssel

Die `keys` Funktion wird zum Abrufen aller Schlüssel für eine bestimmte Zuordnung verwendet.

**Format**

```sql
{MAP}.keys()
```

**Beispiel**

Die folgende PQL-Abfrage ruft alle Schlüssel für die Map ab `identityMap`.

```sql
identityMap.keys()
```

## Werte

Die `values` Funktion wird zum Abrufen aller Werte einer gegebenen Zuordnung verwendet.

**Format**

```sql
{MAP}.values()
```

**Beispiel**

Die folgende PQL-Abfrage ruft alle Werte für die Zuordnung ab `identityMap`.

```sql
identityMap.values()
```

## Nächste Schritte

Jetzt, da Sie Informationen zu Kartenfunktionen erhalten haben, können Sie diese in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).
