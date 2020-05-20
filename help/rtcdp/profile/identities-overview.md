---
title: Identitäten und Identitäts-Namespaces
seo-title: Adobe Experience Platform Identity Service
description: Beschreibung
seo-description: SEO-Beschreibung
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 95%

---


# Identitäten in der Echtzeit-Kundendatenplattform

Mit Adobe Experience Platform Identity Service können Sie sich einen genaueren Überblick über Kunden und ihr Verhalten verschaffen, indem Sie Identitäten über Geräte und Systeme hinweg zusammenführen. In der Regel interagieren Kunden mit Ihrer Marke über verschiedene Kanäle. Dazu können unter anderem das Durchsuchen Ihrer Website im Internet, der Einkauf in einer physischen Filiale, die Teilnahme an Ihrem Treueprogramm oder ein Support-Anruf bei einem Helpdesk gehören. In diesen verschiedenen Systemen wird eine Identität für den Kunden erstellt; Identity Service ermöglicht es, diese Identitäten zusammenzuführen und einen vollständigen Überblick zu erhalten.

Nun können Sie erkennen, dass nicht fünf verschiedene Kunden über fünf verschiedene Kanäle mit Ihrer Marke interagieren, sondern dass es sich dabei um denselben Kunden handelt. So können Sie dafür sorgen, dass er bei jeder Interaktion von einem einheitlichen, personalisierten und relevanten Erlebnis profitiert. Je mehr Informationen über Ihren Kunden bekannt werden (z. B. ein anfänglich anonymer Besucher Ihrer Website, der sich dazu entscheidet, sich für ein Konto zu registrieren und anzumelden), desto klarer wird das Bild Ihres Kunden.

## Identitäts-Namespaces

Identitäts-Namespaces sind eine Komponente von Identity Service und dienen als Indikatoren, die zusätzlichen Kontext für Kundenidentitäten bereitstellen. Ein Beispiel für einen häufig verwendeten ID-Namespace wäre „E-Mail“, sodass Sie bei Verwendung derselben E-Mail-Adresse auf unterschiedlichen Websites verschiedene Identitäten miteinander verknüpfen können, die jeweils eine Unique-Customer-Kennung aufweisen. So können Sie erkennen, dass die verschiedenen Identitäten in Wahrheit demselben Kunden gehören. Mit Experience Platform können Sie ID-Namespaces verwenden, um in der Benutzeroberfläche nach einzelnen Profilen zu suchen. Weiterführende Informationen zum Anzeigen von Profilen finden Sie in der [Übersicht über die Profilansicht](/help/rtcdp/profile/profile-viewer.md). Weitere Informationen zu Identitäts-Namensräumen finden Sie in der Übersicht über den [Identitäts-Namensraum](../../identity-service/namespaces.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, die visuell veranschaulicht, wie Ihr Kunde über unterschiedliche Kanäle hinweg mit Ihrer Marke interagiert. Alle Diagramme zur Kundenidentität werden von Identity Service als Reaktion auf Kundenaktivität nahezu in Echtzeit verwaltet und aktualisiert.

Identity Service verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). Identity Service erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

## Nächste Schritte

Identitäten und Beziehungen zwischen ihnen werden von Identity Service definiert und gepflegt und vom Echtzeit-Kundenprofil genutzt, um ein vollständiges Bild über einzelne Kunden und ihre Interaktionen zu liefern. Weitere Informationen finden Sie in der Dokumentation zum [Identitätsdienst](../../identity-service/home.md).