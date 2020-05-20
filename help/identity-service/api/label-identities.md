---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kennzeichnen eines Felds als Identität
topic: api guide
translation-type: tm+mt
source-git-commit: 40ce232e39f62f1ee478ef05229dd2fc125ee4c0
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 1%

---


# Kennzeichnen eines Felds als Identität

Felder, die persönliche identifizierbare Informationen enthalten, können als Identitätsfelder gekennzeichnet werden. Ein in einem Identitätsfeld bereitgestellter Wert wird vom Identitätsdienst als Identität interpretiert. Der Namensraum der Identität wird als Teil der Kennzeichnung des Feldes angegeben.

Die folgenden Kriterien müssen erfüllt sein, damit ein Feld als Identität gekennzeichnet wird:

- Für die Identität können nur Zeichenfolgentypfelder verwendet werden
- Identitäten werden nur in Datensatz- und Zeitreihendaten erkannt
- Nur PII-Felder sollten als Identität gekennzeichnet werden. Die Auswahl eines Felds, das generische Daten darstellt, führt zu weniger präzisen Beziehungen und möglicherweise zu Fehlern beim Zugriff auf zugehörige Identitäten im Identitätsdiagramm

Anweisungen zur Verwendung der Schema Registry-API zur Kennzeichnung eines Felds als Identität finden Sie unter Deskriptor [erstellen](../../xdm/api/descriptors.md).

## Nächste Schritte

Fahren Sie mit dem nächsten Lernprogramm zur [Liste von Cluster-Identitäten fort.](./list-cluster-identites.md)