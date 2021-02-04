---
keywords: Experience Platform;Startseite;beliebte Themen;Beschriftungskennungen
solution: Experience Platform
title: Kennzeichnen eines Felds als Identität
topic: api guide
description: Felder, die persönliche identifizierbare Informationen (PII) enthalten, können als Identitätsfelder gekennzeichnet werden. Ein in einem Identitätsfeld bereitgestellter Wert wird von Identity Service als Identität interpretiert. Der Namensraum der Identität wird als Teil der Kennzeichnung des Felds angegeben.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 89%

---


# Kennzeichnen eines Felds als Identität

Felder, die persönliche identifizierbare Informationen (PII) enthalten, können als Identitätsfelder gekennzeichnet werden. Ein in einem Identitätsfeld bereitgestellter Wert wird von [!DNL Identity Service] als Identität interpretiert. Der Namensraum der Identität wird als Teil der Kennzeichnung des Felds angegeben.

Die folgenden Kriterien müssen erfüllt sein, damit ein Feld als Identität gekennzeichnet wird:

- Für die Identität können nur Felder des Typs Zeichenfolge verwendet werden
- Identitäten werden nur in Datensatz- und Zeitreihendaten erkannt
- Nur PII-Felder sollten als Identität gekennzeichnet werden. Die Auswahl eines Felds, das generischere Daten darstellt, führt zu weniger präzisen Beziehungen und möglicherweise zu Fehlern beim Zugriff auf zugehörige Identitäten im Identitätsdiagramm

Anweisungen zur Verwendung der Schema Registry-API zur Kennzeichnung eines Felds als Identität finden Sie unter [Erstellen eines Deskriptors](../../xdm/api/descriptors.md).

## Nächste Schritte

Fahren Sie mit dem nächsten Tutorial [Auflisten von Cluster-Identitäten](./list-cluster-identites.md) fort.