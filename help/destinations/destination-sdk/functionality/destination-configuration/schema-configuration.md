---
description: Erfahren Sie, wie Sie das Partnerschema für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Konfiguration des Partnerschemas
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '1715'
ht-degree: 10%

---


# Konfiguration des Partnerschemas

Schemata dienen in Experience Platform zur konsistenten und wiederverwendbaren Beschreibung der Struktur von Daten. Wenn Daten in Platform erfasst werden, werden sie nach einem XDM-Schema strukturiert. Weitere Informationen zum Schemaaufbaumodell, einschließlich Planungsgrundsätzen und Best Practices, finden Sie in den [Grundlagen des Schemaaufbaus](../../../../xdm/schema/composition.md).

Beim Erstellen eines Ziels mit Destination SDK können Sie Ihr eigenes Partnerschema definieren, das von Ihrer Zielplattform verwendet werden soll. Dadurch können Benutzer Profilattribute von Platform bestimmten Feldern zuordnen, die von Ihrer Zielplattform erkannt werden, und zwar in der Platform-Benutzeroberfläche.

Beim Konfigurieren des Partnerschemas für Ihr Ziel können Sie die von Ihrer Zielplattform unterstützte Feldzuordnung anpassen, z. B.:

* Benutzern erlauben, eine `phoneNumber` XDM-Attribut zu einem `phone` -Attribut, das von Ihrer Zielplattform unterstützt wird.
* Erstellen Sie dynamische Partnerschemata, die von Experience Platform dynamisch aufgerufen werden können, um eine Liste aller unterstützten Attribute in Ihrem Ziel abzurufen.
* Definieren Sie erforderliche Feldzuordnungen, die für Ihre Zielplattform erforderlich sind.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder lesen Sie das Handbuch zu [Destination SDK zum Konfigurieren eines dateibasierten Ziels verwenden](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Die Schemaeinstellungen können im `/authoring/destinations` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Schemakonfigurationsoptionen beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, welche Kunden in der Platform-Benutzeroberfläche angezeigt werden.

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |

## Unterstützte Schemakonfiguration {#supported-schema-types}

Destination SDK unterstützt mehrere Schemakonfigurationen:

* Statische Schemata werden durch die `profileFields` -Array im `schemaConfig` Abschnitt. In einem statischen Schema definieren Sie jedes Zielattribut, das in der Experience Platform-Benutzeroberfläche im `profileFields` Array. Wenn Sie Ihr Schema aktualisieren müssen, müssen Sie [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md).
* Dynamische Schemata verwenden einen zusätzlichen Zielservertyp, den so genannten [dynamischer Schemaserver](../../authoring-api/destination-server/create-destination-server.md), um Schemas dynamisch basierend auf Ihrer eigenen API zu erstellen. Dynamische Schemata verwenden nicht die `profileFields` Array. Wenn Sie Ihr Schema aktualisieren müssen, müssen Sie [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md). Stattdessen ruft der dynamische Schemaserver das aktualisierte Schema von Ihrer API ab.
* Innerhalb der Schemakonfiguration haben Sie die Möglichkeit, erforderliche (oder vordefinierte) Zuordnungen hinzuzufügen. Hierbei handelt es sich um Zuordnungen, die Benutzer in der Platform-Benutzeroberfläche anzeigen können. Sie können sie jedoch beim Einrichten einer Verbindung zu Ihrem Ziel nicht ändern. Beispielsweise können Sie erzwingen, dass das Feld für die E-Mail-Adresse immer an das Ziel gesendet wird.

Die `schemaConfig` -Abschnitt verwendet mehrere Konfigurationsparameter, je nach dem benötigten Schematyp, wie in den folgenden Abschnitten dargestellt.

## Erstellen eines statischen Schemas {#attributes-schema}

Um ein statisches Schema mit Profilattributen zu erstellen, definieren Sie die Zielattribute im `profileFields` Array wie unten dargestellt.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
}
```

| Parameter | Typ | Erforderlich/Optional | Beschreibung |
|---------|----------|------|---|
| `profileFields` | Array | Optional | Definiert das Array von Zielattributen, die von Ihrer Zielplattform akzeptiert werden und denen Kunden ihre Profilattribute zuordnen können. Bei Verwendung von `profileFields` -Array, können Sie die `useCustomerSchemaForAttributeMapping` -Parameter vollständig. |
| `useCustomerSchemaForAttributeMapping` | Boolesch | Optional | Aktiviert oder deaktiviert die Zuordnung von Attributen aus dem Kundenschema zu den Attributen, die Sie in der Variablen `profileFields` Array. <ul><li>Wenn auf `true`, sehen Benutzer nur die Quellspalte im Zuordnungsfeld. `profileFields` in diesem Fall nicht anwendbar sind.</li><li>Wenn auf `false`, können Benutzer Quellattribute aus ihrem Schema den Attributen zuordnen, die Sie in der `profileFields` Array.</li></ul> Der Standardwert lautet `false`. |
| `profileRequired` | Boolesch | Optional | Verwendung `true` , wenn Benutzer in der Lage sein sollten, Profilattribute von Experience Platform benutzerdefinierten Attributen auf Ihrer Zielplattform zuzuordnen. |
| `segmentRequired` | Boolesch | Erforderlich | Dieser Parameter ist für Destination SDK erforderlich und sollte immer auf `true`. |
| `identityRequired` | Boolesch | Erforderlich | Legen Sie fest auf `true` , wenn Benutzer in der Lage sein sollten, [Identitätstypen](identity-namespace-configuration.md) von der Experience Platform zu den Attributen, die Sie in der `profileFields` Array . |

{style="table-layout:auto"}

Das daraus resultierende Benutzeroberflächenerlebnis wird in den unten stehenden Bildern angezeigt.

Wenn Benutzer das Zielgruppen-Mapping auswählen, sehen sie die Felder, die in der Variablen `profileFields` Array.

![UI-Bild, das den Bildschirm mit den Zielattributen anzeigt.](../../assets/functionality/destination-configuration/select-attributes.png)

Nach Auswahl der Attribute werden sie in der Spalte mit den Zielfeldern angezeigt.

![Benutzeroberflächenbild mit einem statischen Zielschema mit Attributen](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## Dynamisches Schema erstellen {#dynamic-schema-configuration}

Destination SDK unterstützt die Erstellung von dynamischen Partnerschemata. Im Gegensatz zu statischen Schemata verwendet ein dynamisches Schema keine `profileFields` Array. Stattdessen verwenden dynamische Schemata einen dynamischen Schema-Server, der eine Verbindung zu Ihrer eigenen API herstellt, von der aus die Schemakonfiguration abgerufen wird.

>[!IMPORTANT]
>
>Bevor Sie ein dynamisches Schema erstellen, müssen Sie [Erstellen eines dynamischen Schemaservers](../../authoring-api/destination-server/create-destination-server.md).

In einer dynamischen Schemakonfiguration wird die `profileFields` Array wird durch die `dynamicSchemaConfig` wie unten dargestellt.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parameter | Typ | Erforderlich/Optional | Beschreibung |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | Zeichenfolge | Erforderlich | Gibt an, wie [!DNL Platform]-Kunden eine Verbindung zu Ihrem Ziel herstellen. Akzeptierte Werte sind `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Verwendung `CUSTOMER_AUTHENTICATION` wenn sich Platform-Kunden über eine der beschriebenen Authentifizierungsmethoden bei Ihrem System anmelden [here](customer-authentication.md). </li><li> Verwenden Sie `PLATFORM_AUTHENTICATION`, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrem Ziel existiert und der [!DNL Platform]-Kunde keine Authentifizierungsdaten bereitstellen muss, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie [Erstellen eines Anmeldeinformationsobjekts](../../credentials-api/create-credential-configuration.md) Verwendung der Anmeldeinformationen-API. </li><li>Verwenden Sie `NONE`, wenn keine Authentifizierung erforderlich ist, um Daten an Ihre Zielplattform zu senden. </li></ul> |
| `dynamicEnum.destinationServerId` | Zeichenfolge | Erforderlich | Die `instanceId` des dynamischen Schemaservers. Dieser Zielserver enthält den API-Endpunkt, den die Experience Platform aufruft, um das dynamische Schema abzurufen. |
| `dynamicEnum.value` | Zeichenfolge | Erforderlich | Der Name des dynamischen Schemas, wie in der Konfiguration des dynamischen Schemaservers definiert. |
| `dynamicEnum.responseFormat` | Zeichenfolge | Erforderlich | Immer auf `SCHEMA` beim Definieren eines dynamischen Schemas. |
| `profileRequired` | Boolesch | Optional | Verwendung `true` , wenn Benutzer in der Lage sein sollten, Profilattribute von Experience Platform benutzerdefinierten Attributen auf Ihrer Zielplattform zuzuordnen. |
| `segmentRequired` | Boolesch | Erforderlich | Dieser Parameter ist für Destination SDK erforderlich und sollte immer auf `true`. |
| `identityRequired` | Boolesch | Erforderlich | Legen Sie fest auf `true` , wenn Benutzer in der Lage sein sollten, [Identitätstypen](identity-namespace-configuration.md) von der Experience Platform zu den Attributen, die Sie in der `profileFields` Array . |

