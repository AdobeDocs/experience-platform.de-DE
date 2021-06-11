---
keywords: Experience Platform;Home;beliebte Themen;Identität;Identität;XDM-Diagramme;Identity Service;Identity Service
solution: Experience Platform
title: Identity Service – Übersicht
topic-legacy: overview
description: Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihren Kunden und sein Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle persönliche digitale Erlebnisse sorgen.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 288f24351788ed4b8a0c68cffe5eb5c91ed01691
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 99%

---

# [!DNL Identity Service]Übersicht

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint. Der Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, sich einen besseren Überblick über Ihren Kunden und sein Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle persönliche digitale Erlebnisse sorgen.

## Grundlagen zu [!DNL Identity Service]

Jeden Tag interagieren Kunden mit Ihrem Unternehmen und gehen eine kontinuierlich wachsende Beziehung zu Ihrer Marke ein. Ein typischer Kunde kann in der Dateninfrastruktur Ihres Unternehmens in einer beliebigen Anzahl von Systemen aktiv sein, z. B. in Ihren E-Commerce-, Treueprogramm- und Helpdesk-Systemen. Derselbe Kunde kann auch anonym über verschiedene Geräte interagieren. [!DNL Identity Service] Mit können Sie sich einen Überblick über Ihren Kunden verschaffen und mit ihm verbundene Daten zusammenfassen, die andernfalls auf Silos in verschiedenen Systemen verteilt wären.

Betrachten wir ein alltägliches Beispiel für die Beziehung eines Verbrauchers zu Ihrer Marke:

Maria hat auf Ihrer E-Commerce-Site ein Konto, über das sie bereits mehrere Bestellungen getätigt hat. Normalerweise verwendet sie ihren privaten Laptop zum Einkaufen und meldet sich jedes Mal an. Bei einem Besuch nutzt sie jedoch ihr Tablet, um Sandalen zu bestellen, gibt aber keine Bestellung auf und meldet sich auch nicht an.

An diesem Punkt erscheinen Marias Aktivitäten als zwei separate Profile: ihre E-Commerce-Anmeldung und ihr Tablet-Gerät, möglicherweise identifiziert per Gerätekennung.

Maria setzt ihre Tablet-Sitzung später fort und gibt beim Abonnieren Ihres Newsletters ihre E-Mail-Adresse an. Im Anschluss daran fügt Streaming-Erfassung als Datensatzdaten in ihrem Profil eine neue Identität hinzu. Infolgedessen verknüpft der [!DNL Identity Service] Marias Aktivitäten auf ihrem Tablet nun mit dem Verlauf ihres E-Commerce-Kontos.

Bis zum nächsten Klick auf das Tablet könnten Ihre Zielinhalte Marias gesamtes Profil inklusive Verlauf widerspiegeln, statt nur das Tablet eines unbekannten Kunden.

Die Identitätsbeziehungen, die [!DNL Identity Service] definiert und pflegt, werden vom [!DNL Real-time Customer Profile] genutzt, um das vollständige Bild eines Kunden und seiner Interaktionen mit Ihrer Marke zu erstellen. Weiterführende Informationen finden Sie in der [Übersicht zu Echtzeit-Kundenprofil](../profile/home.md).

### Identitäten

Eine Identität besteht aus Daten, die für eine Entität (normalerweise eine Person) eindeutig sind. Eine Identität wie z. B. eine Anmeldekennung, eine ECID oder eine Treueprogramm-ID wird als bekannte Identität bezeichnet.

Personenbezogene Daten (PII) wie E-Mail-Adresse und Telefonnummer dienen zur direkten Identifizierung eines Kunden. Infolgedessen werden personenbezogene Daten dazu verwendet, um verschiedene Identitäten eines Kunden systemübergreifend abzugleichen.

Unbekannte oder anonyme Identitäten identifizieren ein Gerät, ohne dass die Person identifiziert wird, die dieses Gerät nutzt. Diese Kategorie enthält Daten wie die IP-Adresse und Cookie-ID des Besuchers. Während Verhaltensdaten von einem Gerät mithilfe unbekannter Identitäten gesammelt werden können, ist eine Zuordnung dieser Identitäten über verschiedene Geräte oder Medien hinweg begrenzt, bis Ihr Kunde während der Journey personenbezogene Daten angibt.

