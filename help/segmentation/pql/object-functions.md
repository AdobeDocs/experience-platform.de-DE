---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;object functions;object;
solution: Experience Platform
title: Objektfunktionen
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 80%

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