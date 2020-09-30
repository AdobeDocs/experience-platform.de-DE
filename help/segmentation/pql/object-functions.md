---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;object functions;object;
solution: Experience Platform
title: Objektfunktionen
topic: developer guide
description: Profil Query Language (PQL) bietet Funktionen, die die Interaktion mit Objekten erleichtern.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 82%

---


# Objektfunktionen

[!DNL Profile Query Language] (PQL) Angebot-Funktionen, um die Interaktion mit Objekten zu vereinfachen. More information about other PQL functions can be found in the [[!DNL Profile Query Language] overview](./overview.md).

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

Nachdem Sie die Objektfunktionen kennengelernt haben, können Sie sie nun in Ihren PQL-Abfragen nutzen. Weitere Informationen zu anderen PQL-Funktionen finden Sie in [Profil Query Language – Übersicht](./overview.md).