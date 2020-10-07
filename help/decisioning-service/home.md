---
keywords: Experience Platform;home;popular topics;offer management;Offer Management;Journey;customer journey;journey;decision events;decision event;Decision events
solution: Experience Platform
title: Decisioning Service
topic: overview
description: Decisioning Service bietet die Möglichkeit, personalisierte, optimierte und orchestrierte Erlebnisse in Anwendungen zu erstellen, die in Adobe Experience Platform ausgeführt werden. Mithilfe von Decisioning Service können Sie die beste Option aus einer Reihe verfügbarer Optionen bestimmen. Diese Optionen, auch als Alternativen bezeichnet, könnten Angebote, Produktempfehlungen, Inhaltskomponenten für ein Web-Erlebnis, Gesprächsskripte und zu ergreifende Maßnahmen sein.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 80%

---


# Decisioning Service – Übersicht

[!DNL Decisioning Service] bietet die Möglichkeit, personalisierte, optimierte und orchestrierte Erlebnisse in Anwendungen zu erstellen, die in Adobe Experience Platform ausgeführt werden. Using [!DNL Decisioning Service], you can determine the best *option* from a set of available choices. Diese Optionen, auch als Alternativen bezeichnet, könnten Angebote, Produktempfehlungen, Inhaltskomponenten für ein Web-Erlebnis, Gesprächsskripte und zu ergreifende Maßnahmen sein. Derzeit wird der Anwendungsfall *Entscheidungsfindung bei Angeboten* unterstützt, wobei Entscheidungsoptionen spezifisch als Angebote modelliert werden. Unterstützung für weitere Anwendungsfälle ist geplant.

With [!DNL Decisioning Service], customers can reuse business logic as well as share a catalog of options across channels and applications. Statt Entscheidungsoptionen - und Strategien zu ihrer Auswahl - tief in einer Anwendung zu verwalten, können sie jetzt unabhängig davon genutzt werden, wann, wie und auf welchem Kanal der Endbenutzer mit einem Unternehmen oder einer Organisation interagiert.

Entscheidungsstrategien können die vielen Interaktionen berücksichtigen, die ein Kunde über verschiedene Kanäle und Anwendungen hinweg hatte. Beispielsweise könnte eine Aktivität der Callcenter-Anwendung dafür sorgen, dass eine Marketing-Nachricht nach einer Beschwerde aktiviert oder für einige Zeit unterdrückt wird; die Nachricht selbst kann auf früheren Käufen und Rezensionen basieren, die der Kunde veröffentlicht hat.

[!DNL Decisioning Service] erleichtert die Personalisierung weiterentwickelter Erlebnisse.

| Vor der Erlebnisentscheidung | Nach der Erlebnisentscheidung |
| --- | --- |
| Personalisieren und optimieren Sie die Benutzererlebnisse in einem einzigen Kanal oder in einem kleinen Satz von Erlebnis-Touchpoints. | Erlebnisse sind über einzelne Interaktionen hinweg aufeinander abgestimmte Reaktionen. |
| Optimierungen konzentrieren sich auf eine einzelne und normalerweise kurze Phase der Journey des Endbenutzers. | Entscheidungen basieren auf dem gesamten Interaktionsverlauf, der von in der Vergangenheit ermittelten Verhaltensweisen bis hin zum aktuellen situationsspezifischen Kontext reicht. |
| Optionen und Strategien zum Auswählen, welche von ihnen während des Erlebnisses eines Kunden angezeigt werden sollen, werden normalerweise tief in einer Anwendung codiert. | Strategien zur Auswahl der besten Option werden außerhalb der kanalspezifischen Anwendungen definiert und sind dadurch wiederverwendbar. |
| Kundenerlebnisse werden anhand eines vereinfachenden Ziels personalisiert und optimiert, z. B. um auf einer Web-Seite die Anzahl erfolgreicher Kassengänge oder die Akzeptanz eines Angebots zu erhöhen, das in einer Interaktion mit einem Kundenbetreuer präsentiert wird. | Kundenerlebnisse werden auf der Grundlage eines ganzheitlichen Verständnisses der aktuellen Bedürfnisse des Kunden optimiert und an alle Erlebnisse des Benutzers angepasst, ob diese gut oder schlecht waren. Eine Marketing-Kampagne ist beispielsweise unter Umständen nicht für Kunden geeignet, die kürzlich eine Beschwerde wegen eines Produkts oder einer Dienstleistung eingereicht haben. |

[!DNL Decisioning Service] weitet Ihre Fähigkeiten bei der Personalisierung von Erlebnissen vom Targeting in einem einzigen Kanal auf die Ermittlung der Gesamtstufe im Lebenszyklus aus, in der sich die Interaktion von Kunden mit Ihrer Marke gerade befindet – und das unabhängig vom Kanal. Eine Lebenszyklusphase ist viel komplexer als eine Segmentzugehörigkeit und basiert fast immer auf komplexen Ereignis-Streams, Verfahrensregeln und prognostizierten Attributen.

