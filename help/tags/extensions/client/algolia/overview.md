---
title: Algolia Tags-Erweiterung - Übersicht
description: Erfahren Sie mehr über die Algolia Tags-Erweiterung in Adobe Experience Platform.
source-git-commit: 5b488a596472fe61b487f75ad62d741237caa820
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 2%

---

# [!DNL Algolia] Tags-Erweiterung - Übersicht

Mit der [!DNL Algolia] Tags-Erweiterung können Marketing-Fachleute problemlos Regeln einrichten, mit denen Benutzerinteraktionsdaten an [!DNL Algolia] gesendet werden, damit Sie personalisiertere KI-Such- und -Erkennungserlebnisse bereitstellen können.

Diese Erweiterung basiert auf einer wichtigen Funktion:

* **[!DNL Algolia]Insights**: Erfasst automatisch Benutzerinteraktionsereignisse und sendet diese an [!DNL Algolia]. Dadurch werden leistungsstarke Analysen, personalisierte Erlebnisse und eine verbesserte Suchrelevanz ermöglicht.

## Voraussetzungen {#prerequisites}

Sie müssen über ein gültiges [!DNL Algolia] verfügen, um diese Erweiterung verwenden zu können. Gehen Sie zur [[!DNL Algolia] Anmeldeseite](https://dashboard.algolia.com/users/sign_up), um ein Konto zu erstellen, falls Sie noch keines haben.

### Sammeln erforderlicher Konfigurationsdetails {#configuration-details}

Um [!DNL Algolia] mit Adobe Experience Platform zu verbinden, benötigen Sie die folgenden Informationen:

| Anmeldedaten | Beschreibung | Beispiel |
| --- | --- | --- |
| Anwendungs-ID | Ihre Anwendungs-ID finden Sie [ Abschnitt „API](https://www.algolia.com/account/api-keys/all)Schlüssel“ in Ihrem [!DNL Algolia]-Dashboard. | 0ABCDEFG12 |
| API-Schlüssel suchen | Ihren API-Schlüssel für die Suche finden Sie [ Abschnitt ](https://www.algolia.com/account/api-keys/all)API-Schlüssel“ in Ihrem [!DNL Algolia]-Dashboard. | 1234a12345678901b1234567890c1ab1 |

## Installieren und Konfigurieren der [!DNL Algolia] Insights-Erweiterung {#install-configure}

Um die [!DNL Algolia] Insights-Erweiterung zu installieren, navigieren Sie zur [!UICONTROL Datenerfassungs-Benutzeroberfläche] und wählen Sie **[!UICONTROL Tags]** aus der linken Navigationsleiste aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, klicken Sie im linken **auf** Erweiterungen und wählen Sie dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!DNL Algolia] Insights und wählen Sie dann **[!UICONTROL Installieren]** aus.

![](../../../images/extensions/client/algolia/install.png)

In der Konfigurationsansicht, die angezeigt wird, müssen Sie die folgenden Details angeben:

| Eigenschaft | Beschreibung |
| --- | --- |
| Anwendungs-ID | Geben Sie die [!UICONTROL Anwendungs-ID] ein, die Sie zuvor im Abschnitt [Konfigurationsdetails](#configuration-details) erfasst haben. |
| API-Schlüssel suchen | Geben Sie den [!UICONTROL Such-API-Schlüssel] ein, den Sie zuvor im Abschnitt [Konfigurationsdetails](#configuration-details) erfasst haben. |
| Indexname | Der [!UICONTROL Indexname] enthält die Produkte oder Inhalte.  Dieser Index wird als Standard verwendet. |
| Benutzer-Token-Datenelement | Das Datenelement, das das Benutzer-Token zurückgibt. |
| Authentifiziertes Benutzer-Token-Datenelement | Legen Sie das Datenelement fest, das das Token für authentifizierte Benutzer zurückgibt. |
| Währung | Wählen Sie einen Währungstyp.  Der Standardwert ist auf `USD` festgelegt. |

![](../../../images/extensions/client/algolia/configure.png)

## [!DNL Algolia] Insights-Erweiterung - Aktionstypen {#action-types}

[!DNL Algolia] unterstützt eine Reihe vordefinierter Standardereignisse mit jeweils spezifischen Kontexten und Eigenschaften. Die in der [!DNL Algolia]-Erweiterung verfügbaren Aktionen werden diesen Ereignistypen zugeordnet, sodass Sie die Ereignisse, die Sie an [!DNL Algolia] senden, einfach anhand ihres Typs kategorisieren und konfigurieren können.

### Einblicke laden {#load-insights}

>[!NOTE]
>
>In den meisten Fällen wird empfohlen, [!DNL Algolia] Insights auf jeder Seite Ihrer Site zu laden.

Fügen Sie die Aktion **[!UICONTROL Einblicke laden]** zu Ihrer Tag-Regel hinzu, wo es am sinnvollsten ist, [!DNL Algolia] Einblicke basierend auf dem Kontext Ihrer Regel zu laden. Diese Aktion lädt die `search-insights.js` auf der Seite.

Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und wählen Sie **[!UICONTROL Insights laden]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Insight-Bibliotheksversion] | Die [!DNL Algolia] Insights-Version. Die Standardeinstellung lautet `2.13.0`. |
| [!UICONTROL Benutzer-Opt-out-Datenelement] | Das Datenelement, das die Tracking-Voreinstellungen des Benutzers erfasst. |
| [!UICONTROL Benutzer-Token-Cookie verwenden] | Aktivieren Sie dieses Kontrollkästchen, damit [!DNL Algolia] ein Benutzer-Token-Cookie generieren können. Standardmäßig ist diese Option auf `false` festgelegt. |

![](../../../images/extensions/client/algolia/load-insights.png)

### Angeklickt {#clicked}

Fügen Sie die Aktion **[!UICONTROL Klicken]** zu Ihrer Tag-Regel hinzu, um angeklickte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen und wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und **[!UICONTROL angeklickt]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Ereignisname] | Der Ereignisname, der verwendet werden kann, um dieses Klickereignis weiter einzuengen. |
| Datenelement für Ereignisdetails | Das Datenelement, das die Ereignisdetails abruft, einschließlich `indexName`, `objectIDs` und optional `queryID`, `position`. Wenn sowohl `queryID` als auch `position` enthalten sind, wird das Ereignis als *angeklickte Objekt-IDs nach der Suche* kategorisiert, andernfalls wird es als *angeklickte Objekt-IDs*-Ereignis behandelt. Wenn das Datenelement keinen Indexnamen bereitstellt, wird der standardmäßige Indexname beim Senden des Ereignisses verwendet. |

![](../../../images/extensions/client/algolia/clicked.png)

### Konvertiert {#converted}

Fügen Sie die Aktion **[!UICONTROL Konvertiert]** zu Ihrer Tag-Regel hinzu, um konvertierte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und wählen Sie **[!UICONTROL Konvertiert]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| Ereignisname | Der Ereignisname, der verwendet wird, um dieses &quot;**&quot;-** weiter einzuengen. |
| Datenelement für Ereignisdetails | Das Datenelement, das die Ereignisdetails abruft, einschließlich `indexName`, `objectId` und optional `queryId`. Wenn das Datenelement `queryId` enthält, wird das Ereignis als *Nach Suche konvertiert“ klassifiziert* andernfalls wird es als *Konvertiert*-Ereignisklasse betrachtet. Wenn das Datenelement keinen Indexnamen bereitstellt, wird der standardmäßige Indexname beim Senden des Ereignisses verwendet. |

![](../../../images/extensions/client/algolia/converted.png)

### Zum Warenkorb hinzufügen {#added-to-cart}

Fügen Sie die Aktion **[!UICONTROL Zum Warenkorb hinzugefügt]** zu Ihrer Tag-Regel hinzu, um hinzugefügte Warenkorbereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und wählen Sie **[!UICONTROL Zum Warenkorb hinzugefügt]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| Ereignisname | Der Ereignisname, der verwendet wird, um dieses &quot;**&quot;-** weiter einzuengen. |
| Datenelement für Ereignisdetails | Das Datenelement, das die Ereignisdetails abruft, einschließlich `indexName`, `objectId` und optional `queryId`, `objectData`. Wenn das Datenelement `queryId` enthält, wird das Ereignis als *Zu Warenkorb-Objekt-IDs hinzugefügt nach der Suche* klassifiziert, andernfalls wird es als Ereignisklasse *Zu Warenkorb-Objekt-IDs hinzugefügt* betrachtet. Wenn das Datenelement keinen Indexnamen bereitstellt, wird der standardmäßige Indexname beim Senden des Ereignisses verwendet. |
| Währung | Gibt den Währungstyp an, z. B. `USD`. |

![](../../../images/extensions/client/algolia/added-to-cart.png)

### Purchased {#purchased}

Fügen Sie die Aktion **[!UICONTROL Zum Warenkorb hinzugefügt]** zu Ihrer Tag-Regel hinzu, um gekaufte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und wählen Sie **[!UICONTROL Erworben]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| Ereignisname | Der Ereignisname, der verwendet wird, um dieses „Kauf“-**weiter** verfeinern. |
| Datenelement für Ereignisdetails | Das Datenelement, das die Ereignisdetails abruft, einschließlich `indexName`, `objectId` und optional `queryId`. Wenn das Datenelement `queryId` enthält, wird das Ereignis nach der Suche als *Erworbene Objekt-IDs* klassifiziert, andernfalls wird es als Ereignisklasse *Erworbene Objekt-IDs* betrachtet. Wenn das Datenelement keinen Indexnamen bereitstellt, wird der standardmäßige Indexname beim Senden des Ereignisses verwendet. |

![](../../../images/extensions/client/algolia/purchased.png)

### Angesehen {#viewed}

Fügen Sie die Aktion **[!UICONTROL Zum Warenkorb hinzugefügt]** zu Ihrer Tag-Regel hinzu, um gekaufte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen und wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und **[!UICONTROL Angezeigt]** als [!UICONTROL Aktionstyp].

![](../../../images/extensions/client/algolia/viewed.png)

| Eigenschaft | Beschreibung |
| --- | --- |
| Ereignisname | Der Ereignisname, der verwendet wird, um dieses Ereignis **Ansicht** weiter einzuengen. |
| Datenelement für Ereignisdetails | Das Datenelement, das die Ereignisdetails abruft, einschließlich `indexName` und `objectId`. Wenn `indexName` nicht verfügbar ist, wird der standardmäßige Indexname beim Senden der Ereignisse verwendet. |

## [!DNL Algolia] Insights-Erweiterung - Datenelemente {#data-elements}

[!DNL Algolia] unterstützt einen Satz vordefinierter Datenelemente mit jeweils spezifischen Kontexten und Eigenschaften. In den folgenden Abschnitten werden die in der [!DNL Algolia] Insights-Erweiterung verfügbaren Datenelemente beschrieben.

### Datensatz {#dataset}

Das DataSet-Datenelement ruft Daten ab, die mit HTML-Elementen verknüpft sind. Diese werden dann in [!DNL Algolia] verwendet.

| Eigenschaft | Beschreibung |
| --- | --- |
| Treffer-Element/div-Klassenname | Der HTML-Elementname und/oder CSS-Klassenname, der die Datensatzattribute einschließlich `data-insights-object-id` und optional `data-insights-query-id` und `data-insights-position` auf dem HTML-Element enthält. |
| Indexname Element div/Klassenname | Der HTML-Elementname und/oder CSS-Klassenname mit den Datensatzattributen (`data-indexname`) im HTML-Element. |

![](../../../images/extensions/client/algolia/dataset.png)

Dieses Datenelement gibt zurück:

```javascript
{
  timestamp,
    queryID,
    indexName,
    objectIDs,
    positions
}
```

Ein Beispiel für HTML, das einen Datensatz enthält:

```html
<div data-indexname="acme_master_default_products" class="instant-search-comp__hits">
  <div class="hit-card"
    data-insights-object-id="${hit.objectID}"
    data-insights-position="${hit.__position}"
    data-insights-query-id="${hit.__queryID}">
    <h4 class="hit-name">...</h4>   
  </div>
</div>
```

### Abfragezeichenfolge {#query-string}

Das Datenelement Abfragezeichenfolge extrahiert Daten aus der URL-Abfragezeichenfolge zur Verwendung in [!DNL Algolia].

| Eigenschaft | Beschreibung |
| --- | --- |
| Objektname des ID-Parameters | Der Abfrageparametername, der die Objekt-ID enthält. |
| Indexname Parametername (optional) | Der Abfrageparametername, der den Indexnamen enthält. |
| Parametername der Abfrage-ID (optional) | Der Name des Abfrageparameters, der die Abfrage-ID enthält. |
| Name des Positionsparameters (optional) | Der Name des Abfrageparameters, der die Position enthält. |

![](../../../images/extensions/client/algolia/query-string.png)

Dieses Datenelement gibt zurück:

```javascript
{
  timestamp,
    queryID,
    indexName,
    objectIDs
}
```

Ein Beispiel für HTML mit Abfrageparametern.

```
<a href="product.html?objectID=${hit.objectID}&queryID=${hit.__queryID}&indexName=${indexName}&position=${hit.position}">Read More</a>
```

### Speicherung {#storage}

Das Datenspeicherelement ruft Daten aus dem Sitzungsspeicher ab, um sie in [!DNL Algolia] Aktionen zu verwenden.

Dieses Datenelement ruft Ereignisdetails aus dem Sitzungsspeicher ab. Es ist keine Konfiguration erforderlich. Die Daten werden während der *-*-Ereignisaktion automatisch hinzugefügt und während der *Konvertieren*-Ereignisaktion entfernt.

![](../../../images/extensions/client/algolia/storage.png)

Dieses Datenelement gibt zurück, was im Sitzungsspeicher gespeichert ist.

```javascript
{
  timestamp,
    queryID,
    indexName,
    objectIDs
}
```

## Nach der Suche angeklickt oder konvertiert {#clicked-converted-after-search}

Die Ereignisse *Nach Suche geklickt* oder *Nach Suche konvertiert* erfordern eine `queryId` und `position` ist auch für *Nach Suche geklickt* erforderlich. Diese Eigenschaften sind verfügbar, wenn das `insights`-Flag in den Abfrageparametern InstantSearch und/oder AutoVervollständigen aktiviert ist. In den folgenden Ressourcen erfahren Sie, wie Sie Insights für Ihre Site konfigurieren:

* [Einrichten von Insights zur automatischen Vervollständigung](https://www.algolia.com/doc/ui-libraries/autocomplete/api-reference/autocomplete-js/autocomplete/#param-insights)
* [Einrichten von Insights auf InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/events/js/#set-the-insights-option-to-true)
* [Erste Schritte mit Klick- und Konversionsereignissen](https://www.algolia.com/doc/guides/sending-events/implementing/how-to/sending-events-backend/)
* [Senden [!DNL Algolia] Insights-Ereignisse](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/sending-algolia-insights-events/)
* [[!DNL Algolia] Launch-Erweiterung - GitHub-Repository](https://github.com/algolia/algolia-launch-extension)
* [Dokumentation zu InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/)
* [[!DNL Algolia] Insights-API-Dokumentation](https://www.algolia.com/doc/rest-api/insights/)

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde beschrieben, wie Sie Daten mithilfe der [!DNL Algolia Insights]-Tag-Erweiterung an [!DNL Algolia] senden. Wenn Sie planen, Server-seitige Ereignisse auch an [!DNL Algolia] zu senden, können Sie jetzt mit der Installation und Konfiguration der Erweiterung [[!DNL Conversions API] Ereignisweiterleitung“ ](../../server/algolia/overview.md).

Weiterführende Informationen zu Tags in Experience Platform finden Sie in der [Übersicht zu Tags](../../../home.md).
