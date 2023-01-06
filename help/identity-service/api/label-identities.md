---
keywords: Experience Platform; Startseite; beliebte Themen; Beschriftungsidentitäten
solution: Experience Platform
title: Kennzeichnen eines Felds als Identität
description: Felder, die persönliche identifizierbare Informationen (PII) enthalten, können als Identitätsfelder gekennzeichnet werden. Ein in einem Identitätsfeld bereitgestellter Wert wird von Identity Service als Identität interpretiert. Der Namensraum der Identität wird als Teil der Kennzeichnung des Felds angegeben.
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 73%

---

# Kennzeichnen eines Felds als Identität

Felder, die persönliche identifizierbare Informationen (PII) enthalten, können als Identitätsfelder gekennzeichnet werden. Ein in einem Identitätsfeld bereitgestellter Wert wird als Identität interpretiert von [!DNL Identity Service]. Der Namensraum der Identität wird als Teil der Kennzeichnung des Felds angegeben.

Die folgenden Kriterien müssen erfüllt sein, damit ein Feld als Identität gekennzeichnet wird:

- Für die Identität können nur Felder des Typs Zeichenfolge verwendet werden
- Identitäten werden nur in Datensatz- und Zeitreihendaten erkannt
- Nur PII-Felder sollten als Identität gekennzeichnet werden. Die Auswahl eines Felds, das generischere Daten darstellt, führt zu weniger präzisen Beziehungen und möglicherweise zu Fehlern beim Zugriff auf zugehörige Identitäten im Identitätsdiagramm

Anweisungen zur Verwendung der Schema Registry-API zur Kennzeichnung eines Felds als Identität finden Sie unter [Endpunktleitfaden für Deskriptoren](../../xdm/api/descriptors.md#create).

## Nächste Schritte

Fahren Sie mit dem nächsten Tutorial [Auflisten von Cluster-Identitäten](./list-cluster-identites.md) fort.
