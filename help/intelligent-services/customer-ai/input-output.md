---
keywords: Experience Platform;Erste Schritte;Kundenhilfe;beliebte Themen;Kundenai-Eingabe;Kundenai-Ausgabe
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Eingabe und Ausgabe in der Kundentechnik
topic-legacy: Getting started
description: Erfahren Sie mehr über die erforderlichen Ereignis, Eingaben und Ausgaben, die von der KUNDENKI verwendet werden.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2876'
ht-degree: 13%

---

# Eingabe und Ausgabe in der Kundentransfer-API

Im folgenden Dokument werden die verschiedenen erforderlichen Ereignis, Eingaben und Ausgaben erläutert, die in der Kundentechnik verwendet werden.

## Erste Schritte

Die Kunden-AI analysiert einen der folgenden Datensätze, um die Ergebnisse der Kurn- oder Konversionsintensität vorherzusagen:

- Consumer Experience Ereignis (CEE)-Datensatz
- Adobe Analytics-Daten mit [Analytics-Quellanschluss](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager-Daten mit dem [Audience Manager-Quellanschluss](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>Die Aufstockung der Daten über die Quellanschlüsse dauert bis zu vier Wochen. Wenn Sie kürzlich einen Connector eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die für die Kunden-API erforderliche Mindestlänge aufweist. Überprüfen Sie anhand der Informationen im Abschnitt [Verlaufsdaten](#data-requirements), ob Sie über genügend Daten für Ihr Prognoseziel verfügen.

Dieses Dokument erfordert ein grundlegendes Verständnis des CEE-Schemas. Bitte lesen Sie die [Dokumentation zur Datenvorbereitung für intelligente Dienste](../data-preparation.md), bevor Sie fortfahren.

In der folgenden Tabelle sind einige häufig verwendete Terminologie für dieses Dokument aufgeführt:

| Begriff | Definition |
| --- | --- |
| [Experience-Datenmodell (XDM)](../../xdm/home.md) | XDM ist das Fundament, das es Adobe Experience Cloud, powered by Adobe Experience Platform, ermöglicht, die richtige Botschaft an die richtige Person, auf dem richtigen Kanal, genau im richtigen Moment zu senden. Das XDM-System ist die Methode, auf der Experience Platform basiert. Es stellt Experience-Datenmodell-Schemata zur Verwendung durch Platform-Dienste bereit. |
| XDM-Schema | Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, die Bedeutung beizubehalten und somit Wert aus Daten zu ziehen. Bevor Daten in Plattform aufgenommen werden können, muss ein Schema zusammengestellt werden, um die Datenstruktur zu beschreiben und Beschränkungen für den Datentyp bereitzustellen, der in den einzelnen Feldern enthalten sein kann. Schema bestehen aus einer XDM-Basisklasse und Null oder mehr Mixins. |
| XDM-Klasse | Alle XDM-Schemas beschreiben Daten, die als Datensatz- oder Zeitreihen kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen beschreiben die kleinste Anzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten darzustellen. |
| [Mixins](../../xdm/schema/composition.md) | Eine Komponente, die ein oder mehrere Felder in einem Schema definiert. Mixins erzwingen, wie die Felder in der Hierarchie des Schemas angezeigt werden, und weisen daher in jedem Schema dieselbe Struktur auf, in dem sie enthalten sind. Mixins sind nur mit bestimmten Klassen kompatibel, die durch ihr `meta:intendedToExtend`-Attribut gekennzeichnet sind. |
| [Datentyp](../../xdm/schema/composition.md) | Eine Komponente, die auch ein oder mehrere Felder für ein Schema bereitstellen kann. Im Gegensatz zu Mixins sind Datentypen jedoch nicht auf eine bestimmte Klasse beschränkt. Dadurch werden Datentypen flexibler, um häufig verwendete Datenstrukturen zu beschreiben, die über mehrere Schema mit potenziell unterschiedlichen Klassen hinweg wiederverwendet werden können. Die in diesem Dokument beschriebenen Datentypen werden sowohl von den mittel- als auch von den Adobe Analytics-Schemas unterstützt. |
| Churn | Eine Messung des Prozentsatzes der Konten, die ihre Abonnements stornieren oder nicht verlängern. Eine hohe Rate der Abwanderung kann sich negativ auf den monatlichen wiederkehrenden Umsatz (MRR) auswirken und auch auf Unzufriedenheit mit einem Produkt oder einer Dienstleistung hindeuten. |
| [Echtzeit-Kundenprofil](../../profile/home.md) | Echtzeit-Customer-Profil bietet ein zentrales Profil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die über alle Systeme aggregiert werden, sowie umsetzbare Zeitstempelkonten von Ereignissen, an denen die Einzelperson beteiligt ist, die in einem der mit der Experience Platform verwendeten Systeme aufgetreten sind. |

## Daten zur Kundenaktieneingabe

>[!TIP]
>
> Die KUNDENKI ermittelt automatisch, welche Ereignis für Prognosen nützlich sind, und gibt eine Warnung aus, wenn die verfügbaren Daten nicht ausreichen, um Qualitätsprognosen zu erstellen.

Kunden-AI unterstützt Datasets von CEE, Adobe Analytics und Adobe Audience Manager. Das CEE-Schema erfordert, dass Sie Mixins während der Erstellung des Schemas hinzufügen. Wenn Sie Adobe Analytics- oder Adobe Audience Manager-Datensätze verwenden, ordnet der Quell-Connector direkt die standardmäßigen Ereignis (Commerce, Webseitendetails, Anwendung und Suche) zu, die während des Verbindungsprozesses unten aufgeführt werden.

Weitere Informationen zum Zuordnen von Adobe Analytics-Daten oder Audience Manager-Daten finden Sie im Handbuch [Analytics field mappings](../../sources/connectors/adobe-applications/analytics.md) oder [Audience Manager field mappings](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

### Standardmäßige Ereignis, die von der Kundenunterstützung verwendet werden{#standard-events}

XDM Experience Ereignisses werden zur Bestimmung verschiedener Kundenverhalten verwendet. Je nachdem, wie Ihre Daten strukturiert sind, umfassen die unten aufgeführten Ereignistypen möglicherweise nicht alle Verhaltensweisen Ihres Kunden. Es liegt an Ihnen, zu bestimmen, welche Felder über die erforderlichen Daten verfügen, um die Aktivität von Webbenutzern eindeutig und eindeutig zu identifizieren. Je nach Prognoseziel können sich die erforderlichen Felder ändern.

Die Kundenunterstützung nutzt verschiedene Ereignistyp zum Erstellen von Modellfunktionen. Diese Ereignistyp werden automatisch mit mehreren XDM-Mixins zu Ihrem Schema hinzugefügt.

>[!NOTE]
>
>Wenn Sie Adobe Analytics- oder Adobe Audience Manager-Daten verwenden, wird das Schema automatisch mit den für die Datenerfassung erforderlichen Standard-Ereignissen erstellt. Wenn Sie ein eigenes benutzerdefiniertes CEE-Schema zur Datenerfassung erstellen, müssen Sie überlegen, welche Mixins zur Datenerfassung erforderlich sind.

Es ist nicht erforderlich, Daten für jedes der unten aufgeführten Standardszenarien zu haben, aber für bestimmte Ereignis sind bestimmte Ereignis erforderlich. Wenn Sie über Standarddaten für Ereignis verfügen, sollten Sie diese in Ihr Schema aufnehmen. Wenn Sie z. B. eine Customer AI-Anwendung zum Vorhersagen von Kaufdaten erstellen möchten, ist es sinnvoll, Daten aus den Datentypen `Commerce` und `Web page details` zu haben.

Um ein Mixin in der Plattform-Benutzeroberfläche Ansicht, wählen Sie auf der linken Leiste die Registerkarte **[!UICONTROL Schema]** und anschließend die Registerkarte **[!UICONTROL Mixins]**.


| Mixin | Ereignistyp | XDM-Feldpfad |
| --- | --- | --- |
| [!UICONTROL Commerce-Details] | order | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | checkouts | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | purchases | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Webdetails] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Anwendungsdetails] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstallalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Suchdetails] | search | search.keywords |

Darüber hinaus kann die Kundenunterstützung mithilfe von Abonnement-Daten bessere Kanzmodelle erstellen. Für jedes Profil werden Abonnement-Daten mit dem Datentypformat [[!UICONTROL Abonnement]](../../xdm/data-types/subscription.md) benötigt. Die meisten Felder sind optional. Es wird jedoch dringend empfohlen, Daten für so viele Felder wie möglich bereitzustellen, z. B. `startDate`, `endDate` und andere relevante Details.

### Historische Daten {#data-requirements}

Für die Kunden-API sind historische Daten für die Modellschulung erforderlich. Die erforderliche Datenmenge basiert jedoch auf zwei Schlüsselelementen: Ergebnisfenster und förderfähige Bevölkerung.

Standardmäßig sucht die Kunden-API, ob ein Benutzer in den letzten 120 Tagen Aktivität hatte, wenn während der Anwendungskonfiguration keine geeignete Populationsdefinition angegeben wurde. Darüber hinaus erfordert die KUNDENKUNDENKRANKHEIT mindestens 500 qualifizierte und 500 nicht qualifizierte Ereignisse (insgesamt 1000) historische Daten, die auf einer voraussichtlichen Zieldefinition basieren.

In den folgenden Beispielen wird eine einfache Formel verwendet, mit der Sie die erforderliche Mindestdatenmenge festlegen können. Wenn Sie mehr als die Mindestanforderung haben, liefert Ihr Modell wahrscheinlich genauere Ergebnisse. Wenn Sie weniger als den erforderlichen Mindestwert haben, schlägt das Modell fehl, da für die Modellschulung nicht genügend Daten vorhanden sind.

**Formel**:

Mindestlänge der erforderlichen Daten = förderfähige Bevölkerung + Ergebnisfenster

>[!NOTE]
>
> 30 ist die Mindestanzahl Tage, die für die förderfähige Bevölkerung erforderlich ist. Wenn dies nicht angegeben wird, ist der Standardwert 120 Tage.

Beispiele :

- Sie möchten vorhersagen, ob ein Kunde in den nächsten 30 Tagen wahrscheinlich eine Uhr kaufen wird. Sie möchten außerdem Benutzer bewerten, die in den letzten 60 Tagen über eine gewisse Aktivität im Internet verfügen. In diesem Fall ist die Mindestdatenlänge = 60 Tage + 30 Tage erforderlich. Die förderfähige Bevölkerung beträgt 60 Tage, das Ergebnisfenster insgesamt 90 Tage.

- Sie möchten vorhersagen, ob der Benutzer in den nächsten 7 Tagen wahrscheinlich eine Uhr kaufen wird. In diesem Fall ist die Mindestdatenlänge = 120 Tage + 7 Tage erforderlich. Die förderfähige Bevölkerung beträgt standardmäßig 120 Tage und das Ergebnisfenster insgesamt 127 Tage.

- Sie möchten vorhersagen, ob der Kunde in den nächsten 7 Tagen wahrscheinlich eine Uhr kaufen wird. Sie möchten außerdem Benutzer bewerten, die in den letzten 7 Tagen über eine gewisse Aktivität im Internet verfügen. In diesem Fall ist die Mindestdatenlänge = 30 Tage + 7 Tage erforderlich. Die förderfähige Bevölkerung benötigt mindestens 30 Tage und das Ergebnisfenster beträgt 7 Tage und insgesamt 37 Tage.

Zusätzlich zu den erforderlichen Mindestdaten funktioniert die Kundentreueanweisung auch am besten mit aktuellen Daten. In diesem Anwendungsfall erstellt die Kunden-API eine Prognose für die Zukunft, die auf den neuesten Verhaltensdaten eines Benutzers basiert. Mit anderen Worten: Jüngere Daten werden wahrscheinlich eine genauere Prognose liefern.

### Beispielszenarios

In diesem Abschnitt werden verschiedene Szenarien für Kunden-AI-Instanzen sowie die erforderlichen und empfohlenen Ereignistyp beschrieben. Weitere Informationen zum Mixin und seinem Feldpfad finden Sie in der obigen Tabelle [Standard-Ereignisse](#standard-events).

>[!NOTE]
>
> Erforderliche Ereignistyp werden verwendet, um die Aktivität von Webbenutzern eindeutig und eindeutig zu identifizieren. Die Anzahl der erforderlichen Ereignistyp ändert sich je nach Prognoseziel und -struktur Ihres Schemas. Wenn Sie sich nicht sicher sind, ob ein bestimmter Ereignistyp erforderlich ist, sollten Sie diesen Ereignistyp beim Aufbau Ihres CEE-Schemas einbeziehen. Wenn Sie Adobe Analytics- oder Adobe Audience Manager-Daten verwenden, sollten die erforderlichen Standard-Ereignis je nach Streaming-Daten verfügbar sein.

### Szenario 1: Kaufkonversion auf einer E-Commerce-Website für den Einzelhandel

**Prognoseziel:** Prognostizieren Sie die Konversionstendenz für die in Frage kommenden Profile, einen bestimmten Bekleidungsartikel auf einer Website zu erwerben.

**Erforderliche Standard-Ereignistyp:**

Die unten aufgeführten Ereignistypen sind für eine optimale Kundenachvermessung mit diesem bestimmten Prognoseziel erforderlich. Es ist möglich, ein erforderliches Ereignis je nach Prognoseziel auszuschließen, allerdings kann das Ausschließen mehrerer Ereignis zu schlechten Ergebnissen führen.

- bestellen
- Checkouts
- Einkäufe
- webVisit
- search

**Zusätzliche empfohlene Standard-Ereignistyp:**

Die verbleibenden [Ereignistyp](#standard-events) können je nach Komplexität des Ziels und der für die Aktivierung infrage kommenden Population beim Konfigurieren der Customer AI-Instanz erforderlich sein. Wenn die Daten für einen bestimmten Datentyp verfügbar sind, wird empfohlen, diese Daten in Ihr Schema aufzunehmen.

### Szenario 2: Konvertierung von Abonnements auf einer Website des Medienstreaming-Dienstes

**Prognoseziel:** Prognostizieren Sie, dass sich die förderfähigen Profile einer bestimmten Abonnement-Stufe, wie z. B. einem Standard- oder einem Premium-Abonnement, verpflichten.

**Erforderliche Standard-Ereignistyp:**

Die unten aufgeführten Ereignistypen sind für eine optimale Kundenachvermessung mit diesem bestimmten Prognoseziel erforderlich. Es ist möglich, ein erforderliches Ereignis je nach Prognoseziel auszuschließen, allerdings kann das Ausschließen mehrerer Ereignis zu schlechten Ergebnissen führen.

- bestellen
- Checkouts
- Einkäufe
- webVisit
- search

In diesem Beispiel werden `order`, `checkouts` und `purchases` verwendet, um anzugeben, dass ein Abonnement gekauft wurde und dessen Typ.

Für ein genaues Abonnement wird außerdem empfohlen, einige der verfügbaren Eigenschaften des Datentyps [a1/> zu verwenden.](../../xdm/data-types/subscription.md)

**Zusätzliche empfohlene Standard-Ereignistyp:**

Die verbleibenden [Ereignistyp](#standard-events) können je nach Komplexität des Ziels und der für die Aktivierung infrage kommenden Population beim Konfigurieren der Customer AI-Instanz erforderlich sein. Wenn die Daten für einen bestimmten Datentyp verfügbar sind, wird empfohlen, diese Daten in Ihr Schema aufzunehmen.

### Szenario 3: Churn auf einer E-Commerce-Website

**Prognoseziel:** Vorhersagen der Wahrscheinlichkeit, dass ein Ereignis nicht eintritt

**Erforderliche Standard-Ereignistyp:**

Die unten aufgeführten Ereignistypen sind für eine optimale Kundenachvermessung mit diesem bestimmten Prognoseziel erforderlich. Es ist möglich, ein erforderliches Ereignis je nach Prognoseziel auszuschließen, allerdings kann das Ausschließen mehrerer Ereignis zu schlechten Ergebnissen führen.

- bestellen
- Checkouts
- Einkäufe
- webVisit
- search

**Zusätzliche empfohlene Standard-Ereignistyp:**

Die verbleibenden [Ereignistyp](#standard-events) können je nach Komplexität des Ziels und der für die Aktivierung infrage kommenden Population beim Konfigurieren der Customer AI-Instanz erforderlich sein. Wenn die Daten für einen bestimmten Datentyp verfügbar sind, wird empfohlen, diese Daten in Ihr Schema aufzunehmen.

### Szenario 4: Upsell-Konvertierung auf einer E-Commerce-Website

**Prognoseziel:** Prognostizieren Sie die Kaufneigung der Bevölkerung, die ein bestimmtes Produkt gekauft hat, zum Kauf eines neuen verwandten Produkts.

**Erforderliche Standard-Ereignistyp:**

Die unten aufgeführten Ereignistypen sind für eine optimale Kundenachvermessung mit diesem bestimmten Prognoseziel erforderlich. Es ist möglich, ein erforderliches Ereignis je nach Prognoseziel auszuschließen, allerdings kann das Ausschließen mehrerer Ereignis zu schlechten Ergebnissen führen.

- bestellen
- Checkouts
- Einkäufe
- webVisit
- search

**Zusätzliche empfohlene Standard-Ereignistyp:**

Die verbleibenden [Ereignistyp](#standard-events) können je nach Komplexität des Ziels und der für die Aktivierung infrage kommenden Population beim Konfigurieren der Customer AI-Instanz erforderlich sein. Wenn die Daten für einen bestimmten Datentyp verfügbar sind, wird empfohlen, diese Daten in Ihr Schema aufzunehmen.

### Szenario 5: Abbestellen (churn) auf einer Online-Nachrichtenseite

**Prognoseziel:** Prognostizieren Sie die Tendenz der förderfähigen Bevölkerung, sich im nächsten Monat von einem Dienst abzumelden.

**Erforderliche Standard-Ereignistyp:**

Die unten aufgeführten Ereignistypen sind für eine optimale Kundenachvermessung mit diesem bestimmten Prognoseziel erforderlich. Es ist möglich, ein erforderliches Ereignis je nach Prognoseziel auszuschließen, allerdings kann das Ausschließen mehrerer Ereignis zu schlechten Ergebnissen führen.

- webVisit
- search

Für ein genaues Abonnement wird außerdem empfohlen, einige der verfügbaren Eigenschaften des Datentyps [a1/> zu verwenden.](../../xdm/data-types/subscription.md)

**Zusätzliche empfohlene Standard-Ereignistyp:**

Die verbleibenden [Ereignistyp](#standard-events) können je nach Komplexität des Ziels und der für die Aktivierung infrage kommenden Population beim Konfigurieren der Customer AI-Instanz erforderlich sein. Wenn die Daten für einen bestimmten Datentyp verfügbar sind, wird empfohlen, diese Daten in Ihr Schema aufzunehmen.

### Szenario 6: Mobilanwendung starten

**Prognoseziel:** Prognostizieren Sie die Tendenz berechtigter Profil, eine kostenpflichtige Mobilanwendung in den nächsten X Tagen zu starten. Dies ähnelt der Prognose des Key Performance Indicator (KPI) von &quot;Monatsaktive Benutzer&quot;.

**Erforderliche Standard-Ereignistyp:**

Die unten aufgeführten Ereignistypen sind für eine optimale Kundenachvermessung mit diesem bestimmten Prognoseziel erforderlich. Es ist möglich, ein erforderliches Ereignis je nach Prognoseziel auszuschließen, allerdings kann das Ausschließen mehrerer Ereignis zu schlechten Ergebnissen führen.

- bestellen
- Checkouts
- Einkäufe
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstallalls
- applicationLaunches
- applicationUpgrades

In diesem Beispiel werden `order`, `checkouts` und `purchases` verwendet, wenn eine Mobilanwendung gekauft werden muss.

**Zusätzliche empfohlene Standard-Ereignistyp:**

Die verbleibenden [Ereignistyp](#standard-events) können je nach Komplexität des Ziels und der für die Aktivierung infrage kommenden Population beim Konfigurieren der Customer AI-Instanz erforderlich sein. Wenn die Daten für einen bestimmten Datentyp verfügbar sind, wird empfohlen, diese Daten in Ihr Schema aufzunehmen.

### Szenario 7: Erreichtes Merkmal (Adobe Audience Manager)

**Prognoseziel:** Prognostizieren Sie die Tendenz, einige Eigenschaften zu realisieren.

**Erforderliche Standard-Ereignistyp:**

Um Eigenschaften aus Adobe Audience Manager verwenden zu können, müssen Sie eine Quellverbindung mit dem [Audience Manager-Quellanschluss](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md) erstellen. Der Quell-Connector erstellt das Schema automatisch mit den richtigen Mixins. Sie müssen keine zusätzlichen Ereignistyp manuell hinzufügen, damit das Schema mit der Kundenunterstützung funktioniert.

Wenn Sie eine neue Kunden-AI-Instanz konfigurieren, können `audienceName` und `audienceID` verwendet werden, um eine bestimmte Eigenschaft für die Bewertung auszuwählen, während Sie Ihr Ziel definieren.

## Ausgabedaten von Customer AI

Customer AI generiert mehrere Attribute für einzelne Profile, die als geeignet gelten. Es gibt zwei Möglichkeiten, das Ergebnis (Output) auf Basis des von Ihnen bereitgestellten Ergebnisses zu konsumieren. Wenn Sie über einen Dataset mit aktiviertem Kundendaten in Echtzeit verfügen, können Sie Einblicke aus dem Echtzeit-Profil des Kunden im [Segmentaufbau](../../segmentation/ui/segment-builder.md) nutzen. Wenn Sie keinen Profil-aktivierten Datensatz haben, können Sie [den Client-AI-Output](./user-guide/download-scores.md)-Datensatz herunterladen, der auf dem Datensee verfügbar ist.

>[!NOTE]
>
> Ausgabewerte werden vom Echtzeit-Kundensegment verwendet, das zum Erstellen und Definieren von Segmenten verwendet werden kann.

Die folgende Tabelle beschreibt die verschiedenen Attribute, die in der Ausgabe der Customer AI gefunden wurden:

| Attribut | Beschreibung |
| ----- | ----------- |
| Ergebnis | Die relative Wahrscheinlichkeit, mit der ein Kunde das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Dieser Wert ist nicht als Prozentsatz der Wahrscheinlichkeit zu behandeln, sondern vielmehr als die Wahrscheinlichkeit eines Individuums im Vergleich zur Gesamtbevölkerung. Dieser Wert liegt im Bereich von 0 bis 100. |
| Wahrscheinlichkeit | Dieses Attribut ist die wahre Wahrscheinlichkeit eines Profils, dass es das das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Beim Vergleich der Ausgaben über verschiedene Ziele hinweg wird empfohlen, dass Sie die Wahrscheinlichkeit über das Perzentil oder das Ergebnis in Betracht ziehen. Die Wahrscheinlichkeit sollte immer bei der Bestimmung der durchschnittlichen Wahrscheinlichkeit für die gesamte geeignete Bevölkerung verwendet werden, da die Wahrscheinlichkeit für Ereignisse, die nicht häufig auftreten, tendenziell niedriger liegt. Werte für den Wahrscheinlichkeitsbereich zwischen 0 und 1. |
| Perzentil | Dieser Wert enthält Informationen zur Leistung eines Profils im Vergleich zu anderen Profilen mit ähnlichen Werten. Ein Profil mit einem Perzentil-Rang von 99 für Kundenabwanderung weist beispielsweise darauf hin, dass es ein höheres Risiko für Abwanderungen aufweist als 99 % aller anderen Profile, die bewertet wurden. Die Perzentile liegen zwischen 1 und 100. |
| Tendenztyp | Der ausgewählte Tendenztyp. |
| Datum der Auswertung | Das Datum, an dem die Auswertung erfolgte. |
| Einflussfaktoren | Prognostizierte Gründe, warum ein Profil wahrscheinlich konvertiert oder abwandert. Die Faktoren bestehen aus den folgenden Attributen:<ul><li>Code: Das Profil- oder Verhaltensattribut, das das prognostizierte Ergebnis eines Profils positiv beeinflusst. </li><li>Wert: Der Wert des Profil- oder Verhaltensattributs.</li><li>Wichtigkeit: Gibt an, welche Gewichtung das Profil- oder Verhaltensattribut auf das prognostizierte Ergebnis hat (niedrig, mittel, hoch)</li></ul> |

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet haben und alle Ihre Anmeldedaten und Schema vorhanden sind, führen Sie Beginn unter [Eine Kundeninstanz konfigurieren](./user-guide/configure.md) aus. Dieser Leitfaden führt Sie durch das Erstellen einer Instanz für die Kundenunterstützung.
