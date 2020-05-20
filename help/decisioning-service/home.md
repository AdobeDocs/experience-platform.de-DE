---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entscheidungsdienst
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 0%

---


# Übersicht über den Entscheidungsdienst

Der Entscheidungsdienst bietet die Möglichkeit, personalisierte, optimierte und orchestrierte Erlebnisse in Anwendungen zu erstellen, die auf der Adobe Experience Platform ausgeführt werden. Mithilfe des Entscheidungsdienstes können Sie die beste *Option* aus einer Reihe verfügbarer Optionen bestimmen. Diese Optionen, auch als Alternativen bezeichnet, könnten Angebot, Produktempfehlungen, Inhaltskomponenten für ein Web-Erlebnis, Gesprächsskripte und zu ergreifende Maßnahmen sein. Derzeit werden der Anwendungsfall und die Domäne der Entscheidungsfindung für *Angebot* unterstützt, wobei Entscheidungsoptionen spezifisch als Angebote modelliert werden, wobei weitere Anwendungsfälle unterstützt werden.

Mit dem Entscheidungsdienst können Kunden Geschäftslogik wiederverwenden und einen Optionskatalog für verschiedene Kanal und Anwendungen freigeben. Statt Entscheidungsoptionen - und Auswahlstrategien - tief in einer Anwendung zu verwalten, können sie jetzt unabhängig davon genutzt werden, wann, wie und auf welchem Kanal der Endbenutzer mit einem Unternehmen oder einer Organisation interagiert.

Entscheidungsstrategien können die vielen Interaktionen berücksichtigen, die ein Kunde über viele Kanal und Anwendungen hinweg hatte. Beispielsweise könnte die Aktivität der Call-Center-Anwendung eine Marketingnachricht nach einer Beschwerde für einige Zeit aktivieren oder unterdrücken, und diese Nachricht selbst kann auf Käufen und Rezensionen basieren, die vom Kunden veröffentlicht wurden.

Der Entscheidungsdienst erleichtert die Personalisierung weiterentwickelter Erlebnisse.

| Vor der Erlebnisentscheidung | Nach der Erlebnisentscheidung |
| --- | --- |
| Personalisieren und optimieren Sie die Benutzererfahrungen in einem einzigen Kanal oder in einem kleinen Satz von Erlebnis-Touchpoints. | Erlebnisse sind aufeinander abgestimmte Reaktionen über Interaktionen hinweg. |
| Optimierungen konzentrieren sich auf eine einzelne und normalerweise kurze Phase der Reise des Endbenutzers. | Die Entscheidungen basieren auf dem gesamten Interaktionsverlauf, der von in der Vergangenheit entdeckten Verhaltensweisen bis hin zum aktuellen situationsspezifischen Kontext reicht. |
| Optionen und die Strategien zur Auswahl, welche während des Kundenerlebnisses angezeigt werden sollen, werden normalerweise tief in einer Anwendung codiert. | Strategien zur Auswahl der besten Option werden außerhalb der Kanal-spezifischen Anwendungen definiert und wiederverwendbar. |
| Kundenerlebnisse werden nach einem vereinfachenden Ziel personalisiert und optimiert, z.B. die Anzahl erfolgreicher Kassengänge auf einer Webseite oder die Akzeptanz eines Angebots, das in Interaktion mit einem Kundenbetreuer präsentiert wird. | Kundenerlebnisse werden auf der Grundlage eines ganzheitlichen Verständnisses der aktuellen Bedürfnisse des Kunden optimiert und an alle Erlebnisse des Benutzers angepasst, ob gut oder schlecht. Eine Marketing-Kampagne ist beispielsweise nicht geeignet für Kunden, die kürzlich eine Beschwerde über ein Produkt oder eine Dienstleistung eingereicht haben. |

Der Entscheidungsdienst verschiebt Ihre Fähigkeiten zur Personalisierung Ihres Erlebnisses von Targeting in einem einzigen Kanal bis zur Bestimmung der Gesamtphase im Lebenszyklus der Interaktion Ihrer Kunden mit Ihrer Marke, unabhängig von den Kanal. Eine Lebenszyklusphase ist viel komplexer als eine Segmentmitgliedschaft und basiert fast immer auf komplexen Ereignissen, Geschäftsregeln und prognostizierten Attributen.

Andere Begriffe, die von Produkten und Dienstleistungen verwendet werden, um ähnliche Anwendungsfälle zu bedienen:

- Echtzeit-Interaktionsmanagement (RTIM)
- Reisemanagement
- Marketing und Personalisierung von Omniture Kanal
- Echtzeit-Entscheidungsfindung

## Wie funktioniert der Entscheidungsdienst?

Erlebnisse können mit dem Entscheidungsdienst in Echtzeit angepasst werden, wenn Ihr Kunde über einen eingehenden Kanal wie Ihre Site oder mobile App mit Ihrer Marke interagiert. Die Entscheidungsfindung kann auch verwendet werden, um Nachrichten über ausgehende Kanal wie eine E-Mail- oder eine Push-Benachrichtigung anzupassen.

