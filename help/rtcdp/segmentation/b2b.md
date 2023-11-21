---
title: Anwendungsfälle für die Segmentierung für Real-time Customer Data Platform B2B Edition
description: Ein Überblick über die verschiedenen Anwendungsfälle der Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Audiences, Segments, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 0%

---

# Anwendungsfälle für die Segmentierung für Real-time Customer Data Platform B2B Edition

Dieses Dokument enthält Beispiele für Segmentdefinitionen in Adobe Real-time Customer Data Platform B2B Edition und wie verschiedene Attributtypen für gängige B2B-Anwendungsfälle kombiniert werden können. Informationen dazu, wie Ziele in Ihren B2B-Workflow integriert werden können, finden Sie im Abschnitt [End-to-End-Tutorial](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Die für diese Anwendungsfälle der Segmentierung erforderlichen Attribute stehen nur Kunden von Real-time Customer Data Platform B2B Edition zur Verfügung. Wenn Sie Real-time Customer Data Platform B2B Edition nicht verwenden, lesen Sie den Abschnitt [Segmentierungsübersicht](./segmentation-overview.md) anstatt.

## Voraussetzungen {#prerequisites}

Bevor Sie die Segmentierungsattribute für B2B-Klassen verwenden können, müssen Sie die folgenden Schritte ausführen:

1. Erstellen Sie Schemas, die die B2B-Klassen verwenden. Die B2B Edition-Klassen umfassen Konto, Kampagne, Chancen, Marketingliste und mehr. Informationen über [Einrichten von Schemata zur Verwendung mit B2B-Klassen](../schemas/b2b.md) finden Sie in der Schemadokumentation.
1. Erstellen Sie Beziehungen zwischen Ihren Experience-Datenmodell (XDM) B2B-Schemas. Segmente, die auf B2B Edition-Attributen basieren, erfordern Beziehungen zwischen den Klassen, um die erweiterte Funktion zur B2B-Segmentierung vollständig zu nutzen. Siehe die Dokumentation unter [wie eine Beziehung zwischen zwei B2B-Schemas definiert wird](../../xdm/tutorials/relationship-b2b.md) für weitere Informationen.
1. Erfassen Sie Daten mithilfe von Datensätzen, die auf Ihren B2B-Schemas basieren. Weitere Informationen finden Sie in der Quelldokumentation für [Informationen zur Datenerfassung](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Lesen Sie die [Segment Builder-Benutzerhandbuch](../../segmentation/ui/segment-builder.md) für eine detailliertere Anleitung zum Erstellen von Zielgruppen.

Sobald diese Anforderungen erfüllt sind, können Sie diese Attribute für gängige B2B-Anwendungsfälle kombinieren.

## Erste Schritte {#getting-started}

Sobald die Vereinigungsschemas für die B2B-Klassen Beziehungen hergestellt haben und zum Erfassen von Daten verwendet wurden, werden ihre Attribute in der linken Leiste des Segment Builder verfügbar gemacht.

B2B-Klassen und ihre Attribute werden mit einem `B2B` im Arbeitsbereich &quot;Segmentierung&quot;, um sie von den in Real-time Customer Data Platform standardmäßig verfügbaren zu unterscheiden.

Um Zielgruppen für B2B-Anwendungsfälle effektiv erstellen zu können, ist es wichtig, über eine genaue Kenntnis des Schemas zu verfügen und zu verstehen, wie das Datenmodell aussieht. Beachten Sie auch den Pfad, den die Daten von einem Datenobjekt zum anderen führen.

Die folgende Abbildung zeigt die Beziehungen zwischen den B2B-Klassen, die in Real-Time CDP B2B Edition verfügbar sind.

![B2B-Klasse ERD](../assets/segmentation/b2b-classes.png)

Da Ihr Datenmodell kompliziert sein kann, können Sie über die Platform-Benutzeroberfläche eine detailliertere visuelle Darstellung Ihres Datenmodells anzeigen, um die relevanten Attribute für Ihren Anwendungsfall zu finden. Beginnen Sie mit der Platform-Benutzeroberfläche und wählen Sie im linken Navigationsbereich Schemas aus.

Wählen Sie das entsprechende Schema aus der verfügbaren Liste aus und wählen Sie die entsprechende Beziehung aus der [!UICONTROL Komposition] Seitenleiste. Im folgenden Beispiel zeigt die Auswahl der Beziehung &quot;Person&quot;an, welches Attribut im aktuellen Schema auf das zugehörige Schema &quot;Person&quot;verweist (wenn es das Quellschema in der Beziehung ist) oder durch das Schema &quot;Person&quot;referenziert wird (wenn es das Referenzschema in der Beziehung ist).

![Quellschlüsselbeispiel mithilfe der Personenbeziehung im Arbeitsbereich &quot;Schema&quot;](../assets/segmentation/source-key-schema-relationship-example.png)

Diese Beziehung wird im Segment Builder durch die Verwendung von `Key` Ordner wie in der Abbildung unten dargestellt.

![Quellschlüsselbeispiel zur Verwendung des Segment-Builders im Segmentierungsarbeitsbereich](../assets/segmentation/source-key-segmentation-example.png)

Weitere Informationen finden Sie unter [Schemata in der Dokumentation zu Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) für weitere Informationen zu den verfügbaren B2B-Klassen.

Die folgenden Anwendungsfälle liefern Informationen darüber, welche Klassen verwendet werden, um Beziehungen zwischen den verschiedenen Schemas herzustellen, um diese Ergebnisse zu erzielen. Diese Beispiele helfen Ihnen bei der Erstellung eigener Segmente.

## Beispiele für verschiedene Anwendungsfälle der Segmentierung {#use-cases}

Die folgenden Anwendungsfälle stehen für die Segmentierung mit der B2B Edition zur Verfügung. In jedem Beispiel wird beschrieben, was die Zielgruppe tut, und welche Klassen für die Erstellung verwendet wurden. Die bereitgestellten Bilder markieren den Dateipfad im [!UICONTROL Attribute] Seitenleiste, die die Struktur des Schemas widerspiegelt. Die [!UICONTROL Segmenteigenschaften] rechts neben der Anzeige eine schriftliche Aufschlüsselung der Attribute der Audience enthalten.

### Beispiel 1: Suche nach &quot;Entscheidungsträgern&quot;für B2B-Chancen {#find-decision-maker}

Finden Sie alle Menschen, die der &quot;Entscheidungsträger&quot;jeder Gelegenheit sind. Diese Zielgruppe erfordert eine Verknüpfung zwischen der [!UICONTROL Individuelles XDM-Profil] und [!UICONTROL XDM Business Opportunity-Personenbeziehung] -Klasse.

![Benutzeroberfläche mit Beispiel 1-Einstellungen](../assets/segmentation/example-1.png)

### Beispiel 2: Ermitteln von B2B-Profilen, die Chancen im Vergleich zu einem bestimmten Dollarbetrag erhalten {#find-opportunities-amount}

Finden Sie alle Personen, die direkt mit allen Möglichkeiten verbunden sind, deren Opportunitätsbetrag größer ist als der angegebene Betrag ($1 Million). Diese Zielgruppe erfordert eine Verknüpfung zwischen der [!UICONTROL Individuelles XDM-Profil] -Klasse, [!UICONTROL XDM Business Opportunity-Personenbeziehung] -Klasse und [!UICONTROL XDM-Geschäftschancen] -Klasse.

![Benutzeroberfläche mit Beispiel 2-Einstellungen](../assets/segmentation/example-2.png)

### Beispiel 3: Ermitteln von B2B-Profilen, die Chancen nach Standort zugewiesen sind {#find-opportunities-location}

Finden Sie alle Personen, die allen Möglichkeiten direkt zugewiesen sind, in denen sich das Konto an einem bestimmten Ort (Kanada) befindet. Diese Zielgruppe erfordert eine Verknüpfung zwischen der [!UICONTROL Individuelles XDM-Profil] -Klasse, [!UICONTROL XDM Business Opportunity-Personenbeziehung] -Klasse, [!UICONTROL XDM-Geschäftschancen] -Klasse und [!UICONTROL XDM-Geschäftskonto] -Klasse.

![Benutzeroberfläche mit Beispiel 3-Einstellungen](../assets/segmentation/example-3.png)

### Beispiel 4: Suche nach &quot;Entscheidungsträgern&quot;für Chancen nach Branche und Browsing-Verhalten {#find-industry-browsing-behavior}

Finden Sie alle Personen, die ein &quot;Entscheidungsträger&quot;sind, von jeder Gelegenheit, wo sich das Konto in der &quot;Finance&quot;-Branche befindet, und besuchten Sie die Preisseite in den letzten drei Tagen. Diese Zielgruppe erfordert eine Verknüpfung zwischen der [!UICONTROL Individuelles XDM-Profil] -Klasse, [!UICONTROL XDM Business Opportunity-Personenbeziehung] -Klasse, [!UICONTROL XDM-Geschäftschancen] -Klasse und [!UICONTROL XDM-Geschäftskonto] -Klasse und [!UICONTROL XDM ExperienceEvent] -Klasse.

![Benutzeroberfläche mit Beispiel 4-Einstellungen](../assets/segmentation/example-4.png)

### Beispiel 5: B2B-Profile nach Möglichkeiten nach Abteilungsname und Opportunitätsbetrag suchen {#find-department-opportunity-amount}

Finden Sie alle Personen, die in einer Personalabteilung arbeiten und über ein Konto verfügen, das mindestens eine offene Chance im Wert des angegebenen Betrags (1 Million Dollar) oder mehr hat. Diese Zielgruppe erfordert eine Verknüpfung zwischen der [!UICONTROL Individuelles XDM-Profil] -Klasse, [!UICONTROL XDM-Geschäftskonto] -Klasse und [!UICONTROL XDM-Geschäftschancen] -Klasse.

![Benutzeroberfläche mit Beispiel-5-Einstellungen](../assets/segmentation/example-5.png)

### Beispiel 6: B2B-Profile nach Berufsbezeichnung und Jahresumsatz ermitteln {#find-by-job-title-and-revenue}

Finden Sie alle Personen, deren Berufsbezeichnung Vizepräsident ist und die einen beliebigen Jahresumsatz von mindestens 100 Millionen Euro haben und die die Preisseite im letzten Monat mindestens dreimal besucht haben. Diese Zielgruppe erfordert eine Verknüpfung zwischen der [!UICONTROL Individuelles XDM-Profil] -Klasse, [!UICONTROL XDM-Geschäftskonto] -Klasse und [!UICONTROL XDM ExperienceEvent] -Klasse.

![Benutzeroberfläche mit Beispiel 6-Einstellungen](../assets/segmentation/example-6.png)

### Beispiel 7: &quot;Entscheidungsträger&quot;nach Opportunitätsstatus und Browsing-Verhalten suchen {#find-by-opportunity-status-and-browsing-behavior}

Finden Sie alle Personen, die ein &quot;Entscheidungsträger&quot;jeder verlorenen Gelegenheit sind und die Preisseite in der letzten Woche besucht haben. Diese Zielgruppe erfordert eine Verknüpfung zwischen der [!UICONTROL Individuelles XDM-Profil] -Klasse, [!UICONTROL XDM Business Opportunity-Personenbeziehung] -Klasse, [!UICONTROL XDM-Geschäftschancen] -Klasse und [!UICONTROL XDM ExperienceEvent] -Klasse.

![Benutzeroberfläche mit Beispiel 7-Einstellungen](../assets/segmentation/example-7.png)

### Beispiel 8: Verwenden verwandter Konten zum Erweitern der Segmentierungsreichweite {#related-accounts}

Finden Sie alle Personen, die in einer Personalabteilung (HR) arbeiten und mit einem beliebigen Konto in Verbindung stehen. *oder eines der damit verbundenen Konten* die mindestens eine offene Chance im Wert des angegebenen Betrags (1 Million Dollar) oder mehr hat. Diese Zielgruppe erfordert eine Verknüpfung zwischen der [!UICONTROL Individuelles XDM-Profil] -Klasse, [!UICONTROL XDM-Geschäftskonto] -Klasse und [!UICONTROL XDM-Geschäftschancen] -Klasse.

![Benutzeroberfläche zur Segmentierung verwandter Konten](../assets/segmentation/example-8.png)

### Beispiel 9: Nutzen Sie Lead-Bewertungen und/oder Kontobewertungen zur Profilqualifizierung {#account-scoring}

Finden Sie alle Profile mit einem Lead-Ergebnis über 80.

![Benutzeroberfläche mit Segmentierung für prädiktive Lead- und Kontobewertung](../assets/segmentation/example-9.png)

### Beispiel 10: Suchen Sie nach B2B-Profilen, die mit Konten verknüpft sind, deren übergeordnete Organisation über einen bestimmten Dollarbetrag Umsatz verfügt {#find-parent-org-amount}

Finden Sie alle Personen, die mit Konten verknüpft sind, deren übergeordnete Organisation einen Umsatz hat, der über dem angegebenen Betrag liegt ($100.000.000).

![Benutzeroberfläche mit übergeordneter Segmentierungsorganisation](../assets/segmentation/example-10.png)

### Beispiel 11: B2B-Profile nach Berufsbezeichnung und Kontoname mit aktiver Beziehung suchen {#find-by-job-title-and-account-name}

Suchen Sie alle Personen, die ein &quot;Manager&quot;sind, im Konto &quot;Acme&quot;, wobei die Kontobeziehung &quot;aktiv&quot;ist.

![Benutzeroberfläche mit übergeordneter Segmentierungsorganisation](../assets/segmentation/example-11.png)

### Beispiel 12: Finden Sie B2B-Profile für Kampagnen, bei denen die tatsächlichen Kosten die budgetedCost übersteigen. {#find-actualcost-exceed-budgetcost}

Finden Sie alle Personen, die für Kampagnen angesprochen werden, bei denen die tatsächlichen Kosten die budgetedCost überstiegen haben.

![Benutzeroberfläche mit übergeordneter Segmentierungsorganisation](../assets/segmentation/example-12.png)

### Beispiel 13: Suchen Sie nach B2B-Profilen, die zu einer statischen Marketo-Liste gehören, und isDeleted=false {#find-marketo-static-list}

Suchen Sie alle Personen, die zur statischen Marketo-Liste &quot;Jubiläumsbenutzer&quot;gehören, wobei isDeleted=false lautet.

![Benutzeroberfläche mit übergeordneter Segmentierungsorganisation](../assets/segmentation/example-13.png)

## Nächste Schritte {#next-steps}

Nach der Lektüre dieser Übersicht haben Sie jetzt ein Verständnis der Segmentierungsmöglichkeiten, die mit Real-Time CDP, B2B Edition verfügbar sind. Weitere Informationen zum Segmentierungsdienst finden Sie in der [Dokumentation zur Segmentierung](../../segmentation/home.md).
