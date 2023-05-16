---
description: Erfahren Sie, wie Sie die Zielbereitstellungseinstellungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden, um anzugeben, wohin die exportierten Daten gehen und welche Authentifizierungsregel an dem Ort verwendet wird, an dem die Daten landen.
title: Zielbereitstellung
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 8%

---


# Zielbereitstellung

Um mehr Kontrolle darüber zu erhalten, wo die in Ihr Ziel exportierten Daten landen, können Sie in Destination SDK die Zielversandeinstellungen festlegen.

Im Abschnitt Zielbereitstellung wird angegeben, wohin die exportierten Daten gehen und welche Authentifizierungsregel an dem Ort verwendet wird, an dem die Daten landen.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder sehen Sie die folgenden Übersichtsseiten zur Zielkonfiguration:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Die Konfiguration der Zielversandeinstellungen erfolgt über die `/authoring/destinations` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Zielbereitstellungsoptionen beschrieben, die Sie für Ihr Ziel verwenden können.

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

Bei der Konfiguration Ihrer Zielversandeinstellungen können Sie mithilfe der in der folgenden Tabelle beschriebenen Parameter definieren, an welche Stelle die exportierten Daten gesendet werden sollen.

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `authenticationRule` | Zeichenfolge | Gibt an, wie [!DNL Platform] sollte eine Verbindung zu Ihrem Ziel herstellen. Unterstützte Werte:<ul><li>`CUSTOMER_AUTHENTICATION`: Verwenden Sie diese Option, wenn sich Platform-Kunden über eine der beschriebenen Authentifizierungsmethoden bei Ihrem System anmelden. [here](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Verwenden Sie diese Option, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel und der [!DNL Platform] Der Kunde muss keine Authentifizierungsberechtigungen bereitstellen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe der [API-Anmeldeinformationen](../../credentials-api/create-credential-configuration.md) Konfiguration. </li><li>`NONE`: Verwenden Sie diese Option, wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `destinationServerId` | Zeichenfolge | Die `instanceId` des [Zielserver](../../authoring-api/destination-server/create-destination-server.md) an die Sie Daten exportieren möchten. |
| `deliveryMatchers.type` | Zeichenfolge | <ul><li>Legen Sie bei der Konfiguration des Zielversands für dateibasierte Ziele immer Folgendes fest: `SOURCE`.</li><li>Beim Konfigurieren des Zielversands für ein Streaming-Ziel muss die `deliveryMatchers` nicht erforderlich.</li></ul> |
| `deliveryMatchers.value` | Zeichenfolge | <ul><li>Legen Sie bei der Konfiguration des Zielversands für dateibasierte Ziele immer Folgendes fest: `batch`.</li><li>Beim Konfigurieren des Zielversands für ein Streaming-Ziel muss die `deliveryMatchers` nicht erforderlich.</li></ul> |

{style="table-layout:auto"}

## Zielversandeinstellungen für Streaming-Ziele {#destination-delivery-streaming}

Das folgende Beispiel zeigt, wie die Zielbereitstellungseinstellungen für ein Streaming-Ziel konfiguriert werden sollten. Beachten Sie Folgendes: `deliveryMatchers` für Streaming-Ziele nicht erforderlich ist.

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

Das folgende Beispiel zeigt, wie die Zielbereitstellungseinstellungen für ein dateibasiertes Ziel konfiguriert werden sollen. Beachten Sie Folgendes: `deliveryMatchers` -Abschnitt ist für dateibasierte Ziele erforderlich.

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

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, wie Sie die Orte konfigurieren können, an denen Ihr Ziel Daten exportieren soll, sowohl für Streaming- als auch für dateibasierte Ziele.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)