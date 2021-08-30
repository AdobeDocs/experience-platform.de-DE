---
keywords: Experience Platform;Home;beliebte Themen;Identität;Identität;XDM-Diagramme;Identity Service;Identity Service
solution: Experience Platform
title: Identity Service – Übersicht
topic-legacy: overview
description: Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihren Kunden und sein Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle persönliche digitale Erlebnisse sorgen.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 947d8803416cee584b35a8d480929e2684d0057f
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 57%

---

# [!DNL Identity Service]Übersicht

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird schwieriger, wenn Ihre Kundendaten über verschiedene Systeme verteilt sind, wodurch jeder einzelne Kunde über mehrere &quot;Identitäten&quot;verfügt.

Adobe Experience Platform Identity Service bietet Ihnen einen umfassenden Überblick über Ihre Kunden und ihr Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit für effektive, persönliche digitale Erlebnisse sorgen können.

Mit [!DNL Identity Service] können Sie:

- Stellen Sie sicher, dass Ihre Kunden durch jede Interaktion ein konsistentes, personalisiertes und relevantes Erlebnis erhalten.
- Verbinden Sie mehrere Identitäten aus unterschiedlichen Quellen und erstellen Sie eine umfassende Ansicht Ihrer Kunden.
- Verwenden Sie ein Identitätsdiagramm, um verschiedene Identitäts-Namespaces zuzuordnen. So erhalten Sie eine visuelle Darstellung der Interaktion Ihrer Kunden mit Ihrer Marke über verschiedene Kanäle hinweg.

## Erste Schritte

Bevor wir in die Details von [!DNL Identity Service] eintauchen, hier eine kurze Zusammenfassung der Schlüsselbegriffe:

| Begriff | Definition |
| --- | --- |
| Identität | Eine Identität besteht aus Daten, die für eine Entität (normalerweise eine Person) eindeutig sind. Eine Identität, z. B. eine Anmelde-ID, eine ECID oder eine Treueprogramm-ID, wird auch als &quot;bekannte Identität&quot;bezeichnet. |
| ECID | Experience Cloud ID (ECID) ist ein freigegebener Identitäts-Namespace, der in Experience Platform- und Adobe Experience Cloud-Anwendungen verwendet wird. ECID bietet eine Grundlage für die Kundenidentität und wird als primäre ID für Geräte und als Basisknoten für Identitätsdiagramme verwendet. Weitere Informationen finden Sie in der [ECID-Übersicht](./ecid.md) . |
| Identitäts-Namespace | Ein Identitäts-Namespace dient zur Unterscheidung des Kontexts oder des Typs einer Identität. Beispielsweise unterscheidet eine Identität &quot;name<span>@email.com&quot;als E-Mail-Adresse oder &quot;443522&quot;als numerische CRM-ID. Identitäts-Namespaces werden verwendet, um einzelne Identitäten nachzuschlagen und den Kontext für Identitätswerte bereitzustellen. Auf diese Weise können Sie feststellen, dass zwei [!DNL Profile]-Fragmente, die unterschiedliche primäre IDs enthalten, aber denselben Wert für den Identitäts-Namespace `email` aufweisen, tatsächlich dieselbe Person sind. Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identitäts-Namespaces](./namespaces.md). |
| Identitätsdiagramm | Ein Identitätsdiagramm ist eine Zusammenstellung von Beziehungen zwischen verschiedenen Identitäten, anhand derer Sie visualisieren und besser verstehen können, welche Kundenidentitäten zusammengeführt werden und wie. Weitere Informationen finden Sie im Tutorial zu [Verwendung des Identitätsdiagramm-Viewers](./ui/identity-graph-viewer.md) . |
| Persönlich identifizierbare Informationen (PII) | PII sind Informationen, mit denen ein Kunde direkt identifiziert werden kann, z. B. eine E-Mail-Adresse oder eine Telefonnummer. PII-Werte werden häufig zur Übereinstimmung verwendet. die verschiedenen Identitäten eines Kunden in verschiedenen Systemen. |
| Eindeutige Identität | Eine eindeutige Identität ist eine Identität, die nur in einer bestimmten Sandbox vorhanden ist. |
| Unbekannte oder anonyme Identitäten | Unbekannte oder anonyme Identitäten sind Indikatoren, die Geräte isolieren, ohne die tatsächliche Person zu identifizieren, die das Gerät verwendet. Unbekannte und anonyme Identitäten umfassen Informationen wie die IP-Adresse und Cookie-ID eines Besuchers. Unbekannte und anonyme Identitäten können zwar Verhaltensdaten bereitstellen, sind jedoch begrenzt, bis ein Kunde seine personenbezogenen Daten bereitstellt. |

