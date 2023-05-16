---
description: Erfahren Sie, wie Sie Eingabefelder in der Experience Platform-Benutzeroberfläche erstellen, mit denen Ihre Benutzer verschiedene Informationen angeben können, die für die Verbindung und den Export von Daten zu Ihrem Ziel relevant sind.
title: Benutzerdefinierte Datenfelder
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 13%

---


# Benutzereingaben über Kundendatenfelder konfigurieren

Beim Herstellen einer Verbindung zu Ihrem Ziel in der Experience Platform-Benutzeroberfläche müssen Ihre Benutzer möglicherweise bestimmte Konfigurationsdetails angeben oder bestimmte Optionen auswählen, die Sie ihnen zur Verfügung stellen. In der Destination SDK werden diese Optionen als Kundendatenfelder bezeichnet.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder sehen Sie die folgenden Übersichtsseiten zur Zielkonfiguration:

* [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## Anwendungsbeispiele für Kundendatenfelder {#use-cases}

Verwenden Sie Kundendatenfelder für eine Vielzahl von Anwendungsfällen, in denen Benutzer Daten in die Experience Platform-Benutzeroberfläche eingeben müssen. Verwenden Sie beispielsweise Kundendatenfelder, wenn Benutzer Folgendes bereitstellen müssen:

* Cloud-Speicher-Behälternamen und -pfade für dateibasierte Ziele.
* Das Format, das von den Kundendatenfeldern akzeptiert wird.
* Verfügbare Dateikomprimierungstypen, aus denen Benutzer auswählen können.
* Listen der verfügbaren Endpunkte für Echtzeit-Integrationen (Streaming).

Sie können Kundendatenfelder über die `/authoring/destinations` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Konfigurationstypen von Kundendatenfeldern beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, was Kunden in der Experience Platform-Benutzeroberfläche sehen werden.

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

Bei der Erstellung Ihrer eigenen Kundendatenfelder können Sie die in der folgenden Tabelle beschriebenen Parameter verwenden, um ihr Verhalten zu konfigurieren.

| Parameter | Typ | Erforderlich/Optional | Beschreibung |
|---------|----------|------|---|
| `name` | Zeichenfolge | Erforderlich | Geben Sie einen Namen für das benutzerdefinierte Feld ein, das Sie einführen. Dieser Name ist in der Platform-Benutzeroberfläche nur sichtbar, wenn die Variable `title` leer ist oder fehlt. |
| `type` | Zeichenfolge | Erforderlich | Gibt den Typ des benutzerdefinierten Felds an, das Sie einführen. Akzeptierte Werte: <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | Zeichenfolge | Optional | Gibt den Namen des Felds an, wie er von Kunden in der Platform-Benutzeroberfläche angezeigt wird. Wenn dieses Feld leer ist oder fehlt, übernimmt die Benutzeroberfläche den Feldnamen von der `name` -Wert. |
| `description` | Zeichenfolge | Optional | Geben Sie eine Beschreibung für das benutzerdefinierte Feld ein. Diese Beschreibung ist in der Platform-Benutzeroberfläche nicht sichtbar. |
| `isRequired` | Boolesch | Optional | Gibt an, ob Benutzer im Zielkonfigurations-Workflow einen Wert für dieses Feld angeben müssen. |
| `pattern` | Zeichenfolge | Optional | Erzwingt bei Bedarf ein Muster für das benutzerdefinierte Feld. Verwenden Sie reguläre Ausdrücke, um ein Muster zu erzwingen. Wenn Ihre Kunden-IDs beispielsweise keine Zahlen oder Unterstriche enthalten, geben Sie in dieses Feld `^[A-Za-z]+$` ein. |
| `enum` | Zeichenfolge | Optional | Rendert das benutzerdefinierte Feld als Dropdown-Menü und listet die für den Benutzer verfügbaren Optionen auf. |
| `default` | Zeichenfolge | Optional | Definiert den Standardwert aus einer `enum`-Liste. |
| `hidden` | Boolesch | Optional | Gibt an, ob das Kundendatenfeld in der Benutzeroberfläche angezeigt wird oder nicht. |
| `unique` | Boolesch | Optional | Verwenden Sie diesen Parameter, wenn Sie ein Kundendatenfeld erstellen müssen, dessen Wert über alle vom Unternehmen der Benutzenden eingerichteten Zieldatenflüsse hinweg eindeutig sein muss. Beispiel: Das Feld **[!UICONTROL Integrationsalias]** im Ziel [Benutzerdefinierte Personalisierung](../../../catalog/personalization/custom-personalization.md) muss eindeutig sein, d. h., zwei separate Datenflüsse zu diesem Ziel dürfen für dieses Feld nicht denselben Wert aufweisen. |
| `readOnly` | Boolesch | Optional | Gibt an, ob der Kunde den Wert des Felds ändern kann oder nicht. |

{style="table-layout:auto"}

Im folgenden Beispiel wird die Variable `customerDataFields` definiert zwei Felder, die Benutzer beim Herstellen einer Verbindung zum Ziel in die Platform-Benutzeroberfläche eingeben müssen:

* `Account ID`: Eine Benutzerkonto-ID für Ihre Zielplattform.
* `Endpoint region`: Der regionale Endpunkt der API, mit der sie eine Verbindung herstellen. Die `enum` erstellt ein Dropdown-Menü mit den in definierten Werten, die von den Benutzern ausgewählt werden können.

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

Das daraus resultierende Benutzeroberflächenerlebnis wird in der Abbildung unten dargestellt.

![UI-Bild, das ein Beispiel für Kundendatenfelder zeigt.](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## Namen und Beschreibungen der Zielverbindung {#names-description}

Beim Erstellen eines neuen Ziels fügt Destination SDK automatisch **[!UICONTROL Name]** und **[!UICONTROL Beschreibung]** -Felder zum Bildschirm für die Zielverbindung in der Platform-Benutzeroberfläche. Wie Sie im obigen Beispiel sehen können, wird die **[!UICONTROL Name]** und **[!UICONTROL Beschreibung]** -Felder werden in der Benutzeroberfläche gerendert, ohne in die Konfiguration der Kundendatenfelder einbezogen zu werden.

>[!IMPORTANT]
>
>Wenn Sie **[!UICONTROL Name]** und **[!UICONTROL Beschreibung]** -Felder in der Konfiguration der Kundendatenfelder sehen, wie sie in der Benutzeroberfläche dupliziert wurden.

## Kundendatenfelder bestellen {#ordering}

Die Reihenfolge, in der Sie die Kundendatenfelder zur Zielkonfiguration hinzufügen, wird in der Platform-Benutzeroberfläche angezeigt.

Beispielsweise wird die folgende Konfiguration entsprechend in der Benutzeroberfläche angezeigt, wobei die Optionen in der Reihenfolge angezeigt werden **[!UICONTROL Name]**, **[!UICONTROL Beschreibung]**, **[!UICONTROL Bucket-Name]**, **[!UICONTROL Ordnerpfad]**, **[!UICONTROL Dateityp]**, **[!UICONTROL Komprimierungsformat]**.

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
   "description":"Select the exported file type.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "hidden":false,
   "enum":[
      "csv",
      "json",
      "parquet"
   ],
   "default":"csv"
},
{
   "name":"compression",
   "title":"Compression format",
   "description":"Select the desired file compression format.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "enum":[
      "SNAPPY",
      "GZIP",
      "DEFLATE",
      "NONE"
   ]
}
]
```

![Bild, das die Reihenfolge der Dateiformatierungsoptionen in der Benutzeroberfläche &quot;Experience Platform&quot;anzeigt.](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## Kundendatenfelder gruppieren {#grouping}

Sie können mehrere Kundendatenfelder in einem Abschnitt gruppieren. Beim Einrichten der Verbindung zum Ziel in der Benutzeroberfläche können Benutzer eine visuelle Gruppierung ähnlicher Felder sehen und davon profitieren.

Verwenden Sie dazu `"type": "object"` , um die Gruppe zu erstellen und die gewünschten Kundendatenfelder in einer `properties` -Objekt, wie in der Abbildung unten gezeigt, wobei die Gruppierung **[!UICONTROL CSV-Optionen]** hervorgehoben ist.

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Bild mit Kundendatenfeldern, die in der Benutzeroberfläche gruppiert werden.](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## Erstellen von Dropdown-Selektoren für Kundendatenfelder {#dropdown-selectors}

In Situationen, in denen Sie Benutzern die Auswahl zwischen verschiedenen Optionen ermöglichen möchten, z. B. welche Zeichen zum Trennen der Felder in CSV-Dateien verwendet werden sollen, können Sie Dropdown-Felder zur Benutzeroberfläche hinzufügen.

Verwenden Sie dazu die `namedEnum` -Objekt wie unten gezeigt und konfigurieren Sie eine `default` für die Optionen, die der Benutzer auswählen kann.

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Bildschirmaufzeichnung mit einem Beispiel für Dropdown-Selektoren, die mit der oben gezeigten Konfiguration erstellt wurden.](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## Bedingte Kundendatenfelder erstellen {#conditional-options}

Sie können bedingte Kundendatenfelder erstellen, die im Aktivierungs-Workflow nur angezeigt werden, wenn Benutzer eine bestimmte Option auswählen.

Beispielsweise können Sie bedingte Dateiformatierungsoptionen erstellen, die nur angezeigt werden, wenn Benutzer einen bestimmten Dateityp auswählen.

Die folgende Konfiguration erstellt eine bedingte Gruppierung für CSV-Dateiformatierungsoptionen. Die CSV-Dateioptionen werden nur angezeigt, wenn der Benutzer CSV als gewünschten Dateityp für den Export auswählt.

Um ein Feld als bedingt festzulegen, verwenden Sie die `conditional` -Parameter wie unten gezeigt:

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

In einem größeren Kontext können Sie die `conditional` -Feld, das in der folgenden Zielkonfiguration verwendet wird, neben dem `fileType` und `csvOptions` -Objekt, in dem es definiert ist.

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

Unten sehen Sie den resultierenden Bildschirm der Benutzeroberfläche, der auf der oben beschriebenen Konfiguration basiert. Wenn der Benutzer den Dateityp CSV auswählt, werden in der Benutzeroberfläche zusätzliche Dateiformatierungsoptionen angezeigt, die auf den CSV-Dateityp verweisen.

![Bildschirmaufzeichnung mit der Option zur Formatierung bedingter Dateien für CSV-Dateien.](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## Zugriff auf vorlagenbasierte Kundendatenfelder {#accessing-templatized-fields}

Wenn für Ihr Ziel Benutzereingaben erforderlich sind, müssen Sie Ihren Benutzern eine Auswahl von Kundendatenfeldern bereitstellen, die sie über die Platform-Benutzeroberfläche ausfüllen können. Anschließend müssen Sie Ihren Zielserver so konfigurieren, dass die Benutzereingabe aus den Kundendatenfeldern korrekt gelesen wird. Dies erfolgt über vorlagenbasierte Felder.

Vorlagenfelder verwenden das Format `{{customerData.fieldName}}`, wobei `fieldName` ist der Name des Kundendatenfelds, aus dem Sie Informationen lesen. Alle in der Vorlage enthaltenen Kundendatenfelder erhalten vorangestellt durch `customerData.` und in doppelte Klammern eingeschlossen `{{ }}`.

Betrachten wir beispielsweise die folgende Amazon S3-Zielkonfiguration:

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

Diese Konfiguration fordert Ihre Benutzer zur Eingabe ihrer [!DNL Amazon S3] Behältername und Ordnerpfad in die entsprechenden Kundendatenfelder.

Damit die Experience Platform ordnungsgemäß eine Verbindung zu [!DNL Amazon S3]muss Ihr Zielserver so konfiguriert sein, dass die Werte aus diesen beiden Kundendatenfeldern gelesen werden, wie unten dargestellt:

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

Die Vorlagenwerte `{{customerData.bucketName}}` und `{{customerData.path}}` Lesen Sie die vom Benutzer eingegebenen Werte, damit Experience Platform erfolgreich eine Verbindung zur Zielplattform herstellen kann.

Weitere Informationen zum Konfigurieren des Zielservers zum Lesen von Vorlagenfeldern finden Sie in der Dokumentation unter [hartcodierte oder vorlagenbasierte Felder](../destination-server/server-specs.md#templatized-fields).

## Nächste Schritte {#next-steps}

Nachdem Sie diesen Artikel gelesen haben, sollten Sie besser verstehen, wie Sie Ihren Benutzern erlauben können, Informationen über Kundendatenfelder in die Experience Platform-Benutzeroberfläche einzugeben. Jetzt wissen Sie auch, wie Sie das richtige Kundendatenfeld für Ihren Anwendungsfall auswählen und Kundendatenfelder in der Platform-Benutzeroberfläche konfigurieren, bestellen und gruppieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)