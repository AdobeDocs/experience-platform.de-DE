---
keywords: Experience Platform;Home;beliebte Themen;Identität;Identität;XDM-Diagramme;Identitätsdienst;Identitätsdienst
solution: Experience Platform
title: Übersicht über den Identitätsdienst
topic: Übersicht
description: Mit dem Adobe Experience Platform Identity Service erhalten Sie eine bessere Ansicht Ihrer Kunden und ihres Verhaltens, indem Sie Identitäten zwischen Geräten und Systemen überbrücken und so wirkungsvolle persönliche digitale Erlebnisse in Echtzeit bereitstellen.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 70%

---


# [!DNL Identity Service]Übersicht

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint. Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, eine bessere Ansicht Ihres Kundenverhaltens zu erzielen, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit wirkungsvolle persönliche digitale Erlebnisse bereitstellen können.

## Grundlagen zu [!DNL Identity Service]

Jeden Tag interagieren Kunden mit Ihrem Unternehmen und gehen eine kontinuierlich wachsende Beziehung zu Ihrer Marke ein. Ein typischer Kunde kann in der Dateninfrastruktur Ihres Unternehmens in einer beliebigen Anzahl von Systemen aktiv sein, z. B. in Ihren E-Commerce-, Treueprogramm- und Helpdesk-Systemen. Derselbe Kunde kann auch anonym über verschiedene Geräte interagieren. [!DNL Identity Service]Mit können Sie sich einen Überblick über Ihren Kunden verschaffen und mit ihm verbundene Daten zusammenfassen, die andernfalls auf Silos in verschiedenen Systemen verteilt wären.

Betrachten wir ein alltägliches Beispiel für die Beziehung eines Verbrauchers zu Ihrer Marke:

Maria hat auf Ihrer E-Commerce-Site ein Konto, über das sie bereits mehrere Bestellungen getätigt hat. Normalerweise verwendet sie ihren privaten Laptop zum Einkaufen und meldet sich jedes Mal an. Bei einem Besuch nutzt sie jedoch ihr Tablet, um Sandalen zu bestellen, gibt aber keine Bestellung auf und meldet sich auch nicht an.

An diesem Punkt erscheinen Marias Aktivitäten als zwei separate Profile: ihre E-Commerce-Anmeldung und ihr Tablet-Gerät, möglicherweise identifiziert per Gerätekennung.

Maria setzt ihre Tablet-Sitzung später fort und gibt beim Abonnieren Ihres Newsletters ihre E-Mail-Adresse an. Im Anschluss daran fügt Streaming-Erfassung als Datensatzdaten in ihrem Profil eine neue Identität hinzu. Infolgedessen bezieht sich [!DNL Identity Service] jetzt Marias Tablet-Geräte-Aktivität mit ihrem E-Commerce-Kontoverlauf.

Bis zum nächsten Klick auf das Tablet könnten Ihre Zielinhalte Marias gesamtes Profil inklusive Verlauf widerspiegeln, statt nur das Tablet eines unbekannten Kunden.

Die Identitätsbeziehungen, die [!DNL Identity Service] definiert und unterhält, werden von [!DNL Real-time Customer Profile] genutzt, um ein vollständiges Bild eines Kunden und dessen Interaktionen mit Ihrer Marke zu erstellen. Weiterführende Informationen finden Sie in der [Übersicht zu Echtzeit-Kundenprofil](../profile/home.md).

### Identitäten

Eine Identität besteht aus Daten, die für eine Entität (normalerweise eine Person) eindeutig sind. Eine Identität wie z. B. eine Anmeldekennung, eine ECID oder eine Treueprogramm-ID wird als bekannte Identität bezeichnet.

Personenbezogene Daten (PII) wie E-Mail-Adresse und Telefonnummer dienen zur direkten Identifizierung eines Kunden. Infolgedessen werden personenbezogene Daten dazu verwendet, um verschiedene Identitäten eines Kunden systemübergreifend abzugleichen.

Unbekannte oder anonyme Identitäten identifizieren ein Gerät, ohne dass die Person identifiziert wird, die dieses Gerät nutzt. Diese Kategorie enthält Daten wie die IP-Adresse und Cookie-ID des Besuchers. Während Verhaltensdaten von einem Gerät mithilfe unbekannter Identitäten gesammelt werden können, ist eine Zuordnung dieser Identitäten über verschiedene Geräte oder Medien hinweg begrenzt, bis Ihr Kunde während der Journey personenbezogene Daten angibt.

