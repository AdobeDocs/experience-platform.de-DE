---
title: Algolia Tags-Erweiterung - Übersicht
description: Erfahren Sie mehr über die Algolia Tags-Erweiterung in Adobe Experience Platform.
exl-id: 8409bf8b-fae2-44cc-8466-9942f7d92613
source-git-commit: 6eee26df3841a7829625361fc726bf59a278f867
workflow-type: tm+mt
source-wordcount: '1954'
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

Um die [!DNL Algolia] Insights-Erweiterung zu installieren, navigieren Sie zum [!UICONTROL Data Collection UI] und wählen Sie **[!UICONTROL Tags]** in der linken Navigationsleiste aus. Wählen Sie hier eine Eigenschaft aus, der die Erweiterung hinzugefügt werden soll, oder erstellen Sie stattdessen eine neue Eigenschaft.

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Extensions]** und wählen Sie dann die Registerkarte **[!UICONTROL Catalog]** aus. Suchen Sie nach der Karte [!DNL Algolia] Insights und wählen Sie dann **[!UICONTROL Install]** aus.

![](../../../images/extensions/client/algolia/install.png)

In der Konfigurationsansicht, die angezeigt wird, müssen Sie die folgenden Details angeben:

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Application ID] | Geben Sie die [!UICONTROL Application Id] ein, die Sie zuvor im Abschnitt [Konfigurationsdetails](#configuration-details) erfasst haben. |
| [!UICONTROL Search API Key] | Geben Sie die [!UICONTROL Search API Key] ein, die Sie zuvor im Abschnitt [Konfigurationsdetails](#configuration-details) erfasst haben. |
| [!UICONTROL Index Name] | Die [!UICONTROL Index Name] enthält die Produkte oder Inhalte.  Dieser Index wird als Standard verwendet. |
| [!UICONTROL User Token Data Element] | Das Datenelement, das das Benutzer-Token zurückgibt. |
| [!UICONTROL Authenticated User Token Data Element] | Legen Sie das Datenelement fest, das das Token für authentifizierte Benutzer zurückgibt. |
| [!UICONTROL Currency Code] | Geben Sie den Währungscode im ISO-4217-Format ein, z. B. USD oder EUR. Dieses Feld unterstützt Datenelemente. |

![](../../../images/extensions/client/algolia/configure.png)

## [!DNL Algolia] Insights-Erweiterung - Aktionstypen {#action-types}

[!DNL Algolia] unterstützt eine Reihe vordefinierter Standardereignisse mit jeweils spezifischen Kontexten und Eigenschaften. Die in der [!DNL Algolia]-Erweiterung verfügbaren Aktionen werden diesen Ereignistypen zugeordnet, sodass Sie die Ereignisse, die Sie an [!DNL Algolia] senden, einfach anhand ihres Typs kategorisieren und konfigurieren können.

### Einblicke laden {#load-insights}

>[!NOTE]
>
>In den meisten Fällen wird empfohlen, [!DNL Algolia] Insights auf jeder Seite Ihrer Site zu laden.

Fügen Sie die **[!UICONTROL Load Insights]** Aktion Ihrer Tag-Regel an der Stelle hinzu, an der es am sinnvollsten ist, [!DNL Algolia] Insights basierend auf dem Kontext Ihrer Regel zu laden. Diese Aktion lädt die `search-insights.js` auf der Seite.

Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Extension] und **[!UICONTROL Load Insights]** als [!UICONTROL Action Type] aus.

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Insight Library Version] | Die [!DNL Algolia] Insights-Version. Die Standardeinstellung lautet `2.17.3`. |
| [!UICONTROL User Opt Out Data Element] | Das Datenelement, das die Tracking-Voreinstellungen des Benutzers erfasst. |
| [!UICONTROL Use User Token Cookie] | Aktivieren Sie dieses Kontrollkästchen, damit [!DNL Algolia] ein Benutzer-Token-Cookie generieren können. Standardmäßig ist diese Option auf `true` festgelegt. |

![](../../../images/extensions/client/algolia/load-insights.png)

### Angeklickt {#clicked}

