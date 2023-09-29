---
keywords: Experience Platform;Startseite;beliebte Themen;Identität;Identität;XDM-Diagramme;Identity Service;Identity Service
solution: Experience Platform
title: Identity Service – Übersicht
description: Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihren Kunden und sein Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle persönliche digitale Erlebnisse sorgen.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 100%

---

# [!DNL Identity Service] – Übersicht

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihrer Kundinnen und Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

Mit [!DNL Identity Service] können Sie:

- Sicherstellen, dass Ihre Kunden durch jede Interaktion ein konsistentes, personalisiertes und relevantes Erlebnis erhalten.
- Mehrere Identitäten aus unterschiedlichen Quellen verbinden und eine umfassende Ansicht Ihrer Kunden erstellen.
- Ein Identitätsdiagramm verwenden, um verschiedene Identitäts-Namespaces zuzuordnen, wodurch Sie eine visuelle Darstellung der Interaktion Ihrer Kunden mit Ihrer Marke über verschiedene Kanäle hinweg erhalten.

## Erste Schritte

Bevor wir in die Details von [!DNL Identity Service] eintauchen, hier eine kurze Zusammenfassung der Schlüsselbegriffe:

| Begriff | Definition |
| --- | --- |
| Identität | Eine Identität besteht aus Daten, die für eine Entität (normalerweise eine Person) eindeutig sind. Eine Identität wie z. B. eine Anmeldekennung, eine ECID oder eine Kundentreue-ID wird als „bekannte Identität“ bezeichnet. |
| ECID | Experience Cloud ID (ECID) ist ein geteilter Identity-Namespace, der in Programmen von Experience Platform und Adobe Experience Cloud verwendet wird. ECID bietet eine Grundlage für die Kundenidentität und wird als primäre ID für Geräte und als Basisknoten für Identitätsdiagramme verwendet. Weiterführende Informationen dazu finden Sie in der [ECID-Übersicht](./ecid.md). |
| Identity-Namespace | Ein Identity-Namespace dient zur Unterscheidung des Kontexts oder des Typs einer Identität. Beispielsweise unterscheidet eine Identität zwischen „name<span>@email.com“ als E-Mail-Adresse und „443522“ als numerischer CRM-ID. Identity-Namespaces werden verwendet, um einzelne Identitäten nachzuschlagen und den Kontext für Identitätswerte bereitzustellen. Auf diese Weise können Sie etwa feststellen, dass zwei [!DNL Profile]-Fragmente, die unterschiedliche primäre IDs enthalten, aber denselben Wert für den Identity-Namespace `email` aufweisen, tatsächlich dieselbe Person betreffen. Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identitäts-Namespaces](./namespaces.md). |
| Identitätsdiagramm | Ein Identitätsdiagramm ist eine Zusammenstellung von Beziehungen zwischen verschiedenen Identitäten, anhand derer Sie visualisieren und besser verstehen können, welche Kundenidentitäten zusammengeführt werden und wie. Weitere Informationen finden Sie im Tutorial zur [Verwendung des Identitätsdiagramm-Viewers](./ui/identity-graph-viewer.md). |
| Persönlich identifizierbare Informationen (PII) | PII sind Informationen, mit denen ein Kunde direkt identifiziert werden kann, z. B. eine E-Mail-Adresse oder eine Telefonnummer. PII-Werte werden häufig verwendet, um die verschiedenen Identitäten eines Kunden in verschiedenen Systemen abzugleichen. |
| Unbekannte oder anonyme Identitäten | Unbekannte oder anonyme Identitäten sind Indikatoren, die Geräte isolieren, ohne die tatsächliche Person zu identifizieren, die das Gerät verwendet. Unbekannte und anonyme Identitäten umfassen Informationen wie die IP-Adresse oder eine Cookie-ID eines Besuchers. Unbekannte und anonyme Identitäten können zwar Verhaltensdaten liefern, sind jedoch von begrenztem Nutzen, bis ein Kunde seine personenbezogenen Daten bereitstellt. |

