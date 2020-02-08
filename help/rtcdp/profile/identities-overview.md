---
title: Identifikations- und Identitätsnamensräume
seo-title: Identity-Dienst für Adobe Experience Platform
description: Beschreibung
seo-description: seo description
translation-type: tm+mt
source-git-commit: 5cba5a1e8139dd85f23250d42a1cd8d2318eb916

---


# Identitäten in Echtzeit-CDP

Mit dem Identitätsdienst für Adobe Experience Platform erhalten Sie einen besseren Überblick über Ihre Kunden und ihr Verhalten, indem Sie Identitäten zwischen Geräten und Systemen zusammenführen. In der Regel interagieren Ihre Kunden über mehrere Kanäle mit Ihrer Marke. Dazu gehören das Durchsuchen Ihrer Website online, der Einkauf im Geschäft, die Teilnahme an Ihrem Treueprogramm oder der Aufruf eines Helpdesk für Support, um nur einige zu nennen. Auf diesen verschiedenen Systemen wird eine Identität für diesen Kunden erstellt, und der Identitätsdienst ermöglicht es, diese Identitäten zusammenzuführen, um das vollständige Bild zu sehen.

Statt dass fünf verschiedene Kunden über fünf verschiedene Kanäle mit Ihrer Marke interagieren, können Sie erkennen, dass es sich um denselben Kunden handelt, und Sie können sicherstellen, dass diese durch jede Interaktion ein einheitliches, personalisiertes und relevantes Erlebnis erhalten. Je mehr Informationen über Ihren Kunden bekannt werden (z. B. ein anonymer Browser Ihrer Website beschließt, sich für ein Konto und eine Anmeldung anzumelden), desto klarer wird das Bild Ihres Kunden.

## Identitätsnamensräume

Identitätsnamensräume sind eine Komponente des Identitätsdienstes und dienen als Indikatoren, die zusätzliche Kontexte für Kundenidentitäten bereitstellen. Ein Beispiel für einen häufig verwendeten ID-Namespace wäre &quot;E-Mail&quot;, bei dem Sie mit der Verwendung derselben E-Mail-Adresse auf mehreren Websites verschiedene Identitäten miteinander verbinden können, wobei jede mit einer eindeutigen Kunden-ID versehen werden kann, da diese tatsächlich demselben Kunden gehört. Mit Experience Platform können Sie ID-Namespaces verwenden, um in der Benutzeroberfläche nach einzelnen Profilen zu suchen. Weitere Informationen zum Anzeigen von Profilen finden Sie in der [Profil-Viewer-Übersicht](/help/rtcdp/profile/profile-viewer.md). Weitere Informationen zu Identitäts-Namespaces finden Sie in der Übersicht über den [Identitäts-Namespace unter Adobe I/O](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitätsnamen, die Ihnen visuell veranschaulicht, wie Ihr Kunde über verschiedene Kanäle mit Ihrer Marke interagiert. Alle Diagramme zur Kundenidentität werden vom Identitätsdienst in Echtzeit verwaltet und aktualisiert, je nach Kundenaktivität.

Der Identitätsdienst verwaltet ein Identitätsdiagramm, das nur von Ihrem Unternehmen angezeigt wird und auf der Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). Der Identitätsdienst erweitert Ihr privates Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, wodurch eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

## Nächste Schritte

Identitäten und die Beziehungen zwischen ihnen werden vom Identitätsdienst definiert und gepflegt und vom Echtzeit-Kundenprofil genutzt, um ein vollständiges Bild der einzelnen Kunden und ihrer Interaktionen zu erstellen. Weitere Informationen finden Sie in der Dokumentation zum [Identitätsdienst auf der Adobe-Website](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_architectural_overview.md).