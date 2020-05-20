---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 6%

---


# Übersicht über den Identitätsdienst

Die Bereitstellung relevanter digitaler Erlebnisse erfordert ein vollständiges Verständnis Ihres Kunden. Dies wird schwieriger, wenn Ihre Kundendaten über verschiedene Systeme verteilt sind, sodass jeder einzelne Kunde mehrere &quot;Identitäten&quot;zu haben scheint. Der Identitätsdienst für Adobe Experience Platform hilft Ihnen, eine bessere Ansicht Ihres Kundenverhaltens und seines Verhaltens zu erzielen, indem Identitäten geräteübergreifend und systemübergreifend überbrückt werden. So können Sie wirkungsvolle persönliche digitale Erlebnisse in Echtzeit bereitstellen.

## Identitätsdienst

Jeden Tag interagieren Kunden mit Ihrem Unternehmen und etablieren eine stetig wachsende Beziehung zu Ihrer Marke. Ein typischer Kunde kann in einer beliebigen Anzahl von Systemen in der Dateninfrastruktur Ihres Unternehmens tätig sein, z. B. in Ihren E-Commerce-, Loyalität- und Help-Desk-Systemen. Derselbe Kunde kann sich auch anonym an einer beliebigen Anzahl von Geräten beteiligen. Mit dem Identitätsdienst können Sie ein vollständiges Bild Ihres Kunden zusammenstellen und damit zusammenhängende Daten zusammenstellen, die andernfalls über verschiedene Systeme hinweg simuliert werden könnten.

Betrachten Sie ein alltägliches Beispiel für die Beziehung eines Verbrauchers zu Ihrer Marke:

Maria hat auf Ihrer E-Commerce-Site ein Konto, auf dem sie bereits einige Bestellungen abgeschlossen hat. Normalerweise verwendet sie ihren persönlichen Laptop zum Laden, wo sie sich jedes Mal anmeldet. Während eines Besuchs benutzt sie jedoch ihr Tablet, um Sandalen zu bestellen, gibt aber keine Bestellung auf und meldet sich nicht an.

An dieser Stelle erscheint Marias Aktivität in zwei separaten Profilen: ihre eCommerce-Anmeldung und ihr Tablet-Gerät, möglicherweise identifiziert durch Geräte-ID.

Maria setzt später ihre Tablet-Sitzung fort und gibt beim Abonnieren Ihres Newsletters ihre E-Mail-Adresse ein. Auf diese Weise fügt die Streaming-Erfassung eine neue Identität als Datensatzdaten in ihrem Profil hinzu. Infolgedessen bezieht sich der Identitätsdienst nun auf Marias Aktivität für Tablet-Geräte mit ihrem E-Commerce-Kontoverlauf.

Durch den nächsten Klick auf ihr Tablet könnten Ihre zielgerichteten Inhalte Marias gesamtes Profil und seine Geschichte widerspiegeln, statt nur ein Tablet eines unbekannten Kunden zu verwenden.

Die Identitätsbeziehungen, die Identity Service definiert und pflegt, werden vom Echtzeit-Customer Profil genutzt, um ein vollständiges Bild von einem Kunden und dessen Interaktionen mit Ihrer Marke zu erstellen. Weitere Informationen finden Sie in der Übersicht über das [Echtzeit-Profil](../profile/home.md).

### Identitäten

Eine Identität sind Daten, die für eine Entität eindeutig sind, normalerweise für eine einzelne Person. Eine Identität wie eine Anmelde-ID, eine ECID oder eine Loyalität-ID wird als **bekannte Identität** bezeichnet.

PII wie E-Mail-Adresse und Telefonnummer dient zur direkten Identifizierung eines Kunden. Infolgedessen wird PII verwendet, um die verschiedenen Identitäten eines Kunden systemübergreifend abzugleichen.

**Unbekannte oder anonyme Identitäten** verschlüsseln ein Gerät, ohne die tatsächliche Person zu identifizieren, die es verwendet. Diese Kategorie enthält Informationen wie die IP-Adresse und die Cookie-ID eines Besuchers. Während Verhaltensdaten von einem Gerät mithilfe unbekannter Identitäten gesammelt werden können, ist die Zuordnung dieser Identitäten zu anderen Geräten oder Medien begrenzt, bis Ihr Kunde während der Reise PII-Daten bereitstellt.

