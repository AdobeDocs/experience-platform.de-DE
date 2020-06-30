---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 5%

---


# [!DNL Identity Service]Übersicht

Die Bereitstellung relevanter digitaler Erlebnisse erfordert ein vollständiges Verständnis Ihres Kunden. Dies wird schwieriger, wenn Ihre Kundendaten über verschiedene Systeme verteilt sind, sodass jeder einzelne Kunde mehrere &quot;Identitäten&quot;zu haben scheint. Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, eine bessere Ansicht Ihres Kundenverhaltens zu erzielen, indem Identitäten zwischen Geräten und Systemen überbrückt werden, sodass Sie in Echtzeit wirkungsvolle persönliche digitale Erlebnisse bereitstellen können.

## Erläuterungen [!DNL Identity Service]

Jeden Tag interagieren Kunden mit Ihrem Unternehmen und etablieren eine stetig wachsende Beziehung zu Ihrer Marke. Ein typischer Kunde kann in einer beliebigen Anzahl von Systemen in der Dateninfrastruktur Ihres Unternehmens tätig sein, z. B. in Ihren E-Commerce-, Loyalität- und Help-Desk-Systemen. Derselbe Kunde kann sich auch anonym an einer beliebigen Anzahl von Geräten beteiligen. [!DNL Identity Service] ermöglicht es Ihnen, ein vollständiges Bild Ihres Kunden zusammenzustellen und damit zusammenhängende Daten zu aggregieren, die andernfalls über verschiedene Systeme hinweg simuliert werden könnten.

Betrachten Sie ein alltägliches Beispiel für die Beziehung eines Verbrauchers zu Ihrer Marke:

Maria hat auf Ihrer E-Commerce-Site ein Konto, auf dem sie bereits einige Bestellungen abgeschlossen hat. Normalerweise verwendet sie ihren persönlichen Laptop zum Laden, wo sie sich jedes Mal anmeldet. Während eines Besuchs benutzt sie jedoch ihr Tablet, um Sandalen zu bestellen, gibt aber keine Bestellung auf und meldet sich nicht an.

An dieser Stelle erscheint Marias Aktivität in zwei separaten Profilen: ihre eCommerce-Anmeldung und ihr Tablet-Gerät, möglicherweise identifiziert durch Geräte-ID.

Maria setzt später ihre Tablet-Sitzung fort und gibt beim Abonnieren Ihres Newsletters ihre E-Mail-Adresse ein. Auf diese Weise fügt die Streaming-Erfassung eine neue Identität als Datensatzdaten in ihrem Profil hinzu. Infolgedessen bezieht sich [!DNL Identity Service] jetzt Marias Aktivität für Tablet-Geräte mit ihrer E-Commerce-Kontogeschichte.

Durch den nächsten Klick auf ihr Tablet könnten Ihre zielgerichteten Inhalte Marias gesamtes Profil und seine Geschichte widerspiegeln, statt nur ein Tablet eines unbekannten Kunden zu verwenden.

Die Identitätsbeziehungen, die [!DNL Identity Service] [!DNL Real-time Customer Profile] definieren und pflegen, werden genutzt, um ein vollständiges Bild von einem Kunden und dessen Interaktionen mit Ihrer Marke zu erstellen. Weitere Informationen finden Sie in der Übersicht über das [Echtzeit-Profil](../profile/home.md).

### Identitäten

Eine Identität sind Daten, die für eine Entität eindeutig sind, normalerweise für eine einzelne Person. Eine Identität wie eine Anmelde-ID, eine ECID oder eine Loyalität-ID wird als **bekannte Identität** bezeichnet.

PII wie E-Mail-Adresse und Telefonnummer dient zur direkten Identifizierung eines Kunden. Infolgedessen wird PII verwendet, um die verschiedenen Identitäten eines Kunden systemübergreifend abzugleichen.

**Unbekannte oder anonyme Identitäten** verschlüsseln ein Gerät, ohne die tatsächliche Person zu identifizieren, die es verwendet. Diese Kategorie enthält Informationen wie die IP-Adresse und die Cookie-ID eines Besuchers. Während Verhaltensdaten von einem Gerät mithilfe unbekannter Identitäten gesammelt werden können, ist die Zuordnung dieser Identitäten zu anderen Geräten oder Medien begrenzt, bis Ihr Kunde während der Reise PII-Daten bereitstellt.

