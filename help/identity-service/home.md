---
keywords: Experience Platform;Startseite;beliebte Themen;Identität;Identität;XDM-Diagramme;Identity Service;Identity Service
solution: Experience Platform
title: Identity Service – Übersicht
description: Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihren Kunden und sein Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle persönliche digitale Erlebnisse sorgen.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ed2c9824d4c2f7bf8dd6a2f8431e93fe833c899c
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 9%

---

# Adobe Experience Platform Identity Service

Um relevante digitale Erlebnisse bereitstellen zu können, benötigen Sie eine umfassende und genaue Darstellung der realen Einheiten, aus denen sich Ihr Kundenstamm zusammensetzt.

Unternehmen und Unternehmen stehen heutzutage vor einer großen Menge unterschiedlicher Datensätze: Ihre einzelnen Kunden sind durch eine Vielzahl unterschiedlicher Kennungen repräsentiert. Ihr Kunde kann mit verschiedenen Webbrowsern (Safari, Google Chrome), Hardwaregeräten (Smartphones, Laptops) und anderen Personen-IDs (CRM-IDs, E-Mail-Konten) verknüpft werden. Dadurch entsteht eine unzusammenhängende Sicht auf Ihren Kunden.

Sie können diese Probleme mit dem Adobe Experience Platform Identity Service und seinen Funktionen lösen, um:

* Generieren Sie eine **Identitätsdiagramm** , die unterschiedliche Identitäten miteinander verknüpfen, sodass Sie eine visuelle Darstellung erhalten, wie ein Kunde über verschiedene Kanäle mit Ihrer Marke interagiert.
* Erstellen Sie ein Diagramm für das Echtzeit-Kundenprofil, das dann verwendet wird, um durch Zusammenführen von Attributen und Verhaltensweisen eine umfassende Ansicht des Kunden zu erstellen.
* Führen Sie mithilfe der verschiedenen Tools eine Validierung und ein Debugging durch.

In diesem Dokument erhalten Sie einen Überblick über Identity Service und darüber, wie Sie seine Funktionen im Kontext von Experience Platform verwenden können.

## Terminologie {#terminology}

Bevor Sie sich mit den Details von Identity Service befassen, lesen Sie bitte die folgende Tabelle, um eine Zusammenfassung der Schlüsselbegriffe zu erhalten:

| Begriff | Definition |
| --- | --- |
| Identität | Eine Identität sind Daten, die für eine Entität eindeutig sind. In der Regel handelt es sich hierbei um ein echtes Objekt, z. B. eine Person, ein Hardwaregerät oder einen Webbrowser (dargestellt durch ein Cookie). Eine voll qualifizierte Identität besteht aus zwei Elementen: einer **Identitäts-Namespace** und **Identitätswert**. |
| Identity-Namespace | Ein Identity-Namespace ist der Kontext einer bestimmten Identität. Beispiel: ein Namespace von `Email` könnte mit dem Identitätswert übereinstimmen: **julien<span>@acme.com**. Auf ähnliche Weise wird ein Namespace von `Phone` könnte mit dem Identitätswert übereinstimmen: `555-555-1234`. Weitere Informationen finden Sie im Abschnitt [Übersicht über Identitäts-Namespace](./features/namespaces.md). |
| Identitätswert | Ein Identitätswert ist eine Zeichenfolge, die eine reale Entität darstellt und innerhalb von Identity Service über einen Namespace kategorisiert wird. Beispielsweise der Identitätswert (Zeichenfolge) **julien<span>@acme.com** könnte als `Email` Namespace. |
| Identitätstyp | Ein Identitätstyp ist eine Komponente eines Identitäts-Namespace. Der Identitätstyp gibt an, ob Identitätsdaten in einem Identitätsdiagramm verknüpft sind. |
| Link | Ein Link oder eine Verknüpfung ist eine Methode, um festzustellen, dass zwei unterschiedliche Identitäten dieselbe Entität repräsentieren. Beispielsweise eine Verknüpfung zwischen`Email` = julien<span>@acme.com und &quot;`Phone` = 555-555-1234&quot; bedeutet, dass beide Identitäten dieselbe Entität repräsentieren. Dies deutet darauf hin, dass der Kunde, der mit Ihrer Marke sowohl mit der E-Mail-Adresse von julien interagiert hat<span>@acme.com und die Telefonnummer 555-555-1234 ist identisch. |
| Identity Service | Identity Service ist ein Dienst innerhalb von Experience Platform, der Identitäten verknüpft (oder aufhebt), um Identitätsdiagramme zu verwalten. |
| Identitätsdiagramm | Das Identitätsdiagramm ist eine Sammlung von Identitäten, die einen einzelnen Kunden repräsentieren. Weitere Informationen finden Sie im Handbuch unter [Verwenden des Identitätsdiagramm-Viewers](./features/identity-graph-viewer.md). |
| Echtzeit-Kundenprofil | Das Echtzeit-Kundenprofil ist ein Dienst in Adobe Experience Platform, der Folgendes ermöglicht: <ul><li>Führt Profilfragmente zusammen, um ein Profil zu erstellen, das auf einem Identitätsdiagramm basiert.</li><li>Segmente von Profilen, damit sie zur Aktivierung an das Ziel gesendet werden können.</li></ul> |
| Profil | Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson. Ein Profil besteht aus vier Elementen: <ul><li>Attribute: Attribute liefern Informationen wie Name, Alter oder Geschlecht.</li><li>Verhalten: Verhalten liefert Informationen zu den Aktivitäten eines bestimmten Profils. Beispielsweise kann ein Profilverhalten erkennen, ob ein bestimmtes Profil &quot;nach Sandalen suchen&quot;oder &quot;T-Shirts bestellen&quot;war.</li><li>Identitäten: Bei einem zusammengeführten Profil werden hierdurch Informationen zu allen Identitäten bereitgestellt, die mit der Person verknüpft sind. Identitäten können in drei Kategorien unterteilt werden: Person (CRMID, E-Mail, Telefon), Gerät (IDFA, GAID) und Cookie (ECID, AAID).</li><li>Zielgruppenmitgliedschaften: Die Gruppen, zu denen das Profil gehört (treue Benutzer, in Kalifornien lebende Benutzer usw.)</li></ul> |

