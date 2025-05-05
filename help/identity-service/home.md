---
keywords: Experience Platform;Startseite;beliebte Themen;Identität;Identität;XDM-Diagramme;Identity Service;Identity Service
solution: Experience Platform
title: Identity Service – Übersicht
description: Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihren Kunden und sein Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle persönliche digitale Erlebnisse sorgen.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 8%

---

# Adobe Experience Platform Identity Service

Um relevante digitale Erlebnisse bereitzustellen, benötigen Sie eine umfassende und genaue Darstellung der realen Entitäten, aus denen Ihr Kundenstamm besteht.

Organisationen und Unternehmen sehen sich heutzutage mit einer großen Anzahl unterschiedlicher Datensätze konfrontiert: Ihre einzelnen Kunden werden durch eine Vielzahl verschiedener Kennungen dargestellt. Ihre Kundin bzw. Ihr Kunde kann mit verschiedenen Webbrowsern (Safari, Google Chrome), Hardwaregeräten (Smartphones, Laptops) und anderen Personenkennungen (CRMIDs, E-Mail-Konten) verknüpft werden. Dadurch entsteht eine uneinheitliche Sicht auf Ihren Kunden.

Sie können diese Herausforderungen mit dem Adobe Experience Platform Identity Service und seinen Funktionen zu folgenden Zwecken lösen:

* Erzeugen Sie ein **Identitätsdiagramm**, das unterschiedliche Identitäten miteinander verknüpft, sodass Sie visuell darstellen können, wie ein Kunde über verschiedene Kanäle hinweg mit Ihrer Marke interagiert.
* Erstellen Sie ein Diagramm für das Echtzeit-Kundenprofil, das dann verwendet wird, um eine umfassende Ansicht des Kunden zu erstellen, indem Attribute und Verhaltensweisen zusammengeführt werden.
* Führen Sie Validierung und Debugging mit den verschiedenen Tools durch.

Dieses Dokument bietet einen Überblick über Identity Service und darüber, wie Sie dessen Funktionen im Kontext von Experience Platform verwenden können.

## Terminologie {#terminology}

Bevor Sie sich mit den Details von Identity Service befassen, lesen Sie bitte die folgende Tabelle für eine Zusammenfassung der Schlüsselbegriffe:

| Begriff | Definition |
| --- | --- |
| Identität | Eine Identität besteht aus Daten, die eindeutig für eine Entität sind. In der Regel handelt es sich dabei um ein reales Objekt, z. B. eine einzelne Person, ein Hardwaregerät oder einen Webbrowser (dargestellt durch ein Cookie). Eine vollständig qualifizierte Identität besteht aus zwei Elementen: einem **Identity-Namespace** und einem **Identity-Wert**. |
| Identity-Namespace | Ein Identity-Namespace ist der Kontext einer bestimmten Identität. Beispielsweise könnte ein Namespace von `Email` mit dem Identitätswert übereinstimmen: **julien<span>@acme.com**. Ebenso könnte ein Namespace von `Phone` dem Identitätswert entsprechen: `555-555-1234`. Weitere Informationen finden Sie unter [Übersicht über Identity-Namespaces](./features/namespaces.md). |
| Identitätswert | Ein Identitätswert ist eine Zeichenfolge, die eine reale Entität darstellt und innerhalb von Identity Service über einen Namespace kategorisiert ist. Beispielsweise kann der Identitätswert (Zeichenfolge) **julien<span>@acme.com** als `Email` Namespace kategorisiert werden. |
| Identitätstyp | Ein Identitätstyp ist eine Komponente eines Identity-Namespace. Der Identitätstyp gibt an, ob Identitätsdaten in einem Identitätsdiagramm verknüpft sind oder nicht. |
| Link | Eine Relation oder eine Relation ist eine Methode, um festzustellen, ob zwei unterschiedliche Identitäten dieselbe Entität repräsentieren. Eine Relation zwischen &quot;`Email` = julien<span>@acme.com“ und &quot;`Phone` = 555-555-1234“ bedeutet beispielsweise, dass beide Identitäten dieselbe Entität darstellen. Dies deutet darauf hin, dass der Kunde, der mit Ihrer Marke sowohl mit der E-Mail-Adresse julien<span>@acme.com als auch mit der Telefonnummer 555-555-1234 interagiert hat, identisch ist. |
| Identity Service | Identity Service ist ein Service innerhalb von Experience Platform, der Identitäten verknüpft (oder deren Verknüpfung aufhebt), um Identitätsdiagramme zu verwalten. |
| Identitätsdiagramm | Das Identitätsdiagramm ist eine Sammlung von Identitäten, die einen einzelnen Kunden darstellen. Weitere Informationen finden sich im Handbuch unter [Verwenden des Identitätsdiagramm-Viewers](./features/identity-graph-viewer.md). |
| Echtzeit-Kundenprofil | Das Echtzeit-Kundenprofil ist ein Service innerhalb von Adobe Experience Platform, der Folgendes ermöglicht: <ul><li>Führt Profilfragmente basierend auf einem Identitätsdiagramm zusammen, um ein Profil zu erstellen.</li><li>Profile segmentieren, sodass sie dann zur Aktivierung an das Ziel gesendet werden können.</li></ul> |
| Profil | Ein Profil ist eine Darstellung eines Subjekts, einer Organisation oder einer Einzelperson. Ein Profil besteht aus vier Elementen: <ul><li>Attribute: Attribute geben Informationen wie Namen, Alter oder Geschlecht an.</li><li>Verhalten: Verhaltensweisen geben Informationen über die Aktivitäten eines bestimmten Profils. Beispielsweise kann ein Profilverhalten erkennen, ob ein bestimmtes Profil „nach Sandalen gesucht“ oder „T-Shirts bestellt“ hat.</li><li>Identitäten: Bei einem zusammengeführten Profil enthält dies Informationen zu allen Identitäten, die mit der Person verknüpft sind. Identitäten können in drei Kategorien eingeteilt werden: Person (CRMID, E-Mail, Telefon), Gerät (IDFA, GAID) und Cookie (ECID, AAID).</li><li>Zielgruppenzugehörigkeiten: Die Gruppen, zu denen das Profil gehört (loyale Benutzer, in Kalifornien lebende Benutzer usw.)</li></ul> |