Andere Bezeichnungen, die bei Produkten und Dienstleistungen verwendet werden, um ähnliche Anwendungsfälle zu bedienen:

- Real-time Interaction Management (RTIM)
- Journey-Verwaltung
- Omnichannel-Marketing und -Personalisierung
- Echtzeitbasierte Entscheidungsfindung

## How does [!DNL Decisioning Service] work?

Experiences can be customized using [!DNL Decisioning Service] in real time, as your customer engages with your brand via an inbound channel, such as your site or mobile app. Die Entscheidungsfindung kann auch verwendet werden, um Nachrichten über ausgehende Kanäle anzupassen (wie E-Mail oder Push-Benachrichtigung).

Entscheidungen können auf vielerlei Weise getroffen werden. Eine Möglichkeit besteht darin, Optionen nacheinander zu eliminieren, bis entweder nur noch eine übrig ist oder die Optionen reduziert werden und eine Untergruppe übrig bleibt oder aus dem reduzierten Satz ein zufälliger Gewinner ausgewählt wird. Eine Variante dieses Ansatzes besteht darin, zur Auswahl der Gewinnoption eine berechnete Formel zu verwenden. Die Rangeinordnung der zulässigen Optionen erfolgt über eine Funktion. Bei der Entscheidungsfindung für Angebote kann diese Funktion die Kosten und den Wert des Angebots für das Unternehmen berechnen sowie anhand einer vorab festgelegten Methode die Wahrscheinlichkeit ermitteln, dass das Angebot vom Endbenutzer angenommen wird. Die dadurch entstehenden Werte könnten zum Ordnen der Angebote genutzt werden.

Alternativ oder zusätzlich könnte eine Strategie auf Ergebnissen basieren, die aus früheren Interaktionen mit ähnlichen Kunden, denen ähnliche Optionen vorgeschlagen wurden, gewonnen werden. Bei dieser Strategie ist die Funktion, die die Prioritätswerte berechnet hat, erlernt. Der optimale Ergebniswert hängt von den Zielsetzungen der Aktivität ab; der Leistungsindikator für die Vorhersage bestimmt, wie oft das Ergebnis nach dem Vorschlagen der Option erreicht wurde.

### Entscheidungsstrategie

Entscheidungsstrategien werden mit Objekten konfiguriert, die als Aktivitäten bezeichnet werden. Jede Entscheidungsstrategie ist im Wesentlichen ein Algorithmus oder eine Funktion, der bzw. die N Optionen {o1, o2, ...oN} als Eingabe verwendet und eine geordnete Liste von Optionen erzeugt (o1, o2,...oK), wobei die erste Option in der Liste gemäß einem Optimierungskriterium als die beste Option angesehen wird, die zweite Option in der Ergebnisliste dann als die zweitbeste Option usw.

An jeder Stelle der Customer Journey wird die beste Option für eine bestimmte Aktivität anhand aktuellster Kontextvariablen, Regeln und Begrenzungen neu ausgewertet. Kontextvariablen enthalten die in gespeicherten Datensätze [!DNL Real Time Customer Profile]. Eine zentrale Datensatzentität ist das Profil eines Kunden, andere Entitäten wie operative Geschäftsdaten stehen der Aktivität aber gleichermaßen zur Verfügung.

Der Algorithmus oder die Funktion, der bzw. die die Liste der Top-K-Optionen erzeugt, variiert je nach Anwendungsfall. Die internen Komponenten dieses Algorithmus unterscheiden sich je nach Anwendungsfall. Die Komponenten werden zur Entwurfszeit in einem Repository definiert und für die fallspezifische Entscheidungsstrategie in Anweisungen „kompiliert“.

![decision-optimization](./images/decisioning-optimization.png)

## Arbeiten mit [!DNL Decisioning Service]

The [!DNL Decisioning Service], like other [!DNL Platform] services, adopts an API first philosophy. Das bedeutet, dass die API die primäre Schnittstelle ist, über die alle Funktionen, einschließlich Verwaltungsfunktionen, verfügbar gemacht werden. It also means that other [!DNL Platform] services, Adobe solutions, and 3rd party integrations use the same APIs.

You can use [!DNL Decisioning Service] in a synchronous request-response interaction mode facilitated by a simple HTTP REST API. Der API-Aufruf gibt die derzeit beste Option für ein einzelnes Profil zurück. Die Auswahl der derzeit besten Option ändert sich je nach den Regeln und Begrenzungen, die für alle Optionen gelten, die von einer bestimmten Aktivität in Betracht gezogen werden. Die REST-API ermöglicht es auch, die nächste beste Option für mehrere Aktivitäten gleichzeitig abzurufen. Dies erlaubt eine Vermittlung von Optionen über verschiedene Kanäle hinweg. Wenn Antworten für mehrere Aktivitäten zusammen abgerufen werden, können zusätzliche Regeln angewendet werden.

