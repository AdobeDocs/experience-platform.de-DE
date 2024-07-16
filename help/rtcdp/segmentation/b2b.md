---
title: Anwendungsfälle für die Segmentierung für Real-time Customer Data Platform B2B Edition
description: Ein Überblick über die verschiedenen Anwendungsfälle der Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Audiences, Segments, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 8a487d948d2eb7db167298b61045ef8dd2099da6
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# Anwendungsfälle für die Segmentierung für Real-time Customer Data Platform B2B Edition

Dieses Dokument enthält Beispiele für Segmentdefinitionen in Adobe Real-time Customer Data Platform B2B Edition und wie verschiedene Attributtypen für gängige B2B-Anwendungsfälle kombiniert werden können. Informationen dazu, wie Ziele in Ihren B2B-Workflow passen, finden Sie im [End-to-End-Tutorial](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Die für diese Anwendungsfälle der Segmentierung erforderlichen Attribute stehen nur Kunden von Real-time Customer Data Platform B2B Edition zur Verfügung. Wenn Sie Real-time Customer Data Platform B2B Edition nicht verwenden, lesen Sie stattdessen die [Segmentierungsübersicht](./segmentation-overview.md) .

## Voraussetzungen {#prerequisites}

Bevor Sie die Segmentierungsattribute für B2B-Klassen verwenden können, müssen Sie die folgenden Schritte ausführen:

1. Erstellen Sie Schemas, die die B2B-Klassen verwenden. Die B2B Edition-Klassen umfassen Konto, Kampagne, Chancen, Marketingliste und mehr. Informationen zu [Einrichten von Schemas für die Verwendung mit B2B-Klassen](../schemas/b2b.md) finden Sie in der Schemadokumentation.
2. Erstellen Sie Beziehungen zwischen Ihren Experience-Datenmodell (XDM) B2B-Schemas. Zielgruppen, die auf B2B Edition-Attributen basieren, erfordern Beziehungen zwischen den Klassen, um die erweiterte Funktion zur B2B-Segmentierung vollständig zu nutzen. Weitere Informationen finden Sie in der Dokumentation zu [Definieren einer Beziehung zwischen zwei B2B-Schemas](../../xdm/tutorials/relationship-b2b.md) .
3. Erfassen Sie Daten mithilfe von Datensätzen, die auf Ihren B2B-Schemas basieren. Informationen zum Erfassen von Daten finden Sie in der Quelldokumentation für [ .](../../sources/connectors/adobe-applications/marketo/marketo.md)
4. Weitere Informationen zum Erstellen von Zielgruppen finden Sie im [Segment Builder-Benutzerhandbuch](../../segmentation/ui/segment-builder.md) .

Sobald diese Anforderungen erfüllt sind, können Sie diese Attribute für gängige B2B-Anwendungsfälle kombinieren.

## Erste Schritte {#getting-started}

Sobald die Vereinigungsschemas für die B2B-Klassen Beziehungen hergestellt haben und zum Erfassen von Daten verwendet wurden, werden ihre Attribute in der linken Leiste des Segment Builder verfügbar gemacht.

B2B-Klassen und ihre Attribute werden mit einer `B2B` -Beschriftung im Segmentierungsarbeitsbereich angehängt, um sie von den in Real-time Customer Data Platform standardmäßig verfügbaren Klassen zu unterscheiden.

Um Zielgruppen für B2B-Anwendungsfälle effektiv erstellen zu können, ist es wichtig, über eine genaue Kenntnis des Schemas zu verfügen und zu verstehen, wie das Datenmodell aussieht. Beachten Sie auch den Pfad, den die Daten von einem Datenobjekt zum anderen führen.

Die folgende Abbildung zeigt die Beziehungen zwischen den B2B-Klassen, die in Real-Time CDP B2B Edition verfügbar sind.

![B2B-Klasse ERD](../assets/segmentation/b2b-classes.png)

Da Ihr Datenmodell kompliziert sein kann, können Sie über die Platform-Benutzeroberfläche eine detailliertere visuelle Darstellung Ihres Datenmodells anzeigen, um die relevanten Attribute für Ihren Anwendungsfall zu finden. Beginnen Sie mit der Platform-Benutzeroberfläche und wählen Sie im linken Navigationsbereich Schemas aus.

Wählen Sie das entsprechende Schema aus der verfügbaren Liste aus und wählen Sie die entsprechende Beziehung aus der Seitenleiste [!UICONTROL Komposition] aus. Im folgenden Beispiel zeigt die Auswahl der Beziehung &quot;Person&quot;an, welches Attribut im aktuellen Schema auf das zugehörige Schema &quot;Person&quot;verweist (wenn es das Quellschema in der Beziehung ist) oder durch das Schema &quot;Person&quot;referenziert wird (wenn es das Referenzschema in der Beziehung ist).

![Beispiel für Quell-Schlüssel bei Verwendung der Personenbeziehung im Schema-Arbeitsbereich](../assets/segmentation/source-key-schema-relationship-example.png)

Diese Beziehung spiegelt sich im Segment Builder durch die Verwendung von `Key` -Ordnern wider, wie in der Abbildung unten dargestellt.

![Quell-Key-Beispiel für die Verwendung des Segment-Builders im Segmentierungsarbeitsbereich](../assets/segmentation/source-key-segmentation-example.png)

Weitere Informationen zu den verfügbaren B2B-Klassen finden Sie in der Dokumentation zu den [Schemas in der Real-time Customer Data Platform B2B Edition-Dokumentation](../schemas/b2b.md) .

Die folgenden Anwendungsfälle liefern Informationen darüber, welche Klassen verwendet werden, um Beziehungen zwischen den verschiedenen Schemas herzustellen, um diese Ergebnisse zu erzielen. Anhand dieser Beispiele können Sie Ihre eigenen Zielgruppen erstellen.

## Beispiele für verschiedene Anwendungsfälle der Segmentierung {#use-cases}

Die folgenden Anwendungsfälle stehen für die Segmentierung mit der B2B Edition zur Verfügung. In jedem Beispiel wird beschrieben, was die Zielgruppe tut, und welche Klassen für die Erstellung verwendet wurden. Die bereitgestellten Bilder markieren den Dateipfad in der Seitenleiste [!UICONTROL Attribute] , die die Struktur des Schemas widerspiegelt. Der Abschnitt [!UICONTROL Segmenteigenschaften] rechts neben der Anzeige enthält eine schriftliche Aufschlüsselung der Attribute der Zielgruppe.

### Beispiel 1: Suche nach &quot;Entscheidungsträgern&quot;für B2B-Chancen {#find-decision-maker}

Finden Sie alle Menschen, die der &quot;Entscheidungsträger&quot;jeder Gelegenheit sind. Diese Zielgruppe erfordert eine Verknüpfung zwischen der Klasse [!UICONTROL XDM Individual Profile] und der Klasse [!UICONTROL XDM Business Opportunity Person Relation] .

![UI, die Beispiel 1-Einstellungen anzeigt](../assets/segmentation/example-1.png)

### Beispiel 2: Ermitteln von B2B-Profilen, die Chancen im Vergleich zu einem bestimmten Dollarbetrag erhalten {#find-opportunities-amount}

Finden Sie alle Personen, die direkt mit allen Möglichkeiten verbunden sind, deren Opportunitätsbetrag größer ist als der angegebene Betrag ($1 Million). Diese Zielgruppe erfordert eine Verknüpfung zwischen der Klasse [!UICONTROL XDM Individual Profile] , der Klasse [!UICONTROL XDM Business Opportunity Person Relation] und der Klasse [!UICONTROL XDM Business Opportunity] .

![UI, die Beispiel 2-Einstellungen anzeigt](../assets/segmentation/example-2.png)

### Beispiel 3: Ermitteln von B2B-Profilen, die Chancen nach Standort zugewiesen sind {#find-opportunities-location}

Finden Sie alle Personen, die allen Möglichkeiten direkt zugewiesen sind, in denen sich das Konto an einem bestimmten Ort (Kanada) befindet. Diese Zielgruppe erfordert eine Verknüpfung zwischen der Klasse [!UICONTROL XDM Individual Profile] , der Klasse [!UICONTROL XDM Business Opportunity Person Relation] , der Klasse [!UICONTROL XDM Business Opportunity] und der Klasse [!UICONTROL XDM Business Account] .

![UI mit Beispiel 3-Einstellungen](../assets/segmentation/example-3.png)

### Beispiel 4: Suche nach &quot;Entscheidungsträgern&quot;für Chancen nach Branche und Browsing-Verhalten {#find-industry-browsing-behavior}

Finden Sie alle Personen, die ein &quot;Entscheidungsträger&quot;sind, von jeder Gelegenheit, wo sich das Konto in der &quot;Finance&quot;-Branche befindet, und besuchten Sie die Preisseite in den letzten drei Tagen. Diese Zielgruppe erfordert eine Verknüpfung zwischen der Klasse [!UICONTROL XDM Individual Profile] , der Klasse [!UICONTROL XDM Business Opportunity Person Relation] , der Klasse [!UICONTROL XDM Business Opportunity] und der Klasse [!UICONTROL XDM Business Account] und der Klasse [!UICONTROL XDM ExperienceEvent] .

![UI mit Beispiel 4-Einstellungen](../assets/segmentation/example-4.png)

### Beispiel 5: B2B-Profile nach Möglichkeiten nach Abteilungsname und Opportunitätsbetrag suchen {#find-department-opportunity-amount}

Finden Sie alle Personen, die in einer Personalabteilung arbeiten und über ein Konto verfügen, das mindestens eine offene Chance im Wert des angegebenen Betrags (1 Million Dollar) oder mehr hat. Diese Zielgruppe erfordert eine Verknüpfung zwischen der Klasse [!UICONTROL XDM Individual Profile] , der Klasse [!UICONTROL XDM Business Account] und der Klasse [!UICONTROL XDM Business Opportunity] .

![UI mit Beispiel-5-Einstellungen](../assets/segmentation/example-5.png)

### Beispiel 6: B2B-Profile nach Berufsbezeichnung und Jahresumsatz ermitteln {#find-by-job-title-and-revenue}

Finden Sie alle Personen, deren Berufsbezeichnung Vizepräsident ist und die einen beliebigen Jahresumsatz von mindestens 100 Millionen Euro haben und die die Preisseite im letzten Monat mindestens dreimal besucht haben. Diese Zielgruppe erfordert eine Verknüpfung zwischen der Klasse [!UICONTROL XDM Individual Profile] , der Klasse [!UICONTROL XDM Business Account] und der Klasse [!UICONTROL XDM ExperienceEvent] .

![UI mit Beispiel 6-Einstellungen](../assets/segmentation/example-6.png)

### Beispiel 7: &quot;Entscheidungsträger&quot;nach Opportunitätsstatus und Browsing-Verhalten suchen {#find-by-opportunity-status-and-browsing-behavior}

Finden Sie alle Personen, die ein &quot;Entscheidungsträger&quot;jeder verlorenen Gelegenheit sind und die Preisseite in der letzten Woche besucht haben. Diese Zielgruppe erfordert eine Verknüpfung zwischen der Klasse [!UICONTROL XDM Individual Profile] , der Klasse [!UICONTROL XDM Business Opportunity Person Relation] , der Klasse [!UICONTROL XDM Business Opportunity] und der Klasse [!UICONTROL XDM ExperienceEvent] .

![UI mit Beispiel 7-Einstellungen](../assets/segmentation/example-7.png)

### Beispiel 8: Verwenden verwandter Konten zum Erweitern der Segmentierungsreichweite {#related-accounts}

Finden Sie alle Personen, die in einer Personalabteilung (HR) arbeiten und mit einem Konto *oder einem verwandten Konto* des Kontos verbunden sind, das mindestens eine offene Chance im Wert des angegebenen Betrags ($1 Million) oder mehr hat. Diese Zielgruppe erfordert eine Verknüpfung zwischen der Klasse [!UICONTROL XDM Individual Profile] , der Klasse [!UICONTROL XDM Business Account] und der Klasse [!UICONTROL XDM Business Opportunity] .

![UI, die die Segmentierung für verwandte Konten anzeigt](../assets/segmentation/example-8.png)

### Beispiel 9: Nutzen Sie Lead-Bewertungen und/oder Kontobewertungen zur Profilqualifizierung {#account-scoring}

Finden Sie alle Profile mit einem Lead-Ergebnis über 80.

![UI, die die Segmentierung für die prädiktive Lead- und Kontobewertung anzeigt](../assets/segmentation/example-9.png)

### Beispiel 10: Suchen Sie nach B2B-Profilen, die mit Konten verknüpft sind, deren übergeordnete Organisation über einen bestimmten Dollarbetrag Umsatz verfügt {#find-parent-org-amount}

Finden Sie alle Personen, die mit Konten verknüpft sind, deren übergeordnete Organisation einen Umsatz hat, der über dem angegebenen Betrag liegt ($100.000.000).

![UI, die die übergeordnete Segmentierung der Segmentierung anzeigt](../assets/segmentation/example-10.png)

### Beispiel 11: B2B-Profile nach Berufsbezeichnung und Kontoname mit aktiver Beziehung suchen {#find-by-job-title-and-account-name}

Suchen Sie alle Personen, die ein &quot;Manager&quot;sind, im Konto &quot;Acme&quot;, wobei die Kontobeziehung &quot;aktiv&quot;ist.

![UI, die die übergeordnete Segmentierung der Segmentierung anzeigt](../assets/segmentation/example-11.png)

### Beispiel 12: Finden Sie B2B-Profile für Kampagnen, bei denen die tatsächlichen Kosten die budgetedCost übersteigen. {#find-actualcost-exceed-budgetcost}

Finden Sie alle Personen, die für Kampagnen angesprochen werden, bei denen die tatsächlichen Kosten die budgetedCost überstiegen haben.

![UI, die die übergeordnete Segmentierung der Segmentierung anzeigt](../assets/segmentation/example-12.png)

### Beispiel 13: Suchen Sie nach B2B-Profilen, die zu einer statischen Marketo-Liste gehören, und isDeleted=false {#find-marketo-static-list}

Suchen Sie alle Personen, die zur statischen Marketo-Liste &quot;Jubiläumsbenutzer&quot;gehören, wobei isDeleted=false lautet.

![UI, die die übergeordnete Segmentierung der Segmentierung anzeigt](../assets/segmentation/example-13.png)

## Nächste Schritte {#next-steps}

Nach der Lektüre dieser Übersicht haben Sie jetzt ein Verständnis der Segmentierungsmöglichkeiten, die mit Real-Time CDP, B2B Edition verfügbar sind. Weitere Informationen zum Segmentierungsdienst finden Sie in der [Dokumentation zur Segmentierung](../../segmentation/home.md) .