{style="table-layout:auto"}

## Was ist Identity Service?

![Identitätszusammenfügung in Experience Platform](./images/identity-service-stitching.png)

Im B2C-Kontext (Business-to-Customer) interagieren Kunden mit Ihrem Unternehmen und stellen eine Beziehung zu Ihrer Marke her. Ein typischer Kunde kann in der Dateninfrastruktur Ihres Unternehmens in einer beliebigen Anzahl von Systemen aktiv sein. Jeder Kunde kann in Ihren E-Commerce-, Treueprogramm- und Helpdesk-Systemen aktiv sein. Derselbe Kunde kann auch anonym oder über authentifizierte Mittel auf eine beliebige Anzahl verschiedener Geräte zugreifen.

Betrachten Sie die folgende Kunden-Journey:

* Julien hat auf Ihrer E-Commerce-Website ein Konto erstellt und in der Vergangenheit einige Artikel bestellt. Julien verwendet normalerweise ihren privaten Laptop zum Einkaufen und meldet sich bei jeder Verwendung bei ihrem Konto an.
* Bei einem ihrer Besuche auf Ihrer Website sucht sie jedoch mit einem Tablet nach Sandalen. Da sie während dieser Sitzung ein anderes Gerät verwendet hat, meldet sie sich weder an noch gibt sie eine Bestellung auf.
* Zu diesem Zeitpunkt werden Juliens Aktivitäten in zwei separaten Profilen dargestellt:
   * Ihr erstes Profil ist ihre E-Commerce-Anmelde-ID. Dieses Profil wird verwendet, wenn sie eine Kombination aus Benutzername und Kennwort verwendet, um ihre Sitzung auf Ihrer E-Commerce-Site zu authentifizieren. Dieses Profil wird durch eine geräteübergreifende Kennung identifiziert.
   * Ihr zweites Profil ist ihr Tablet. Dieses Profil wurde erstellt, nachdem sie anonym mit einem Tablet auf Ihrer E-Commerce-Site surft, ohne sich bei ihrem Konto anzumelden. Dieses Profil wird durch eine Cookie-Kennung identifiziert.
* Später setzt Julien ihre Tablet-Sitzung fort. Diesmal meldet sie sich jedoch bei ihrem Konto an. Infolgedessen verknüpft Identity Service die Aktivitäten von Julien auf ihrem Tablet nun mit ihrer E-Commerce-Anmelde-ID.
* Künftig könnten Ihre zielgerichteten Inhalte Juliens gesamtes Profil, den Kaufverlauf und die anonyme Browser-Aktivität widerspiegeln.

>[!IMPORTANT]
>
>Mit Identity Service können Sie Identitäten verknüpfen und ein vollständiges Bild Ihres Kunden zusammenstellen, das andernfalls über verschiedene Systeme verstreut sein könnte.

## Was tut Identity Service?

Identity Service bietet die folgenden Vorgänge, um seinen Auftrag zu erfüllen:

* Erstellen Sie benutzerdefinierte Namespaces, die den Anforderungen Ihres Unternehmens entsprechen.
* Erstellen, Aktualisieren und Anzeigen von Identitätsdiagrammen.
* Löschen von Identitäten basierend auf Datensätzen.
* Löschen Sie Identitäten, um die Einhaltung behördlicher Auflagen sicherzustellen.

## Verknüpfen von Identitäten mit Identity Service

Eine Verknüpfung zwischen zwei Identitäten wird hergestellt, wenn der Identity-Namespace und die Identitätswerte übereinstimmen.