Bekannte und anonyme Identitäten sind, wie in der Abbildung unten gezeigt, wichtige Bestandteile von [Identitätsdiagrammen](#identity-graphs), die später in diesem Dokument besprochen werden.

![Identitätszuordnung auf der Plattform](./images/identity-service-stitching.png)

Beispiele für Implementierungen von Identitätsdiensten:

- Eine Telekom-Firma kann sich auf den Wert &quot;Telefonnummer&quot;stützen, bei dem eine Telefonnummer sowohl für Offline- als auch für Online-Datensätze auf dieselbe Interessensgruppe verweist.
- Eine für den Handel bestimmte Firma kann aufgrund des hohen Prozentsatzes anonymer Besucher &quot;E-Mail-Adresse&quot;in Offline-Datensätzen und ECID in Online-Datensätzen verwenden.
- Eine Bank könnte &quot;Kontonummer&quot;in Offline-Datensätzen, wie z. B. Zweigstellen-Transaktionen, bevorzugen. Sie können von der &quot;Anmelde-ID&quot;in Online-Datensätzen abhängig sein, da die meisten Besucher während ihres Besuchs authentifiziert werden.
- Ihre Kunden haben möglicherweise auch eindeutige proprietäre IDs, wie GUID oder andere universelle eindeutige IDs.

### Identitätsdaten

Wenn Sie eine Person fragen würden: &quot;Was ist Ihre ID?&quot; ohne weiteren Kontext wäre es für sie schwierig, eine nützliche Antwort zu geben. Nach der gleichen Logik ist ein Zeichenfolgenwert, der einen Identitätswert darstellt, unabhängig davon, ob es sich um eine vom System erzeugte ID oder eine E-Mail-Adresse handelt, nur dann vollständig, wenn ein Qualifizierer mit dem Zeichenfolgenwertkontext bereitgestellt wird: der Identitäts-Namensraum.

## Identitäts-Namensraum und Identitätsdiagramme

Ihre Kunden können mit Ihrer Marke durch eine Kombination aus Online- und Offline-Kanälen interagieren, was die Herausforderung darstellt, diese fragmentierten Interaktionen in einer einzigen Kundenidentität zu vereinbaren.

Die Erlebnisplattform geht diese Herausforderung durch zwei Konzepte an: [Identitäts-Namensraum](#identity-namespaces) und [Identitätsdiagramme](#identity-graphs).

### Identitäts-Namespaces

Wenn Ihr Kunde über mehrere Kanal hinweg mit Ihrer Marke interagiert, einschließlich Web, Mobilanwendung, Call-Center oder einem Store, kann es schwierig sein, diese zu verstehen und zu bedienen, wenn Sie ihre Aktivität nicht über Kanal hinweg beobachten und verfolgen können.

Verstehen Sie Ihre Kunden über mehrere Geräte und Kanal hinweg, indem Sie sie in jedem Kanal erkennen. Adobe Experience Platform erreicht dies mithilfe von Identitäts-Namensräumen.
Ein Identitäts-Namensraum ist eine ID wie Geräte-ID oder E-Mail-ID, mit der der Kontext, aus dem Daten stammen, angegeben wird. Identitäts-Namensraum werden zum Nachschlagen oder Verknüpfen einzelner Identitäten und zum Bereitstellen von Kontext für Identitätswerte verwendet, um Datenkollisionen zu verhindern. Beispielsweise kann sich die ID &quot;123456&quot;auf eine Person in Ihrem E-Commerce-System und auf eine andere Person in Ihrem Help-Desk-System beziehen. Weitere Informationen finden Sie unter Übersicht über den [Identitäts-Namensraum](./namespaces.md).

### Identitätsdiagramme

Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäts-Namespaces, die visuell veranschaulicht, wie Ihr Kunde über unterschiedliche Kanäle hinweg mit Ihrer Marke interagiert.

Alle Diagramme zur Kundenidentität werden von Identity Service als Reaktion auf Kundenaktivität nahezu in Echtzeit verwaltet und aktualisiert.

Identity Service verwaltet ein Identitätsdiagramm, das nur für Ihr Unternehmen sichtbar ist und auf Grundlage Ihrer Daten erstellt wird (als privates Diagramm bezeichnet). Identity Service erweitert das private Diagramm, wenn ein erfasster Datensatz mehr als eine Identität enthält, indem eine Beziehung zwischen den gefundenen Identitäten hinzugefügt wird.

Als Beispiel für die möglichen Arten von Faktoren, die bei der Bereitstellung und Kennzeichnung von Identitätsdaten zu berücksichtigen sind, kann die Verwendung von Telefonnummern wie &quot;Handy&quot;zu mehr Beziehungen führen, als Sie im Identitätsdiagramm beabsichtigen. Viele Mitarbeiter beziehen sich auf die gleiche Anzahl von Arbeitsplätzen, und &quot;Zuhause&quot; und &quot;mobil&quot; dienen besser dazu, Beziehungen so präzise wie möglich zu halten.

## Identitätsdaten für den Identitätsdienst bereitstellen

In diesem Abschnitt wird beschrieben, wie Daten, die der Adobe Experience Platform bereitgestellt werden, verarbeitet werden, bevor sie vom Identitätsdienst zum Aufbau eines Identitätsdiagramms für jeden Kunden verwendet werden.

### Bestimmen von Identitätsfeldern

Abhängig von Ihrer Strategie zur Unternehmenserfassung bestimmen die Datenfelder, die Sie als Identitäten bezeichnen, welche Daten in Ihrer Identitätskarte enthalten sind. Um den größtmöglichen Nutzen aus Adobe Experience Platform und den umfassendsten Kundenidentitäten zu ziehen, sollten Sie Online- und Offlinedaten hochladen.

- Online-Daten sind Daten, die die Präsenz und das Verhalten im Internet beschreiben, z. B. Benutzernamen und E-Mail-Adressen.

- Offline-Daten beziehen sich auf Daten, die nicht direkt mit der Online-Präsenz zusammenhängen, wie z. B. IDs aus CRM-Systemen. Diese Art von Daten macht Ihre Identitäten robuster und unterstützt den Zusammenhalt von Daten in verschiedenen Systemen.

### Zusätzliche Identitäts-Namensraum erstellen

Während Experience Platform eine Vielzahl von Standard-Namensräumen Angebot, müssen Sie möglicherweise zusätzliche Namensraum erstellen, um Ihre Identitäten korrekt zu kategorisieren. Weitere Informationen finden Sie im Abschnitt zum [Anzeigen und Erstellen von Namensräumen für Ihr Unternehmen](./namespaces.md) in der Übersicht über Identitäts-Namensraum.

>[!NOTE] Identitäts-Namensraum sind ein Qualifikator für Identitäten. Nachdem ein Namensraum erstellt wurde, kann er daher nicht mehr gelöscht werden.

### Identitätsdaten in Experience Data Model (XDM) einschließen

Als standardisiertes Framework, mit dem Plattform Kundendaten organisiert, ermöglicht Experience Data Model (XDM) die Freigabe und das Verständnis von Daten über Experience Platform und andere Dienste, die mit Plattform interagieren. Weitere Informationen finden Sie in der [XDM-Systemübersicht](../xdm/home.md).

Sowohl Schema für Datensätze als auch für Zeitreihen bieten die Möglichkeit, Identitätsdaten einzubeziehen. Beim Erfassen von Daten erstellt das Identitätsdiagramm neue Beziehungen zwischen Datenfragmenten aus verschiedenen Namensräumen, wenn festgestellt wird, dass sie gemeinsame Identitätsdaten gemeinsam nutzen.

### Markieren von XDM-Feldern als Identität

Jedes Feld des Typs `string` in Schemas, das XDM-Klassen für Datensätze oder Zeitreihen implementiert, kann als Identitätsfeld bezeichnet werden. Daher werden alle in dieses Feld erfassten Daten als Identitätsdaten betrachtet.

Identitätsfelder ermöglichen auch die Verknüpfung von Identitäten, wenn sie gemeinsame PII-Daten verwenden.
Wenn Sie beispielsweise Telefonnummernfelder als Identitätsfelder kennzeichnen, zeichnet der Identitätsdienst automatisch die Beziehungen zu den anderen Personen auf, bei denen festgestellt wurde, dass sie dieselbe Telefonnummer verwenden.

>[!NOTE] Der Namensraum der resultierenden Identitäten wird zum Zeitpunkt der Feldbeschriftung bereitgestellt.

### Datensatz für Identitätsdienst konfigurieren

Während der Streaming-Erfassung extrahiert der Identitätsdienst automatisch Identitätsdaten aus den Daten der Datensatz- und Zeitreihen. Bevor Daten jedoch erfasst werden können, müssen sie für den Identitätsdienst aktiviert werden. Weitere Informationen finden Sie im Lernprogramm zum [Konfigurieren eines Datasets für Echtzeit-Kunden- und Identitätsdienst mit APIs](../profile/tutorials/dataset-configuration.md) .

### Daten in den Identitätsdienst einbeziehen

Der Identitätsdienst nutzt XDM-konforme Daten, die entweder durch [Stapelverarbeitung](../ingestion/batch-ingestion/overview.md) oder [Streaming-Erfassung](../ingestion/streaming-ingestion/overview.md)an Experience Platform gesendet werden.

## Datenverwaltung

Die Adobe Experience Platform wurde unter Berücksichtigung der Privatsphäre entwickelt und enthält einen Rahmen zur Datenverwaltung, um Ihre Kunden-PII-Daten zu schützen. Identitätsdaten unter dem Namensraum &quot;email&quot;oder &quot;phone&quot;werden standardmäßig verschlüsselt. Um jedoch sicherzustellen, dass sensible Daten verschlüsselt werden, bevor sie bestehen bleiben, können Datenverwendungsbeschriftungen auf Daten angewendet werden, die bei der Erfassung oder beim Eintreffen in die Plattform erfasst werden. Weitere Informationen finden Sie in der Übersicht über die [Datenverwaltung](../data-governance/home.md).

## Nächste Schritte

Jetzt, da Sie die Schlüsselkonzepte des Identitätsdienstes und seiner Rolle in Experience Platform verstehen, können Sie mit der Arbeit mit Ihrem Identitätsdiagramm mithilfe der [Identitätsdienst-API](./api/getting-started.md)beginnen.