---
title: Verwenden von Wetterdaten aus DNL The Wetter Channel
description: Verwenden Sie Wetterdaten aus DNL The Weather Channel , um die Daten zu verbessern, die Sie über Datastreams erfassen.
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 4%

---

# Verwenden von Wetterdaten aus [!DNL The Weather Channel]

Adobe hat sich mit [!DNL [The Weather Company]](https://www.ibm.com/weather) , um den zusätzlichen Kontext des Wetters in den Vereinigten Staaten auf die Daten zu übertragen, die über Datenspeicher erfasst wurden. Sie können diese Daten für Analysen, Targeting und Segmenterstellung in Experience Platform verwenden.

Es gibt 3 Datentypen, die in verfügbar sind [!DNL The Weather Channel]:

* **[!UICONTROL Aktuelles Wetter]**: Die aktuellen Wetterbedingungen des Benutzers basierend auf seinem Standort. Dazu gehören aktuelle Temperatur, Rezeption, Cloud-Abdeckung und mehr.
* **[!UICONTROL Vorhergesagtes Wetter]**: In der Prognose sind die 1,2,3,5,7 und die 10-tägigen Prognosen für den Standort des Nutzers enthalten.
* **[!UICONTROL Trigger]**: Trigger sind spezifische Kombinationen, die sich unterschiedlichen semantischen Wetterbedingungen zuordnen. Es gibt drei verschiedene Wettertypen:

   * **[!UICONTROL Wetter-Trigger]**: Semantisch aussagekräftige Bedingungen wie kaltes oder regnerisches Wetter. Diese können sich in ihren Definitionen in verschiedenen Klimazonen unterscheiden.
   * **[!UICONTROL Produkt-Trigger]**: Bedingungen, die zum Kauf verschiedener Produktarten führen würden. Beispiel: Die kalten Wettervorhersagen könnten dazu führen, dass der Kauf von Regenmänteln wahrscheinlicher ist.
   * **[!UICONTROL Schweres Wetter - Trigger]**: Schwere Wetterwarnungen wie Winterstürme oder Hurrikan-Warnungen.

## Voraussetzungen {#prerequisites}

Bevor Sie Wetterdaten verwenden, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Sie müssen die von Ihnen verwendeten Wetterdaten lizenzieren, von [!DNL The Weather Channel]. Er wird es dann auf Ihrem Konto aktivieren.
* Wetterdaten sind nur über Datastreams verfügbar. Um Wetterdaten zu verwenden, müssen Sie [!DNL Web SDK], [!DNL Mobile Edge Extension] oder [Server-API](../../../server-api/overview.md) , um diese Daten zu nutzen.
* Ihr Datastream muss über [[!UICONTROL Geo-Position]](../configure.md#advanced-options) aktiviert.
* Fügen Sie die [Wetterfeldgruppe](#schema-configuration) dem verwendeten Schema.

## Bereitstellung {#provisioning}

Sobald Sie die Daten lizenziert haben von [!DNL The Weather Channel], wird Ihr Konto auf die Daten zugreifen können. Als Nächstes müssen Sie sich an die Kundenunterstützung von Adobe wenden, damit die Daten in Ihrem Datastream aktiviert werden. Nach der Aktivierung werden die Daten automatisch angehängt.

Sie können überprüfen, ob es hinzugefügt wird, indem Sie mit dem Debugger einen Edge-Trace ausführen oder mithilfe von Assurance einen Treffer durch das [!DNL Edge Network].

### Schemakonfiguration {#schema-configuration}

Sie müssen die Wetterfeldgruppen zu Ihrem Experience Platform-Schema hinzufügen, die dem Ereignisdatensatz entsprechen, den Sie in Ihrem Datastream verwenden. Es stehen fünf Feldergruppen zur Verfügung:

* [!UICONTROL Vorhergesagtes Wetter]
* [!UICONTROL Aktuelles Wetter]
* [!UICONTROL Produkt-Trigger]
* [!UICONTROL Relative Trigger]
* [!UICONTROL Schweres Wetter - Trigger]

## Zugriff auf Wetterdaten {#access-weather-data}

Sobald Ihre Daten lizenziert und verfügbar sind, können Sie sie in den Adobe-Diensten auf verschiedene Arten aufrufen.

### Adobe Analytics {#analytics}

In [!DNL Adobe Analytics], sind die Wetterdaten für die Zuordnung über Verarbeitungsregeln verfügbar, zusammen mit dem Rest Ihrer [!DNL XDM] Schema.

Die Liste der Felder, die Sie zuordnen können, finden Sie im [Wetterreferenz](weather-reference.md) Seite. Wie bei allen [!DNL XDM] Schemas, den Schlüsseln das Präfix `a.x`. Beispiel: ein Feld mit dem Namen `weather.current.temperature.farenheit` würde in [!DNL Analytics] as `a.x.weather.current.temperature.farenheit`.

![Benutzeroberfläche für Verarbeitungsregeln](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

In [!DNL Adobe Customer Journey Analytics], sind die Wetterdaten im Datensatz verfügbar, der im Datastream angegeben ist. Solange die Wetterattribute [zu Ihrem Schema hinzugefügt wurde](#prerequisites-prerequisites), können sie [Hinzufügen zu einer Datenansicht](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=de) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

Die Wetterdaten sind im [Real-time Customer Data Platform](../../../rtcdp/overview.md), zur Verwendung in Segmenten. Wetterdaten werden an Ereignisse angehängt.

![Segment Builder mit Wetterereignissen](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

Da sich die Wetterbedingungen häufig ändern, empfiehlt Adobe, die Segmente zeitlich zu begrenzen, wie im Beispiel oben gezeigt. Einen kalten Tag in den letzten ein oder zwei Tagen zu haben ist viel wirkungsvoller als einen kalten Tag vor 6 Monaten.

Siehe [Wetterreferenz](weather-reference.md) für die verfügbaren Felder.

### Adobe Target {#target}

In [!DNL Adobe Target]können Sie mithilfe von Wetterdaten die Personalisierung in Echtzeit vorantreiben. Wetterdaten werden an [!DNL Target] as [!UICONTROL mBox] Parameter und Sie können darauf über eine benutzerdefinierte [!UICONTROL mBox] Parameter.

![Target Audience Builder](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

Der Parameter ist die [!DNL XDM] Pfad zu einem bestimmten Feld. Siehe [Wetterreferenz](weather-reference.md) für die verfügbaren Felder und die entsprechenden Pfade.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments können Sie nun besser verstehen, wie Sie Wetterdaten in verschiedenen Adobe-Lösungen verwenden können. Weitere Informationen zur Zuordnung der Wetterdaten finden Sie in der [Feldzuordnungsreferenz](weather-reference.md).