Ein typisches Anmeldeereignis (**zwei Identitäten)** Experience Platform:

* Die Personenkennung (z. B. eine CRMID), die einen authentifizierten Benutzer darstellt.
* Die Browser-Kennung (z. B. eine ECID), die den Webbrowser darstellt.

Siehe folgendes Beispiel:

* Sie melden sich mit Ihrer Benutzername- und Passwortkombination auf einer E-Commerce-Website mit Ihrem Laptop an. Dieses Ereignis qualifiziert Sie als authentifizierten Benutzer, sodass Identity Service Ihre CRMID erkennt.
* Ihre Nutzung eines Browsers für den Zugriff auf die E-Commerce-Website wird auch von Identity Service als Ereignis erkannt. Dieses Ereignis wird in Identity Service durch eine ECID dargestellt.
* Im Hintergrund verarbeitet Identity Service die beiden Ereignisse wie folgt: `CRM_ID:ABC, ECID:123`.
   * CRMID: ABC ist der Namespace und der Wert, der Sie als authentifizierten Benutzer repräsentiert.
   * ECID: 123 ist der Namespace und der Wert, der für die Nutzung Ihres Webbrowsers auf Ihrem Laptop steht.
* Wenn Sie sich anschließend mit denselben Anmeldeinformationen auf derselben E-Commerce-Website anmelden, aber den Webbrowser auf Ihrem Smartphone anstatt den Webbrowser auf Ihrem Laptop verwenden, wird in Identity Service eine neue ECID registriert.
* Hinter den Kulissen verarbeitet Identity Service dieses neue Ereignis wie `{CRM_ID:ABC, ECID:456}`, wobei CRM_ID: ABC Ihre authentifizierte Kunden-ID und ECID:456 den Webbrowser auf Ihrem Mobilgerät darstellt.

In Anbetracht der oben genannten Szenarien stellt Identity Service eine Verbindung zwischen `{CRM_ID:ABC, ECID:123}` und `{CRM_ID:ABC, ECID:456}` her. Dies führt zu einem Identitätsdiagramm, in dem Sie drei Identitäten „besitzen“: eine für Personen-ID (CRMID) und zwei für Cookie-IDs (ECIDs).

Weitere Informationen finden Sie im Handbuch unter [Verknüpfen von Identitäten mit Identity Service](./features/identity-linking-logic.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identity-Namespaces, anhand derer Sie visualisieren und besser verstehen können, welche Kundenidentitäten zusammengeführt werden und wie. Lesen Sie das Tutorial [Verwenden des Identitätsdiagramm-Viewers](./features/identity-graph-viewer.md) für weitere Informationen.

Das folgende Video soll Ihnen Identitäten und Identitätsdiagramme näherbringen.

>[!VIDEO](https://video.tv.adobe.com/v/3422772?quality=12&learn=on&captions=ger)

## Grundlegendes zur Rolle von Identity Service in der Experience Platform-Infrastruktur

Identity Service spielt eine wichtige Rolle in Experience Platform. Zu diesen wichtigen Integrationen gehören die folgenden:

* [Schemata](../xdm/home.md): Innerhalb eines bestimmten Schemas ermöglichen die als Identität markierten Schemafelder die Erstellung von Identitätsdiagrammen.
* [Datensätze](../catalog/datasets/overview.md): Wenn ein Datensatz für die Aufnahme in das Echtzeit-Kundenprofil aktiviert ist, werden Identitätsdiagramme aus dem Datensatz generiert, da der Datensatz mindestens zwei als Identität markierte Felder enthält.
* [Web SDK](../web-sdk/home.md): Web SDK sendet Erlebnisereignisse an Adobe Experience Platform, und Identity Service generiert ein Diagramm, wenn zwei oder mehr Identitäten im Ereignis vorhanden sind.
* [Echtzeit-Kundenprofil](../profile/home.md): Bevor Attribute und Ereignisse für ein bestimmtes Profil zusammengeführt werden, kann das Echtzeit-Kundenprofil auf das Identitätsdiagramm verweisen. Weitere Informationen finden Sie im Handbuch unter [Grundlagen der Beziehung zwischen Identity Service und Echtzeit-Kundenprofil](./identity-and-profile.md).
* [Ziele](../destinations/home.md): Ziele können Profilinformationen basierend auf einem Identity-Namespace an andere Systeme senden, z. B. an Hash-E-Mails.
* [Segmentübereinstimmung](../segmentation/ui/segment-match/overview.md): Die Segmentübereinstimmung stimmt mit zwei Profilen in zwei verschiedenen Sandboxes überein, die denselben Identity-Namespace und denselben Identitätswert haben.
* [Privacy Service](../privacy-service/home.md): Wenn die Löschanfrage `identity` enthält, kann die angegebene Namespace- und Identitätswertkombination mithilfe der Datenschutzanfrageverarbeitungsfunktion in Privacy Service aus Identity Service gelöscht werden.

