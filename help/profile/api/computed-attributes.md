---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Berechnete Attribute - Echtzeit-Client-Profil-API
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '2404'
ht-degree: 83%

---


# (Alpha) Endpunkt &quot;Berechnete Attribute&quot;

>[!IMPORTANT]
>Die in diesem Dokument beschriebene Funktion für berechnete Attribute ist derzeit als Alphaversion erhältlich und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Mit berechneten Attributen können Sie den Wert von Feldern anhand anderer Werte, Berechnungen und Ausdrücke automatisch berechnen. Berechnete Attribute agieren auf der Profilebene, d. h., Sie können Werte über alle Datensätze und Ereignisse hinweg aggregieren.

Jedes berechnete Attribut enthält einen Ausdruck (oder „Regel“), der eingehende Daten auswertet und den sich ergebenden Wert in einem Profilattribut oder Ereignis speichert. Diese Berechnungen helfen Ihnen dabei, verschiedene Fragen zu beantworten, zum Beispiel zum Lebenszeitkaufwert, zur Zeit zwischen Käufen oder zur Zahl der Anwendungsöffnungen – ohne jedes Mal, wenn Sie bestimmte Informationen benötigen, manuell komplexe Berechnungen durchführen zu müssen.

In diesem Handbuch werden berechnete Attribute in Adobe Experience Platform genauer beschrieben. Außerdem finden Sie Beispiel-API-Aufrufe zur Ausführung grundlegender CRUD-Vorgänge mithilfe des `/config/computedAttributes`-Endpunkts.

## Erste Schritte

