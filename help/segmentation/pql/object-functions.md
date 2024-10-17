---
solution: Experience Platform
title: PQL-Objektfunktionen
description: Profile Query Language (PQL) bietet Funktionen, die die Interaktion mit Objekten vereinfachen.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 52%

---

# Objektfunktionen

[!DNL Profile Query Language] (PQL) bietet Funktionen, die die Interaktion mit Objekten vereinfachen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [[!DNL Profile Query Language] Übersicht](./overview.md) .

## Ist null

Die Funktion `isNull` bestimmt, ob eine Objektreferenz nicht als boolescher Wert vorhanden ist.

**Format**

```sql
{OBJECT}.isNull()
```

**Beispiel**

Die folgende PQL-Abfrage prüft, ob die Privatadresse der Person nicht vorhanden ist.

```sql
person.homeAddress.isNull()
```

## Is not null

Die Funktion `isNotNull` bestimmt, ob eine Objektreferenz als boolescher Wert vorhanden ist.

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

Nachdem Sie die Objektfunktionen kennengelernt haben, können Sie sie nun in Ihren PQL-Abfragen nutzen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).