Bekannte und anonyme Identitäten sind, wie in der Abbildung unten gezeigt, wichtige Bestandteile von [Identitätsdiagrammen](#identity-graphs), die später in diesem Dokument besprochen werden.

![Identitätszuordnung bei Platform](./images/identity-service-stitching.png)

Beispiele für [!DNL Identity Service] Implementierungen:

- Eine Telekom-Firma kann sich auf den Wert &quot;Telefonnummer&quot;stützen, bei dem eine Telefonnummer sowohl für Offline- als auch für Online-Datensätze auf dieselbe Interessensgruppe verweist.
- Eine für den Handel bestimmte Firma kann aufgrund des hohen Prozentsatzes anonymer Besucher &quot;E-Mail-Adresse&quot;in Offline-Datensätzen und ECID in Online-Datensätzen verwenden.
- Eine Bank könnte &quot;Kontonummer&quot;in Offline-Datensätzen, wie z. B. Zweigstellen-Transaktionen, bevorzugen. Sie können von der &quot;Anmelde-ID&quot;in Online-Datensätzen abhängig sein, da die meisten Besucher während ihres Besuchs authentifiziert werden.
- Ihre Kunden haben möglicherweise auch eindeutige proprietäre IDs, wie GUID oder andere universelle eindeutige IDs.

### Identitätsdaten

Wenn Sie eine Person fragen würden: &quot;Was ist Ihre ID?&quot; ohne weiteren Kontext wäre es für sie schwierig, eine nützliche Antwort zu geben. Nach der gleichen Logik ist ein Zeichenfolgenwert, der einen Identitätswert darstellt, unabhängig davon, ob es sich um eine vom System erzeugte ID oder eine E-Mail-Adresse handelt, nur dann vollständig, wenn ein Qualifizierer mit dem Zeichenfolgenwertkontext bereitgestellt wird: der Identitäts-Namensraum.

## Identitäts-Namensraum und Identitätsdiagramme

Ihre Kunden können mit Ihrer Marke durch eine Kombination aus Online- und Offline-Kanälen interagieren, was die Herausforderung darstellt, diese fragmentierten Interaktionen in einer einzigen Kundenidentität zu vereinbaren.

[!DNL Experience Platform] diese Herausforderung durch zwei Konzepte angehen: [Identitäts-Namensraum](#identity-namespaces) und [Identitätsdiagramme](#identity-graphs).

### Identitäts-Namespaces

Wenn Ihr Kunde über mehrere Kanal hinweg mit Ihrer Marke interagiert, einschließlich Web, Mobilanwendung, Call-Center oder einem Store, kann es schwierig sein, diese zu verstehen und zu bedienen, wenn Sie ihre Aktivität nicht über Kanal hinweg beobachten und verfolgen können.

Verstehen Sie Ihre Kunden über mehrere Geräte und Kanal hinweg, indem Sie sie in jedem Kanal erkennen. Adobe Experience Platform erreicht dies mithilfe von Identitäts-Namensräumen.
Ein Identitäts-Namensraum ist eine ID wie Geräte-ID oder E-Mail-ID, mit der der Kontext, aus dem Daten stammen, angegeben wird. Identitäts-Namensraum werden zum Nachschlagen oder Verknüpfen einzelner Identitäten und zum Bereitstellen von Kontext für Identitätswerte verwendet, um Datenkollisionen zu verhindern. Beispielsweise kann sich die ID &quot;123456&quot;auf eine Person in Ihrem E-Commerce-System und auf eine andere Person in Ihrem Help-Desk-System beziehen. Weitere Informationen finden Sie unter Übersicht über den [Identitäts-Namensraum](./namespaces.md).

### Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, die visuell veranschaulicht, wie Ihr Kunde über unterschiedliche Kanäle hinweg mit Ihrer Marke interagiert.

All customer identity graphs are collectively managed and updated by [!DNL Identity Service] in near real-time, in response to customer activity.

[!DNL Identity Service] verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). [!DNL Identity Service] erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

Als Beispiel für die möglichen Arten von Faktoren, die bei der Bereitstellung und Kennzeichnung von Identitätsdaten zu berücksichtigen sind, kann die Verwendung von Telefonnummern wie &quot;Handy&quot;zu mehr Beziehungen führen, als Sie im Identitätsdiagramm beabsichtigen. Viele Mitarbeiter beziehen sich auf die gleiche Anzahl von Arbeitsplätzen, und &quot;Zuhause&quot; und &quot;mobil&quot; dienen besser dazu, Beziehungen so präzise wie möglich zu halten.

## Identitätsdaten bereitstellen an [!DNL Identity Service]

In diesem Abschnitt wird beschrieben, wie Daten, die der Adobe Experience Platform bereitgestellt werden, verarbeitet werden, bevor sie zum Aufbau eines Identitätsdiagramms für jeden Kunden verwendet werden [!DNL Identity Service] können.

### Bestimmen von Identitätsfeldern

Abhängig von Ihrer Strategie zur Unternehmenserfassung bestimmen die Datenfelder, die Sie als Identitäten bezeichnen, welche Daten in Ihrer Identitätskarte enthalten sind. Um den größtmöglichen Nutzen aus der Adobe Experience Platform und den umfassendsten Kundenidentitäten zu ziehen, sollten Sie Online- und Offlinedaten hochladen.

- Online-Daten sind Daten, die die Präsenz und das Verhalten im Internet beschreiben, z. B. Benutzernamen und E-Mail-Adressen.

- Offline-Daten beziehen sich auf Daten, die nicht direkt mit der Online-Präsenz zusammenhängen, wie z. B. IDs aus CRM-Systemen. Diese Art von Daten macht Ihre Identitäten robuster und unterstützt den Zusammenhalt von Daten in verschiedenen Systemen.

### Zusätzliche Identitäts-Namensraum erstellen

Während [!DNL Experience Platform] Angebote für eine Reihe von Standard-Namensräumen erforderlich sind, müssen Sie möglicherweise zusätzliche Namensraum erstellen, um Ihre Identitäten korrekt zu kategorisieren. Weitere Informationen finden Sie im Abschnitt zum [Anzeigen und Erstellen von Namensräumen für Ihr Unternehmen](./namespaces.md) in der Übersicht über Identitäts-Namensraum.

>[!NOTE] Identitäts-Namensraum sind ein Qualifikator für Identitäten. Nachdem ein Namensraum erstellt wurde, kann er daher nicht mehr gelöscht werden.

### Identitätsdaten in [!DNL Experience Data Model] (XDM) einschließen

Als standardisiertes Framework, mit dem Kundendaten [!DNL Platform] organisiert werden, ermöglicht [!DNL Experience Data Model] (XDM) die Freigabe und das Verständnis von Daten über andere Dienste [!DNL Experience Platform] und andere Dienste, mit denen interagiert [!DNL Platform]. Weitere Informationen finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

Sowohl Schema für Datensätze als auch für Zeitreihen bieten die Möglichkeit, Identitätsdaten einzubeziehen. Beim Erfassen von Daten erstellt das Identitätsdiagramm neue Beziehungen zwischen Datenfragmenten aus verschiedenen Namensräumen, wenn festgestellt wird, dass sie gemeinsame Identitätsdaten gemeinsam nutzen.

### Markieren von XDM-Feldern als Identität

Jedes Feld des Typs `string` in Schemas, das XDM-Klassen für Datensätze oder Zeitreihen implementiert, kann als Identitätsfeld bezeichnet werden. Daher werden alle in dieses Feld erfassten Daten als Identitätsdaten betrachtet.

Identitätsfelder ermöglichen auch die Verknüpfung von Identitäten, wenn sie gemeinsame PII-Daten verwenden.
Wenn Sie z. B. Telefonnummernfelder als Identitätsfelder kennzeichnen, zeichnet [!DNL Identity Service] automatisch die Beziehungen zu den anderen Personen auf, bei denen festgestellt wurde, dass sie dieselbe Telefonnummer verwenden.

>[!NOTE] Der Namensraum der resultierenden Identitäten wird zum Zeitpunkt der Feldbeschriftung bereitgestellt.

### Dataset konfigurieren für [!DNL Identity Service]

Extrahiert während des Streaming-Erfassungsvorgangs [!DNL Identity Service ]automatisch Identitätsdaten aus Datensatz- und Zeitreihendaten. Bevor Daten jedoch erfasst werden können, müssen sie aktiviert werden [!DNL Identity Service]. Weitere Informationen finden Sie im Lernprogramm zum [Konfigurieren eines Datasets für Echtzeit-Kunden- und Identitätsdienst mit APIs](../profile/tutorials/dataset-configuration.md) .

### Daten einbeziehen in [!DNL Identity Service]

[!DNL Identity Service] nutzt XDM-konforme Daten, die [!DNL Experience Platform] entweder durch [Stapelverarbeitung](../ingestion/batch-ingestion/overview.md) oder [Streaming-Erfassung](../ingestion/streaming-ingestion/overview.md)gesendet werden.

## Datenverwaltung

Die Adobe Experience Platform wurde unter Berücksichtigung der Privatsphäre entwickelt und enthält einen Rahmen zur Datenverwaltung, um Ihre Kunden-PII-Daten zu schützen. Identitätsdaten unter dem Namensraum &quot;email&quot; oder &quot;phone&quot; werden standardmäßig verschlüsselt. Um jedoch sicherzustellen, dass sensible Daten verschlüsselt werden, bevor sie bestehen bleiben, können Datenverwendungsbeschriftungen bei der Erfassung oder beim Eintreffen auf Daten angewendet werden [!DNL Platform]. Weitere Informationen finden Sie in der Übersicht über die [Datenverwaltung](../data-governance/home.md).

## Nächste Schritte

Jetzt, da Sie die wichtigsten Konzepte [!DNL Identity Service] und ihre Rolle in [!DNL Experience Platform]verstehen, können Sie lernen, wie Sie mit Ihrem Identitätsdiagramm mit dem [!DNL Identity Service API](./api/getting-started.md).