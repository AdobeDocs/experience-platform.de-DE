---
description: Erfahren Sie, wie Sie die Attribute der Benutzeroberfläche, wie z. B. den Dokumentations-Link, die Kategorie der Zielkarte sowie den Verbindungstyp und die Häufigkeit der Zielverbindungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Benutzeroberflächenattribute
exl-id: aed8d868-c516-45da-b224-c7e99e4bfaf1
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 99%

---

# Benutzeroberflächenattribute

Benutzeroberflächenattribute definieren die visuellen Elemente, die Adobe für Ihre Zielkarte in der Adobe Experience Platform-Benutzeroberfläche anzeigen soll, z. B. das Zielplattformlogo, einen Link zur Dokumentationsseite, eine Zielbeschreibung und deren Kategorie und Typ.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation zu [Konfigurationsoptionen](../configuration-options.md) oder auf den folgenden Übersichtsseiten zur Zielkonfiguration:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Wenn Sie durch Destination SDK [ein Ziel erstellen](../../authoring-api/destination-configuration/create-destination-configuration.md), werden im Abschnitt `uiAttributes` die folgenden visuellen Eigenschaften Ihrer Zielkarte definiert:

* Die URL Ihrer Zieldokumentationsseite im [Zielkatalog](../../../catalog/overview.md).
* Die URL, unter der das Symbol gehostet wird, das auf der Zielkatalogkarte angezeigt werden soll.
* Die Kategorie, unter der Ihr Ziel in der Platform-Benutzeroberfläche angezeigt wird.
* Die Häufigkeit des Datenexports für Ihr Ziel.
* Der Zielverbindungstyp, z. B. Amazon S3, Azure Blob usw.

Sie können Benutzeroberflächenattribute über den Endpunkt `/authoring/destinations` konfigurieren. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Benutzeroberflächenattribute beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, was Kundinnen und Kunden in der Benutzeroberfläche von Experience Platform sehen werden.

![Screenshot der Benutzeroberfläche mit den Benutzeroberflächenattributen in der Experience Platform-Oberfläche](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

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

`documentationLink` ist ein Zeichenfolgenparameter, der auf die Dokumentationsseite im [Zielkatalog](../../../catalog/overview.md) für Ihr Ziel verweist. Jedes produktbezogene Ziel in Adobe Experience Platform muss über eine entsprechende Dokumentationsseite verfügen. [Erfahren Sie, wie Sie eine Zieldokumentationsseite für Ihr Ziel erstellen](../../docs-framework/documentation-instructions.md). Beachten Sie, dass dies für private/benutzerdefinierte Ziele nicht erforderlich ist.

Verwenden Sie das folgende Format: `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, wobei `YOURDESTINATION` der Name Ihres Ziels ist. Für ein Ziel mit dem Namen „Moviestar“ würden Sie `http://www.adobe.com/go/destinations-moviestar-en` verwenden.

Benutzerinnen und Benutzer können Ihren Dokumentations-Link über die Zielkatalogseite in der Benutzeroberfläche anzeigen und aufrufen. Dafür müssen sie zu Ihrer Zielkarte navigieren und **[!UICONTROL Mehr Aktionen]** gefolgt von **[!UICONTROL Dokumentation anzeigen]** wählen, wie in der Abbildung unten dargestellt.

![UI-Bild, das den Ort des Dokumentations-Links anzeigt.](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>Dieser Link funktioniert erst, nachdem Adobe Ihr Ziel live geschaltet hat und die Dokumentation veröffentlicht wurde.

### `category` {#category}

`category` ist ein Zeichenfolgenparameter, der auf die Ihrem Ziel in Adobe Experience Platform zugewiesene Kategorie verweist. Weitere Informationen finden Sie unter [Zielkategorien](../../../destination-types.md). Verwenden Sie einen der folgenden Werte: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

Benutzerinnen und Benutzer können die Liste der Zielkategorien auf der linken Seite des Bildschirms im Zielkatalog sehen, wie in der Abbildung unten dargestellt.

![UI-Bild, das den Ort der Zielkategorie anzeigt.](../../assets/functionality/destination-configuration/ui-attributes-category.png)

<!-- ### `iconUrl` {#icon-url}

`iconUrl` is a string parameter that refers to the URL where you hosted the icon to be displayed in the destinations catalog card. For private custom integrations, this is not required. For productized configurations, you need to share an icon with the Adobe team when you [submit the destination for review](../../guides/submit-destination.md#logo).

Users can see the icon on your destination card, as shown in the image below.

![UI image showing the icon location.](../../assets/functionality/destination-configuration/ui-attributes-icon.png) -->

### `connectionType` {#connection-type}

`connectionType` ist ein Zeichenfolgenparameter, der sich je nach Ziel auf den Verbindungstyp bezieht. Unterstützte Werte: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

Benutzerinnen und Benutzer können den Zielverbindungstyp auf der Registerkarte [Durchsuchen](../../../ui/destinations-workspace.md#browse) des Arbeitsbereichs „Ziele“ sehen.

![UI-Bild, das den Ort des Verbindungstyps in der Benutzeroberfläche anzeigt.](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` ist ein Zeichenfolgenparameter, der sich auf den von Ihrem Ziel unterstützten Typ des Datenexports bezieht. Setzen Sie diesen auf `Streaming` für API-basierte Integrationen oder auf `Batch`, wenn Sie Dateien in Ihre Ziele exportieren.

Die Benutzerinnen und Benutzer können den Häufigkeitstyp auf der Seite **[!UICONTROL Datenfluss-Ausführungen]** jeder Zielverbindung sehen.

![UI-Bild, das den Ort des Häufigkeitstyps in der Benutzeroberfläche zeigt.](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

Wenn das Ziel, das Sie mit Destination SDK erstellen, einer begrenzten Anzahl von Kundinnen und Kunden zur Verfügung steht, können Sie die Zielkarte aus dem Zielkatalog als Beta markieren.

Zu diesem Zweck können Sie den Parameter `isBeta: "true"` im Abschnitt „Benutzeroberflächenattribute“ der Zielkonfiguration verwenden, um die Zielkarte entsprechend zu markieren.

![UI-Bild, das eine als Beta markierte Zielkarte zeigt.](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, welche Benutzeroberflächenattribute Sie für Ihr Ziel konfigurieren können und wo die Benutzerinnen und Benutzer sie in der Platform-Benutzeroberfläche sehen.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth2-Autorisierung](oauth2-authorization.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)