Bekannte und anonyme Identitäten sind (wie in der folgenden Abbildung gezeigt) wichtige Komponenten von [Identitätsdiagrammen](#identity-graphs) und werden später in diesem Dokument genauer besprochen.

![Identitätszusammenfügung in Platform](./images/identity-service-stitching.png)

Zu den Beispielen für Implementierungen von [!DNL Identity Service] gehören:

- Ein Telekommunikationsunternehmen verlässt sich möglicherweise auf den Wert „Telefonnummer“, wobei eine Telefonnummer sowohl in Offline- als auch Online-Datensätzen auf dieselbe Person verweist.
- Ein Einzelhandelsunternehmen kann aufgrund des hohen Prozentsatzes an anonymen Besuchern in Offline-Datensätzen die „E-Mail-Adresse“ und in Online-Datensätzen die „ECID“ verwenden.
- Eine Bank könnte in Offline-Datensätzen, wie z. B. Transaktionen in Zweigstellen, die „Kontonummer“ bevorzugen. Bei Online-Datensätzen könnte sie hingegen die „Anmeldekennung“ nutzen, da die meisten Besucher während ihres Besuchs authentifiziert werden.
- Möglicherweise verfügen Ihre Kunden auch über eindeutige proprietäre Kennungen, wie die GUID oder andere Universally Unique Identifiers.

### Identitätsdaten

Wenn Sie eine Person ohne weiteren Kontext fragen würden, wie ihre Identität lautet, würde es ihr wahrscheinlich schwer fallen, eine sinnvolle Antwort zu geben. Nach der gleichen Logik ist ein Zeichenfolgenwert, der einen Identitätswert darstellt (unabhängig davon, ob es sich um eine vom System erzeugte Kennung oder eine E-Mail-Adresse handelt), nur dann vollständig, wenn ein Qualifizierer mit dem Kontext des Zeichenfolgenwerts angegeben wird: der Identitäts-Namespace.

## Identitäts-Namespaces und Identitätsdiagramme

Ihre Kunden können mit Ihrer Marke über eine Kombination aus Online- und Offline-Kanälen interagieren. Das bringt die Herausforderung mit sich, diese fragmentierten Interaktionen in einer zentralen Kundenidentität abzustimmen.

[!DNL Experience Platform] löst diese Herausforderung mit zwei Konzepten: mit [Identitäts-Namespaces](#identity-namespaces) und [Identitätsdiagrammen](#identity-graphs).

Das folgende Video soll Ihnen das Verständnis von Identitäten und Identitätsdiagrammen erleichtern. Im folgenden Video werden die drei Möglichkeiten der Identitätssammlung, der Identitätsdiagramme und der APIs behandelt. Es beschreibt auch, wie deterministische und probabilistische Algorithmen zum Erstellen von Diagrammen für die private Identität verwendet werden, und erörtert die Rolle von Diagrammen für die private Identität, die Adobe Experience Platform Identity Service Co-Op-Diagramme und die Diagramme von Drittanbietern.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Identitäts-Namespaces

Wenn Ihr Kunde über verschiedene Kanäle mit Ihrer Marke interagiert (einschließlich Web, App, Callcenter oder Geschäft), wird es schwierig, sie zu verstehen und zu bedienen, wenn Sie ihre Aktivitäten nicht kanalübergreifend beobachten und verfolgen können.

Kunden über verschiedene Geräte und Kanäle hinweg zu verstehen, beginnt damit, dass Sie sie in jedem Kanal erkennen. Adobe Experience Platform erlaubt das mithilfe von Identitäts-Namespaces.
Ein Identitäts-Namespace ist eine Kennung (wie z. B. eine Geräte-ID oder E-Mail-ID), mit der der Kontext, aus dem Daten stammen, angegeben wird. Identitäts-Namespaces dienen zum Nachschlagen oder Verknüpfen einzelner Identitäten sowie zum Bereitstellen von Kontext für Identitätswerte, um Datenkollisionen zu verhindern. Beispielsweise kann sich die Kennung „123456“ auf eine Person in Ihrem E-Commerce-System sowie auf eine andere Person in Ihrem Helpdesk-System beziehen. Weiterführende Informationen finden Sie in der [Übersicht zu Identitäts-Namespaces](./namespaces.md).

### Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, die visuell veranschaulicht, wie Ihr Kunde über unterschiedliche Kanäle hinweg mit Ihrer Marke interagiert.

Alle Diagramme zur Kundenidentität werden von [!DNL Identity Service] als Reaktion auf Kundenaktivität gemeinsam nahezu in Echtzeit verwaltet und aktualisiert.

[!DNL Identity Service] verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). [!DNL Identity Service] erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

Als Beispiel für die möglichen Arten von Faktoren, die bei der Bereitstellung und Kennzeichnung von Identitätsdaten zu berücksichtigen sind, kann die Verwendung von Telefonnummern wie „Geschäftlich“ zu mehr Beziehungen führen, als Sie im Identitätsdiagramm haben möchten. Viele Mitarbeiter beziehen sich auf die gleiche geschäftliche Nummer, sodass „Privat“ und „Mobil“ besser dazu geeignet sind, Beziehungen so präzise wie möglich zu halten.

Weitere Informationen finden Sie im Tutorial zum [Zugriff auf den Identitätsdiagramm-Viewer](./ui/identity-graph-viewer.md)

## Bereitstellen von Identitätsdaten für [!DNL Identity Service]

In diesem Abschnitt wird beschrieben, wie an Adobe Experience Platform bereitgestellte Daten verarbeitet werden, bevor sie von [!DNL Identity Service] zum Erstellen eines Identitätsdiagramms für einen einzelnen Kunden verwendet werden.

### Identitätsfelder bestimmen

Je nach der Strategie Ihres Unternehmens zur Datenerfassung bestimmen die Datenfelder, die Sie als Identitäten kennzeichnen, darüber, welche Daten in Ihre Identitätszuordnung aufgenommen werden. Um größtmöglichen Nutzen aus Adobe Experience Platform und den umfassendsten Kundenidentitäten zu ziehen, sollten Sie sowohl Online- als auch Offline-Daten hochladen.

- Online-Daten sind Daten, die die Präsenz und das Verhalten im Internet beschreiben, z. B. Benutzernamen und E-Mail-Adressen.

- Offline-Daten beziehen sich auf Daten, die nicht direkt mit einer Online-Präsenz zusammenhängen, wie z. B. Kennungen aus CRM-Systemen. Solche Daten macht Ihre Identitäten robuster und fördern die Kohärenz von Daten in verschiedenen Systemen.

### Zusätzliche Identitäts-Namespaces erstellen

Zwar bietet [!DNL Experience Platform] eine Vielzahl von standardmäßigen Namespaces, doch müssen Sie möglicherweise zusätzliche Namespaces erstellen, um Ihre Identitäten korrekt zu kategorisieren. Weiterführende Informationen finden Sie im Abschnitt zum [Anzeigen und Erstellen von Namespaces für Ihre Organisation](./namespaces.md) in der Übersicht zu Identitäts-Namespaces.

>[!NOTE]
>
>Identitäts-Namespaces sind ein Qualifizierer für Identitäten. Nachdem ein Namespace erstellt wurde, kann er daher nicht mehr gelöscht werden.

### Identitätsdaten in [!DNL Experience Data Model] (XDM) einschließen

Als standardisiertes Framework, mit dem [!DNL Platform] Kundendaten organisiert, ermöglicht [!DNL Experience Data Model] (XDM) das Teilen und Verstehen von Daten über [!DNL Experience Platform] und andere Services hinweg, die mit [!DNL Platform] interagieren. Weiterführende Informationen finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

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

[!DNL Identity Service] nutzt XDM-konforme Daten, die entweder per [Batch-Aufnahme](../ingestion/batch-ingestion/overview.md) oder per [Streaming-Aufnahme](../ingestion/streaming-ingestion/overview.md) an [!DNL Experience Platform] gesendet werden.

Das folgende Video soll Ihnen das Verständnis für Identity Service erleichtern. In diesem Video erfahren Sie, wie Sie Datenfelder als Identitäten kennzeichnen, Identitätsdaten aufnehmen und dann überprüfen, ob die Daten in das private Diagramm von Adobe Experience Platform Identity Service gelangt sind.

>[!WARNING]
>
>Die im folgenden Video angezeigte [!DNL Platform]-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Data Governance

Adobe Experience Platform wurde mit Blick auf Datenschutz entwickelt und umfasst ein Data-Governance-Framework, um personenbezogene Daten Ihrer Kunden zu schützen. Identitätsdaten unter den Namespaces „E-Mail-Adresse“ oder „Telefonnummer“ werden standardmäßig verschlüsselt. Um aber sicherzustellen, dass sensible Daten vor dem Speichern verschlüsselt werden, können Datennutzungskennzeichnungen auf Daten angewendet werden, während diese aufgenommen werden oder wenn sie in [!DNL Platform] eintreffen. Weiterführende Informationen finden Sie in der [Übersicht zu Data Governance](../data-governance/home.md).

## Nächste Schritte

Sie kennen nun die Schlüsselkonzepte von [!DNL Identity Service] und dessen Rolle in [!DNL Experience Platform] und können als Nächstes erfahren, wie Sie Ihr Identitätsdiagramm mithilfe der [[!DNL Identity Service API]](./api/getting-started.md) verwenden.
