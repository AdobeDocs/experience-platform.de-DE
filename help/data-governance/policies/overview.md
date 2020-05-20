---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Übersicht über die Datenverwendungsrichtlinien
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 2%

---


# Übersicht über die Datenverwendungsrichtlinien

Damit Datenverwendungsbeschriftungen die Datenkonformität effektiv unterstützen können, müssen Datenverwendungsrichtlinien implementiert werden. Datenverwendungs-Richtlinien sind Regeln, die die Arten von Marketingaktionen beschreiben, die Sie für Daten in Experience Platform ausführen dürfen oder von denen Sie eingeschränkt sind.

Ein Beispiel für eine Marketingaktion könnte der Wunsch sein, einen Datensatz in einen Drittanbieter-Service zu exportieren. Wenn eine Richtlinie besagt, dass bestimmte Datentypen, wie z. B. persönliche identifizierbare Informationen (PII), nicht exportiert werden können und eine &quot;I&quot;-Beschriftung (Identitätsdaten) auf den Datensatz angewendet wurde, erhalten Sie eine Antwort des Policy Service, in der Sie darauf hingewiesen werden, dass eine Datenverwendungsrichtlinie verletzt wurde.

## So erstellen und arbeiten Sie mit Datenverwendungsrichtlinien

Sobald die Beschriftungen für die Datenverwendung angewendet wurden, können Datenverwaltungen Richtlinien mithilfe der [DUL Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)erstellen.

Als Datenmanager können Sie die Policy Service API verwenden, um Richtlinien im Zusammenhang mit Marketingaktionen zu verwalten und auszuwerten, die für Daten mit DULE-Beschriftungen durchgeführt werden. Mithilfe der API können Sie Richtlinien erstellen und aktualisieren, den Status einer Richtlinie ermitteln und mit Marketingaktionen bewerten, ob eine bestimmte Aktion eine Datenverwendungsrichtlinie verletzt.

Innerhalb der Policy Service-API werden alle Richtlinien und Marketingaktionen als entweder `core` oder `custom` Ressourcen bezeichnet. `core` Ressourcen werden von Adobe definiert und verwaltet, während `custom` Ressourcen von einzelnen Kunden erstellt und gepflegt werden. Die `custom` Ressourcen sind daher einzigartig und nur für die Organisation sichtbar, die sie geschaffen hat.

Weitere Informationen zum Ausführen der von der DUL Policy Service API bereitgestellten wichtigen Vorgänge finden Sie im Entwicklerhandbuch für den [Policy Service](../api/getting-started.md). Eine schrittweise Anleitung zum Arbeiten mit DULE-Richtlinien finden Sie im Lernprogramm zum [Erstellen und Evaluieren von DULE-Richtlinien](create.md).