Bekannte und anonyme Identitäten sind (wie in der folgenden Abbildung gezeigt) wichtige Komponenten von [Identitätsdiagrammen](#identity-graphs) und werden später in diesem Dokument genauer besprochen.

![Identitätszusammenfügung in Platform](./images/identity-service-stitching.png)

Beispiele für Implementierungen von [!DNL Identity Service]:

- Ein Telekommunikationsunternehmen verlässt sich möglicherweise auf den Wert „Telefonnummer“, wobei eine Telefonnummer sowohl in Offline- als auch Online-Datensätzen auf dieselbe Person verweist.
- Ein Einzelhandelsunternehmen kann aufgrund des hohen Prozentsatzes an anonymen Besuchern in Offline-Datensätzen die „E-Mail-Adresse“ und in Online-Datensätzen die „ECID“ verwenden.
- Eine Bank könnte in Offline-Datensätzen, wie z. B. Transaktionen in Zweigstellen, die „Kontonummer“ bevorzugen. Bei Online-Datensätzen könnte sie hingegen die „Anmeldekennung“ nutzen, da die meisten Besucher während ihres Besuchs authentifiziert werden.
- Möglicherweise verfügen Ihre Kunden auch über eindeutige proprietäre Kennungen, wie die GUID oder andere Universally Unique Identifiers.

### Identitätsdaten

Wenn Sie eine Person ohne weiteren Kontext fragen würden, wie ihre Identität lautet, würde es ihr wahrscheinlich schwer fallen, eine sinnvolle Antwort zu geben. Nach der gleichen Logik ist ein Zeichenfolgenwert, der einen Identitätswert darstellt (unabhängig davon, ob es sich um eine vom System erzeugte Kennung oder eine E-Mail-Adresse handelt), nur dann vollständig, wenn ein Qualifizierer mit dem Kontext des Zeichenfolgenwerts angegeben wird: der Identitäts-Namespace.

## Identitäts-Namespaces und Identitätsdiagramme

Ihre Kunden können mit Ihrer Marke über eine Kombination aus Online- und Offline-Kanälen interagieren. Das bringt die Herausforderung mit sich, diese fragmentierten Interaktionen in einer zentralen Kundenidentität abzustimmen.

[!DNL Experience Platform] löst diese Herausforderung mit zwei Konzepten: mit [Identitäts-Namespaces](#identity-namespaces) und [Identitätsdiagrammen](#identity-graphs).

Das folgende Video soll Ihr Verständnis von Identitäten und Identitätsdiagrammen unterstützen. Im folgenden Video werden die drei Funktionen von Identity Collection, Identity Graphs und APIs behandelt. Es beschreibt auch, wie deterministische und probabilistische Algorithmen zum Erstellen von Diagrammen für die private Identität verwendet werden, und beschreibt die Rolle von Diagrammen für die private Identität, von Adobe Experience Platform Identity Service Co-Op-Diagrammen und von Grafiken von Drittanbietern.

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

Alle Diagramme zur Kundenidentität werden gemeinsam von [!DNL Identity Service] als Reaktion auf die Aktivität der Kunden in Echtzeit verwaltet und aktualisiert.

[!DNL Identity Service] verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). [!DNL Identity Service] erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

Als Beispiel für die möglichen Arten von Faktoren, die bei der Bereitstellung und Kennzeichnung von Identitätsdaten zu berücksichtigen sind, kann die Verwendung von Telefonnummern wie „Geschäftlich“ zu mehr Beziehungen führen, als Sie im Identitätsdiagramm haben möchten. Viele Mitarbeiter beziehen sich auf die gleiche geschäftliche Nummer, sodass „Privat“ und „Mobil“ besser dazu geeignet sind, Beziehungen so präzise wie möglich zu halten.

Weitere Informationen finden Sie im Tutorial zum Zugriff auf den Identitätsdiagramm-Viewer](./ui/identity-graph-viewer.md)[

## Identitätsdaten für [!DNL Identity Service] bereitstellen

In diesem Abschnitt wird beschrieben, wie an Adobe Experience Platform übermittelte Daten verarbeitet werden, bevor [!DNL Identity Service] zum Aufbau eines Identitätsdiagramms für jeden Kunden verwendet wird.

### Identitätsfelder bestimmen

Je nach der Strategie Ihres Unternehmens zur Datenerfassung bestimmen die Datenfelder, die Sie als Identitäten kennzeichnen, darüber, welche Daten in Ihre Identitätszuordnung aufgenommen werden. Um größtmöglichen Nutzen aus Adobe Experience Platform und den umfassendsten Kundenidentitäten zu ziehen, sollten Sie sowohl Online- als auch Offline-Daten hochladen.

- Online-Daten sind Daten, die die Präsenz und das Verhalten im Internet beschreiben, z. B. Benutzernamen und E-Mail-Adressen.

- Offline-Daten beziehen sich auf Daten, die nicht direkt mit einer Online-Präsenz zusammenhängen, wie z. B. Kennungen aus CRM-Systemen. Solche Daten macht Ihre Identitäten robuster und fördern die Kohärenz von Daten in verschiedenen Systemen.

### Zusätzliche Identitäts-Namespaces erstellen

Während [!DNL Experience Platform] eine Reihe von Standard-Namensräumen Angebot, müssen Sie möglicherweise zusätzliche Namensraum erstellen, um Ihre Identitäten korrekt zu kategorisieren. Weiterführende Informationen finden Sie im Abschnitt zum [Anzeigen und Erstellen von Namespaces für Ihre Organisation](./namespaces.md) in der Übersicht zu Identitäts-Namespaces.

>[!NOTE]
>
> Identitäts-Namespaces sind ein Qualifizierer für Identitäten. Nachdem ein Namespace erstellt wurde, kann er daher nicht mehr gelöscht werden.

### Identitätsdaten in [!DNL Experience Data Model] (XDM) einschließen

Als standardisiertes Framework, mit dem [!DNL Platform] Kundendaten organisiert, ermöglicht [!DNL Experience Data Model] (XDM) die Freigabe und das Verständnis von Daten über [!DNL Experience Platform] und andere Dienste, die mit [!DNL Platform] interagieren. Weiterführende Informationen finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

Sowohl Datensatz- als auch Zeitreihenschemas bieten die Möglichkeit, Identitätsdaten einzubeziehen. Beim Erfassen von Daten erstellt das Identitätsdiagramm neue Beziehungen zwischen Datenfragmenten aus verschiedenen Namespaces, wenn festgestellt wird, dass sie gemeinsame Identitätsdaten aufweisen.

### Markieren von XDM-Feldern als Identität

Jedes Feld vom Typ `string` in Schemas, die XDM-Klassen für Datensätze oder Zeitreihen implementieren, kann als Identitätsfeld gekennzeichnet werden. In der Folge würden alle in diesem Feld erfassten Daten als Identitätsdaten betrachtet.

Identitätsfelder erlauben auch eine Verknüpfung von Identitäten, wenn diese gemeinsame personenbezogene Daten aufweisen.
Wenn Sie z. B. Telefonnummernfelder als Identitätsfelder kennzeichnen, zeigt [!DNL Identity Service] automatisch die Beziehungen zu den anderen Personen an, bei denen festgestellt wurde, dass sie dieselbe Telefonnummer verwenden.

>[!NOTE]
>
>Der Namespace der resultierenden Identitäten wird zum Zeitpunkt der Kennzeichnung des Felds bereitgestellt.

### Datensatz für [!DNL Identity Service] konfigurieren

Während der Streaming-Erfassung extrahiert [!DNL Identity Service ]automatisch Identitätsdaten aus Datensatz- und Zeitreihendaten. Bevor Daten jedoch erfasst werden können, müssen sie für [!DNL Identity Service] aktiviert werden. Weiterführende Informationen finden Sie in der Anleitung zum [Konfigurieren eines Datensatzes für Echtzeit-Kundenprofil und Identity Service mit APIs](../profile/tutorials/dataset-configuration.md).

### Daten in [!DNL Identity Service] aufnehmen

[!DNL Identity Service] nutzt XDM-konforme Daten, die  [!DNL Experience Platform] entweder durch  [Batch-](../ingestion/batch-ingestion/overview.md) Erfassung oder  [Streaming-Erfassung](../ingestion/streaming-ingestion/overview.md) gesendet werden.

Das folgende Video soll Ihr Verständnis von Identitätsdienst unterstützen. In diesem Video wird gezeigt, wie Datenfelder als Identitäten gekennzeichnet werden, Identitätsdaten erfasst und anschließend überprüft werden, ob die Daten in das Adobe Experience Platform Identity Service Private Graph eingegeben wurden.

>[!WARNING]
>
>Die im folgenden Video angezeigte [!DNL Platform]-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Data Governance

Adobe Experience Platform wurde mit Blick auf Datenschutz entwickelt und umfasst ein Data-Governance-Framework, um personenbezogene Daten Ihrer Kunden zu schützen. Identitätsdaten unter dem Namensraum &quot;email&quot; oder &quot;phone&quot; werden standardmäßig verschlüsselt. Um jedoch sicherzustellen, dass sensible Daten verschlüsselt werden, bevor sie bestehen bleiben, können Datenverwendungsbeschriftungen auf Daten angewendet werden, die bei der Erfassung oder beim Eintreffen in [!DNL Platform] erfasst werden. Weiterführende Informationen finden Sie in der [Übersicht zu Data Governance](../data-governance/home.md).

## Nächste Schritte

Nachdem Sie nun die Schlüsselkonzepte von [!DNL Identity Service] und ihre Rolle innerhalb von [!DNL Experience Platform] kennen, können Sie lernen, wie Sie mit Ihrem Identitätsdiagramm mit dem [[!DNL Identity Service API]](./api/getting-started.md) arbeiten.
