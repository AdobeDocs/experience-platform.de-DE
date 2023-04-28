---
keywords: Experience Platform;Erste Schritte;Kunden-KI;beliebte Themen;Kunden-KI-Eingabe;Kunden-KI-Ausgabe;Datenanforderungen
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Datenanforderungen in Kunden-KI
topic-legacy: Getting started
description: Erfahren Sie mehr über die erforderlichen Ereignisse, Eingaben und Ausgaben, die von Kunden-KI verwendet werden.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: ht
source-wordcount: '2484'
ht-degree: 100%

---


# Eingaben und Ausgaben in Kunden-KI

Im folgenden Dokument werden die verschiedenen erforderlichen Ereignisse, Eingaben und Ausgaben beschrieben, die in Kunden-KI verwendet werden.

## Erste Schritte {#getting-started}

Im Folgenden finden Sie die Schritte zum Erstellen von Tendenzmodellen und zum Identifizieren von Zielgruppen für personalisiertes Marketing in Kunden-KI:

1. Skizzieren Sie Anwendungsfälle: Wie können Tendenzmodelle dazu beitragen, Zielgruppen für personalisiertes Marketing zu identifizieren? Was sind meine Geschäftsziele und entsprechende Taktiken, um das Ziel zu erreichen? An welcher Stelle passt die Tendenzmodellierung in diesen Prozess?

2. Priorisieren Sie die Anwendungsfälle: Was sind die höchsten Prioritäten für das Unternehmen?

3. Erstellen Sie Modelle in Kunden-KI: Sehen Sie sich diese [Schnellanleitung](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=de) an und lesen Sie unser [Handbuch für die Benutzeroberfläche](../customer-ai/user-guide/configure.md), um zu erfahren, wie Sie ein Modell schrittweise erstellen können.

4. [Erstellen Sie Segmente](../customer-ai/user-guide/create-segment.md) mithilfe von Modellergebnissen.

5. Nehmen Sie zielgerichtete Geschäftsaktionen auf Grundlage dieser Segmente vor. Überwachen Sie die Ergebnisse und führen Sie Aktionen zur Verbesserung durch.

Im Folgenden finden Sie Beispielkonfigurationen für Ihr erstes Modell.  Das in diesem Dokument erstellte Beispielmodell verwendet ein Kunden-KI-Modell, um vorherzusagen, wer in den nächsten 30 Tagen wahrscheinlich eine Konversion zu einem Einzelhandelsgeschäft durchführen wird. Bei dem Eingabedatensatz handelt es sich um einen Adobe Analytics-Datensatz.

| Schritt | Definition | Beispiel |
| ---- | ------ | ------- |
| Setup | Geben Sie grundlegende Informationen zum Modell an. | **Name**: Stiftkauf-Tendenzmodell <br> **Modelltyp**: Konversion |
| Auswählen von Daten | Geben Sie die zum Erstellen des Modells verwendeten Datensätze an. | **Datensatz**: Adobe Analytics-Datensatz <br> **Identität**: Stellen Sie sicher, dass die Identitätsspalte für jeden Datensatz als gemeinsame Identität festgelegt ist. |
| Ziel definieren | Definieren Sie das Ziel, die geeignete Population, benutzerspezifische Ereignisse und Profilattribute. | **Prognoseziel**: Legen Sie `commerce.purchases.value` so fest, dass dies Stiften entspricht <br> **Ergebnisfenster**: 30 Tage. |
| Optionen festlegen | Richten Sie den Zeitplan für die Modellaktualisierung ein und aktivieren Sie Bewertungen für das Profil | **Zeitplan**: Wöchentlich <br> **Für Profil aktivieren**: Dies muss aktiviert sein, damit die Modellausgabe in der Segmentierung verwendet werden kann. |

## Datenübersicht {#data-overview}

In den folgenden Abschnitten werden die verschiedenen erforderlichen Ereignisse, Eingaben und Ausgaben beschrieben, die in Kunden-KI verwendet werden.

