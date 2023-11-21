---
keywords: Identitäten rtcdp;rtcdp Identitäten;rtcdp-Identitäten;Real-Time CDP-Identitäten
title: Identitäten in Real-time Customer Data Platform
description: Mit Adobe Experience Platform Identity Service können Sie sich einen genaueren Überblick über Kundinnen und Kunden und ihr Verhalten verschaffen, indem Sie Identitäten über Geräte und Systeme hinweg zusammenführen.
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 100%

---

# Übersicht zu Identitäten

Mit Adobe Experience Platform [!DNL Identity Service] können Sie sich einen genaueren Überblick über Kundinnen und Kunden und ihr Verhalten verschaffen, indem Sie Identitäten über Geräte und Systeme hinweg zusammenführen. In der Regel interagieren Kundinnen und Kunden mit Ihrer Marke über verschiedene Kanäle. Dazu können unter anderem das Durchsuchen Ihrer Website im Internet, der Einkauf in einer physischen Filiale, die Teilnahme an Ihrem Treueprogramm oder ein Support-Anruf bei einem Helpdesk gehören. In diesen verschiedenen Systemen wird jeweils eine Kundenidentität erstellt. [!DNL Identity Service] ermöglicht es, diese Identitäten zusammenzuführen, um einen vollständigen Überblick zu erhalten.

Nun können Sie erkennen, dass nicht fünf verschiedene Kunden über fünf verschiedene Kanäle mit Ihrer Marke interagieren, sondern dass es sich dabei um denselben Kunden handelt. So können Sie dafür sorgen, dass er bei jeder Interaktion von einem einheitlichen, personalisierten und relevanten Erlebnis profitiert. Je mehr Informationen über Ihren Kunden bekannt werden (z. B. ein anfänglich anonymer Besucher Ihrer Website, der sich dazu entscheidet, sich für ein Konto zu registrieren und anzumelden), desto klarer wird das Bild Ihres Kunden.

## Identitäts-Namespaces

Identity-Namespaces sind eine [!DNL Identity Service]-Komponente und dienen als Indikatoren, die zusätzlichen Kontext für Kundenidentitäten bereitstellen. Ein Beispiel für einen häufig verwendeten ID-Namespace wäre „E-Mail“, sodass Sie bei Verwendung derselben E-Mail-Adresse auf unterschiedlichen Websites verschiedene Identitäten miteinander verknüpfen können, die jeweils eine Unique-Customer-ID aufweisen. So können Sie erkennen, dass die verschiedenen Identitäten in Wahrheit derselben Kundin oder demselben Kunden gehören. Mit [!DNL Experience Platform] können Sie ID-Namespaces verwenden, um in der Benutzeroberfläche nach einzelnen Profilen zu suchen. Weiterführende Informationen zum Anzeigen von Profilen finden Sie in der [Übersicht zum Durchsuchen von Profilen](profile-browse.md). Weiterführende Informationen zu Identitäts-Namespaces finden Sie unter [Identitäts-Namespaces – Übersicht](../../identity-service/namespaces.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, die visuell veranschaulicht, wie Ihr Kunde über unterschiedliche Kanäle hinweg mit Ihrer Marke interagiert. Alle Diagramme zur Kundenidentität werden von [!DNL Identity Service] als Reaktion auf Kundenaktivität gemeinsam nahezu in Echtzeit verwaltet und aktualisiert.

[!DNL Identity Service] verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). [!DNL Identity Service] erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

## Nächste Schritte

Identitäten und die Beziehungen zwischen ihnen werden vom [!DNL Identity Service] definiert und gepflegt und vom [!DNL Real-Time Customer Profile] genutzt, um ein vollständiges Bild über einzelne Kundinnen und Kunden und ihre Interaktionen zu liefern. Weiterführende Informationen finden Sie in der [Dokumentation zum Identity Service](../../identity-service/home.md).
