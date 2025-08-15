---
title: Algolia Tags-Erweiterung - Übersicht
description: Erfahren Sie mehr über die Algolia Tags-Erweiterung in Adobe Experience Platform.
exl-id: 8409bf8b-fae2-44cc-8466-9942f7d92613
source-git-commit: 904200c5d3ef2be58582e4679109390e8d4aebc1
workflow-type: tm+mt
source-wordcount: '1977'
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

Nachdem Sie die gewünschte Eigenschaft ausgewählt oder erstellt haben, klicken Sie im linken **[!UICONTROL auf]** Erweiterungen und wählen Sie dann die Registerkarte **[!UICONTROL Katalog]** aus. Suchen Sie nach der Karte [!DNL Algolia] Insights und wählen Sie dann **[!UICONTROL Installieren]** aus.

![](../../../images/extensions/client/algolia/install.png)

In der Konfigurationsansicht, die angezeigt wird, müssen Sie die folgenden Details angeben:

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Anwendungs-ID] | Geben Sie die [!UICONTROL Anwendungs-ID] ein, die Sie zuvor im Abschnitt [Konfigurationsdetails](#configuration-details) erfasst haben. |
| [!UICONTROL API-Schlüssel suchen] | Geben Sie den [!UICONTROL Such-API-Schlüssel] ein, den Sie zuvor im Abschnitt [Konfigurationsdetails](#configuration-details) erfasst haben. |
| [!UICONTROL Indexname] | Der [!UICONTROL Indexname] enthält die Produkte oder Inhalte.  Dieser Index wird als Standard verwendet. |
| [!UICONTROL Benutzer-Token-Datenelement] | Das Datenelement, das das Benutzer-Token zurückgibt. |
| [!UICONTROL Authentifiziertes Benutzer-Token-Datenelement] | Legen Sie das Datenelement fest, das das Token für authentifizierte Benutzer zurückgibt. |
| [!UICONTROL Währung] | Wählen Sie einen Währungstyp. Der Standardwert ist auf `USD` festgelegt. |

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
| [!UICONTROL Datenelement „Ereignisdetails“] | Das Datenelement gibt Ereignisdetails zurück, darunter: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` (optional)</li><li>`position` (optional)</li></ul> |
| [!UICONTROL Datensatz-ID-Datenelement] | Die Datensatz-ID wird als Schlüssel für die Ereignisdaten verwendet, die während eines `click` im Speicher des Browsers gespeichert werden. Standardmäßig dient die Seiten-URL als Datensatz-ID. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Datensatz-ID als Zeichenfolge zurückgibt. |

>[!NOTE]
>
>Wenn sowohl `queryID` als auch `position` enthalten sind, wird das Ereignis als (**Objekt-IDs nach der Suche)**. Andernfalls wird es als Ereignis **angeklickte Objekt-IDs** klassifiziert.
>&#x200B;><br>
>&#x200B;>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.

![](../../../images/extensions/client/algolia/clicked.png)

Weitere Informationen zu den Ereigniskategorien finden Sie unter [Angeklickte Objekt-IDs nach der Suche](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids-after-search/)
und [angeklickte Objekt-IDs](https://www.algolia.com/doc/api-reference/api-methods/clicked-object-ids/) Handbücher.

### Konvertiert {#converted}

Fügen Sie die Aktion **[!UICONTROL Konvertiert]** zu Ihrer Tag-Regel hinzu, um konvertierte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und wählen Sie **[!UICONTROL Konvertiert]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Ereignisname] | Der Ereignisname, der verwendet wird, um dieses &quot;**&quot;-** weiter einzuengen. |
| [!UICONTROL Datenelement „Ereignisdetails“] | Das Datenelement gibt Ereignisdetails zurück, darunter: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`queryID` (optional)</li></ul> |
| [!UICONTROL Entfernen von Ereignisdaten deaktivieren] | Bei einem Konversionsereignis werden die Ereignisdaten aus dem Speicher entfernt. Wenn diese Daten für nachfolgende Konversionsereignisse benötigt werden, deaktivieren Sie den Entfernungsprozess, um sicherzustellen, dass die Ereignisdaten verfügbar bleiben. |
| [!UICONTROL Datensatz-ID-Datenelement] | Die Datensatz-ID wird als Schlüssel zum Nachschlagen der Ereignisdaten verwendet, die im Browser-Speicher gespeichert sind. Die Seiten-URL ist die standardmäßige Datensatz-ID. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Datensatz-ID als Zeichenfolge zurückgibt. |

>[!NOTE]
>
>Wenn das Datenelement `queryId` enthält, wird das Ereignis als „Nach **Suche konvertiert“**. Andernfalls wird es als &quot;**&quot;-** klassifiziert.
>&#x200B;><br>
>&#x200B;>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.

![](../../../images/extensions/client/algolia/converted.png)

Weitere Informationen zu den Ereigniskategorien finden Sie in den Handbüchern [Konvertierte Objekt-IDs nach ](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids-after-search/) und [Konvertierte Objekt-IDs](https://www.algolia.com/doc/api-reference/api-methods/converted-object-ids/) .

### Zum Warenkorb hinzufügen {#added-to-cart}

Fügen Sie die Aktion **[!UICONTROL Zum Warenkorb hinzugefügt]** zu Ihrer Tag-Regel hinzu, um hinzugefügte Warenkorbereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und wählen Sie **[!UICONTROL Zum Warenkorb hinzugefügt]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Ereignisname] | Der Ereignisname, der verwendet wird, um dieses &quot;**&quot;-** weiter einzuengen. |
| [!UICONTROL Datenelement „Ereignisdetails“] | Das Datenelement gibt Ereignisdetails zurück, darunter: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`<ul><li>`queryID` (optional)</li><li>`price`</li><li>`quantity`</li><li>`discount`</li></ul></li><li>`queryID` (optional)</li></ul>. |
| [!UICONTROL Währung] | Wählen Sie einen Währungstyp. Der Standardwert ist auf `USD` festgelegt. |

>[!NOTE]
>
>Wenn das Datenelement `queryId` enthält, wird das Ereignis als &quot;**zu Warenkorb-Objekt-IDs nach der Suche hinzugefügt“**. Andernfalls wird es als Ereignis **Zu Warenkorb-Objekt-IDs hinzugefügt** klassifiziert.
>&#x200B;><br>
>&#x200B;>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.
>&#x200B;><br>
>&#x200B;>Wenn die standardmäßigen Datenelemente Ihre Anforderungen nicht erfüllen, kann ein benutzerdefiniertes Datenelement erstellt werden, das die gewünschten Ereignisdetails zurückgibt.

![](../../../images/extensions/client/algolia/added-to-cart.png)

Weitere Informationen zu den Ereigniskategorien finden Sie in den Handbüchern [Zu Warenkorb-Objekt-IDs nach der Suche hinzugefügt](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids-after-search/) und [Zu Warenkorb-Objekt-IDs hinzugefügt](https://www.algolia.com/doc/api-reference/api-methods/added-to-cart-object-ids/).

### Purchased {#purchased}

Fügen Sie die **[!UICONTROL Purchased]**-Aktion zu Ihrer Tag-Regel hinzu, um gekaufte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen, wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und wählen Sie **[!UICONTROL Erworben]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Ereignisname] | Der Ereignisname, der verwendet wird, um dieses „Kauf“-**weiter** verfeinern. |
| [!UICONTROL Datenelement „Ereignisdetails“] | Das Datenelement gibt Ereignisdetails zurück, darunter: <ul><li>`indexName`</li><li>`objectIDs`</li><li>`objectData`<ul><li>`queryID` (optional)</li><li>`price`</li><li>`quantity`</li><li>`discount`</li></ul></li><li>`queryID` (optional)</li></ul>. |
| [!UICONTROL Währung] | Wählen Sie einen Währungstyp. Der Standardwert ist auf `USD` festgelegt. |

>[!NOTE]
>
>Wenn das Datenelement `queryId` enthält, wird das Ereignis als „Erworbene Objekt **IDs nach der Suche“**. Andernfalls wird es als Ereignis &quot;**Objektkennungen“**.
>&#x200B;><br>
>&#x200B;>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.
>&#x200B;><br>
>&#x200B;>Wenn die standardmäßigen Datenelemente Ihre Anforderungen nicht erfüllen, kann ein benutzerdefiniertes Datenelement erstellt werden, das die gewünschten Ereignisdetails zurückgibt.

![](../../../images/extensions/client/algolia/purchased.png)

Weitere Informationen zu den Ereigniskategorien finden Sie unter [Erworbene Objekt-IDs nach der Suche](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids-after-search/)
und [Kennungen für gekaufte Objekte](https://www.algolia.com/doc/api-reference/api-methods/purchased-object-ids/) Anleitungen.

### Angesehen {#viewed}

Fügen Sie die Aktion **[!UICONTROL Angezeigt]** zu Ihrer Tag-Regel hinzu, um gekaufte Ereignisse an [!DNL Algolia] zu senden. Erstellen Sie eine neue Tag-Regel oder öffnen Sie eine vorhandene. Definieren Sie die Bedingungen entsprechend Ihren Anforderungen und wählen Sie dann **[!UICONTROL Algolia]** als [!UICONTROL Erweiterung] und **[!UICONTROL Angezeigt]** als [!UICONTROL Aktionstyp].

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Ereignisname] | Der Ereignisname, der verwendet wird, um dieses Ereignis **Ansicht** weiter einzuengen. |
| [!UICONTROL Datenelement „Ereignisdetails“] | Das Datenelement gibt Ereignisdetails zurück, darunter: <ul><li>`indexName`</li><li>`objectIDs`</li></ul> |

>[!NOTE]
>
>Wenn das Datenelement keinen `indexName` bereitstellt, wird der **Standardindexname** beim Senden des Ereignisses verwendet.

![](../../../images/extensions/client/algolia/viewed.png)

Weitere Informationen zum Ansichtsereignis finden Sie im Handbuch [Angezeigte Objekt-IDs](https://www.algolia.com/doc/api-reference/api-methods/viewed-object-ids/) .

## [!DNL Algolia] Insights-Erweiterung - Datenelemente {#data-elements}

[!DNL Algolia] unterstützt einen Satz vordefinierter Datenelemente mit jeweils spezifischen Kontexten und Eigenschaften. In den folgenden Abschnitten werden die in der [!DNL Algolia] Insights-Erweiterung verfügbaren Datenelemente beschrieben.

### Datensatz {#dataset}

Das DataSet-Datenelement ruft Daten ab, die mit HTML-Elementen verknüpft sind. Diese werden dann in [!DNL Algolia] verwendet.

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Treffer-Element/div-Klassenname] | Der HTML-Elementname und/oder CSS-Klassenname, der die Datensatzattribute einschließlich `data-insights-object-id` und optional `data-insights-query-id` und `data-insights-position` auf dem HTML-Element enthält. |
| [!UICONTROL Indexname Element div/class name] | Der HTML-Elementname und/oder CSS-Klassenname mit den Datensatzattributen (`data-indexname`) im HTML-Element. |
| [!UICONTROL Datenelement der Abfrage-ID] | Die Abfrage-ID wird aus dem Datensatz im HTML-Element abgerufen. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Abfrage-ID als Zeichenfolge zurückgibt. |
| [!UICONTROL Objekt-IDs-Datenelement] | Die Objekt-IDs werden aus dem Datensatz im HTML-Element abgerufen. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Objekt-IDs als Array zurückgibt. |
| [!UICONTROL Positioniert das Datenelement] | Die Positionen werden aus dem Datensatz im HTML-Element abgerufen. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Positionen als Array zurückgibt. |
| [!UICONTROL Datenelement „Indexname] | Der Indexname wird aus dem Datensatz im HTML-Element abgerufen. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das den Indexnamen als Zeichenfolge zurückgibt. |

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
| [!UICONTROL Objekt-ID-Parametername] | Der Abfrageparametername, der die Objekt-ID enthält. |
| [!UICONTROL Indexname Parametername] | Der Abfrageparametername, der den Indexnamen enthält. |
| [!UICONTROL Abfrage-ID-Parametername] | Der Name des Abfrageparameters, der die Abfrage-ID enthält. |
| [!UICONTROL Position Parametername] | Der Name des Abfrageparameters, der die Position enthält. |

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

| Eigenschaft | Beschreibung |
| --- | --- |
| [!UICONTROL Datensatz-ID-Datenelement] | Die Datensatz-ID wird als Schlüssel zum Nachschlagen der Ereignisdaten verwendet, die im Browser-Speicher gespeichert sind. Die Seiten-URL ist die standardmäßige Datensatz-ID. Um dieses Verhalten zu überschreiben, verwenden Sie diese Eigenschaft, um ein Datenelement bereitzustellen, das die Datensatz-ID als Zeichenfolge zurückgibt. |

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
* [Algolia Launch-Erweiterung - Code-Repository](https://github.com/algolia/algolia-launch-extension)

## Nächste Schritte {#next-steps}

In diesem Handbuch wurde beschrieben, wie Sie Daten mithilfe der [!DNL Algolia]-Tag-Erweiterung an [!DNL Algolia Insights] senden. Wenn Sie planen, Server-seitige Ereignisse auch an [!DNL Algolia] zu senden, können Sie jetzt mit der Installation und Konfiguration der Erweiterung [[!DNL Conversions API] Ereignisweiterleitung“ ](../../server/algolia/overview.md).

Weiterführende Informationen zu Tags in Experience Platform finden Sie in der [Übersicht zu Tags](../../../home.md).