Kunden-KI analysiert die folgenden Datensätze, um Tendenzwerte für Abwanderungen (ab wann eine Kundin oder ein Kunde das Produkt wahrscheinlich nicht mehr verwenden wird) oder Konversionen (wann eine Kundin oder ein Kunde einen Kauf tätigt) vorherzusagen:

- Adobe Analytics-Daten unter Verwendung des [Analytics-Quell-Connectors](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager-Daten unter Verwendung des [Audience Manager-Quell-Connectors](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Erlebnisereignis-Datensatz](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=de)
- [Kundenerlebnisereignis-Datensatz](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html?lang=de#cee-schema)

Sie können mehrere Datensätze aus verschiedenen Quellen hinzufügen, wenn jeder Datensatz denselben Identitätstyp (Namespace), etwa eine ECID, aufweist. Weitere Informationen zum Hinzufügen mehrerer Datensätze finden Sie im [Benutzerhandbuch für Kunden-KI](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Die Aufstockung von Daten durch Quell-Connectoren kann bis zu vier Wochen dauern. Wenn Sie kürzlich einen Connector eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die für Kunden-KI erforderliche Mindestlänge von Daten aufweist. Lesen Sie den Abschnitt zu [historischen Daten](#data-requirements), um sich zu vergewissern, dass Sie über genügend Daten für Ihr Prognoseziel verfügen.

In der folgenden Tabelle sind einige der in diesem Dokument häufig verwendeten Begriffe aufgeführt:

| Begriff | Definition |
| --- | --- |
| [Experience-Datenmodell (XDM)](../../xdm/home.md) | XDM ist der grundlegende Rahmen, durch den Adobe Experience Cloud als Teil von Adobe Experience Platform die richtige Botschaft der richtigen Person zur richtigen Zeit auf dem richtigen Kanal präsentieren kann. Platform verwendet das XDM-System, um Daten auf eine bestimmte Weise zu organisieren, die die Verwendung für Platform-Services vereinfacht. |
| [XDM-Schema](../../xdm/schema/composition.md) | Schemata dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen. Bevor Daten in Platform aufgenommen werden können, muss ein Schema erstellt werden, das die Datenstruktur beschreibt und den Datentyp entsprechend dem jeweiligen Feld einschränkt. Schemata bestehen aus einer XDM-Basisklasse und keiner, einer oder mehreren Schemafeldgruppen. |
| [XDM-Klasse](../../xdm/schema/field-constraints.md) | Alle XDM-Schemata beschreiben Daten, die als `Experience Event` kategorisiert werden können. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema bei der Ersterstellung zugewiesen wird. XDM-Klassen beschreiben die Mindestanzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten zu haben. |
| [Feldergruppen](../../xdm/schema/composition.md) | Eine Komponente, die ein oder mehrere Felder in einem Schema definiert. Feldergruppen erzwingen die Art und Weise, wie ihre Felder in der Hierarchie des Schemas angezeigt werden, und weisen daher in jedem Schema, in dem sie enthalten sind, dieselbe Struktur auf. Feldgruppen sind nur mit bestimmten Klassen kompatibel, angegeben durch ihr `meta:intendedToExtend`-Attribut. |
| [Datentyp](../../xdm/schema/composition.md) | Eine Komponente, die ebenfalls ein oder mehrere Felder für ein Schema bereitstellen kann. Im Gegensatz zu Feldgruppen sind Datentypen jedoch nicht auf eine bestimmte Klasse beschränkt. Dadurch stellen Datentypen eine flexiblere Möglichkeit dar, um allgemeine Datenstrukturen zu beschreiben, die über mehrere Schemata mit potenziell unterschiedlichen Klassen hinweg wiederverwendet werden können. Die in diesem Dokument beschriebenen Datentypen werden sowohl von CEE- als auch von Adobe Analytics-Schemata unterstützt. |
| [Echtzeit-Kundenprofil](../../profile/home.md) | Das Echtzeit-Kundenprofil bietet ein zentralisiertes Kundenprofil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die systemübergreifend aggregiert werden, sowie relevante, mit einem Zeitstempel versehene Ereignisse, an denen die entsprechende Person beteiligt ist und die in einem der Systeme stattfanden, die Sie in Verbindung mit Experience Platform verwenden. |

## Kunden-KI-Eingabedaten {#customer-ai-input-data}

Bei Eingabedatensätzen wie Adobe Analytics und Adobe Audience Manager ordnen die entsprechenden Quell-Connectoren die Ereignisse standardmäßig während des Verbindungsprozesses direkt in diesen Standardfeldgruppen („Commerce“, „Web“, „Anwendung“ und „Suche“) zu. Die folgende Tabelle zeigt die Ereignisfelder in den Standardfeldgruppen für Kunden-KI.

Weitere Informationen zum Zuordnen von Adobe Analytics- oder Audience Manager-Daten finden Sie im Handbuch zu Analytics-Feldzuordnungen bzw. im [Handbuch zu Audience Manager-Feldzuordnungen](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

Sie können XDM-Schemata für Erlebnis- oder Kundenerlebnisereignisse bei Eingabedatensätzen verwenden, die nicht über einen der oben genannten Connectoren aufgefüllt werden. Während der Schema-Erstellung können zusätzliche XDM-Feldergruppen hinzugefügt werden. Die Feldergruppen können von Adobe (wie die Standardfeldgruppen) oder als benutzerdefinierte Feldergruppen bereitgestellt werden, die der Datendarstellung in Platform entsprechen.

>[!IMPORTANT]
>
>Sie müssen sicherstellen, dass diese Eingabedatensätze mit Daten aufgefüllt werden. Wenn keine Ereignisse aus Standardfeldgruppen in den Eingabedatensätzen vorhanden sind, müssen Sie während des Konfigurations-Workflows benutzerspezifische Ereignisse hinzufügen. Weitere Informationen finden Sie in den Beschreibungen zu benutzerspezifischen Ereignissen.

### Von Kunden-KI verwendete Standardfeldgruppen {#standard-events}

Erlebnisereignisse werden zur Bestimmung verschiedener Kundenverhaltensweisen verwendet. Je nach Strukturierung der Daten umfassen die unten aufgeführten Ereignistypen möglicherweise nicht alle Verhaltensweisen Ihrer Kundin oder Ihres Kunden. Sie müssen selbst bestimmen, welche Felder über die erforderlichen Daten verfügen, um Web- oder andere kanalspezifische Benutzeraktivitäten klar und eindeutig zu identifizieren. Abhängig vom Prognoseziel können unterschiedliche Felder erforderlich sein.

>[!NOTE]
>
>Wenn Sie Adobe Analytics- oder Adobe Audience Manager-Daten verwenden, wird das Schema automatisch mit den erforderlichen Standardereignissen erstellt, die zum Erfassen Ihrer Daten benötigt werden. Wenn Sie Ihr eigenes benutzerdefiniertes EE-Schema zur Datenerfassung erstellen, müssen Sie überlegen, welche Feldergruppen zum Erfassen Ihrer Daten erforderlich sind.

Kunden-KI verwendet die Ereignisse standardmäßig in diesen vier Standardfeldgruppen: „Commerce“, „Web“, „Anwendung“ und „Suche“. Es ist nicht erforderlich, dass Daten für jedes Ereignis in den unten aufgeführten Standardfeldgruppen vorhanden sind. Bei bestimmten Szenarien werden jedoch bestimmte Ereignisse vorausgesetzt. Wenn Ereignisse in den Standardfeldgruppen verfügbar sind, wird empfohlen, diese in Ihr Schema einzuschließen. Wenn Sie beispielsweise ein Kunden-KI-Modell für die Prognose von Kaufereignissen erstellen möchten, sind dafür Daten aus den Feldergruppen mit Commerce- und Web-Seiten-Details hilfreich.

Um eine Feldergruppe in der Platform-Benutzeroberfläche anzuzeigen, wählen Sie in der linken Leiste die Registerkarte **[!UICONTROL Schemata]** und dann die Registerkarte **[!UICONTROL Feldergruppen]** aus.

| Feldergruppe | Ereignistyp | XDM-Feldpfad |
| --- | --- | --- |
| [!UICONTROL Handelsdetails] | Bestellung | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | checkouts | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | purchases | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Web-Details] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Anwendungsdetails] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Suchdetails] | Suchen | `search.keywords` |

Darüber hinaus kann Kunden-KI mithilfe von Abonnementdaten bessere Abwanderungsmodelle erstellen. Abonnementdaten werden für jedes Profil mit dem Datentypformat [[!UICONTROL Abonnement]](../../xdm/data-types/subscription.md) benötigt. Die meisten Felder sind optional. Für ein optimales Abwanderungsmodell wird jedoch ausdrücklich empfohlen, Daten für so viele Felder wie möglich, z. B. `startDate`, `endDate`, und alle anderen relevanten Details bereitzustellen. Bitte wenden Sie sich an Ihr Konto-Team, um weitere Unterstützung zu dieser Funktion zu erhalten.

### Hinzufügen benutzerspezifischer Ereignisse und Profilattribute {#add-custom-events}

Wenn Sie über Informationen verfügen, die Sie zusätzlich zu den von Kunden-KI eingesetzten [Standardereignisfeldern](#standard-events) einschließen möchten, können Sie durch [Konfiguration benutzerspezifischer Ereignisse](./user-guide/configure.md#custom-events) die vom Modell verwendeten Daten ergänzen.

#### Verwendung benutzerspezifischer Ereignisse

Benutzerspezifische Ereignisse sind erforderlich, wenn die im Schritt zur Datensatzauswahl ausgewählten Datensätze *keine* der von Kunden-KI verwendeten Standardereignisfelder enthalten. Kunden-KI benötigt Informationen zu mindestens einem benutzerbezogenen Verhaltensereignis, das nicht dem Ergebnis entspricht.

Benutzerspezifische Ereignisse sind hilfreich für Folgendes:

- Einbinden von Domain-Wissen oder Vorkenntnissen in das Modell.

- Verbessern der Qualität des Prognosemodells.

- Erhalten zusätzlicher Einblicke und Interpretationen.

Die besten Kandidaten für benutzerspezifische Ereignisse sind Daten, die Domain-Wissen enthalten, welches eine Vorhersage des Ergebnisses ermöglicht. Zu den allgemeinen Beispielen für benutzerspezifische Ereignisse gehören:

- Registrieren eines Kontos

- Abonnieren eines Newsletters

- Anrufen des Kundendiensts

Im Folgenden finden Sie eine Auswahl branchenbezogener Beispiele für benutzerspezifische Ereignisse:

| Branche | Benutzerspezifische Ereignisse |
| --- | --- |
| Einzelhandel | Transaktion im Laden ausführen<br>Für Clubkarte registrieren<br>Mobile-Coupons ausschneiden. |
| Unterhaltung | Saisonmitgliedschaft erwerben <br> Video streamen. |
| Gastgewerbe | Tisch in einem Restaurant reservieren <br> Treuepunkte kaufen. |
| Reisen | Bekannte Informationen über Reisende hinzufügen Meilen kaufen. |
| Kommunikation | Tarif hochstufen/herunterstufen/kündigen. |

Benutzerspezifische Ereignisse müssen benutzerinitiierte Aktionen darstellen, damit sie ausgewählt werden können. Beispielsweise ist „E-Mail-Versand“ eine Aktion, die von einer Marketing-Fachkraft und nicht benutzerseitig initiiert wird. Daher sollte sie nicht als benutzerspezifisches Ereignis verwendet werden.

### Historische Daten

Kunden-KI erfordert historische Daten für das Modell-Training. Wie lange Daten im System vorhanden sein müssen, wird durch zwei Schlüsselelemente bestimmt: das Ergebnisfenster und eine geeignete Population.

Standardmäßig sucht Kunden-KI nach Benutzenden, die in den letzten 45 Tagen aktiv waren, wenn während der Anwendungskonfiguration keine Definition für eine geeigneten Population angegeben wurde. Darüber hinaus benötigt Kunden-KI mindestens 500 qualifizierte und 500 nicht qualifizierte Ereignisse (insgesamt 1000) aus historischen Daten, die auf einer prognostizierten Zieldefinition basieren.

Die folgenden Beispiele zeigen, wie Sie mit einer einfachen Formel die erforderliche Mindestmenge an Daten ermitteln können. Wenn Sie über mehr Daten als die Mindestanforderung verfügen, liefert Ihr Modell wahrscheinlich genauere Ergebnisse. Wird die erforderliche Mindestmenge unterschritten, schlägt das Modell fehl, da in diesem Fall nicht genügend Daten für das Modell-Training vorhanden sind.

**Formel**:

So stellen Sie die erforderliche Mindestaufbewahrungsdauer für die im System vorhandenen Daten fest:

- Zum Erstellen von Funktionen müssen Daten mindestens 30 Tage vorhanden sein. Vergleichen Sie das Eignungs-Lookback-Fenster mit 30 Tagen:

   - Wenn das Eignungs-Lookback-Fenster länger als 30 Tage ist, lautet die Datenanforderung: Eignungs-Lookback-Fenster + Ergebnisfenster.

   - Andernfalls lautet die Datenanforderung: 30 Tage + Ergebnisfenster.

** Wenn mehr als eine Bedingung für die Definition der geeigneten Population vorhanden ist, ist das Eignungs-Lookback-Fenster am längsten.

>[!NOTE]
>
>30 ist die Mindestanzahl von Tagen, die für die geeignete Population erforderlich ist. Wenn dies nicht angegeben wird, beträgt der Standardwert 45 Tage.

**Beispiele**:

- Sie möchten vorhersagen, ob eine Kundin oder ein Kunde in den nächsten 30 Tagen wahrscheinlich eine Uhr für diejenigen kaufen wird, für die in den letzten 60 Tagen eine Web-Aktivität verzeichnet wurde. 

   - Eignungs-Lookback-Fenster = 60 Tage

   - Ergebnisfenster = 30 Tage

   - Erforderliche Daten = 60 Tage + 30 Tage = 90 Tage

- Sie möchten vorhersagen, ob eine Benutzerin oder ein Benutzer in den nächsten sieben Tagen wahrscheinlich eine Uhr kaufen wird, **ohne** eine explizite geeignete Population anzugeben. In diesem Fall wird die geeignete Population standardmäßig auf „diejenigen, die in den letzten 45 Tagen aktiv waren“ festgelegt und das Ergebnisfenster beträgt 7 Tage.

   - Eignungs-Lookback-Fenster = 45 Tage

   - Ergebnisfenster = 7 Tage

   - Erforderliche Daten = 45 Tage + 7 Tage = 52 Tage

- Sie möchten vorhersagen, ob eine Kundin oder ein Kunde in den nächsten sieben Tagen wahrscheinlich eine Uhr für diejenigen kaufen wird, für die in den letzten sieben Tagen eine Web-Aktivität verzeichnet wurde.

   - Eignungs-Lookback-Fenster = 7 Tage

   - Erforderliche Mindestdaten für die Erstellung von Funktionen = 30 Tage

   - Ergebnisfenster = 7 Tage

   - Erforderliche Daten = 30 Tage + 7 Tage = 37 Tage

Kunden-KI benötigt nicht nur eine Mindestzeitspanne, für die die Daten im System vorhanden sein müssen, sondern funktioniert auch am besten mit möglichst aktuellen Daten. Durch Verwendung neuerer Verhaltensdaten liefert Kunden-KI wahrscheinlich eine genauere Prognose des zukünftigen Verhaltens einer Benutzerin oder eines Benutzers.

## Ausgabedaten von Customer AI {#customer-ai-output-data}

Customer AI generiert mehrere Attribute für einzelne Profile, die als geeignet gelten. Es gibt zwei Möglichkeiten, die Bewertung (Ausgabe) basierend auf dem, was Sie bereitgestellt haben, zu nutzen. Wenn Sie über einen Datensatz mit aktiviertem Echtzeit-Kundenprofil verfügen, können Sie Einblicke aus dem Echtzeit-Kundenprofil im [Segment Builder](../../segmentation/ui/segment-builder.md) nutzen. Wenn Sie keinen Datensatz mit aktiviertem Profil haben, können Sie den [Kunden-KI-Ausgabedatensatz herunterladen](./user-guide/download-scores.md), der im Data Lake verfügbar ist.

Den Ausgabedatensatz finden Sie im Platform-Arbeitsbereich **Datensätze**. Alle Kunden-KI-Ausgabedatensätze beginnen mit dem Namen **Kunden-KI-Bewertungen – NAME_DER_APP**. Ebenso beginnen alle Kunden-KI-Ausgabeschemata mit dem Namen **Kunden-KI-Schema – Name_der_App**.

![Name der Ausgabedatensätze in Kunden-KI](./images/user-guide/cai-schema-name-of-app.png)

Die folgende Tabelle beschreibt die verschiedenen Attribute, die in der Ausgabe der Customer AI gefunden wurden:

| Attribut | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Ergebnis] | Die relative Wahrscheinlichkeit, mit der ein Kunde das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Dieser Wert ist nicht als Prozentsatz der Wahrscheinlichkeit zu behandeln, sondern vielmehr als die Wahrscheinlichkeit eines Individuums im Vergleich zur Gesamtbevölkerung. Dieser Wert liegt im Bereich von 0 bis 100. |
| Wahrscheinlichkeit | Dieses Attribut ist die wahre Wahrscheinlichkeit eines Profils, dass es das das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Beim Vergleichen der Ausgaben über verschiedene Ziele hinweg wird empfohlen, die Wahrscheinlichkeit über das Perzentil oder die Bewertung in Betracht zu ziehen. Die Wahrscheinlichkeit sollte immer bei der Bestimmung der durchschnittlichen Wahrscheinlichkeit für die gesamte geeignete Bevölkerung verwendet werden, da die Wahrscheinlichkeit für Ereignisse, die nicht häufig auftreten, tendenziell niedriger liegt. Die Werte für die Wahrscheinlichkeit liegen zwischen 0 und 1. |
| Perzentil | Dieser Wert enthält Informationen zur Leistung eines Profils im Vergleich zu anderen Profilen mit ähnlichen Werten. Ein Profil mit einem Perzentil-Rang von 99 für Kundenabwanderung weist beispielsweise darauf hin, dass es ein höheres Risiko für Abwanderungen aufweist als 99 % aller anderen Profile, die bewertet wurden. Die Perzentile liegen zwischen 1 und 100. |
| Tendenztyp | Der ausgewählte Tendenztyp. |
| Datum der Auswertung | Das Datum, an dem die Auswertung erfolgte. |
| Einflussfaktoren | Dies sind prognostizierte Gründe dafür, warum ein Profil wahrscheinlich konvertiert oder abwandert. Die Faktoren bestehen aus den folgenden Attributen:<ul><li>Code: Das Profil- oder Verhaltensattribut, das das prognostizierte Ergebnis eines Profils positiv beeinflusst. </li><li>Wert: Der Wert des Profil- oder Verhaltensattributs.</li><li>Wichtigkeit: Gibt an, welche Gewichtung das Profil- oder Verhaltensattribut auf das prognostizierte Ergebnis hat (niedrig, mittel, hoch)</li></ul> |

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet und sichergestellt haben, dass alle Ihre Anmeldeinformationen und Schemata vorhanden sind, lesen Sie das Handbuch [Konfigurieren einer Kunden-KI-Instanz](./user-guide/configure.md), das Sie durch ein schrittweises Tutorial zum Erstellen einer Kunden-KI-Instanz führt.