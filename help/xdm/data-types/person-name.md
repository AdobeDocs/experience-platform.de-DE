---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;fullName;xdm:fullName;Personenname;Name;datatype;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp "Person"
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den XDM-Datentyp "Personenname".
exl-id: 5cf55fb1-b6b0-4d1c-93c3-7e2b7766599e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 21%

---

# [!UICONTROL Personenname-] Datentyp

[!UICONTROL Der ] Name einer Person ist ein standardmäßiger XDM-Datentyp, der den vollständigen Namen einer Person beschreibt. Da die Konventionen für Namensstrukturen in den Sprachen und Kulturen sehr unterschiedlich sind, sollten Namen immer mit diesem Datentyp modelliert werden.

Darüber hinaus stellt der Datentyp eine Reihe optionaler Eigenschaften bereit, die in Situationen verwendet werden können, in denen nur ein Fragment des vollständigen Namens verwendet werden muss, z. B. das Erstellen eines formellen oder informellen Begrüßens.

<img src="../images/data-types/person-name.png" width="500" /><br />

| Eigenschaft | Beschreibung |
| --- | --- |
| `courtesyTitle` | Eine Abkürzung des Titels, der Ehrlichkeit oder der Begrüßung einer Person (z. B. `Mr.`, `Miss.` oder `Dr.`). |
| `firstName` | Das erste Segment des Namens in der am häufigsten akzeptierten Schreibreihenfolge in der Sprache des Namens. |
| `fullName` | Der vollständige Name der Person, in der Schreibreihenfolge am häufigsten in der Sprache des Namens akzeptiert. |
| `lastName` | Das letzte Segment des Namens in der am häufigsten akzeptierten Schreibreihenfolge in der Sprache des Namens. |
| `middleName` | Zwischen dem Vor- und dem Nachnamen angegebene mittlere, alternative oder zusätzliche Namen. |
| `suffix` | Eine Gruppe von Briefen, die nach dem Namen einer Person bereitgestellt werden, um zusätzliche Informationen bereitzustellen (z. B. `Jr.`, `Sr.`, `M.D.`, `PhD`, `I`, `II`, `III` usw.). |

Weitere Informationen zum Datentyp für den Personennamen finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person-name.schema.json)