![decisioning-API](./images/decisioning-API.png)

### Integration with other [!DNL Platform] workflows

Use of [!DNL Decisioning Service] is optional and only requires a few steps in addition to the typical steps required to create [!DNL Profile] entities and manage them.

>[!NOTE]
>
>To make the most out of the [!DNL Real-time Customer Profile], the [!DNL Decisioning Service] directly integrates with the profile store. Die API-Aufrufe müssen nur eine der Identitäten für ein bestimmtes Profil angeben.

Die typische Abfolge von Schritten beginnt mit dem Erstellen von Profilen:

- Authentifizieren Sie sich bei [!DNL Experience Platform].
- Definieren Sie ein Schema, das auf der Profilklasse basiert, und definieren Sie optional ein Schema, das auf der Erlebnisereignisklasse basiert.
- Configure a dataset to upload record and time series data to [!DNL Customer Profile].
- Fügen Sie Daten über den im vorherigen Schritt konfigurierten Datensatz hinzu oder streamen Sie Instanzdaten über die Pipeline.
- Stream experience events into the [!DNL Platform] to enrich the profile with behavioral data.

Additionally, to use [!DNL Decisioning Service], the following steps:

- Definieren Sie mithilfe der Repository-APIs Entscheidungskomponenten. Das sind die Geschäftslogikentitäten, die die Entscheidungsstrategie ausmachen. The decision components will be automatically compiled into a format used by the [!DNL Decision Service Runtime]. Die Repository-APIs werden im unten stehenden Diagramm auf der linken Seite dargestellt.
- Rufen Sie die Runtime-API auf, um gemäß der im vorherigen Schritt definierten Geschäftslogik die beste Option abzurufen. The [!DNL Decision Service Runtime] APIs are illustrated on the right side in the diagram below.

![decisioning-API1](./images/decisioning-API1.png)

Die Aktivierung der Geschäftslogikentitäten erfolgt automatisch und kontinuierlich. Sobald eine neue Option im Repository gespeichert und als „genehmigt“ markiert wird, gehört sie zu den Kandidaten für die Einbeziehung in den Satz der verfügbaren Optionen. Sobald eine Entscheidungsregel aktualisiert wird, wird der Regelsatz neu zusammengestellt und für die Laufzeitausführung vorbereitet. Bei diesem automatischen Aktivierungsschritt werden alle von der Geschäftslogik definierten Begrenzungen, die nicht vom Laufzeitkontext abhängen, ausgewertet. The results of this activation step are sent to a cache where they are available to the [!DNL Decisioning Service] runtime. Dies wird im folgenden Diagramm veranschaulicht.

![decisioning-API2](./images/decisioning-API2.png)

Once the option sets, rule sets and constraints are activated, and have been pushed to [!DNL Decisioning Service] nodes, a simple API is used to post a request for a decision. Die API wird in der Regel von einem Versanddienst aufgerufen, der dann die vorgeschlagene Option nimmt (z. B. nächste beste Aktion oder nächstes bestes Angebot) und das Erlebnis zusammensetzt oder die Aktion ausführt. Wenn es sich bei dem Vorschlag um ein Angebot handelt, wird der Inhalt, der dieses Angebot darstellt, nachgeschlagen und in ein Erlebnis eingefügt, das dem Endbenutzer angezeigt wird. Dies wird im folgenden Diagramm veranschaulicht.

![decisioning-API3](./images/decisioning-API3.png)

[!DNL Delivery Service] Assembliert Daten für die Entscheidungsanforderung. Er ermittelt die Kennung der Profilentität, für die die beste Option ausgewählt werden soll. It also assembles any context data that is not stored in [!DNL Customer Profile] but is potentially used by the decision logic.

Die Entscheidungslogik ist anhand von Aktivitäten organisiert, von denen jede einen Filter für die Untergruppe der Optionen angibt, die für diese Aktivität berücksichtigt werden sollten, zusammen mit einer einzelnen Fallback-Option.

Eine Entscheidung wird getroffen, indem zunächst Begrenzungen angewendet werden, um die Anzahl der Optionen zu verringern, und die verbleibenden Optionen dann nach Rang geordnet werden. Although most of the logic is evaluated inside [!DNL Decisioning Service], various adjunct services are used to help with these two aspects. Beispielsweise verwaltet ein Begrenzungsdienst Obergrenzen dafür, wie oft eine Option bei jeder Entscheidung verwendet werden kann; ein anderer Dienst hostet vielleicht ein maschinelles Lernmodell, das zur Berechnung der Werte für ein Profil und eine Option genutzt wird.

Weiterführende Informationen zur Verwendung der Repository-APIs finden Sie in der Anleitung zum [Verwalten von Entscheidungsentitäten und Regeln mithilfe von APIs](./tutorials/entities.md).

To learn more about using the [!DNL Decisioning Service] runtime, see the tutorial on [Working with the Decisioning Service runtime using APIs](./tutorials/runtime.md)