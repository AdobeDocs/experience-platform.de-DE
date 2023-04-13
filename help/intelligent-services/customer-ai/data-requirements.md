---
keywords: Experience Platform; Erste Schritte; Kundenunterstützung; beliebte Themen; Eingabe der Kundenunterstützung; Ausgabe der Kundenunterstützung Datenanforderungen
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Datenanforderungen in Customer AI
topic-legacy: Getting started
description: Erfahren Sie mehr über die erforderlichen Ereignisse, Eingaben und Ausgaben, die von Customer AI verwendet werden.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 17%

---


# Eingabe und Ausgabe in Customer AI

Im folgenden Dokument werden die verschiedenen erforderlichen Ereignisse, Eingaben und Ausgaben beschrieben, die in Customer AI verwendet werden.

## Erste Schritte {#getting-started}

Im Folgenden finden Sie die Schritte zum Erstellen von Tendenzmodellen und zum Identifizieren von Zielgruppen für personalisiertes Marketing in Customer AI:

1. Konkrete Anwendungsfälle: Wie können Tendenzmodelle dazu beitragen, Zielgruppen für personalisiertes Marketing zu identifizieren? Welches sind meine Geschäftsziele und entsprechende Taktiken, um das Ziel zu erreichen? Wo kann die Tendenzmodellierung in diesen Prozess passen?

2. Anwendungsfälle priorisieren: Welches sind die höchsten Prioritäten für das Unternehmen?

3. Erstellen von Modellen in Customer AI: Sehen Sie sich dies an [Schnellanleitung](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=de) und lesen Sie unsere [UI-Handbuch](../customer-ai/user-guide/configure.md) für einen schrittweisen Prozess zum Erstellen eines Modells.

4. [Segmente erstellen](../customer-ai/user-guide/create-segment.md) Modellergebnisse verwenden.

5. Nehmen Sie zielgerichtete Geschäftsaktionen auf der Grundlage dieser Segmente vor. Überwachen Sie die Ergebnisse und führen Sie die Aktionen zur Verbesserung durch.

Im Folgenden finden Sie Beispielkonfigurationen für Ihr erstes Modell.  Das in diesem Dokument erstellte Beispielmodell verwendet ein Customer AI-Modell, um vorherzusagen, wer in den nächsten 30 Tagen wahrscheinlich für ein Einzelhandelsgeschäft konvertieren wird. Der Eingabedatensatz ist ein Adobe Analytics-Datensatz.

| Schritt | Definition | Beispiel |
| ---- | ------ | ------- |
| Setup | Geben Sie grundlegende Informationen zum Modell an. | **Name**: Pensionskaufmodell <br> **Modelltyp**: Konversion |
| Auswählen von Daten | Geben Sie die zum Erstellen des Modells verwendeten Datensätze an. | **Datensatz**: Adobe Analytics-Datensatz <br> **Identität**: Stellen Sie sicher, dass die Identitätsspalte für jeden Datensatz als gemeinsame Identität festgelegt ist. |
| Ziel definieren | Definieren Sie das Ziel, die geeignete Population, benutzerspezifische Ereignisse und Profilattribute. | **Prognoseziel**: Auswählen `commerce.purchases.value` entspricht Bleistift <br> **Ergebnisfenster**: 30 Tage. |
| Festlegen von Optionen | Richten Sie den Zeitplan für die Modellaktualisierung ein und aktivieren Sie Bewertungen für Profil . | **Zeitplan**: Wöchentlich <br> **Profil aktivieren**: Dies muss aktiviert sein, damit die Modellausgabe in der Segmentierung verwendet werden kann. |

## Datenübersicht {#data-overview}

In den folgenden Abschnitten werden die verschiedenen erforderlichen Ereignisse, Eingaben und Ausgaben beschrieben, die in Customer AI verwendet werden.

