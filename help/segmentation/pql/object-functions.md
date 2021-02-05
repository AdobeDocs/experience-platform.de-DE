---
keywords: Experience Platform;Home;beliebte Themen;Segmentierung;Segmentierung;Segmentierungsdienst;pql;PQL;Profil-Abfrage-Sprache;Objektfunktionen;Objekt
solution: Experience Platform
title: PQL-Objektfunktionen
topic: developer guide
description: Profil Query Language (PQL) bietet Funktionen, die die Interaktion mit Objekten erleichtern.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 70%

---


# Objektfunktionen

[!DNL Profile Query Language] (PQL) Angebot-Funktionen, um die Interaktion mit Objekten zu vereinfachen. Weitere Informationen zu anderen PQL-Funktionen finden Sie im [[!DNL Profile Query Language] overview](./overview.md).

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