---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: d02f12202e51b00453f719604052a54f6fcfe4ab
workflow-type: tm+mt
source-wordcount: '1672'
ht-degree: 73%

---


# [!DNL Identity Service]Übersicht

Die Bereitstellung relevanter digitaler Erlebnisse setzt ein umfassendes Verständnis Ihres Kunden voraus. Das ist schwierig, wenn Ihre Kundendaten auf verschiedene Systeme verteilt sind, sodass jeder Kunde unterschiedliche „Identitäten“ zu haben scheint. Adobe Experience Platform [!DNL Identity Service] helps you to gain a better view of your customer and their behavior by bridging identities across devices and systems, allowing you to deliver impactful, personal digital experiences in real-time.

## Erläuterungen [!DNL Identity Service]

Jeden Tag interagieren Kunden mit Ihrem Unternehmen und gehen eine kontinuierlich wachsende Beziehung zu Ihrer Marke ein. Ein typischer Kunde kann in der Dateninfrastruktur Ihres Unternehmens in einer beliebigen Anzahl von Systemen aktiv sein, z. B. in Ihren E-Commerce-, Treueprogramm- und Helpdesk-Systemen. Derselbe Kunde kann auch anonym über verschiedene Geräte interagieren. [!DNL Identity Service]Mit können Sie sich einen Überblick über Ihren Kunden verschaffen und mit ihm verbundene Daten zusammenfassen, die andernfalls auf Silos in verschiedenen Systemen verteilt wären.

Betrachten wir ein alltägliches Beispiel für die Beziehung eines Verbrauchers zu Ihrer Marke:

Maria hat auf Ihrer E-Commerce-Site ein Konto, über das sie bereits mehrere Bestellungen getätigt hat. Normalerweise verwendet sie ihren privaten Laptop zum Einkaufen und meldet sich jedes Mal an. Bei einem Besuch nutzt sie jedoch ihr Tablet, um Sandalen zu bestellen, gibt aber keine Bestellung auf und meldet sich auch nicht an.

An diesem Punkt erscheinen Marias Aktivitäten als zwei separate Profile: ihre E-Commerce-Anmeldung und ihr Tablet-Gerät, möglicherweise identifiziert per Gerätekennung.

Maria setzt ihre Tablet-Sitzung später fort und gibt beim Abonnieren Ihres Newsletters ihre E-Mail-Adresse an. Im Anschluss daran fügt Streaming-Erfassung als Datensatzdaten in ihrem Profil eine neue Identität hinzu. As a result, [!DNL Identity Service] now relates Mary&#39;s tablet device activity with her eCommerce account history.

Bis zum nächsten Klick auf das Tablet könnten Ihre Zielinhalte Marias gesamtes Profil inklusive Verlauf widerspiegeln, statt nur das Tablet eines unbekannten Kunden.

The identity relationships that [!DNL Identity Service] defines and maintains are leveraged by [!DNL Real-time Customer Profile] to build a complete picture of a customer and their interactions with your brand. Weiterführende Informationen finden Sie in der [Übersicht zu Echtzeit-Kundenprofil](../profile/home.md).

### Identitäten

Eine Identität besteht aus Daten, die für eine Entität (normalerweise eine Person) eindeutig sind. Eine Identität wie z. B. eine Anmeldekennung, eine ECID oder eine Treueprogramm-ID wird als **bekannte Identität** bezeichnet.

Personenbezogene Daten (PII) wie E-Mail-Adresse und Telefonnummer dienen zur direkten Identifizierung eines Kunden. Infolgedessen werden personenbezogene Daten dazu verwendet, um verschiedene Identitäten eines Kunden systemübergreifend abzugleichen.

**Unbekannte oder anonyme Identitäten** identifizieren ein Gerät, ohne dass die Person identifiziert wird, die dieses Gerät nutzt. Diese Kategorie enthält Daten wie die IP-Adresse und Cookie-ID des Besuchers. Während Verhaltensdaten von einem Gerät mithilfe unbekannter Identitäten gesammelt werden können, ist eine Zuordnung dieser Identitäten über verschiedene Geräte oder Medien hinweg begrenzt, bis Ihr Kunde während der Journey personenbezogene Daten angibt.