{style="table-layout:auto"}

## Was ist Identity Service?

![Identitätszusammenfügung in Platform](./images/identity-service-stitching.png)

In einem B2C-Kontext (Business-To-Customer) interagieren Kunden mit Ihrem Unternehmen und etablieren eine Beziehung zu Ihrer Marke. Ein typischer Kunde kann in einer beliebigen Anzahl von Systemen in der Dateninfrastruktur Ihres Unternehmens aktiv sein. Jeder Kunde kann in Ihrem E-Commerce-, Treueprogramm- und Helpdesk-System aktiv sein. Derselbe Kunde kann sich auch anonym oder auf authentifiziertem Wege auf einer beliebigen Anzahl verschiedener Geräte engagieren.

Betrachten Sie die folgende Customer Journey:

* Julien hat ein Konto auf Ihrer E-Commerce-Website erstellt und einige Artikel in der Vergangenheit bestellt. Julien verwendet normalerweise ihren persönlichen Laptop, um mit jeder Nutzungsdauer einzukaufen und sich bei ihrem Konto anzumelden.
* Während eines Besuchs auf Ihrer Site verwendet sie jedoch ein Tablet, um nach Sandalen zu suchen. Da sie ein anderes Gerät verwendet hat, meldet sie sich während dieser Sitzung weder an noch gibt sie eine Bestellung auf.
* An dieser Stelle werden die Aktivitäten von Julien in zwei separaten Profilen dargestellt:
   * Ihr erstes Profil ist ihre E-Commerce-Anmelde-ID. Dieses Profil wird verwendet, wenn sie eine Kombination aus Benutzername und Kennwort verwendet, um ihre Sitzung auf Ihrer E-Commerce-Site zu authentifizieren. Dieses Profil wird durch eine geräteübergreifende Kennung identifiziert.
   * Ihr zweites Profil ist ihr Tablet-Gerät. Dieses Profil wurde erstellt, nachdem sie Ihre E-Commerce-Site anonym mit einem Tablet besucht hat, ohne sich bei ihrem Konto anzumelden. Dieses Profil wird durch eine Cookie-Kennung identifiziert.
* Später setzt Julien ihre Tablet-Sitzung fort. Dieses Mal meldet sie sich jedoch bei ihrem Konto an. Daher verknüpft Identity Service nun die Aktivität des Tablet-Geräts von Julien mit ihrer E-Commerce-Anmelde-ID.
* In Zukunft könnten Ihre zielgerichteten Inhalte das vollständige Profil, den Kaufverlauf und die anonyme Browsing-Aktivität von Julien widerspiegeln.

>[!IMPORTANT]
>
>Sie können Identity Service verwenden, um Identitäten zu verknüpfen und ein vollständiges Bild Ihres Kunden zusammenzustellen, das andernfalls auf verschiedene Systeme verteilt wäre.

## Was macht Identity Service?

Identity Service bietet die folgenden Vorgänge, um seinen Auftrag zu erfüllen:

* Erstellen Sie benutzerdefinierte Namespaces, die den Anforderungen Ihres Unternehmens entsprechen.
* Identitätsdiagramme erstellen, aktualisieren und anzeigen.
* Identitäten basierend auf Datensätzen löschen.
* Identitäten löschen, um die Einhaltung von Vorschriften sicherzustellen.

## Verknüpfen von Identitäten mit Identity Service

Eine Verknüpfung zwischen zwei Identitäten wird hergestellt, wenn der Identitäts-Namespace und die Identitätswerte übereinstimmen.