{style="table-layout:auto"}

## Erforderliche Zuordnungen {#required-mappings}

Innerhalb der Schemakonfiguration haben Sie neben Ihrem statischen oder dynamischen Schema die Möglichkeit, erforderliche (oder vordefinierte) Zuordnungen hinzuzufügen. Hierbei handelt es sich um Zuordnungen, die Benutzer in der Platform-Benutzeroberfläche anzeigen können. Sie können sie jedoch beim Einrichten einer Verbindung zu Ihrem Ziel nicht ändern.

Beispielsweise können Sie erzwingen, dass das Feld für die E-Mail-Adresse immer an das Ziel gesendet wird.

>[!NOTE]
>
>Die folgenden Kombinationen erforderlicher Zuordnungen werden derzeit unterstützt:
>* Sie können ein erforderliches Quellfeld und ein erforderliches Zielfeld konfigurieren. In diesem Fall können Benutzer keine der beiden Felder bearbeiten oder auswählen und nur die Auswahl anzeigen.
>* Sie können nur ein erforderliches Zielfeld konfigurieren. In diesem Fall können Benutzer ein Quellfeld auswählen, das dem Ziel zugeordnet werden soll.
>
> Die Konfiguration eines nur erforderlichen Quellfelds ist derzeit *not* unterstützt.