Entscheidungen können auf vielerlei Weise getroffen werden. Eine Möglichkeit besteht darin, Optionen nacheinander zu entfernen, bis entweder nur eine übrig bleibt oder die Optionen heruntergepeilt wurden und eine Untergruppe verbleibt oder ein Gewinner zufällig aus dem reduzierten Satz ausgewählt wird. Eine Variante dieses Ansatzes zur Auswahl der Gewinnoption nach einer berechneten Formel. Die Rangordnung der zulässigen Optionen erfolgt über eine Funktion. Bei der Angebot-Entscheidungsfindung könnte diese Funktion die Kosten und den Wert des Angebots für das Unternehmen berechnen und die Wahrscheinlichkeit, dass das Angebot vom Endbenutzer akzeptiert wird, anhand einer vorab festgelegten Methode ermitteln. Das Ergebnis kann zur Bestellung der Angebot verwendet werden.

Alternativ oder zusätzlich könnte eine Strategie auf Ergebnissen basieren, die aus früheren Interaktionen mit ähnlichen Kunden, denen ähnliche Optionen vorgeschlagen wurden, gewonnen wurden. In dieser Strategie wird die Funktion, die die Prioritätswerte berechnet hat, erlernt. Der optimale Ergebniswert ist an die Zielsetzungen der Aktivität gebunden, und der Leistungsindikator für die Vorhersage bestimmt, wie oft das Ergebnis nach dem Vorschlag der Option erreicht wurde.

### Entscheidungsstrategie

Entscheidungsstrategien werden über Objekte konfiguriert, die als _Aktivitäten_ bezeichnet werden. Jede Entscheidungsstrategie ist im Wesentlichen ein Algorithmus oder eine Funktion, die die N-Optionen {o1, o2, ...oN} als Eingabe verwendet und eine geordnete Liste von Optionen erzeugt (o1, o2,...oK), wobei die erste Option in der Liste gemäß einem Optimierungskriterium als die beste Option angesehen wird, die zweite Option in der Ergebnisoption dann als die zweitbeste Option usw.

Zu jeder Zeit während der Customer Journey wird die beste Option für eine bestimmte Aktivität anhand der aktuellsten Kontextvariablen, Regeln und Einschränkungen neu bewertet. Kontextvariablen enthalten die im Echtzeit-Kundenkonto gespeicherten Datensätze. Eine zentrale Datensatzeinheit ist das Profil eines Kunden, aber andere Entitäten wie operative Geschäftsdaten stehen der Aktivität gleichermaßen zur Verfügung.

Der Algorithmus oder die Funktion, die die Liste der Top-K-Optionen erzeugt, variiert je nach Anwendungsfall. Die internen Komponenten dieses Algorithmus unterscheiden sich je nach Anwendungsfall. Die Komponenten werden zur Entwurfszeit in einem Repository definiert und &quot;kompiliert&quot;in Anweisungen für die fallspezifische Entscheidungsstrategie.

![Entscheidungsoptimierung](./images/decisioning-optimization.png)

## Arbeiten mit dem Entscheidungsdienst

Der Entscheidungsdienst verfolgt wie andere Plattformdienste eine erste API-Philosophie. Das bedeutet, dass die API die primäre Schnittstelle ist, auf der alle Funktionen, einschließlich Verwaltungsfunktionen, über APIs zur Verfügung gestellt werden. Das bedeutet auch, dass andere Plattformdienste, Adobe-Lösungen und Drittanbieter-Integrationen dieselben APIs verwenden.

Sie können den Entscheidungsdienst in einem synchronen Interaktionsmodus für Anforderung und Antwort verwenden, der durch eine einfache HTTP-REST-API erleichtert wird. Der API-Aufruf gibt die derzeit beste Option für ein einzelnes Profil zurück. Die Auswahl der derzeit besten Option ändert sich je nach den Regeln und Einschränkungen, die für alle Optionen gelten, die von einer bestimmten Aktivität in Betracht gezogen werden. Die REST-API ermöglicht es, die nächste beste Option für mehrere Aktivitäten gleichzeitig zu erhalten. Dies ermöglicht die Schiedsgerichtsbarkeit von Optionen über Kanäle hinweg. Wenn Antworten für mehrere Aktivitäten zusammen abgerufen werden, können zusätzliche Regeln angewendet werden.

![decisioning-API](./images/decisioning-API.png)

### Integration in andere Workflows

Die Verwendung des Entscheidungsdienstes ist optional und erfordert nur einige Schritte zusätzlich zu den typischen Schritten, die zum Erstellen und Verwalten von Profil-Entitäten erforderlich sind.

>[!NOTE] Um das Echtzeit-Profil des Kunden optimal zu nutzen, integriert sich der Entscheidungsdienst direkt in den Profil Store. Die API-Aufrufe müssen nur eine der Identitäten für ein bestimmtes Profil angeben.

