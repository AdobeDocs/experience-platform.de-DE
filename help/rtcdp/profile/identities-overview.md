---
title: Identitäten und Identitäts-Namespaces
seo-title: Adobe Experience Platform Identity Service
description: Beschreibung
seo-description: SEO-Beschreibung
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 72%

---


# Identitäten in der Echtzeit-Kundendatenplattform

Adobe Experience Platform [!DNL Identity Service] helps you to gain a better view of your customers and their behavior by bridging together identities across devices and systems. In der Regel interagieren Kunden mit Ihrer Marke über verschiedene Kanäle. Dazu können unter anderem das Durchsuchen Ihrer Website im Internet, der Einkauf in einer physischen Filiale, die Teilnahme an Ihrem Treueprogramm oder ein Support-Anruf bei einem Helpdesk gehören. Across these multiple systems, there is an identity created for that customer, and [!DNL Identity Service] makes it possible to bring those identities together to see the complete picture.

Nun können Sie erkennen, dass nicht fünf verschiedene Kunden über fünf verschiedene Kanäle mit Ihrer Marke interagieren, sondern dass es sich dabei um denselben Kunden handelt. So können Sie dafür sorgen, dass er bei jeder Interaktion von einem einheitlichen, personalisierten und relevanten Erlebnis profitiert. Je mehr Informationen über Ihren Kunden bekannt werden (z. B. ein anfänglich anonymer Besucher Ihrer Website, der sich dazu entscheidet, sich für ein Konto zu registrieren und anzumelden), desto klarer wird das Bild Ihres Kunden.

## Identitäts-Namespaces

Identity namespaces are a component of [!DNL Identity Service] and serve as indicators providing additional context to customer identities. Ein Beispiel für einen häufig verwendeten ID-Namespace wäre „E-Mail“, sodass Sie bei Verwendung derselben E-Mail-Adresse auf unterschiedlichen Websites verschiedene Identitäten miteinander verknüpfen können, die jeweils eine Unique-Customer-Kennung aufweisen. So können Sie erkennen, dass die verschiedenen Identitäten in Wahrheit demselben Kunden gehören. [!DNL Experience Platform]Mit können Sie ID-Namespaces verwenden, um in der Benutzeroberfläche nach einzelnen Profilen zu suchen. Weiterführende Informationen zum Anzeigen von Profilen finden Sie in der [Übersicht über die Profilansicht](/help/rtcdp/profile/profile-viewer.md). Weiterführende Informationen zu Identitäts-Namespaces finden Sie unter [Identitäts-Namespaces – Übersicht](../../identity-service/namespaces.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, die visuell veranschaulicht, wie Ihr Kunde über unterschiedliche Kanäle hinweg mit Ihrer Marke interagiert. All customer identity graphs are collectively managed and updated by [!DNL Identity Service] in near real-time, in response to customer activity.

[!DNL Identity Service] verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). [!DNL Identity Service] erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

## Nächste Schritte

Identities, and the relationships between them, are defined and maintained by [!DNL Identity Service] and leveraged by [!DNL Real-time Customer Profile] to build a complete picture of each individual customer and their interactions. Weiterführende Informationen finden Sie in der [Dokumentation zum Identity Service](../../identity-service/home.md).