## Was ist [!DNL Identity Service]?

Jeden Tag interagieren Kunden mit Ihrem Unternehmen und gehen eine kontinuierlich wachsende Beziehung zu Ihrer Marke ein. Ein typischer Kunde kann in der Dateninfrastruktur Ihres Unternehmens in einer beliebigen Anzahl von Systemen aktiv sein, z. B. in Ihren E-Commerce-, Treueprogramm- und Helpdesk-Systemen. Derselbe Kunde kann auch anonym über verschiedene Geräte interagieren. [!DNL Identity Service] Mit können Sie sich einen Überblick über Ihren Kunden verschaffen und mit ihm verbundene Daten zusammenfassen, die andernfalls auf Silos in verschiedenen Systemen verteilt wären.

Betrachten wir ein alltägliches Beispiel für die Beziehung eines Verbrauchers zu Ihrer Marke:

- Maria hat auf Ihrer E-Commerce-Website ein Konto, über das sie bereits mehrere Bestellungen getätigt hat. Normalerweise verwendet sie ihren privaten Laptop zum Einkaufen und meldet sich jedes Mal an. Bei einem Besuch nutzt sie jedoch ihr Tablet, um Sandalen zu bestellen, gibt aber keine Bestellung auf und meldet sich auch nicht an.
- An dieser Stelle erscheint Marias Aktivität in zwei separaten Profilen:
   - Ihre E-Commerce-Anmeldung
   - Ihr Tablet-Gerät, möglicherweise identifiziert durch seine Geräte-ID
- Maria setzt ihre Tablet-Sitzung später fort und gibt beim Abonnieren Ihres Newsletters ihre E-Mail-Adresse an. Im Anschluss daran fügt Streaming-Erfassung als Datensatzdaten in ihrem Profil eine neue Identität hinzu. Infolgedessen verknüpft [!DNL Identity Service] Marias Aktivitäten auf ihrem Tablet nun mit dem Verlauf ihres E-Commerce-Kontos.
- Bis zum nächsten Klick auf das Tablet könnten Ihre Zielinhalte Marias gesamtes Profil inklusive Verlauf widerspiegeln, statt nur das Tablet eines unbekannten Kunden.

![Identitätszusammenfügung in Platform](./images/identity-service-stitching.png)

Im Wesentlichen können Sie sich mit [!DNL Identity Service] ein vollständiges Bild von Ihrem Kunden machen, indem zusammengehörige Daten zusammengefasst werden, die andernfalls über verschiedene Systeme verstreut sein könnten. Die Identitätsbeziehungen, die [!DNL Identity Service] definiert und pflegt, werden vom Echtzeit-Kundenprofil genutzt, um das vollständige Bild einer Kundin oder eines Kunden und deren Interaktionen mit Ihrer Marke zu erstellen. Weiterführende Informationen finden Sie in der [Übersicht zum Echtzeit-Kundenprofil](../profile/home.md).

### Anwendungsfälle

Zu den Beispielen für Implementierungen von [!DNL Identity Service] gehören:

- Ein Telekommunikationsunternehmen verlässt sich möglicherweise auf den Wert „Telefonnummer“, wobei eine Telefonnummer sowohl in Offline- als auch Online-Datensätzen auf dieselbe Person verweist.
- Ein Einzelhandelsunternehmen kann aufgrund des hohen Prozentsatzes an anonymen Besuchern in Offline-Datensätzen die „E-Mail-Adresse“ und in Online-Datensätzen die „ECID“ verwenden.
- Eine Bank könnte in Offline-Datensätzen, wie z. B. Transaktionen in Zweigstellen, die „Kontonummer“ bevorzugen. Bei Online-Datensätzen könnte sie hingegen die „Anmeldekennung“ nutzen, da die meisten Besucher während ihres Besuchs authentifiziert werden.
- Möglicherweise verfügen Ihre Kunden auch über eindeutige proprietäre Kennungen, wie die GUID oder andere Universally Unique Identifiers.