The API endpoint used in this guide is part of the [Real-time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer beliebigen [!DNL Experience Platform] API erforderlich sind.

## Berechnete Attribute

Adobe Experience Platform enables you to easily import and merge data from multiple sources in order to generate [!DNL Real-time Customer Profiles]. Jedes Profil enthält wichtige Daten zu einer Person, wie z. B. ihre Kontaktdaten, Präferenzen und den Kaufverlauf, sodass eine 360-Grad-Ansicht des Kunden entsteht.

Manche der im Profil erfassten Daten sind beim direkten Lesen der Datenfelder leicht verständlich (z. B. „Vorname“), während bei anderen Daten mehrere Berechnungen oder andere Felder und Werte erforderlich sind, um die Daten zu generieren (z. B. „Lebenszeitkaufsumme“). To make this data easier to understand at a glance, [!DNL Platform] allows you to create **[!UICONTROL computed attributes]** that automatically perform these references and calculations, returning the value in the appropriate field.

Berechnete Attribute umfassen das Erstellen eines Ausdrucks (oder „Regel“), der auf eingehende Daten angewendet wird und den sich ergebenden Wert in einem Profilattribut oder Ereignis speichert. Ausdrücke können auf unterschiedliche Weise definiert werden. So können Sie festlegen, dass eine Regel nur eingehende Ereignisse, ein eingehendes Ereignis und Profildaten oder ein eingehendes Ereignis, Profildaten und historische Ereignisse auswertet.

### Anwendungsbeispiele

Anwendungsbeispiele für berechnete Attribute können von einfachen Berechnungen hin zu sehr komplexen Verweisen reichen. Im Folgenden finden Sie einige Anwendungsbeispiele für berechnete Attribute:

1. **[!UICONTROL Prozent]:**Ein einfaches, berechnetes Attribut könnte darin bestehen, zwei numerische Felder in einem Datensatz zu nehmen und sie zu teilen, um einen Prozentwert zu erstellen. Sie könnten beispielsweise die Gesamtzahl der an eine Person gesendeten E-Mails durch die Zahl der von der Person geöffneten E-Mails teilen. Wenn Sie das sich ergebende Feld für berechnete Attribute ansehen, erkennen Sie schnell den Prozentsatz der Gesamt-E-Mails, die von der Person geöffnet wurden.
1. **[!UICONTROL Anwendungsnutzung]:**Ein weiteres Beispiel ist die Möglichkeit, die Anzahl der Aggregat zu bestimmen, die ein Benutzer zum Öffnen der Anwendung benötigt. Wenn Sie die Gesamtzahl der Anwendungsöffnungen anhand einzelner Öffnungsereignisse verfolgen, können Sie Anwendern bei der 100. Öffnung besondere Angebote oder Nachrichten zukommen lassen, um die Interaktion mit Ihrer Marke zu stärken.
1. **[!UICONTROL Lebenszeitwerte]:**Die Erfassung laufender Gesamtsummen, z. B. eines Kaufwerts für einen Kunden über die gesamte Lebensdauer, kann sehr schwierig sein. Dafür muss die historische Gesamtsumme bei jedem Auftreten eines neuen Kaufereignisses aktualisiert werden. Mit einem berechneten Attribut können Sie dies wesentlich einfacher tun, indem Sie den Lebenszeitwert in einem einzelnen Feld pflegen, das nach jedem erfolgreichen Kaufereignis, das mit dem Kunden verbunden ist, automatisch aktualisiert wird.

## Berechnetes Attribut konfigurieren

Um ein berechnetes Attribut zu konfigurieren, müssen Sie zunächst das Feld ermitteln, das den berechneten Attributwert enthält. Dieses Feld kann mit einem Mixin erstellt werden, um das Feld einem vorhandenen Schema hinzuzufügen, oder durch Auswahl eines Felds, das Sie bereits in einem Schema definiert haben.

>[!NOTE]
>Berechnete Attribute können keinen Feldern in Adobe-definierten Mixins hinzugefügt werden. Das Feld muss sich im `tenant`-Namespace befinden, d. h. es muss ein Feld sein, das Sie definieren und einem Schema hinzufügen.

In order to successfully define a computed attribute field, the schema must be enabled for [!DNL Profile] and appear as part of the union schema for the class upon which the schema is based. For more information on [!DNL Profile]-enabled schemas and unions, please review the section of the [!DNL Schema Registry] developer guide section on [enabling a schema for Profile and viewing union schemas](../../xdm/api/getting-started.md). Außerdem empfehlen wir Ihnen, den [Abschnitt über Vereinigungen](../../xdm/schema/composition.md) in der Grundlagendokumentation zur Schemakomposition zu lesen.

The workflow in this tutorial uses a [!DNL Profile]-enabled schema and follows the steps for defining a new mixin containing the computed attribute field and ensuring it is the correct namespace. Wenn Sie bereits über ein Feld verfügen, das sich in einem Profil-aktivierten Schema im richtigen Namespace befindet, können Sie direkt mit dem [Erstellen eines berechneten Attributs](#create-a-computed-attribute) fortfahren.

### Schema anzeigen

In den folgenden Schritten nutzen Sie die Benutzeroberfläche von Adobe Experience Platform, um ein Schema zu suchen, ein Mixin hinzuzufügen und ein Feld zu definieren. If you prefer to use the [!DNL Schema Registry] API, please refer to the [Schema Registry developer guide](../../xdm/api/getting-started.md) for steps on how to create a mixin, add a mixin to a schema, and enable a schema for use with [!DNL Real-time Customer Profile].

Klicken Sie in der Benutzeroberfläche in der linken Leiste auf **[!UICONTROL Schemas]** und nutzen Sie die Suchleiste auf dem Tab *[!UICONTROL Durchsuchen]*, um das Schema, das Sie aktualisieren möchten, zu suchen.

![](../images/computed-attributes/Schemas-Browse.png)

Once you have located the schema, click its name to open the [!DNL Schema Editor] where you can make edits to the schema.

![](../images/computed-attributes/Schema-Editor.png)

### Mixin erstellen

Um ein neues Mixin zu erstellen, klicken Sie im Abschnitt *[!UICONTROL Komposition]* auf der linken Seite des Editors neben *Mixins* auf **[!UICONTROL Hinzufügen]**. Dadurch wird der Dialog **[!UICONTROL Mixin hinzufügen]** geöffnet, in dem vorhandene Mixins angezeigt werden. Klicken Sie auf das Optionsfeld für **[!UICONTROL Neues Mixin erstellen]**, um Ihr neues Mixin zu definieren.

Geben Sie dem Mixin einen Namen und eine Beschreibung und klicken Sie anschließend auf **[!UICONTROL Mixin hinzufügen]**.

![](../images/computed-attributes/Add-mixin.png)

### Berechnetes Attributfeld für das Schema hinzufügen

Ihr neues Mixin sollte nun im Abschnitt *[!UICONTROL Mixins]* unter *[!UICONTROL Komposition]* angezeigt werden. Klicken Sie auf den Namen des Mixins, woraufhin im Abschnitt *[!UICONTROL Struktur]* des Editors mehrere Schaltflächen vom Typ **[!UICONTROL Feld hinzufügen]** angezeigt werden.

Wählen Sie neben dem Namen des Schemas **[!UICONTROL Feld hinzufügen]**, um ein Feld der obersten Ebene hinzuzufügen. Alternativ können Sie das Feld an einer beliebigen Stelle im gewünschten Schema einfügen.

Nachdem Sie auf **[!UICONTROL Feld hinzufügen]** geklickt haben, wird ein neues Objekt mit dem Namen Ihrer Mandantenkennung geöffnet. Dies zeigt, dass sich das Feld im richtigen Namespace befindet. Innerhalb des Objekts wird ein *[!UICONTROL neues Feld]* angezeigt. Dies ist das Feld, in dem Sie das berechnete Attribut definieren werden.

![](../images/computed-attributes/New-field.png)

### Feld konfigurieren

Geben Sie im Abschnitt *[!UICONTROL Feldeigenschaften]* auf der rechten Seite des Editors die erforderlichen Daten für das neue Feld ein, einschließlich Name, Anzeigename und Typ.

>[!NOTE]
>Der Typ für das Feld muss mit dem Typ des berechneten Attributwerts übereinstimmen. Wenn der berechnete Attributwert beispielsweise eine Zeichenfolge ist, muss auch das im Schema definierte Feld eine Zeichenfolge sein.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Übernehmen]**. Daraufhin werden der Name des Felds sowie der Typ im Abschnitt *[!UICONTROL Struktur]* des Editors angezeigt.

![](../images/computed-attributes/Apply.png)

### Schema aktivieren für [!DNL Profile]

Before continuing, ensure that the schema has been enabled for [!DNL Profile]. Klicken Sie im Bereich *[!UICONTROL Struktur]* des Editors auf den Namen des Schemas, um den Tab *[!UICONTROL Schemaeigenschaften]* anzuzeigen. If the **[!UICONTROL Profile]** slider is blue, the schema has been enabled for [!DNL Profile].

>[!NOTE]
>Enabling a schema for [!DNL Profile] cannot be undone, so if you click on the slider once it has been enabled, you do not have to risk disabling it.

![](../images/computed-attributes/Profile.png)

Jetzt können Sie auf **[!UICONTROL Speichern]** klicken, um das aktualisierte Schema zu speichern und mit dem Rest des Tutorials unter Nutzung der API fortzufahren.

### Berechnetes Attribut erstellen {#create-a-computed-attribute}

With your computed attribute field identified, and confirmation that the schema is enabled for [!DNL Profile], you can now configure a computed attribute.

Richten Sie zunächst eine POST-Anfrage an den `/config/computedAttributes`-Endpunkt mit einem Anfragetext, der die Details des berechneten Attributs enthält, das Sie erstellen möchten.

**API-Format**

```http
POST /config/computedAttributes
```

**Anfrage**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Eigenschaft | Beschreibung |
|---|---|
| `name` | Name des berechneten Attributfelds als Zeichenfolge. |
| `path` | Pfad zum Feld mit dem berechneten Attribut. Dieser Pfad befindet sich im `properties`-Attribut des Schemas und sollte NICHT den Feldnamen im Pfad beinhalten. Lassen Sie beim Schreiben des Pfads die verschiedenen Ebenen von `properties`-Attributen weg. |
| `{TENANT_ID}` | Wenn Sie Ihre Mandantenkennung nicht kennen, lesen Sie bitte die Anleitung zum Finden Ihrer Mandantenkennung im [Entwicklerhandbuch zur Schema Registry](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Eine Beschreibung des berechneten Attributs. Dies ist besonders nützlich, wenn verschiedene berechnete Attribute definiert wurden, da sie Kollegen in Ihrer IMS-Organisation hilft, das gewünschte berechnete Attribut zu finden. |
| `expression.value` | Ein gültiger [!DNL Profile Query Language] (PQL-)Ausdruck. Weiterführende Informationen zu PQL und Links zu unterstützten Abfragen finden Sie in der [PQL-Übersicht](../../segmentation/pql/overview.md). |
| `schema.name` | Die Klasse, auf der das Schema mit dem berechneten Attributfeld basiert. Beispiel: `_xdm.context.experienceevent` bei einem Schema, das auf der XDM ExperienceEvent-Klasse basiert. |

**Antwort**

Ein erfolgreich erstelltes berechnetes Attribut gibt den HTTP-Status 200 (OK) und einen Antworttext mit den Details des neu erstellten berechneten Attributs zurück. Zu den Details gehört eine eindeutige, schreibgeschützte, systemgenerierte `id`, die bei anderen API-Vorgängen zum Verweisen auf das berechnete Attribut verwendet werden kann.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `id` | Eine eindeutige, schreibgeschützte, systemgenerierte ID, die bei anderen API-Vorgängen zum Verweisen auf das berechnete Attribut genutzt werden kann. |
| `imsOrgId` | Die IMS-Organisation, die mit dem berechneten Attribut verbunden ist, sollte mit dem in der Anfrage gesendeten Wert übereinstimmen. |
| `sandbox` | Das Sandbox-Objekt enthält Details zur Sandbox, in der das berechnete Attribut konfiguriert wurde. Diese Daten werden aus der in der Anfrage gesendeten Sandbox-Kopfzeile extrahiert. Weiterführende Informationen dazu finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md). |
| `positionPath` | Ein Array, das den dekonstruierten `path` zum in der Anfrage gesendeten Feld enthält. |
| `returnSchema.meta:xdmType` | Der Typ des Felds, in dem das berechnete Attribut gespeichert wird. |
| `definedOn` | Ein Array, das die Vereinigungsschemas anzeigt, auf deren Basis das berechnete Attribut definiert wurde. Enthält ein Objekt pro Vereinigungsschema, d. h. es können mehrere Objekte im gleichen Array vorhanden sein, wenn das berechnete Attribut anhand verschiedener Klassen unterschiedlichen Schemas hinzugefügt wurde. |
| `active` | Ein boolescher Wert, der anzeigt, ob das berechnete Attribut aktuell aktiv ist oder nicht. Der Standardwert ist `true`. |
| `type` | Der Typ der erstellten Ressource; in diesem Fall ist „ComputedAttribute“ der Standardwert. |
| `createEpoch` und `updateEpoch` | Der Zeitpunkt, zu dem das berechnete Attribut erstellt bzw. zuletzt aktualisiert wurde. |


## Berechnete Attribute aufrufen

Beim Arbeiten mit berechneten Attributen unter Verwendung der API gibt es zwei Optionen zum Aufrufen berechneter Attribute, die Ihre Organisation definiert hat. Die erste besteht im Auflisten aller berechneten Attribute, die zweite im Anzeigen eines bestimmten berechneten Attributs anhand seiner eindeutigen `id`.

Schritte zum Auflisten aller berechneten Attribute und Anzeigen eines bestimmten berechneten Attributs werden in den folgenden Abschnitten beschrieben.

### Berechnete Attribute auflisten {#list-computed-attributes}

Ihre IMS-Organisation kann mehrere berechnete Attribute erstellen; durch Richten einer GET-Anfrage an den `/config/computedAttributes`-Endpunkt können Sie alle vorhandenen berechneten Attribute für Ihre Organisation auflisten.

**API-Format**

```http
GET /config/computedAttributes
```

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

Eine erfolgreiche Antwort umfasst ein `_page`-Attribut, das die Gesamtzahl der berechneten Attribute (`totalCount`) und die Zahl der berechneten Attribute auf der Seite (`pageSize`) angibt.

Die Antwort enthält auch ein `children`-Array, das aus einem oder mehreren Objekten besteht, von denen jedes die Details zu einem berechneten Attribut enthält. Wenn Ihre Organisation über keine berechneten Attribute verfügt, lauten die Werte `totalCount` und `pageSize` 0 (null) und ist das `children`-Array leer.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Eigenschaft | Beschreibung |
|---|---|
| `_page.totalCount` | Die Gesamtzahl der von Ihrer IMS-Organisation definierten berechneten Attribute. |
| `_page.pageSize` | Die Zahl der berechneten Attribute, die auf dieser Ergebnisseite zurückgegeben werden. Wenn `pageSize` gleich `totalCount` ist, bedeutet das, dass nur eine Seite mit Ergebnissen vorhanden ist und alle berechneten Attribute zurückgegeben wurden. Wenn die Werte ungleich sind, gibt es weitere Seiten mit Ergebnissen, die aufgerufen werden können. Weiterführende Informationen finden Sie unter `_links.next`. |
| `children` | Ein Array, das aus einem oder mehreren Objekten besteht, von denen jedes die Details zu einem einzelnen berechneten Attribut enthält. Wenn keine berechneten Attribute definiert wurden, ist das `children`-Array leer. |
| `id` | Ein eindeutiger, schreibgeschützter, systemgenerierter Wert, der einem berechneten Attribut bei der Erstellung automatisch zugewiesen wird. Weiterführende Informationen zu den Komponenten eines berechneten Attributobjekts finden Sie im Abschnitt zum [Erstellen eines berechneten Attributs](#create-a-computed-attribute) weiter oben in diesem Tutorial. |
| `_links.next` | Wenn eine einzelne Seite mit berechneten Attributen zurückgegeben wird, ist `_links.next` ein leeres Objekt (wie in der obigen Beispielantwort dargestellt). Wenn Ihre Organisation über viele berechnete Attribute verfügt, werden diese auf mehreren Seiten zurückgegeben, auf die Sie mittels einer GET-Anfrage an den `_links.next`-Wert zugreifen können. |

### Berechnetes Attribut anzeigen {#view-a-computed-attribute}

Sie können ein bestimmtes berechnetes Attribut auch anzeigen, indem Sie eine GET-Anfrage an den `/config/computedAttributes`-Endpunkt richten und die Kennung des berechneten Attributs in den Anfragepfad einschließen.

**API-Format**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{ATTRIBUTE_ID}` | Die Kennung des berechneten Attributs, das Sie anzeigen möchten. |

**Anfrage**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwort**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Berechnetes Attribut aktualisieren

Wenn Sie merken, dass Sie ein vorhandenes berechnetes Attribut aktualisieren müssen, senden Sie eine PATCH-Anfrage an den `/config/computedAttributes`-Endpunkt und schließen die Kennung des berechneten Attributs, das Sie aktualisieren möchten, in den Anfragepfad ein.

**API-Format**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{ATTRIBUTE_ID}` | Die Kennung des berechneten Attributs, das Sie aktualisieren möchten. |

**Anfrage**

Diese Anfrage nutzt die [JSON Patch-Formatierung](http://jsonpatch.com/), um den „value“ (Wert) des Felds „expression“ (Ausdruck) zu aktualisieren.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Eigenschaft | Beschreibung |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Ein gültiger [!DNL Profile Query Language] (PQL-)Ausdruck. Weiterführende Informationen zu PQL und Links zu unterstützten Abfragen finden Sie in der [PQL-Übersicht](../../segmentation/pql/overview.md). |

**Antwort**

Bei erfolgreicher Aktualisierung werden der HTTP-Status 204 (Kein Inhalt) und ein leerer Antworttext zurückgegeben. Wenn Sie sich vergewissern möchten, dass die Aktualisierung erfolgreich war, können Sie eine GET-Anfrage ausführen, um das berechnete Attribut mit seiner Kennung anzuzeigen.

## Berechnetes Attribut löschen

Sie können ein berechnetes Attribut mithilfe der API auch löschen. Dies geschieht durch Richten einer DELETE-Anfrage an den `/config/computedAttributes`-Endpunkt und Einschließen der Kennung des berechneten Attributs, das Sie löschen möchten, in den Anfragepfad.

>[!NHinweis]
>
>
>Seien Sie beim Löschen eines berechneten Attributs vorsichtig, da es möglicherweise in mehr als einem Schema verwendet wird und der DELETE-Vorgang nicht rückgängig gemacht werden kann.

**API-Format**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parameter | Beschreibung |
|---|---|
| `{ATTRIBUTE_ID}` | Die Kennung des berechneten Attributs, das Sie löschen möchten. |

**Anfrage**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Antwort**

Bei erfolgreicher Löschanfrage werden der HTTP-Status 200 (OK) und ein leerer Antworttext zurückgegeben. Um sicherzugehen, dass der Löschvorgang erfolgreich war, können Sie eine GET-Anfrage ausführen und das berechnete Attribut anhand seiner Kennung nachschlagen. Wenn das Attribut gelöscht wurde, erhalten Sie den HTTP-Fehlerstatus 404 (Nicht gefunden).

## Nächste Schritte

Nachdem Sie sich mit den Grundlagen berechneter Attribute vertraut gemacht haben, können Sie nun mit der Definition berechneter Attribute für Ihre Organisation beginnen.