Customer AI analysiert die folgenden Datensätze, um Abwanderungsraten vorherzusagen (wenn ein Kunde wahrscheinlich die Verwendung des Produkts stoppt) oder Konversionen (wenn ein Kunde wahrscheinlich einen Kauf tätigt):

- Adobe Analytics-Daten mit [Analytics-Quell-Connector](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Adobe Audience Manager-Daten mit [Quell-Connector für Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Erlebnisereignis-Datensatz](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [Datensatz für Kundenerlebnis](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

Sie können mehrere Datensätze aus verschiedenen Quellen hinzufügen, wenn jeder Datensatz denselben Identitätstyp (Namespace) wie eine ECID aufweist. Weitere Informationen zum Hinzufügen mehrerer Datensätze finden Sie unter [Benutzerhandbuch für Customer AI](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Die Aufstockung von Daten durch Quell-Connectoren dauert bis zu vier Wochen. Wenn Sie kürzlich einen Connector eingerichtet haben, sollten Sie sicherstellen, dass der Datensatz die für Customer AI erforderliche Mindestlänge von Daten aufweist. Lesen Sie die [historische Daten](#data-requirements) -Abschnitt, um sicherzustellen, dass Sie über genügend Daten für Ihr Prognoseziel verfügen.

In der folgenden Tabelle sind einige häufig verwendete Begriffe in diesem Dokument aufgeführt:

| Begriff | Definition |
| --- | --- |
| [Experience-Datenmodell (XDM)](../../xdm/home.md) | XDM ist das grundlegende Framework, mit dem Adobe Experience Cloud mit Adobe Experience Platform genau zum richtigen Zeitpunkt die richtige Botschaft an die richtige Person auf dem richtigen Kanal senden kann. Platform verwendet das XDM-System, um Daten auf eine bestimmte Weise zu organisieren, die die Verwendung für Platform-Dienste erleichtert. |
| [XDM-Schema](../../xdm/schema/composition.md) | Schemas dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Durch die systemübergreifende einheitliche Definition von Daten wird es einfacher, deren Bedeutung beizubehalten und somit Wert aus Daten zu ziehen. Bevor Daten in Platform erfasst werden können, muss ein Schema erstellt werden, das die Datenstruktur beschreibt und Einschränkungen für den Datentyp enthält, der in jedem Feld enthalten sein kann. Schemas bestehen aus einer zugrunde liegenden XDM-Klasse und keiner oder mehr Schemafeldgruppen. |
| [XDM-Klasse](../../xdm/schema/field-constraints.md) | Alle XDM-Schemata beschreiben Daten, die kategorisiert werden können als `Experience Event`. Das Datenverhalten eines Schemas wird durch die Klasse des Schemas definiert, die einem Schema beim ersten Erstellen zugewiesen wird. XDM-Klassen beschreiben die Mindestanzahl von Eigenschaften, die ein Schema enthalten muss, um ein bestimmtes Datenverhalten zu haben. |
| [Feldergruppen](../../xdm/schema/composition.md) | Eine Komponente, die ein oder mehrere Felder in einem Schema definiert. Feldergruppen erzwingen, wie ihre Felder in der Hierarchie des Schemas angezeigt werden, und weisen daher in jedem Schema, in dem sie enthalten sind, dieselbe Struktur auf. Feldgruppen sind nur mit bestimmten Klassen kompatibel, angegeben durch ihr `meta:intendedToExtend`-Attribut. |
| [Datentyp](../../xdm/schema/composition.md) | Eine Komponente, die auch ein oder mehrere Felder für ein Schema bereitstellen kann. Im Gegensatz zu Feldgruppen sind Datentypen jedoch nicht auf eine bestimmte Klasse beschränkt. Dadurch stellen Datentypen eine flexiblere Möglichkeit dar, um allgemeine Datenstrukturen zu beschreiben, die über mehrere Schemas mit potenziell unterschiedlichen Klassen hinweg wiederverwendet werden können. Die in diesem Dokument beschriebenen Datentypen werden sowohl von den CEE- als auch von Adobe Analytics-Schemata unterstützt. |
| [Echtzeit-Kundenprofil](../../profile/home.md) | Das Echtzeit-Kundenprofil bietet ein zentralisiertes Kundenprofil für zielgerichtetes und personalisiertes Erlebnis-Management. Jedes Profil enthält Daten, die systemübergreifend aggregiert werden, sowie relevante, mit einem Zeitstempel versehene Ereignisse, an denen die entsprechende Person beteiligt ist und die in einem der Systeme stattfanden, die Sie in Verbindung mit Experience Platform verwenden. |

## Input-Daten von Customer AI {#customer-ai-input-data}

Bei Eingabedatensätzen wie Adobe Analytics und Adobe Audience Manager ordnen die entsprechenden Quell-Connectoren die Ereignisse standardmäßig während des Verbindungsprozesses direkt in diesen Standardfeldgruppen (Commerce, Web, Application und Search) zu. Die folgende Tabelle zeigt die Ereignisfelder in den Standardfeldgruppen für Customer AI.

Weitere Informationen zum Zuordnen von Adobe Analytics-Daten oder Audience Manager-Daten finden Sie im Analytics-Feld-Mappings oder -Audience Manager [Handbuch zu Feldzuordnungen](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

Sie können XDM-Schemas für Erlebnis-Ereignis- oder Kundenerlebnis-Ereignisse für Eingabedatensätze verwenden, die nicht über einen der oben genannten Connectoren aufgefüllt werden. Während der Erstellung des Schemas können zusätzliche XDM-Feldergruppen hinzugefügt werden. Die Feldergruppen können durch Adoben wie Standardfeldgruppen oder benutzerdefinierte Feldergruppen bereitgestellt werden, die mit der Datendarstellung in Platform übereinstimmen.

>[!IMPORTANT]
>
>Sie müssen sicherstellen, dass Daten in diese Eingabedatensätze eingefügt werden. Wenn keine Ereignisse aus Standardfeldgruppen in den Eingabedatensätzen gefunden werden, müssen Sie während des Konfigurations-Workflows benutzerdefinierte Ereignisse hinzufügen. Weitere Informationen finden Sie unter Benutzerspezifische Ereignisse.

### Standardfeldgruppen, die von Customer AI verwendet werden {#standard-events}

Erlebnisereignisse werden zur Bestimmung verschiedener Kundenverhaltensweisen verwendet. Je nachdem, wie Ihre Daten strukturiert sind, umfassen die unten aufgeführten Ereignistypen möglicherweise nicht alle Verhaltensweisen Ihres Kunden. Es liegt an Ihnen zu bestimmen, welche Felder über die erforderlichen Daten verfügen, um Web- oder andere kanalspezifische Benutzeraktivitäten eindeutig und eindeutig zu identifizieren. Je nach Prognoseziel können sich die erforderlichen Felder ändern.

>[!NOTE]
>
>Wenn Sie Adobe Analytics- oder Adobe Audience Manager-Daten verwenden, wird das Schema automatisch mit den erforderlichen Standardereignissen erstellt, die zum Erfassen Ihrer Daten erforderlich sind. Wenn Sie Ihr eigenes benutzerdefiniertes EE-Schema zum Erfassen von Daten erstellen, müssen Sie überlegen, welche Feldergruppen zum Erfassen Ihrer Daten erforderlich sind.

Customer AI verwendet die Ereignisse standardmäßig in diesen vier Standardfeldgruppen: Handel, Web, Anwendung und Suche. Es ist nicht erforderlich, Daten für jedes Ereignis in den unten aufgeführten Standardfeldgruppen zu haben. Für bestimmte Szenarien sind jedoch bestimmte Ereignisse erforderlich. Wenn Ereignisse in den Standardfeldgruppen verfügbar sind, wird empfohlen, diese in Ihr Schema einzuschließen. Wenn Sie beispielsweise ein Customer AI-Modell für die Vorhersage von Kaufereignissen erstellen möchten, ist es nützlich, Daten aus den Feldergruppen Commerce und Webseitendetails zu haben.

Um eine Feldergruppe in der Platform-Benutzeroberfläche anzuzeigen, wählen Sie die **[!UICONTROL Schemas]** in der linken Leiste, gefolgt von der Auswahl der **[!UICONTROL Feldergruppen]** Registerkarte.

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

Darüber hinaus kann Customer AI Abonnementdaten verwenden, um bessere Abwanderungsmodelle zu erstellen. Abonnementdaten werden für jedes Profil benötigt, das die [[!UICONTROL Abonnement]](../../xdm/data-types/subscription.md) Datentypformat. Die meisten Felder sind optional. Für ein optimales Abwanderungsmodell wird jedoch dringend empfohlen, Daten für so viele Felder wie möglich bereitzustellen, z. B.: `startDate`, `endDate`und alle anderen relevanten Details. Wenden Sie sich an Ihr Account-Team, um weitere Unterstützung zu dieser Funktion zu erhalten.

### Hinzufügen benutzerdefinierter Ereignisse und Profilattribute {#add-custom-events}

Wenn Sie über Informationen verfügen, die Sie zusätzlich zur Standardeinstellung hinzufügen möchten [Standardereignisfelder](#standard-events) von Customer AI verwendet werden, können Sie die [Benutzerdefinierte Ereigniskonfiguration](./user-guide/configure.md#custom-events) , um die vom Modell verwendeten Daten zu ergänzen.

#### Verwendung benutzerspezifischer Ereignisse

Benutzerdefinierte Ereignisse sind erforderlich, wenn die im Schritt zur Datensatzauswahl ausgewählten Datensätze *Keine* der von Customer AI verwendeten Standardereignisfelder. Customer AI benötigt Informationen zu mindestens einem Benutzerverhaltensereignis, das nicht das Ergebnis ist.

Benutzerdefinierte Ereignisse sind hilfreich für:

- Einbinden von Domain-Kenntnissen oder früherem Fachwissen in das Modell.

- Verbesserung der Qualität des prädiktiven Modells.

- Erhalten zusätzlicher Einblicke und Interpretationen.

Die besten Kandidaten für benutzerspezifische Ereignisse sind Daten, die Domain-Kenntnisse enthalten, die das Ergebnis vorhersagen können. Zu den allgemeinen Beispielen für benutzerspezifische Ereignisse gehören:

- Kontoregistrierung

- Newsletter abonnieren

- Kundendienst aufrufen

Im Folgenden finden Sie eine Auswahl branchenspezifischer Beispiele für benutzerspezifische Ereignisse:

| Branche | Benutzerspezifische Ereignisse |
| --- | --- |
| Einzelhandel | In-Store-Transaktion<br>Für Clubkarte anmelden<br>Beschneiden Sie den mobilen Coupon. |
| Unterhaltung | Saisonmitgliedschaft <br> Streamen von Videos |
| Gastfreundschaft | Reservierung von Restaurants <br> Treuepunkte kaufen. |
| Reise | Bekannte Reisenden-Informationen Kaufmeilen hinzufügen. |
| Kommunikation | Upgrade/Downgrade/Abbruch-Plan. |

Benutzerdefinierte Ereignisse müssen vom Benutzer initiierte Aktionen darstellen, damit sie ausgewählt werden können. Beispielsweise ist &quot;E-Mail-Versand&quot;eine Aktion, die von einem Marketing-Experten und nicht vom Benutzer initiiert wird. Daher sollte sie nicht als benutzerspezifisches Ereignis verwendet werden.

### Historische Daten

Customer AI erfordert historische Daten für die Modellschulung. Die erforderliche Dauer für die Existenz von Daten im System wird durch zwei Schlüsselelemente bestimmt: Ergebnisfenster und förderfähige Bevölkerung.

Standardmäßig sucht Customer AI nach einem Benutzer, der in den letzten 45 Tagen aktiv war, wenn während der Anwendungskonfiguration keine Definition der förderfähigen Population angegeben wurde. Darüber hinaus erfordert Customer AI mindestens 500 qualifizierte und 500 nicht qualifizierte Ereignisse (insgesamt 1000) aus historischen Daten, die auf einer prognostizierten Zieldefinition basieren.

Die folgenden Beispiele zeigen die Verwendung einer einfachen Formel, mit der Sie die erforderliche Mindestmenge an Daten ermitteln können. Wenn Sie über mehr Daten als die Mindestanforderung verfügen, liefert Ihr Modell wahrscheinlich genauere Ergebnisse. Wenn Sie weniger als den erforderlichen Mindestwert haben, schlägt das Modell fehl, da nicht genügend Daten für die Modellschulung vorhanden sind.

**Formel**:

So legen Sie die erforderliche Mindestdauer der im System vorhandenen Daten fest:

- Die zum Erstellen von Funktionen erforderlichen Daten betragen mindestens 30 Tage. Vergleichen Sie das Eignungs-Lookback-Fenster mit 30 Tagen:

   - Wenn das Eignungs-Lookback-Fenster länger als 30 Tage ist, ist die Datenanforderung = Eignungs-Lookback-Fenster + Ergebnisfenster.

   - Andernfalls ist die Datenanforderung = 30 Tage + Ergebnisfenster.

** Wenn mehr als eine Bedingung für die Definition der förderfähigen Population vorhanden ist, ist das Lookback-Fenster für die Berechtigung die längste.

>[!NOTE]
>
>30 ist die Mindestanzahl von Tagen, die für die förderfähige Bevölkerung erforderlich ist. Wenn dies nicht angegeben wird, beträgt der Standardwert 45 Tage.

**Beispiele**:

- Sie möchten vorhersagen, ob ein Kunde in den nächsten 30 Tagen wahrscheinlich eine Uhr für diejenigen kauft, die in den letzten 60 Tagen eine Web-Aktivität haben.

   - Eignungs-Lookback-Fenster = 60 Tage

   - Ergebnisfenster = 30 Tage

   - Erforderliche Daten = 60 Tage + 30 Tage = 90 Tage

- Sie möchten vorhersagen, ob der Benutzer in den nächsten sieben Tagen wahrscheinlich eine Uhr kaufen wird **without** die explizite förderfähige Population. In diesem Fall wird die berechtigte Population standardmäßig auf &quot;diejenigen, die in den letzten 45 Tagen aktiv waren&quot;gesetzt und das Ergebnisfenster beträgt 7 Tage.

   - Eignungs-Lookback-Fenster = 45 Tage

   - Ergebnisfenster = 7 Tage

   - Erforderliche Daten = 45 Tage + 7 Tage = 52 Tage

- Sie möchten vorhersagen, ob der Kunde in den nächsten sieben Tagen wahrscheinlich eine Uhr für diejenigen kaufen wird, die in den letzten sieben Tagen eine Web-Aktivität haben.

   - Eignungs-Lookback-Fenster = 7 Tage

   - Mindestdaten für die Erstellung von Funktionen = 30 Tage

   - Ergebnisfenster = 7 Tage

   - Erforderliche Daten = 30 Tage + 7 Tage = 37 Tage

Obwohl Customer AI einen Mindestzeitraum benötigt, damit die Daten im System vorhanden sind, funktioniert sie auch am besten mit den neuesten Daten. Durch die Verwendung aktuellerer Verhaltensdaten liefert Customer AI wahrscheinlich eine genauere Vorhersage des zukünftigen Verhaltens eines Benutzers.

## Ausgabedaten von Customer AI {#customer-ai-output-data}

Customer AI generiert mehrere Attribute für einzelne Profile, die als geeignet gelten. Es gibt zwei Möglichkeiten, die Punktzahl (Ausgabe) basierend auf dem, was Sie bereitgestellt haben, zu nutzen. Wenn Sie über einen Datensatz mit aktiviertem Echtzeit-Kundenprofil verfügen, können Sie Einblicke aus dem Echtzeit-Kundenprofil im [Segment Builder](../../segmentation/ui/segment-builder.md). Wenn Sie keinen Datensatz mit aktiviertem Profil haben, können Sie [Customer AI-Ausgabe herunterladen](./user-guide/download-scores.md) Datensatz, der im Data Lake verfügbar ist.

Den Ausgabedatensatz finden Sie in Platform . **Datensätze** Arbeitsbereich. Alle Ausgabedatensätze von Customer AI beginnen mit dem Namen **Customer AI-Werte - NAME_OF_APP**. Ebenso beginnen alle Ausgabeschemata von Customer AI mit dem Namen **Customer AI-Schema - Name_of_app**.

![Name der Ausgabedatensätze in Customer AI](./images/user-guide/cai-schema-name-of-app.png)

Die folgende Tabelle beschreibt die verschiedenen Attribute, die in der Ausgabe der Customer AI gefunden wurden:

| Attribut | Beschreibung |
| ----- | ----------- |
| [!UICONTROL Ergebnis] | Die relative Wahrscheinlichkeit, mit der ein Kunde das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Dieser Wert ist nicht als Prozentsatz der Wahrscheinlichkeit zu behandeln, sondern vielmehr als die Wahrscheinlichkeit eines Individuums im Vergleich zur Gesamtbevölkerung. Dieser Wert liegt im Bereich von 0 bis 100. |
| Wahrscheinlichkeit | Dieses Attribut ist die wahre Wahrscheinlichkeit eines Profils, dass es das das prognostizierte Ziel innerhalb des definierten Zeitraums erreicht. Beim Vergleich von Ausgaben über verschiedene Ziele hinweg wird empfohlen, die Wahrscheinlichkeit über das Perzentil oder die Punktzahl zu berücksichtigen. Die Wahrscheinlichkeit sollte immer bei der Bestimmung der durchschnittlichen Wahrscheinlichkeit für die gesamte geeignete Bevölkerung verwendet werden, da die Wahrscheinlichkeit für Ereignisse, die nicht häufig auftreten, tendenziell niedriger liegt. Werte für den Wahrscheinlichkeitsbereich zwischen 0 und 1. |
| Perzentil | Dieser Wert enthält Informationen zur Leistung eines Profils im Vergleich zu anderen Profilen mit ähnlichen Werten. Ein Profil mit einem Perzentil-Rang von 99 für Kundenabwanderung weist beispielsweise darauf hin, dass es ein höheres Risiko für Abwanderungen aufweist als 99 % aller anderen Profile, die bewertet wurden. Die Perzentile liegen im Bereich von 1 bis 100. |
| Tendenztyp | Der ausgewählte Tendenztyp. |
| Datum der Auswertung | Das Datum, an dem die Auswertung erfolgte. |
| Einflussfaktoren | Dies sind prognostizierte Gründe dafür, warum ein Profil wahrscheinlich konvertiert oder abwandert. Diese Faktoren bestehen aus den folgenden Attributen:<ul><li>Code: Das Profil- oder Verhaltensattribut, das das prognostizierte Ergebnis eines Profils positiv beeinflusst. </li><li>Wert: Der Wert des Profil- oder Verhaltensattributs.</li><li>Wichtigkeit: Gibt an, welche Gewichtung das Profil- oder Verhaltensattribut auf das prognostizierte Ergebnis hat (niedrig, mittel, hoch)</li></ul> |

## Nächste Schritte {#next-steps}

Nachdem Sie Ihre Daten vorbereitet und sichergestellt haben, dass alle Ihre Anmeldedaten und Schemata vorhanden sind, lesen Sie den Abschnitt [Konfigurieren einer Customer AI-Instanz](./user-guide/configure.md) Anleitung, die Sie durch ein schrittweises Tutorial zum Erstellen einer Customer AI-Instanz führt.