## Was ist [!DNL Identity Service]?

Jeden Tag interagieren Kunden mit Ihrem Unternehmen und gehen eine kontinuierlich wachsende Beziehung zu Ihrer Marke ein. Ein typischer Kunde kann in einer beliebigen Anzahl von Systemen in der Dateninfrastruktur Ihres Unternehmens tätig sein, z. B. in Ihren E-Commerce-, Treueprogramm- und Helpdesk-Systemen. Derselbe Kunde kann auch anonym über verschiedene Geräte interagieren. [!DNL Identity Service] Mit können Sie sich einen Überblick über Ihren Kunden verschaffen und mit ihm verbundene Daten zusammenfassen, die andernfalls auf Silos in verschiedenen Systemen verteilt wären.

Betrachten wir ein alltägliches Beispiel für die Beziehung eines Verbrauchers zu Ihrer Marke:

- Maria hat auf Ihrer E-Commerce-Site ein Konto, auf dem sie bereits einige Bestellungen getätigt hat. Normalerweise verwendet sie ihren privaten Laptop zum Einkaufen und meldet sich jedes Mal an. Bei einem Besuch nutzt sie jedoch ihr Tablet, um Sandalen zu bestellen, gibt aber keine Bestellung auf und meldet sich auch nicht an.
- An dieser Stelle erscheint Marias Aktivität in zwei separaten Profilen:
   - Ihre E-Commerce-Anmeldung
   - Ihr Tablet-Gerät, möglicherweise identifiziert durch Geräte-ID
- Maria setzt ihre Tablet-Sitzung später fort und gibt beim Abonnieren Ihres Newsletters ihre E-Mail-Adresse an. Im Anschluss daran fügt Streaming-Erfassung als Datensatzdaten in ihrem Profil eine neue Identität hinzu. Daher verknüpft [!DNL Identity Service] nun Marias Aktivität auf Tablet-Geräten mit ihrem E-Commerce-Kontoverlauf.
- Beim nächsten Klick auf ihr Tablet könnten Ihre zielgerichteten Inhalte Marias gesamtes Profil und seinen Verlauf widerspiegeln, anstatt nur ein Tablet, das von einem unbekannten Käufer verwendet wird.

![Identitätszusammenfügung in Platform](./images/identity-service-stitching.png)

[!DNL Identity Service] ermöglicht es Ihnen im Wesentlichen, ein vollständiges Bild Ihres Kunden zusammenzustellen und damit verbundene Daten zu aggregieren, die andernfalls auf verschiedene Systeme verteilt wären. Die Identitätsbeziehungen, die [!DNL Identity Service] definiert und pflegt, werden vom Echtzeit-Kundenprofil genutzt, um ein vollständiges Bild eines Kunden und seiner Interaktionen mit Ihrer Marke zu erstellen. Weiterführende Informationen finden Sie in der [Übersicht zu Echtzeit-Kundenprofil](../profile/home.md).

### Anwendungsfälle

Zu den Beispielen für Implementierungen von [!DNL Identity Service] gehören:

- Ein Telekommunikationsunternehmen verlässt sich möglicherweise auf den Wert „Telefonnummer“, wobei eine Telefonnummer sowohl in Offline- als auch Online-Datensätzen auf dieselbe Person verweist.
- Ein Einzelhandelsunternehmen kann aufgrund des hohen Prozentsatzes an anonymen Besuchern in Offline-Datensätzen die „E-Mail-Adresse“ und in Online-Datensätzen die „ECID“ verwenden.
- Eine Bank könnte in Offline-Datensätzen, wie z. B. Transaktionen in Zweigstellen, die „Kontonummer“ bevorzugen. Bei Online-Datensätzen könnte sie hingegen die „Anmeldekennung“ nutzen, da die meisten Besucher während ihres Besuchs authentifiziert werden.
- Möglicherweise verfügen Ihre Kunden auch über eindeutige proprietäre Kennungen, wie die GUID oder andere Universally Unique Identifiers.