Fügen Sie Ihrer Tag-Regel die Aktion **[!UICONTROL Click]** hinzu, um angeklickte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Extension] und **[!UICONTROL Clicked]** als [!UICONTROL Action Type] aus.

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Event Name] | Der Ereignisname, der verwendet werden kann, um dieses Klickereignis weiter einzuengen. |
| [!UICONTROL Event Details Data Element] | Das Datenelement gibt Ereignisdetails im JSON-Format zurück, einschließlich: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` (optional)</li><li>`positions` (optional)</li><li>`price` (optional)</li><li>`quantity` (optional)</li><li>`discount` (optional)</li><li>`objectData` (optional)</li><li>`currency` (optional)</li></ul> |


>[!NOTE]
>
>Wenn sowohl `queryID` als auch `positions` enthalten sind, wird das Ereignis als (**Objekt-IDs nach der Suche)**. Andernfalls wird es als Ereignis **angeklickte Objekt-IDs** klassifiziert.
><br>
>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.

![](../../../images/extensions/client/algolia/clicked.png)

Weitere Informationen zu den Ereigniskategorien finden Sie unter [Angeklickte Objekt-IDs nach der Suche](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids-after-search/)
und [angeklickte Objekt-IDs](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids/) Handbücher.

### Konvertiert {#converted}

Fügen Sie Ihrer Tag-Regel die Aktion **[!UICONTROL Converted]** hinzu, um konvertierte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Extension] und **[!UICONTROL Converted]** als [!UICONTROL Action Type] aus.

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Event Name] | Der Ereignisname, der verwendet wird, um dieses &quot;**&quot;-** weiter einzuengen. |
| [!UICONTROL Event Details Data Element] | Das Datenelement gibt Ereignisdetails zurück, darunter: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` (optional)</li><li>`recordID` (optional)</li></ul> |

>[!NOTE]
>
>Wenn das Datenelement `queryId` enthält, wird das Ereignis als „Nach **Suche konvertiert“**. Andernfalls wird es als &quot;**&quot;-** klassifiziert.
><br>
>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.

![](../../../images/extensions/client/algolia/converted.png)

Weitere Informationen zu den Ereigniskategorien finden Sie in den Handbüchern [Konvertierte Objekt-IDs nach ](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids-after-search/) und [Konvertierte Objekt-IDs](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids/) .

### Zum Warenkorb hinzufügen {#added-to-cart}

Fügen Sie die **[!UICONTROL Added to Cart]** Aktion zu Ihrer Tag-Regel hinzu, um hinzugefügte Ereignisse zum Warenkorb an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Extension] und **[!UICONTROL Added to cart]** als [!UICONTROL Action Type] aus.

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Event Name] | Der Ereignisname, mit dem dieses Ereignis weiter verfeinert wird **Zum Warenkorb hinzufügen**. |
| [!UICONTROL Event Details Data Element] | Das Datenelement gibt Ereignisdetails im JSON-Format zurück, einschließlich: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` (optional)</li><li>`queryID` (optional)</li><li>`currency` (optional)</li></ul>. |

>[!NOTE]
>
>Wenn das Datenelement `queryId` enthält, wird das Ereignis als &quot;**zu Warenkorb-Objekt-IDs nach der Suche hinzugefügt“**. Andernfalls wird es als Ereignis **Zu Warenkorb-Objekt-IDs hinzugefügt** klassifiziert.
><br>
>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.
><br>
>Wenn die standardmäßigen Datenelemente Ihre Anforderungen nicht erfüllen, kann ein benutzerdefiniertes Datenelement erstellt werden, das die gewünschten Ereignisdetails zurückgibt.

![](../../../images/extensions/client/algolia/added-to-cart.png)

Weitere Informationen zu den Ereigniskategorien finden Sie in den Handbüchern [Zu Warenkorb-Objekt-IDs nach der Suche hinzugefügt](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids-after-search/) und [Zu Warenkorb-Objekt-IDs hinzugefügt](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids/).

### Purchased {#purchased}

Fügen Sie die Aktion **[!UICONTROL Purchased]** Ihrer Tag-Regel hinzu, um gekaufte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Extension] und **[!UICONTROL Purchased]** als [!UICONTROL Action Type] aus.

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Event Name] | Der Ereignisname, der verwendet wird, um dieses „Kauf“-**weiter** verfeinern. |
| [!UICONTROL Event Details Data Element] | Das Datenelement gibt Ereignisdetails im JSON-Format zurück, einschließlich: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`</li><li>`price`</li><li>`quantity`</li><li>`discount` (optional)</li><li>`queryID` (optional)</li><li>`currency` (optional)</li></ul>. |

>[!NOTE]
>
>Die Kaufaktion ruft Ereignisdaten aus dem Browser-Speicher basierend auf den IDs der gekauften Artikel ab. Wenn einer der gekauften Artikel einen `queryID` in seinen gespeicherten Daten enthält, wird das Ereignis nach der Suche **IDs des gekauften Objekts“**. Andernfalls wird es als Ereignis &quot;**Objektkennungen“**.
><br>
>Mit diesem Ansatz kann das Kaufereignis automatisch alle relevanten Kontexte (Abfrage-ID, Indexname, Preis, Menge, Rabatt) aus den früheren Interaktionen des Benutzers mit den Elementen einschließen.

![](../../../images/extensions/client/algolia/purchased.png)

Weitere Informationen zu den Ereigniskategorien finden Sie unter [Erworbene Objekt-IDs nach der Suche](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids-after-search/)
und [Kennungen für gekaufte Objekte](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids/) Anleitungen.