## Identity-Namespace {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Identity-Namespaces"
>abstract="Ein Identity-Namespace dient zur Unterscheidung des Kontexts oder des Typs einer Identität. Beispielsweise unterscheidet eine Identität zwischen „name<span>@email.com“ als E-Mail-Adresse und „443522“ als numerischer CRM-ID."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Identitätswerte"
>abstract="Ein Identitätswert ist eine Kennung, die für eine eindeutige Person, eine eindeutige Organisation oder ein eindeutiges Asset steht. Der Kontext oder der Typ der Identität, den der Wert darstellt, wird durch einen entsprechenden Identity-Namespace definiert. Bei der Zuordnung von Datensatzdaten zu Profilfragmenten müssen Namespace und Identitätswert übereinstimmen. Bei der Zuordnung von Datensatzdaten zu Profilfragmenten müssen Namespace und Identitätswert übereinstimmen."
>text="Learn more in documentation"

Wenn Sie eine Person ohne weiteren Kontext fragen würden, wie ihre Identität lautet, würde es ihr wahrscheinlich schwer fallen, eine sinnvolle Antwort zu geben. Nach der gleichen Logik ist ein Zeichenfolgenwert, der einen Identitätswert darstellt (unabhängig davon, ob es sich um eine vom System erzeugte Kennung oder eine E-Mail-Adresse handelt), nur dann vollständig, wenn ein Qualifizierer mit dem Kontext des Zeichenfolgenwerts angegeben wird: der Identitäts-Namespace.

Es ist möglich, dass Ihre Kunden mit Ihrer Marke über eine Kombination von Online- und Offline-Kanälen interagieren, was die Herausforderung mit sich bringt, diese fragmentierten Interaktionen zu einer einzigen Kundenidentität zusammenzuführen.

Kunden über verschiedene Geräte und Kanäle hinweg zu verstehen, beginnt damit, dass Sie sie in jedem Kanal erkennen. Platform erlaubt das mithilfe von Identity-Namespaces. Ein Identity-Namespace ist eine Kennung wie eine E-Mail-Adresse oder Telefonnummer, die verwendet wird, um zusätzlichen Kontext für Kundenidentitäten bereitzustellen. Identity-Namespaces dienen zum Nachschlagen oder Verknüpfen einzelner Identitäten sowie zum Bereitstellen von Kontext für Identitätswerte. Weiterführende Informationen dazu finden Sie unter [Übersicht zu Identitäts-Namespaces](./namespaces.md).

## Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identity-Namespaces, anhand derer Sie visualisieren und besser verstehen können, welche Kundenidentitäten zusammengeführt werden und wie. Weitere Informationen finden Sie im Tutorial zur [Verwendung des Identitätsdiagramm-Viewers](./ui/identity-graph-viewer.md).

Das folgende Video soll Ihnen Identitäten und Identitätsdiagramme näherbringen.

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

Als standardisiertes Framework, mit dem [!DNL Platform] Kundendaten organisiert, ermöglicht [!DNL Experience Data Model] (XDM) das Teilen und Verstehen von Daten über Experience Platform und andere Services hinweg, die mit [!DNL Platform] interagieren. Weiterführende Informationen finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

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

Während der Streaming-Aufnahme extrahiert [!DNL Identity Service]automatisch Identitätsdaten aus Datensatz- und Zeitreihendaten. Bevor Daten aufgenommen werden können, müssen sie jedoch für [!DNL Identity Service] aktiviert werden. Weiterführende Informationen finden Sie im Tutorial zum [Konfigurieren eines Datensatzes für das Echtzeit-Kundenprofil und Identity Service mit APIs](../profile/tutorials/dataset-configuration.md).

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

Sie kennen nun die Schlüsselkonzepte von [!DNL Identity Service] und dessen Rolle in Experience Platform und können als Nächstes erfahren, wie Sie Ihr Identitätsdiagramm mithilfe der [[!DNL Identity Service API]](./api/getting-started.md) verwenden.