## Identity-Namespaces

Wenn Sie eine Person ohne weiteren Kontext fragen würden, wie ihre Identität lautet, würde es ihr wahrscheinlich schwer fallen, eine sinnvolle Antwort zu geben. Nach der gleichen Logik ist ein Zeichenfolgenwert, der einen Identitätswert darstellt (unabhängig davon, ob es sich um eine vom System erzeugte Kennung oder eine E-Mail-Adresse handelt), nur dann vollständig, wenn ein Qualifizierer mit dem Kontext des Zeichenfolgenwerts angegeben wird: der Identitäts-Namespace.


Ihre Kunden können mit Ihrer Marke über eine Kombination aus Online- und Offline-Kanälen interagieren, was die Herausforderung darstellt, diese fragmentierten Interaktionen mit einer einzigen Kundenidentität abzustimmen.

Kunden über verschiedene Geräte und Kanäle hinweg zu verstehen, beginnt damit, dass Sie sie in jedem Kanal erkennen. Platform erreicht dies mithilfe von Identitäts-Namespaces. Ein Identitäts-Namespace ist eine Kennung wie E-Mail oder Telefon, die verwendet wird, um zusätzlichen Kontext für Kundenidentitäten bereitzustellen. Identitäts-Namespaces werden verwendet, um einzelne Identitäten zu suchen oder zu verknüpfen und Kontext für Identitätswerte bereitzustellen. Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identitäts-Namespaces](./namespaces.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, anhand derer Sie visualisieren und besser verstehen können, welche Kundenidentitäten zusammengeführt werden und wie. Weitere Informationen finden Sie im Tutorial zu [Verwendung des Identitätsdiagramm-Viewers](./ui/identity-graph-viewer.md) .

Das folgende Video soll Ihnen das Verständnis von Identitäten und Identitätsdiagrammen erleichtern. Es umfasst die drei Funktionen der Identitätskollektion, Identitätsdiagramme und der API. Außerdem wird beschrieben, wie deterministische und probabilistische Algorithmen zum Erstellen privater Identitätsdiagramme verwendet werden, und ihre Rolle zusammen mit Diagrammen von Drittanbietern und dem Co-op-Diagramm des Adobe Experience Platform Identity Service erläutert.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Bereitstellen von Identitätsdaten für [!DNL Identity Service]

In diesem Abschnitt wird beschrieben, wie an Adobe Experience Platform bereitgestellte Daten verarbeitet werden, bevor sie von [!DNL Identity Service] zum Erstellen eines Identitätsdiagramms für einen einzelnen Kunden verwendet werden.

### Identitätsfelder bestimmen

Je nach der Strategie Ihres Unternehmens zur Datenerfassung bestimmen die Datenfelder, die Sie als Identitäten kennzeichnen, darüber, welche Daten in Ihre Identitätszuordnung aufgenommen werden. Um größtmöglichen Nutzen aus Adobe Experience Platform und den umfassendsten Kundenidentitäten zu ziehen, sollten Sie sowohl Online- als auch Offline-Daten hochladen.

- Online-Daten sind Daten, die die Präsenz und das Verhalten im Internet beschreiben, z. B. Benutzernamen und E-Mail-Adressen.

- Offline-Daten beziehen sich auf Daten, die nicht direkt mit einer Online-Präsenz zusammenhängen, wie z. B. Kennungen aus CRM-Systemen. Solche Daten macht Ihre Identitäten robuster und fördern die Kohärenz von Daten in verschiedenen Systemen.

### Zusätzliche Identitäts-Namespaces erstellen

Zwar bietet Experience Platform eine Vielzahl von Standard-Namespaces, doch müssen Sie möglicherweise zusätzliche Namespaces erstellen, um Ihre Identitäten korrekt zu kategorisieren. Weiterführende Informationen finden Sie im Abschnitt zum [Anzeigen und Erstellen von Namespaces für Ihre Organisation](./namespaces.md) in der Übersicht zu Identitäts-Namespaces.

>[!NOTE]
>
>Identitäts-Namespaces sind ein Qualifizierer für Identitäten. Nachdem ein Namespace erstellt wurde, kann er daher nicht mehr gelöscht werden.

### Identitätsdaten in [!DNL Experience Data Model] (XDM) einschließen

Als standardisiertes Framework, mit dem [!DNL Platform] Kundendaten organisiert, ermöglicht [!DNL Experience Data Model] (XDM) das Freigeben und Verstehen von Daten über Experience Platform und andere Dienste hinweg, die mit [!DNL Platform] interagieren. Weiterführende Informationen finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

Sowohl Datensatz- als auch Zeitreihenschemas bieten die Möglichkeit, Identitätsdaten einzubeziehen. Beim Erfassen von Daten erstellt das Identitätsdiagramm neue Beziehungen zwischen Datenfragmenten aus verschiedenen Namespaces, wenn festgestellt wird, dass sie gemeinsame Identitätsdaten aufweisen.

### Markieren von XDM-Feldern als Identität

Jedes Feld vom Typ `string` in Schemas, die XDM-Klassen für Datensätze oder Zeitreihen implementieren, kann als Identitätsfeld gekennzeichnet werden. In der Folge würden alle in diesem Feld erfassten Daten als Identitätsdaten betrachtet.

>[!NOTE]
>
>Felder vom Typ Array und Zuordnung werden nicht unterstützt und können nicht als Identitätsfelder markiert und gekennzeichnet werden.

Identitätsfelder erlauben auch eine Verknüpfung von Identitäten, wenn diese gemeinsame personenbezogene Daten aufweisen.
Wenn Sie beispielsweise Telefonnummernfelder als Identitätsfelder kennzeichnen, stellt [!DNL Identity Service] die Beziehungen zu den anderen Personen, bei denen dieselbe Telefonnummer ermittelt wurde, automatisch grafisch dar.

>[!NOTE]
>
>Der Namespace der resultierenden Identitäten wird zum Zeitpunkt der Kennzeichnung des Felds bereitgestellt.

### Datensatz für [!DNL Identity Service] konfigurieren

Während der Streaming-Aufnahme extrahiert [!DNL Identity Service ]automatisch Identitätsdaten aus Datensatz- und Zeitreihendaten. Bevor Daten aufgenommen werden können, müssen sie jedoch für [!DNL Identity Service] aktiviert werden. Weiterführende Informationen finden Sie in der Anleitung zum [Konfigurieren eines Datensatzes für Echtzeit-Kundenprofil und Identity Service mit APIs](../profile/tutorials/dataset-configuration.md).

### Daten in [!DNL Identity Service] aufnehmen

[!DNL Identity Service] nutzt XDM-konforme Daten, die entweder per [Batch-Erfassung](../ingestion/batch-ingestion/overview.md) oder [Streaming-Erfassung](../ingestion/streaming-ingestion/overview.md) an Experience Platform gesendet werden.

Das folgende Video soll Ihnen das Verständnis für Identity Service erleichtern. In diesem Video erfahren Sie, wie Sie Datenfelder als Identitäten kennzeichnen, Identitätsdaten aufnehmen und dann überprüfen, ob die Daten in das private Diagramm von Adobe Experience Platform Identity Service gelangt sind.

>[!WARNING]
>
>Die im folgenden Video angezeigte [!DNL Platform]-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Data Governance

Adobe Experience Platform wurde mit Blick auf Datenschutz entwickelt und umfasst ein Data-Governance-Framework, um personenbezogene Daten Ihrer Kunden zu schützen. Identitätsdaten unter den Namespaces „E-Mail-Adresse“ oder „Telefonnummer“ werden standardmäßig verschlüsselt. Um aber sicherzustellen, dass sensible Daten vor dem Speichern verschlüsselt werden, können Datennutzungskennzeichnungen auf Daten angewendet werden, während diese aufgenommen werden oder wenn sie in [!DNL Platform] eintreffen. Weiterführende Informationen finden Sie in der [Übersicht zu Data Governance](../data-governance/home.md).

## Nächste Schritte

Nachdem Sie nun die Schlüsselkonzepte von [!DNL Identity Service] und deren Rolle in der Experience Platform kennen, können Sie mit der Arbeit mit Ihrem Identitätsdiagramm mit [[!DNL Identity Service API]](./api/getting-started.md) beginnen.