### Angesehen {#viewed}

Fügen Sie die Aktion **[!UICONTROL Viewed]** Ihrer Tag-Regel hinzu, um gekaufte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Extension] und **[!UICONTROL Viewed]** als [!UICONTROL Action Type] aus.

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Event Name] | Der Ereignisname, der verwendet wird, um dieses Ereignis **Ansicht** weiter einzuengen. |
| [!UICONTROL Event Details Data Element] | Das Datenelement gibt Ereignisdetails im JSON-Format zurück, einschließlich: <ul><li>`indexName`</li><li>`objectIDs`</li></ul> |

>[!NOTE]
>
>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.

![](../../../images/extensions/client/algolia/viewed.png)

Weitere Informationen zum Ansichtsereignis finden Sie im Handbuch [Angezeigte Objekt-IDs](https://www.algolia.com/doc/api-reference/api-methods/viewed-object-ids/) .

## [!DNL Algolia] Insights-Erweiterung - Datenelemente {#data-elements}

[!DNL Algolia] unterstützt einen Satz vordefinierter Datenelemente mit jeweils spezifischen Kontexten und Eigenschaften. In den folgenden Abschnitten werden die in der [!DNL Algolia] Insights-Erweiterung verfügbaren Datenelemente beschrieben.

### Datensatz {#dataset}

Das DataSet-Datenelement ruft Daten ab, die mit HTML-Elementen verknüpft sind. Diese werden dann in [!DNL Algolia] verwendet. Dieses Datenelement speichert die abgerufenen Ereignisdaten automatisch im Browser-Speicher zur späteren Verwendung (z. B. bei Konversions- oder Kaufereignissen).

**Allgemeine Konfiguration:**

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Hit Element Div/Class Name] | Der HTML-Elementname und/oder der CSS-Klassenname, der die Datensatzattribute einschließlich `data-insights-object-id` und optional `data-insights-query-id` und `data-insights-position` für das HTML-Element enthält. |
| [!UICONTROL Index Name Element Div/Class Name] | Der HTML-Elementname und/oder CSS-Klassenname mit den Datensatzattributen (`data-indexname`) im HTML-Element. |

**Commerce-Konfiguration (optional):**

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Price Data Element] | Datenelement, das den Preis für das Element zurückgibt. Sofern angegeben, wird dies in die gespeicherten Ereignisdaten für Commerce-Ereignisse aufgenommen. |
| [!UICONTROL Quantity Data Element] | Datenelement, das die Menge für das Element zurückgibt. Die Standardeinstellung ist 1, wenn nicht angegeben. |
| [!UICONTROL Discount Data Element] | Datenelement, das den Rabattdezimalwert für das Element zurückgibt. |
| [!UICONTROL Currency Code] | Der Währungscode im ISO-4217-Format. Wenn kein Währungs-Code angegeben ist, wird die Standardwährung aus der Erweiterungskonfiguration verwendet. |

**Überschreibungen (optional):**

Mit diesen Feldern können Sie das Standardverhalten zum Abrufen von Daten aus HTML-Datensatzattributen überschreiben.

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Record ID Data Element] | Überschreiben Sie den Standardansatz zur Verwendung der Seiten-URL als Datensatz-ID. Die Datensatz-ID wird verwendet, um Daten zu speichern und nachzuschlagen, die für dieses Produkt/diese Seite an [!DNL Algolia] gesendet werden sollen. |
| [!UICONTROL Query ID Data Element] | Die Abfrage-ID wird aus dem Datensatz im HTML-Element abgerufen. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Abfrage-ID als Zeichenfolge zurückgibt. |
| [!UICONTROL Object IDs Data Element] | Die Objekt-IDs werden aus dem Datensatz im HTML-Element abgerufen. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Objekt-IDs als Array zurückgibt. |
| [!UICONTROL Positions Data Element] | Die Positionen werden aus dem Datensatz im HTML-Element abgerufen. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Positionen als Array zurückgibt. |
| [!UICONTROL Index Name Data Element] | Der Indexname wird aus dem Datensatz im HTML-Element abgerufen. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das den Indexnamen als Zeichenfolge zurückgibt. |

![](../../../images/extensions/client/algolia/dataset.png)

Dieses Datenelement gibt zurück:

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,
  objectData,  // Optional: commerce data if price is provided
  currency,    // Optional: if provided
  recordID
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
| [!UICONTROL Object ID Param Name] | Der Abfrageparametername, der die Objekt-ID enthält. |
| [!UICONTROL Index Name Param Name] | Der Abfrageparametername, der den Indexnamen enthält. |
| [!UICONTROL Query ID Param Name] | Der Name des Abfrageparameters, der die Abfrage-ID enthält. |
| [!UICONTROL Position Param Name] | Der Name des Abfrageparameters, der die Position enthält. |