Ein typisches Anmeldeereignis **sendet zwei Identitäten** in Experience Platform:

* Die Personenkennung (z. B. eine CRM-ID), die einen authentifizierten Benutzer darstellt.
* Die Browser-Kennung (z. B. eine ECID), die den Webbrowser darstellt.

Siehe folgendes Beispiel:

* Sie melden sich mit Ihrem Benutzernamen und Passwort auf einer E-Commerce-Website mit Ihrem Laptop an. Dieses Ereignis qualifiziert Sie als authentifizierten Benutzer, sodass Identity Service Ihre CRM-ID erkennt.
* Ihre Verwendung eines Browsers für den Zugriff auf die E-Commerce-Website wird auch von Identity Service als Ereignis erkannt. Dieses Ereignis wird im Identity Service durch eine ECID dargestellt.
* Im Hintergrund verarbeitet Identity Service die beiden Ereignisse wie folgt: `CRM_ID:ABC, ECID:123`.
   * CRM-ID: ABC ist der Namespace und der Wert, der Sie als authentifizierten Benutzer darstellt.
   * ECID: 123 ist der Namespace und der Wert, der für die Nutzung Ihres Webbrowsers auf Ihrem Laptop steht.
* Wenn Sie sich als Nächstes mit denselben Anmeldedaten bei derselben E-Commerce-Website anmelden, aber den Webbrowser auf Ihrem Telefon anstelle des Webbrowsers auf Ihrem Laptop verwenden, wird eine neue ECID im Identity Service registriert.
* Hinter den Kulissen verarbeitet Identity Service dieses neue Ereignis als `{CRM_ID:ABC, ECID:456}`, wobei CRM_ID: ABC Ihre authentifizierte Kunden-ID darstellt und ECID:456 den Webbrowser auf Ihrem Mobilgerät darstellt.

In Anbetracht der obigen Szenarien erstellt Identity Service eine Verknüpfung zwischen `{CRM_ID:ABC, ECID:123}`sowie `{CRM_ID:ABC, ECID:456}`. Dies führt zu einem Identitätsdiagramm, in dem Sie drei Identitäten &quot;besitzen&quot;: eine für die Personen-ID (CRM ID) und zwei für Cookie-IDs (ECIDs).

Weitere Informationen finden Sie im Handbuch unter [Verknüpfen von Identitäten zwischen Identity Service](./features/identity-linking-logic.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identity-Namespaces, anhand derer Sie visualisieren und besser verstehen können, welche Kundenidentitäten zusammengeführt werden und wie. Tutorial lesen unter [Verwenden des Identitätsdiagramm-Viewers](./features/identity-graph-viewer.md) für weitere Informationen.

Das folgende Video soll Ihnen Identitäten und Identitätsdiagramme näherbringen.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Die Rolle von Identity Service in der Experience Platform-Infrastruktur

Identity Service spielt bei der Experience Platform eine wichtige Rolle. Zu diesen wichtigen Integrationen gehören die folgenden:

* [Schemas](../xdm/home.md): Innerhalb eines bestimmten Schemas ermöglichen die Erstellung von Identitätsdiagrammen die Schemafelder, die als Identität markiert sind.
* [Datensätze](../catalog/datasets/overview.md): Wenn ein Datensatz für die Aufnahme in das Echtzeit-Kundenprofil aktiviert ist, werden Identitätsdiagramme aus dem Datensatz generiert, da der Datensatz mindestens zwei als Identität markierte Felder aufweist.
* [Web SDK](../edge/home.md): Web SDK sendet Erlebnisereignisse an Adobe Experience Platform und Identity Service generiert ein Diagramm, wenn im Ereignis zwei oder mehr Identitäten vorhanden sind.
* [Echtzeit-Kundenprofil](../profile/home.md): Bevor Attribute und Ereignisse für ein bestimmtes Profil zusammengeführt werden, kann das Echtzeit-Kundenprofil auf das Identitätsdiagramm verweisen. Weitere Informationen finden Sie im Handbuch unter [Verstehen der Beziehung zwischen Identity Service und Echtzeit-Kundenprofil](./identity-and-profile.md).
* [Ziele](../destinations/home.md): Ziele können Profilinformationen basierend auf einem Identitäts-Namespace an andere Systeme senden, z. B. Hash-E-Mails.
* [Segmentübereinstimmung](../segmentation/ui/segment-match/overview.md): Die Segmentübereinstimmung stimmt mit zwei Profilen in zwei verschiedenen Sandboxes überein, die denselben Identitäts-Namespace und denselben Identitätswert aufweisen.
* [Privacy Service](../privacy-service/home.md): Wenn die Löschanfrage Folgendes enthält: `identity`festgelegt ist, kann die angegebene Kombination aus Namespace und Identitätswert mithilfe der Datenschutzanfrage-Verarbeitungsfunktion in Privacy Service aus dem Identity Service gelöscht werden.

