---
keywords: Experience Platform; Startseite; beliebte Themen; Beschriftungsidentitäten
title: Kennzeichnen eines Felds als Identität in der Benutzeroberfläche
description: Felder, die persönliche identifizierbare Informationen (PII) enthalten, können als Identitätsfelder gekennzeichnet werden. Ein in einem Identitätsfeld bereitgestellter Wert wird von Identity Service als Identität interpretiert. Der Namensraum der Identität wird als Teil der Kennzeichnung des Felds angegeben.
source-git-commit: ae51c9bd07944f26be2809a6d15f9d9e8c2fd5a1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 67%

---

# Kennzeichnen eines Felds als Identität in der Benutzeroberfläche

Felder, die persönliche identifizierbare Informationen (PII) enthalten, können als Identitätsfelder gekennzeichnet werden. Ein in einem Identitätsfeld bereitgestellter Wert wird als Identität interpretiert von [!DNL Identity Service]. Der Namensraum der Identität wird als Teil der Kennzeichnung des Felds angegeben.

Die folgenden Kriterien müssen erfüllt sein, damit ein Feld als Identität gekennzeichnet wird:

* Für die Identität können nur Felder des Typs Zeichenfolge verwendet werden
* Identitäten werden nur in Datensatz- und Zeitreihendaten erkannt
* Nur PII-Felder sollten als Identität gekennzeichnet werden. Die Auswahl eines Felds, das generischere Daten darstellt, führt zu weniger präzisen Beziehungen und möglicherweise zu Fehlern beim Zugriff auf zugehörige Identitäten im Identitätsdiagramm

Anweisungen zur Beschriftung von Identitätsfeldern in der Benutzeroberfläche finden Sie im Handbuch unter [Identitätsfelder in der Benutzeroberfläche definieren](../../xdm/ui/fields/identity.md).

## Nächste Schritte

Weitere Informationen finden Sie unter [!DNL Identity Service], siehe [[!DNL Identity Service] Übersicht](../home.md).