Die typische Abfolge von Beginn mit dem Erstellen von Profilen:

- Authentifizierung für Experience Platform.
- Definieren Sie ein Schema, das auf der Profil-Klasse basiert, und definieren Sie optional ein Schema, das auf der Experience Ereignis-Klasse basiert.
- Konfigurieren Sie einen Datensatz, um Daten aus Datensatz- und Zeitreihen in das Customer Profil hochzuladen.
- Hinzufügen Daten über den im vorherigen Schritt konfigurierten Datensatz oder Stream-Instanzdaten über Pipeline.
- Streamen Sie Erlebnis-Ereignis in die Plattform, um das Profil mit Verhaltensdaten zu bereichern.

Um den Entscheidungsdienst zu verwenden, führen Sie außerdem die folgenden Schritte aus:

- Definieren Sie Entscheidungskomponenten mithilfe der Repository-APIs. Dies sind die Geschäftslogik-Entitäten, die die Entscheidungsstrategie ausmachen. Die Entscheidungskomponenten werden automatisch in ein Format kompiliert, das von der Decision Service Runtime verwendet wird. Die Repository-APIs werden im unten stehenden Diagramm auf der linken Seite dargestellt.
- Rufen Sie die Laufzeit-API auf, um die beste Option gemäß der im vorherigen Schritt definierten Geschäftslogik abzurufen. Die Decision Service Runtime-APIs sind im unten stehenden Diagramm rechts dargestellt.

![decisioning-API1](./images/decisioning-API1.png)

Die Aktivierung der Business-Logik-Entitäten erfolgt automatisch und kontinuierlich. Sobald eine neue Option im Repository gespeichert und als &quot;genehmigt&quot;markiert ist, wird sie in den Satz der verfügbaren Optionen aufgenommen. Sobald eine Entscheidungsregel aktualisiert wird, wird der Regelsatz neu zusammengestellt und für die Ausführung zur Laufzeit vorbereitet. Bei diesem Schritt der automatischen Aktivierung werden alle von der Geschäftslogik definierten Einschränkungen, die nicht vom Laufzeitkontext abhängen, ausgewertet. Die Ergebnisse dieses Aktivierung-Schritts werden an einen Cache gesendet, wo sie für die Laufzeit des Entscheidungsdienstes verfügbar sind. Dies wird im folgenden Diagramm veranschaulicht.

![decisioning-API2](./images/decisioning-API2.png)

Sobald die Option festgelegt, Regelsätze und Beschränkungen aktiviert und an die Entscheidungsdienstknoten gesendet wurde, wird eine einfache API zum Posten einer Anforderung für eine Entscheidung verwendet. Die API wird in der Regel von einem Versand-Dienst aufgerufen, der dann die vorgeschlagene Option übernimmt (z. B. Nächste beste Aktion oder nächstes bestes Angebot) und das Erlebnis zusammenführt oder die Aktion ausführt. Wenn es sich bei dem Vorschlag um ein Angebot handelt, wird der Inhalt, der dieses Angebot darstellt, nachgeschlagen und in ein Erlebnis eingefügt, das dem Endbenutzer bereitgestellt wird. Dies wird im folgenden Diagramm veranschaulicht.

![decisioning-API3](./images/decisioning-API3.png)

Versand Service sammelt Daten für die Entscheidungsanforderung. Er bestimmt die ID der Profil-Entität, für die die beste Option ausgewählt wird. Es werden auch alle Kontextdaten zusammengestellt, die nicht im Customer Profil gespeichert, sondern möglicherweise von der Entscheidungslogik verwendet werden.

Die Entscheidungslogik ist nach Aktivitäten organisiert, von denen jede einen Filter für die Untergruppe der Optionen angibt, die für diese Aktivität berücksichtigt werden sollten, zusammen mit einer einzelnen Ausweichoption.

Jede Entscheidung wird getroffen, indem zunächst Beschränkungen angewendet werden, um die Anzahl der Optionen zu verringern, und dann die verbleibenden Optionen nach Rang geordnet werden. Obwohl der Großteil der Logik innerhalb des Entscheidungsdienstes ausgewertet wird, werden verschiedene Zusatzdienste verwendet, um bei diesen beiden Aspekten zu helfen. Beispielsweise verwaltet ein Capping-Dienst Obergrenzen dafür, wie oft eine Option bei jeder Entscheidung verwendet werden kann, und ein anderer Dienst kann ein maschinelles Lernmodell hosten, das zur Berechnung der Ergebnisse für ein Profil und eine Option verwendet wird.

Weitere Informationen zur Verwendung der Repository-APIs finden Sie im Lernprogramm zur [Verwaltung von Entscheidungsinstanzen und Regeln mithilfe von APIs](./tutorials/entities.md)

Weitere Informationen zur Verwendung der Laufzeit des Entscheidungsdienst finden Sie im Lernprogramm zum [Arbeiten mit der Laufzeit des Entscheidungsdienstes mithilfe von APIs](./tutorials/runtime.md)