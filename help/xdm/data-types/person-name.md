---
keywords: Experience Platform;home;popular topics;schema;XDM;fields;schemas;Schemas;fullName;xdm:fullName;person name;name;datatype;data-type;data-type;data type
solution: Experience Platform
title: Datentyp "Person Name"
description: Erfahren Sie mehr über den XDM-Datentyp "Personenname".
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 6%

---

# [!UICONTROL Personenname] Datentyp

[!UICONTROL Personenname] ist ein standardmäßiger XDM-Datentyp, der den vollständigen Namen einer Person beschreibt. Da die Konventionen für Namensstrukturen von Sprache und Kultur stark variieren, sollten Namen immer mit diesem Datentyp modelliert werden.

Darüber hinaus bietet der Datentyp eine Reihe optionaler Eigenschaften, die in Situationen verwendet werden können, in denen nur ein Fragment des vollständigen Namens verwendet werden muss, z. B. die Erstellung eines formellen oder informellen Grußformels.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `courtesyTitle` | Eine Abkürzung für den Titel, die Ehrlichkeit oder die Anrede einer Person (z. B. `Mr.`, `Miss.`oder `Dr.`). |
| `firstName` | Das erste Segment des Namens in der am häufigsten akzeptierten Schreibreihenfolge in der Sprache des Namens. |
| `fullName` | Der vollständige Name der Person, in der am häufigsten akzeptierten Schreibreihenfolge in der Sprache des Namens. |
| `lastName` | Das letzte Segment des Namens in der am häufigsten akzeptierten Schreibreihenfolge in der Sprache des Namens. |
| `middleName` | Zwischen dem Vor- und dem Nachnamen angegebene mittlere, alternative oder zusätzliche Namen. |
| `suffix` | Eine Gruppe von Briefen, die nach dem Namen einer Person eingereicht werden, um zusätzliche Informationen bereitzustellen (z. B. `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III`usw.). |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp &quot;Personenname&quot;finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person-name.schema.json)
