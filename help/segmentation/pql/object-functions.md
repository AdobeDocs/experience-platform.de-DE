---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Objektfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 91%

---


# Objektfunktionen

[!DNL Profile Query Language] (PQL) Angebot-Funktionen, um die Interaktion mit Objekten zu vereinfachen. Weiterführende Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zu Profil Query Language](./overview.md).

## Is null

Die `isNull`-Funktion ermittelt, ob eine Objektreferenz nicht vorhanden ist.

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

Die `isNotNull`-Funktion ermittelt, ob eine Objektreferenz nicht vorhanden ist.

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

Nachdem Sie die Objektfunktionen kennengelernt haben, können Sie sie nun in Ihren PQL-Abfragen nutzen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in der [Übersicht zur Profil Query Language](./overview.md).