Bekannte und anonyme Identitäten sind (wie in der folgenden Abbildung gezeigt) wichtige Komponenten von [Identitätsdiagrammen](#identity-graphs) und werden später in diesem Dokument genauer besprochen.

![Identitätszusammenfügung in Platform](./images/identity-service-stitching.png)

Examples of [!DNL Identity Service] implementations include:

- Ein Telekommunikationsunternehmen verlässt sich möglicherweise auf den Wert „Telefonnummer“, wobei eine Telefonnummer sowohl in Offline- als auch Online-Datensätzen auf dieselbe Person verweist.
- Ein Einzelhandelsunternehmen kann aufgrund des hohen Prozentsatzes an anonymen Besuchern in Offline-Datensätzen die „E-Mail-Adresse“ und in Online-Datensätzen die „ECID“ verwenden.
- Eine Bank könnte in Offline-Datensätzen, wie z. B. Transaktionen in Zweigstellen, die „Kontonummer“ bevorzugen. Bei Online-Datensätzen könnte sie hingegen die „Anmeldekennung“ nutzen, da die meisten Besucher während ihres Besuchs authentifiziert werden.
- Möglicherweise verfügen Ihre Kunden auch über eindeutige proprietäre Kennungen, wie die GUID oder andere universell eindeutige Kennungen.

### Identitätsdaten

Wenn Sie eine Person ohne weiteren Kontext fragen würden, wie ihre Identität lautet, würde es ihr wahrscheinlich schwer fallen, eine sinnvolle Antwort zu geben. Nach der gleichen Logik ist ein Zeichenfolgenwert, der einen Identitätswert darstellt (unabhängig davon, ob es sich um eine vom System erzeugte Kennung oder eine E-Mail-Adresse handelt), nur dann vollständig, wenn ein Qualifizierer mit dem Kontext des Zeichenfolgenwerts angegeben wird: der Identitäts-Namespace.

## Identitäts-Namespaces und Identitätsdiagramme

Ihre Kunden können mit Ihrer Marke über eine Kombination aus Online- und Offline-Kanälen interagieren. Das bringt die Herausforderung mit sich, diese fragmentierten Interaktionen in einer zentralen Kundenidentität abzustimmen.

[!DNL Experience Platform] löst diese Herausforderung mit zwei Konzepten: mit [Identitäts-Namespaces](#identity-namespaces) und [Identitätsdiagrammen](#identity-graphs).

Das folgende Video soll Ihr Verständnis von Identitäten und Identitätsdiagrammen unterstützen. Im folgenden Video werden die drei Funktionen von Identity Collection, Identity Graphs und APIs behandelt. Es beschreibt auch, wie deterministische und probabilistische Algorithmen zum Aufbau von Privatidentitätsdiagrammen verwendet werden, und beschreibt die Rolle von Privatidentitätsdiagrammen, Adobe Experience Platform Identity Service Co-Op Graph und Drittanbieter-Diagrammen.

>[!IMPORTANT]
>
> Probabilistische Privatgraphen sind noch in der Entwicklung und werden zu einem späteren Zeitpunkt veröffentlicht.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Identitäts-Namespaces

Wenn Ihr Kunde über verschiedene Kanäle mit Ihrer Marke interagiert (einschließlich Web, App, Callcenter oder Geschäft), wird es schwierig, sie zu verstehen und zu bedienen, wenn Sie ihre Aktivitäten nicht kanalübergreifend beobachten und verfolgen können.

Kunden über verschiedene Geräte und Kanäle hinweg zu verstehen, beginnt damit, dass Sie sie in jedem Kanal erkennen. Adobe Experience Platform erlaubt das mithilfe von Identitäts-Namespaces.
Ein Identitäts-Namespace ist eine Kennung (wie z. B. eine Geräte-ID oder E-Mail-ID), mit der der Kontext, aus dem Daten stammen, angegeben wird. Identitäts-Namespaces dienen zum Nachschlagen oder Verknüpfen einzelner Identitäten sowie zum Bereitstellen von Kontext für Identitätswerte, um Datenkollisionen zu verhindern. Beispielsweise kann sich die Kennung „123456“ auf eine Person in Ihrem E-Commerce-System sowie auf eine andere Person in Ihrem Helpdesk-System beziehen. Weiterführende Informationen finden Sie in der [Übersicht zu Identitäts-Namespaces](./namespaces.md).

### Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, die visuell veranschaulicht, wie Ihr Kunde über unterschiedliche Kanäle hinweg mit Ihrer Marke interagiert.

All customer identity graphs are collectively managed and updated by [!DNL Identity Service] in near real-time, in response to customer activity.

[!DNL Identity Service] verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). [!DNL Identity Service] erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

Als Beispiel für die möglichen Arten von Faktoren, die bei der Bereitstellung und Kennzeichnung von Identitätsdaten zu berücksichtigen sind, kann die Verwendung von Telefonnummern wie „Geschäftlich“ zu mehr Beziehungen führen, als Sie im Identitätsdiagramm haben möchten. Viele Mitarbeiter beziehen sich auf die gleiche geschäftliche Nummer, sodass „Privat“ und „Mobil“ besser dazu geeignet sind, Beziehungen so präzise wie möglich zu halten.

## Supplying identity data to [!DNL Identity Service]

This section covers how data provided to Adobe Experience Platform is processed prior to being used by [!DNL Identity Service] to build an identity graph for each customer.

### Identitätsfelder bestimmen

Je nach der Strategie Ihres Unternehmens zur Datenerfassung bestimmen die Datenfelder, die Sie als Identitäten kennzeichnen, darüber, welche Daten in Ihr Identitäts-Mapping aufgenommen werden. Um größtmöglichen Nutzen aus Adobe Experience Platform und den umfassendsten Kundenidentitäten zu ziehen, sollten Sie sowohl Online- als auch Offline-Daten hochladen.

- Online-Daten sind Daten, die die Präsenz und das Verhalten im Internet beschreiben, z. B. Benutzernamen und E-Mail-Adressen.

- Offline-Daten beziehen sich auf Daten, die nicht direkt mit einer Online-Präsenz zusammenhängen, wie z. B. Kennungen aus CRM-Systemen. Solche Daten macht Ihre Identitäten robuster und fördern die Kohärenz von Daten in verschiedenen Systemen.

### Zusätzliche Identitäts-Namespaces erstellen

While [!DNL Experience Platform] offers a variety of standard namespaces, you may need to create additional namespaces to properly categorize your identities. Weiterführende Informationen finden Sie im Abschnitt zum [Anzeigen und Erstellen von Namespaces für Ihre Organisation](./namespaces.md) in der Übersicht zu Identitäts-Namespaces.

>[!NOTE]
>
>Identitäts-Namespaces sind ein Qualifizierer für Identitäten. Nachdem ein Namespace erstellt wurde, kann er daher nicht mehr gelöscht werden.

### Identitätsdaten in [!DNL Experience Data Model] (XDM) einschließen

As the standardized framework by which [!DNL Platform] organizes customer data, [!DNL Experience Data Model] (XDM) allows data to be shared and understood across [!DNL Experience Platform] and other services interacting with [!DNL Platform]. Weiterführende Informationen finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

Sowohl Datensatz- als auch Zeitreihenschemas bieten die Möglichkeit, Identitätsdaten einzubeziehen. Beim Erfassen von Daten erstellt das Identitätsdiagramm neue Beziehungen zwischen Datenfragmenten aus verschiedenen Namespaces, wenn festgestellt wird, dass sie gemeinsame Identitätsdaten aufweisen.

### Markieren von XDM-Feldern als Identität

Jedes Feld vom Typ `string` in Schemas, die XDM-Klassen für Datensätze oder Zeitreihen implementieren, kann als Identitätsfeld gekennzeichnet werden. In der Folge würden alle in diesem Feld erfassten Daten als Identitätsdaten betrachtet.

Identitätsfelder erlauben auch eine Verknüpfung von Identitäten, wenn diese gemeinsame personenbezogene Daten aufweisen.
For example, by labeling phone number fields as identity fields, [!DNL Identity Service] automatically graphs relationships with the other individuals found to be using the same phone number.

>[!NOTE]
>
>Der Namespace der resultierenden Identitäten wird zum Zeitpunkt der Kennzeichnung des Felds bereitgestellt.

### Configure a dataset for [!DNL Identity Service]

During the streaming ingestion process, [!DNL Identity Service ]automatically extracts identity data from record and time series data. However, before data can be ingested, it must be enabled for [!DNL Identity Service]. Weiterführende Informationen finden Sie in der Anleitung zum [Konfigurieren eines Datensatzes für Echtzeit-Kundenprofil und Identity Service mit APIs](../profile/tutorials/dataset-configuration.md).

### Daten einbeziehen in [!DNL Identity Service]

[!DNL Identity Service] nutzt XDM-konforme Daten, die [!DNL Experience Platform] entweder durch [Stapelverarbeitung](../ingestion/batch-ingestion/overview.md) oder [Streaming-Erfassung](../ingestion/streaming-ingestion/overview.md)gesendet werden.

Das folgende Video soll Ihr Verständnis von Identitätsdienst unterstützen. In diesem Video wird gezeigt, wie Datenfelder als Identitäten gekennzeichnet werden, Identitätsdaten erfasst und anschließend überprüft werden, ob die Daten zum privaten Diagramm des Identitätsdienstes der Adobe Experience Platform hinzugefügt wurden.

>[!WARNING]
>
> Die im folgenden Video dargestellte [!DNL Platform] Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Data Governance

Adobe Experience Platform wurde mit Blick auf Datenschutz entwickelt und umfasst ein Data-Governance-Framework, um personenbezogene Daten Ihrer Kunden zu schützen. Identity data under the &quot;email&quot; or &quot;phone&quot; namespace is encrypted by default, but in order to ensure sensitive data is encrypted before it is persisted, data usage labels can be applied to data as it is ingested or once it arrives in [!DNL Platform]. Weiterführende Informationen finden Sie in der [Übersicht zu Data Governance](../data-governance/home.md).

## Nächste Schritte

Now that you understand the key concepts of [!DNL Identity Service] and its role within [!DNL Experience Platform], you can begin to learn how to work with your identity graph using the [!DNL Identity Service API](./api/getting-started.md).