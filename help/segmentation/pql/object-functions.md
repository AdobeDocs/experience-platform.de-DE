---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Objektfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 5%

---


# Objektfunktionen

Profil Abfrage Language (PQL)-Angebote erleichtern die Interaktion mit Objekten. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).

## Ist null

Die `isNull` Funktion bestimmt, ob eine Objektreferenz nicht vorhanden ist.

**Format**

```sql
{OBJECT}.isNull()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob die Privatadresse der Person nicht vorhanden ist.

```sql
person.homeAddress.isNull()
```

## Ist nicht null

Die `isNotNull` Funktion bestimmt, ob eine Objektreferenz vorhanden ist.

**Format**

```sql
{OBJECT}.isNotNull()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob die Privatadresse der Person vorhanden ist.

```sql
person.homeAddress.isNotNull()
```

## Nächste Schritte

Jetzt, da Sie von Objektfunktionen erfahren haben, können Sie sie in Ihren PQL-Abfragen verwenden. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Profil Abfrage Language-Übersicht](./overview.md).