Nachfolgend finden Sie zwei Beispiele für eine Schemakonfiguration mit erforderlichen Zuordnungen und wie diese im Zuordnungsschritt des [Workflow &quot;Daten für Batch-Ziele aktivieren&quot;](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB Erforderliche Quell- und Zielzuordnungen]

Das folgende Beispiel zeigt die erforderlichen Quell- und Zielzuordnungen. Wenn sowohl Quell- als auch Zielfelder als erforderliche Zuordnungen angegeben sind, können Benutzer keines der beiden Felder auswählen oder bearbeiten und nur die vordefinierte Auswahl anzeigen.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| Parameter | Typ | Erforderlich/Optional | Beschreibung |
|---|---|---|---|
| `requiredMappingsOnly` | Boolesch | Optional | Wenn dies auf true festgelegt ist, können Benutzer neben den erforderlichen Zuordnungen, die Sie in der Variablen `requiredMappings` Array. |
| `requiredMappings.sourceType` | Zeichenfolge | Erforderlich | Gibt den Typ der `source` -Feld. Unterstützte Werte: <ul><li>`text/x.schema-path`: Verwenden Sie diesen Wert, wenn die Variable `source` -Feld ist ein Profilattribut aus einem XDM-Schema.</li><li>`text/x.aep-xl`: Verwenden Sie diesen Wert, wenn `source` -Feld wird durch einen regulären Ausdruck definiert. Beispiel: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: Verwenden Sie diesen Wert, wenn `source` -Feld wird durch eine Makrovorlage definiert. Die einzige unterstützte Makrovorlage ist derzeit `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | Zeichenfolge | Erforderlich | Gibt den Wert des Quellfelds an. Unterstützte Werttypen: <ul><li>XDM-Profilattribute. Beispiel: `personalEmail.address`. Wenn Ihr Quellattribut ein XDM-Profilattribut ist, legen Sie die `sourceType` Parameter auf `text/x.schema-path`.</li><li>Reguläre Ausdrücke. Beispiel: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. Wenn Ihr Quellattribut ein regulärer Ausdruck ist, legen Sie die `sourceType` Parameter auf `text/x.aep-xl`.</li><li>Makrovorlagen. Beispiel:`metadata.segment.alias`. Wenn Ihr Quellattribut eine Makrovorlage ist, legen Sie die `sourceType` Parameter auf `text/plain`. Die einzige unterstützte Makrovorlage ist derzeit `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | Zeichenfolge | Erforderlich | Gibt den Wert des Zielfelds an. Wenn sowohl Quell- als auch Zielfelder als erforderliche Zuordnungen angegeben sind, können Benutzer keines der beiden Felder auswählen oder bearbeiten und nur die Auswahl anzeigen. |

{style="table-layout:auto"}

Daher wird die **[!UICONTROL Quellfeld]** und **[!UICONTROL Zielfeld]** -Abschnitte in der Platform-Benutzeroberfläche ausgegraut sind.

![Bild der erforderlichen Zuordnungen im UI-Aktivierungsfluss.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB Erforderliche Zielzuordnung]

Das folgende Beispiel zeigt eine erforderliche Zielzuordnung. Wenn nur das Zielfeld als erforderlich angegeben wird, können Benutzer auswählen, welches Quellfeld ihm zugeordnet werden soll.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| Parameter | Typ | Erforderlich/Optional | Beschreibung |
|---|---|---|---|
| `requiredMappingsOnly` | Boolesch | Optional | Wenn dies auf true festgelegt ist, können Benutzer neben den erforderlichen Zuordnungen, die Sie in der Variablen `requiredMappings` Array. |
| `requiredMappings.destination` | Zeichenfolge | Erforderlich | Gibt den Wert des Zielfelds an. Wenn nur das Zielfeld angegeben ist, können Benutzer ein Quellfeld auswählen, das dem Ziel zugeordnet werden soll. |
| `mandatoryRequired` | Boolesch | Optional | Gibt an, ob die Zuordnung als [mandatory attribute](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | Boolesch | Optional | Gibt an, ob die Zuordnung als [Deduplizierungsschlüssel](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

Daher wird die **[!UICONTROL Zielfeld]** in der Platform-Benutzeroberfläche ausgegraut ist, während die **[!UICONTROL Quellfeld]** -Abschnitt aktiv ist und Benutzer damit interagieren können. Die **[!UICONTROL Obligatorischer Schlüssel]** und **[!UICONTROL Deduplizierungsschlüssel]** -Optionen aktiviert sind und die Benutzer sie nicht ändern können.

![Bild der erforderlichen Zuordnungen im UI-Aktivierungsfluss.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, welche Schematypen von Destination SDK unterstützt werden und wie Sie Ihr Schema konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)