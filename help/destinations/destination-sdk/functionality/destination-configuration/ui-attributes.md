---
description: Erfahren Sie, wie Sie die Attribute der Benutzeroberfläche, wie z. B. den Dokumentationslink, die Kategorie der Zielkarte sowie den Verbindungstyp und die Häufigkeit der Zielverbindungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Benutzeroberflächenattribute
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 9%

---


# Benutzeroberflächenattribute

Benutzeroberflächenattribute definieren die visuellen Elemente, die die Adobe für Ihre Zielkarte in der Adobe Experience Platform-Benutzeroberfläche anzeigen soll, z. B. das Zielplattformlogo, einen Link zur Dokumentationsseite, eine Zielbeschreibung und deren Kategorie und Typ.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder sehen Sie die folgenden Übersichtsseiten zur Zielkonfiguration:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Wann [Erstellen eines Ziels](../../authoring-api/destination-configuration/create-destination-configuration.md) durch Destination SDK, `uiAttributes` -Abschnitt definiert die folgenden visuellen Eigenschaften Ihrer Zielkarte:

* Die URL Ihrer Zieldokumentationsseite in der [Zielkatalog](../../../catalog/overview.md).
* Die URL, unter der das Symbol gehostet wird, das auf der Zielkatalogkarte angezeigt werden soll.
* Die Kategorie, unter der Ihr Ziel in der Platform-Benutzeroberfläche angezeigt wird.
* Die Häufigkeit des Datenexports für Ihr Ziel.
* Der Zielverbindungstyp, z. B. Amazon S3, Azure Blob usw.

Sie können Benutzeroberflächenattribute über die `/authoring/destinations` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Benutzeroberflächenattribute beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, welche Experience Platformen in der Benutzeroberfläche angezeigt werden.

![UI-Screenshot mit den Benutzeroberflächenattributen in der Experience Platform-Benutzeroberfläche](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |

## Unterstützte Parameter {#supported-parameters}

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "connectionType":"S3",
      "frequency":"batch",
      "isBeta":"true"
   }
```

### `documentationLink` {#documentation-link}

`documentationLink` ist ein Zeichenfolgenparameter, der auf die Dokumentationsseite im [Zielkatalog](../../../catalog/overview.md) für Ihr Ziel. Jedes in Adobe Experience Platform erstellte Ziel muss über eine entsprechende Dokumentationsseite verfügen. [Erfahren Sie, wie Sie eine Zieldokumentationsseite erstellen](../../docs-framework/documentation-instructions.md) für Ihr Ziel. Beachten Sie, dass dies für private/benutzerdefinierte Ziele nicht erforderlich ist.

Verwenden Sie das folgende Format: `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` ist der Name Ihres Ziels. Für ein Ziel mit dem Namen „Moviestar“ würden Sie `http://www.adobe.com/go/destinations-moviestar-en` verwenden.

Benutzer können Ihren Dokumentations-Link über die Zielkatalogseite in der Benutzeroberfläche anzeigen und aufrufen. Sie müssen zu Ihrer Zielkarte navigieren und dann **[!UICONTROL Mehr Aktionen]**, und dann **[!UICONTROL Dokumentation anzeigen]**, wie in der Abbildung unten dargestellt.

![UI-Bild, das den Speicherort des Dokumentations-Links anzeigt.](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>Dieser Link funktioniert erst, nachdem Adobe Ihr Ziel live gesetzt und die Dokumentation veröffentlicht hat.

### `category` {#category}

`category` ist ein Zeichenfolgenparameter, der auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie verweist. Weitere Informationen finden Sie unter [Zielkategorien](../../../destination-types.md). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

Benutzer können die Liste der Zielkategorien auf der linken Seite des Bildschirms im Zielkatalog sehen, wie in der Abbildung unten dargestellt.

![UI-Bild, das den Speicherort der Zielkategorie anzeigt.](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` ist ein Zeichenfolgenparameter, der sich je nach Ziel auf den Verbindungstyp bezieht. Unterstützte Werte: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

Benutzer können den Zielverbindungstyp im [Durchsuchen](../../../ui/destinations-workspace.md#browse) im Arbeitsbereich &quot;Ziele&quot;angezeigt.

![UI-Bild, das den Standort des Verbindungstyps in der Benutzeroberfläche anzeigt.](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` ist ein Zeichenfolgenparameter, der sich auf den von Ihrem Ziel unterstützten Datentyp bezieht. Legen Sie fest auf `Streaming` für API-basierte Integrationen oder `Batch` wenn Sie Dateien in Ihre Ziele exportieren.

Die Benutzer können den Häufigkeitstyp im **[!UICONTROL Datenfluss-Abläufe]** Seite jeder Zielverbindung.

![UI-Bild, das den Standort des Häufigkeitstyps in der Benutzeroberfläche anzeigt.](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

Wenn das Ziel, das Sie mit Destination SDK erstellen, einer begrenzten Anzahl von Kunden zur Verfügung steht, können Sie die Zielkarte aus dem Zielkatalog als Beta markieren.

Zu diesem Zweck können Sie die `isBeta: "true"` -Parameter im Abschnitt &quot;Benutzeroberflächenattribute&quot;der Zielkonfiguration, um die Zielkarte entsprechend zu markieren.

![Benutzeroberflächenbild mit einer als Beta markierten Zielkarte.](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, welche Benutzeroberflächenattribute Sie für Ihr Ziel konfigurieren können und wo die Benutzer sie in der Platform-Benutzeroberfläche sehen.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)