![](../../../images/extensions/client/algolia/query-string.png)

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

Ein Beispiel für HTML mit Abfrageparametern:

```html
<a href="product.html?objectID=${hit.objectID}&queryID=${hit.__queryID}&indexName=${indexName}&position=${hit.position}">Read More</a>
```

### Speicherung {#storage}

Das Datenspeicherelement ruft Daten aus dem Sitzungsspeicher des Browsers ab, um sie in [!DNL Algolia] Aktionen zu verwenden. Dieses Datenelement kann auch verwendet werden, um die gespeicherten Daten um zusätzliche Commerce-Informationen zu erweitern.

Dieses Datenelement ruft Ereignisdetails ab, die zuvor im Sitzungsspeicher gespeichert waren (in der Regel vom DataSet-Datenelement während Klickereignissen). Die Daten werden bei Konversionsereignissen automatisch entfernt, es sei denn, die Entfernung wird explizit deaktiviert.

**Überschreibungen (optional):**

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Record ID Data Element] | Die Datensatz-ID wird als Schlüssel zum Nachschlagen der Ereignisdaten verwendet, die im Browser-Speicher gespeichert sind. Die Seiten-URL ist die standardmäßige Datensatz-ID. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Datensatz-ID als Zeichenfolge zurückgibt. |
| [!UICONTROL Price Data Element] | Datenelement, das den Preis für das Element zurückgibt. Wenn angegeben, werden die gespeicherten Ereignisdaten mit Preisinformationen aktualisiert. |
| [!UICONTROL Quantity Data Element] | Datenelement, das die Menge für das Element zurückgibt. Wenn angegeben, werden die gespeicherten Ereignisdaten mit Mengeninformationen aktualisiert. |
| [!UICONTROL Discount Data Element] | Datenelement, das den Rabattdezimalwert für das Element zurückgibt. Wenn angegeben, werden die gespeicherten Ereignisdaten mit Rabattinformationen aktualisiert. |
| [!UICONTROL Currency Code] | Geben Sie den Währungscode im ISO-4217-Format ein. Wenn angegeben, werden die gespeicherten Ereignisdaten mit Währungsinformationen aktualisiert. |

![](../../../images/extensions/client/algolia/storage.png)

Dieses Datenelement gibt zurück, was im Sitzungsspeicher gespeichert ist, einschließlich aller erweiterten Commerce-Daten:

```javascript
{
  timestamp,
  queryID,
  indexName,
  objectIDs,
  positions,      // If available from original event
  objectData,     // Optional: commerce data if price is provided
  currency,       // Optional: if provided
  recordID
}
```

## Nach der Suche angeklickt oder konvertiert {#clicked-converted-after-search}

Die Ereignisse *Nach Suche geklickt* oder *Nach Suche konvertiert* erfordern eine `queryID` und `positions` ist auch für *Nach Suche geklickt* erforderlich. Diese Eigenschaften sind verfügbar, wenn das `insights`-Flag in den Abfrageparametern InstantSearch und/oder AutoVervollständigen aktiviert ist. In den folgenden Ressourcen erfahren Sie, wie Sie Insights für Ihre Site konfigurieren:

* [Einrichten von Insights zur automatischen Vervollständigung](https://www.algolia.com/doc/ui-libraries/autocomplete/api-reference/autocomplete-js/autocomplete/#param-insights)
* [Einrichten von Insights auf InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/events/js/#set-the-insights-option-to-true)
* [Erste Schritte mit Klick- und Konversionsereignissen](https://www.algolia.com/doc/guides/sending-events/implementing/how-to/sending-events-backend/)
* [Senden [!DNL Algolia] Insights-Ereignisse](https://www.algolia.com/doc/ui-libraries/autocomplete/guides/sending-algolia-insights-events/)
* [[!DNL Algolia] Launch-Erweiterung - GitHub-Repository](https://github.com/algolia/algolia-launch-extension)
* [Dokumentation zu InstantSearch.js](https://www.algolia.com/doc/guides/building-search-ui/what-is-instantsearch/js/)
* [[!DNL Algolia] Insights-API-Dokumentation](https://www.algolia.com/doc/rest-api/insights/)
* [Algolia Launch-Erweiterung - Code-Repository](https://github.com/algolia/algolia-launch-extension)

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde beschrieben, wie Sie Daten mithilfe der [!DNL Algolia]-Tag-Erweiterung an [!DNL Algolia Insights] senden. Wenn Sie planen, Server-seitige Ereignisse auch an [!DNL Algolia] zu senden, können Sie jetzt mit der Installation und Konfiguration der Erweiterung [[!DNL Conversions API] Ereignisweiterleitung“ ](../../server/algolia/overview.md).

Weiterführende Informationen zu Tags in Experience Platform finden Sie in der [Übersicht zu Tags](../../../home.md).
