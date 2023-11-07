---
description: Erfahren Sie, wie Sie die Zielbereitstellungseinstellungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden, um anzugeben, wohin die exportierten Daten gehen und welche Authentifizierungsregel an dem Ort verwendet wird, an dem die Daten landen.
title: Zielbereitstellung
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 100%

---

# Zielbereitstellung

Um mehr Kontrolle darüber zu erhalten, wo die in Ihr Ziel exportierten Daten landen, können Sie in Destination SDK die Zielversandeinstellungen festlegen.

Im Abschnitt „Zielbereitstellung“ wird angegeben, wohin die exportierten Daten gehen und welche Authentifizierungsregel an dem Ort verwendet wird, an dem die Daten landen.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation zu [Konfigurationsoptionen](../configuration-options.md) oder auf den folgenden Übersichtsseiten zur Zielkonfiguration:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Die Konfiguration der Zielversandeinstellungen erfolgt über den Endpunkt `/authoring/destinations`. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Zielbereitstellungsoptionen beschrieben, die Sie für Ihr Ziel verwenden können.

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

Bei der Konfiguration Ihrer Zielversandeinstellungen können Sie mithilfe der in der folgenden Tabelle beschriebenen Parameter definieren, an welche Stelle die exportierten Daten gesendet werden sollen.

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform] eine Verbindung zu Ihrem Ziel herstellen soll. Unterstützte Werte:<ul><li>`CUSTOMER_AUTHENTICATION`: Verwenden Sie diese Option, wenn sich Platform-Kundinnen und -Kunden über eine der [hier](customer-authentication.md) beschriebenen Authentifizierungsmethoden bei Ihrem System anmelden.</li><li>`PLATFORM_AUTHENTICATION`: Verwenden Sie diese Option, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel existiert und [!DNL Platform]-Kundinnen bzw. -Kunden keine Authentifizierungsdaten bereitstellen müssen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie ein Anmeldeinformationen-Objekt mithilfe der Konfiguration der [Anmeldeinformationen-API](../../credentials-api/create-credential-configuration.md) erstellen. </li><li>`NONE`: Verwenden Sie diese Option, wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationServerId` | Zeichenfolge | Die `instanceId` des [Ziel-Servers](../../authoring-api/destination-server/create-destination-server.md), an die Sie Daten exportieren möchten. |
| `deliveryMatchers.type` | Zeichenfolge | <ul><li>Legen Sie diese bei der Konfiguration des Zielversands für dateibasierte Ziele immer auf `SOURCE` fest.</li><li>Beim Konfigurieren des Zielversands für ein Streaming-Ziel ist der Abschnitt `deliveryMatchers` nicht erforderlich.</li></ul> |
| `deliveryMatchers.value` | Zeichenfolge | <ul><li>Legen Sie diese bei der Konfiguration des Zielversands für dateibasierte Ziele immer auf `batch` fest.</li><li>Beim Konfigurieren des Zielversands für ein Streaming-Ziel ist der Abschnitt `deliveryMatchers` nicht erforderlich.</li></ul> |

{style="table-layout:auto"}

## Zielversandeinstellungen für Streaming-Ziele {#destination-delivery-streaming}

Das folgende Beispiel zeigt, wie die Zielbereitstellungseinstellungen für ein Streaming-Ziel konfiguriert werden sollten. Beachten Sie, dass der Abschnitt `deliveryMatchers` für Streaming-Ziele nicht erforderlich ist.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Zielversandeinstellungen für dateibasierte Ziele {#destination-delivery-file-based}

Das folgende Beispiel zeigt, wie die Zielversandeinstellungen für ein dateibasiertes Ziel konfiguriert werden sollten. Beachten Sie, dass der Abschnitt `deliveryMatchers` für dateibasierte Ziele erforderlich ist.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, wie Sie die Orte konfigurieren können, an denen Ihr Ziel Daten exportieren soll, und das sowohl für Streaming- als auch für dateibasierte Ziele.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authorization.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)
