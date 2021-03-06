---
keywords: identities rtcdp;rtcdp identities;Echtzeit-cdp identities
title: Identitäten in Real-time Customer Data Platform
description: Mit Adobe Experience Platform Identity Service können Sie sich einen genaueren Überblick über Kunden und ihr Verhalten verschaffen, indem Sie Identitäten über Geräte und Systeme hinweg zusammenführen.
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 5611a5abc7d1ed7781108b6f263e7550092b715d
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 72%

---

# Identitäten - Übersicht

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und ihr Verhalten zu verschaffen, indem Identitäten zwischen Geräten und Systemen zusammengeführt werden. In der Regel interagieren Kunden mit Ihrer Marke über verschiedene Kanäle. Dazu können unter anderem das Durchsuchen Ihrer Website im Internet, der Einkauf in einer physischen Filiale, die Teilnahme an Ihrem Treueprogramm oder ein Support-Anruf bei einem Helpdesk gehören. Auf diesen verschiedenen Systemen wird eine Identität für diesen Kunden erstellt. [!DNL Identity Service] ermöglicht es, diese Identitäten zusammenzuführen, um das vollständige Bild zu sehen.

Nun können Sie erkennen, dass nicht fünf verschiedene Kunden über fünf verschiedene Kanäle mit Ihrer Marke interagieren, sondern dass es sich dabei um denselben Kunden handelt. So können Sie dafür sorgen, dass er bei jeder Interaktion von einem einheitlichen, personalisierten und relevanten Erlebnis profitiert. Je mehr Informationen über Ihren Kunden bekannt werden (z. B. ein anfänglich anonymer Besucher Ihrer Website, der sich dazu entscheidet, sich für ein Konto zu registrieren und anzumelden), desto klarer wird das Bild Ihres Kunden.

## Identitäts-Namespaces

Identitäts-Namespaces sind eine Komponente von [!DNL Identity Service] und dienen als Indikatoren, die zusätzlichen Kontext für Kundenidentitäten bereitstellen. Ein Beispiel für einen häufig verwendeten ID-Namespace wäre „E-Mail“, sodass Sie bei Verwendung derselben E-Mail-Adresse auf unterschiedlichen Websites verschiedene Identitäten miteinander verknüpfen können, die jeweils eine Unique-Customer-ID aufweisen. So können Sie erkennen, dass die verschiedenen Identitäten in Wahrheit demselben Kunden gehören. [!DNL Experience Platform]Mit können Sie ID-Namespaces verwenden, um in der Benutzeroberfläche nach einzelnen Profilen zu suchen. Weitere Informationen zum Anzeigen von Profilen finden Sie in der [Übersicht zum Profil-Browser](profile-browse.md). Weiterführende Informationen zu Identitäts-Namespaces finden Sie unter [Identitäts-Namespaces – Übersicht](../../identity-service/namespaces.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, die visuell veranschaulicht, wie Ihr Kunde über unterschiedliche Kanäle hinweg mit Ihrer Marke interagiert. Alle Diagramme zur Kundenidentität werden von [!DNL Identity Service] als Reaktion auf Kundenaktivität gemeinsam nahezu in Echtzeit verwaltet und aktualisiert.

[!DNL Identity Service] verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). [!DNL Identity Service] erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

## Nächste Schritte

Identitäten und die Beziehungen zwischen ihnen werden von [!DNL Identity Service] definiert und gepflegt und von [!DNL Real-time Customer Profile] genutzt, um ein vollständiges Bild der einzelnen Kunden und ihrer Interaktionen zu erstellen. Weiterführende Informationen finden Sie in der [Dokumentation zum Identity Service](../../identity-service/home.md).
