---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: API-Endpunkt für berechnete Attribute
topic: guide
type: Documentation
description: 'Mit berechneten Attributen können Sie den Wert von Feldern anhand anderer Werte, Berechnungen und Ausdrücke automatisch berechnen. Berechnete Attribute arbeiten mit Echtzeit-Kundendaten, d. h., Sie können Werte für alle in Adobe Experience Platform gespeicherten Datensätze und Ereignis mit Aggregaten versehen. '
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 82%

---


# (Alpha) Endpunkt &quot;Berechnete Attribute&quot;

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebene Funktion für berechnete Attribute ist derzeit als Alphaversion erhältlich und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalität können sich ändern.

Mit berechneten Attributen können Sie den Wert von Feldern anhand anderer Werte, Berechnungen und Ausdrücke automatisch berechnen. Berechnete Attribute agieren auf der Profilebene, d. h., Sie können Werte über alle Datensätze und Ereignisse hinweg aggregieren.

Jedes berechnete Attribut enthält einen Ausdruck oder eine „Regel“, der bzw. die eingehende Daten auswertet und den resultierenden Wert in einem Profilattribut oder Ereignis speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen.

In diesem Handbuch werden berechnete Attribute in Adobe Experience Platform genauer beschrieben. Außerdem finden Sie Beispiel-API-Aufrufe zur Ausführung grundlegender CRUD-Vorgänge mithilfe des `/config/computedAttributes`-Endpunkts.

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil der [Echtzeit-Client-Profil-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Berechnete Attribute

Mit Adobe Experience Platform können Sie einfach Daten aus mehreren Quellen importieren und zusammenführen, um [!DNL Real-time Customer Profiles] zu generieren. Jedes Profil enthält wichtige Daten zu einer Person, wie z. B. ihre Kontaktdaten, Präferenzen und den Kaufverlauf, sodass eine 360-Grad-Ansicht des Kunden entsteht.

Manche der im Profil erfassten Daten sind beim direkten Lesen der Datenfelder leicht verständlich (z. B. „Vorname“), während bei anderen Daten mehrere Berechnungen oder andere Felder und Werte erforderlich sind, um die Daten zu generieren (z. B. „Lebenszeitkaufsumme“). Damit diese Daten auf einen Blick leichter zu verstehen sind, können Sie mit [!DNL Platform] berechnete Attribute erstellen, die automatisch diese Verweise und Berechnungen durchführen und den Wert im entsprechenden Feld zurückgeben.

Berechnete Attribute umfassen das Erstellen eines Ausdrucks (oder „Regel“), der auf eingehende Daten angewendet wird und den sich ergebenden Wert in einem Profilattribut oder Ereignis speichert. Ausdrücke können auf unterschiedliche Weise definiert werden. So können Sie festlegen, dass eine Regel nur eingehende Ereignisse, ein eingehendes Ereignis und Profildaten oder ein eingehendes Ereignis, Profildaten und historische Ereignisse auswertet.

### Anwendungsbeispiele

Anwendungsbeispiele für berechnete Attribute können von einfachen Berechnungen hin zu sehr komplexen Verweisen reichen. Im Folgenden finden Sie einige Anwendungsbeispiele für berechnete Attribute:

1. **[!UICONTROL Prozentwerte]:** Ein einfaches, berechnetes Attribut kann die Entnahme zweier numerischer Felder in einem Datensatz und deren Aufteilung zur Erstellung eines Prozentsatzes sein. Sie könnten beispielsweise die Gesamtzahl der an eine Person gesendeten E-Mails durch die Zahl der von der Person geöffneten E-Mails teilen. Wenn Sie das sich ergebende Feld für berechnete Attribute ansehen, erkennen Sie schnell den Prozentsatz der Gesamt-E-Mails, die von der Person geöffnet wurden.
1. **[!UICONTROL Anwendungsnutzung]:** Ein weiteres Beispiel ist die Möglichkeit, die Anzahl der Anwendungsstarts durch einen Benutzer Aggregat. Wenn Sie die Gesamtzahl der Anwendungsöffnungen anhand einzelner Öffnungsereignisse verfolgen, können Sie Anwendern bei der 100. Öffnung besondere Angebote oder Nachrichten zukommen lassen, um die Interaktion mit Ihrer Marke zu stärken.
1. **[!UICONTROL Lebenszeitwerte]: Das** Sammeln von Gesamtwerten, wie z. B. einem Kaufwert für einen Kunden, kann sehr schwierig sein. Dafür muss die historische Gesamtsumme bei jedem Auftreten eines neuen Kaufereignisses aktualisiert werden. Mit einem berechneten Attribut können Sie dies wesentlich einfacher tun, indem Sie den Lebenszeitwert in einem einzelnen Feld pflegen, das nach jedem erfolgreichen Kaufereignis, das mit dem Kunden verbunden ist, automatisch aktualisiert wird.

## Berechnetes Attribut konfigurieren

Um ein berechnetes Attribut zu konfigurieren, müssen Sie zunächst das Feld ermitteln, das den berechneten Attributwert enthält. Dieses Feld kann mit einem Mixin erstellt werden, um das Feld einem vorhandenen Schema hinzuzufügen, oder durch Auswahl eines Felds, das Sie bereits in einem Schema definiert haben.

>[!NOTE]
>
>Berechnete Attribute können keinen Feldern in Adobe-definierten Mixins hinzugefügt werden. Das Feld muss sich im `tenant`-Namespace befinden, d. h. es muss ein Feld sein, das Sie definieren und einem Schema hinzufügen.

Um ein berechnetes Attributfeld erfolgreich zu definieren, muss das Schema für [!DNL Profile] aktiviert sein und als Teil des Vereinigung-Schemas für die Klasse angezeigt werden, auf der das Schema basiert. Weitere Informationen zu [!DNL Profile]-aktivierten Schemas und Vereinigungen finden Sie im Abschnitt [!DNL Schema Registry] Entwicklerhandbuch unter [Aktivieren eines Schemas zum Profil und Anzeigen von Vereinigung-Schemas](../../xdm/api/getting-started.md). Außerdem empfehlen wir Ihnen, den [Abschnitt über Vereinigungen](../../xdm/schema/composition.md) in der Grundlagendokumentation zur Schemakomposition zu lesen.

Der Arbeitsablauf in diesem Lernprogramm verwendet ein [!DNL Profile]-aktiviertes Schema und führt die Schritte zum Definieren einer neuen Mischung mit dem berechneten Attributfeld und zum Sicherstellen des richtigen Namensraums durch. Wenn Sie bereits über ein Feld verfügen, das sich in einem Profil-aktivierten Schema im richtigen Namespace befindet, können Sie direkt mit dem [Erstellen eines berechneten Attributs](#create-a-computed-attribute) fortfahren.

### Schema anzeigen

In den folgenden Schritten nutzen Sie die Benutzeroberfläche von Adobe Experience Platform, um ein Schema zu suchen, ein Mixin hinzuzufügen und ein Feld zu definieren. Wenn Sie die [!DNL Schema Registry]-API bevorzugen, lesen Sie bitte das [Schema Registry-Entwicklerhandbuch](../../xdm/api/getting-started.md), um zu erfahren, wie Sie eine Mischung erstellen, eine Mischung zu einem Schema hinzufügen und ein Schema für die Verwendung mit [!DNL Real-time Customer Profile] aktivieren.

Klicken Sie in der Benutzeroberfläche in der linken Leiste auf **[!UICONTROL Schemas]** und nutzen Sie die Suchleiste auf dem Tab **[!UICONTROL Durchsuchen]**, um das Schema, das Sie aktualisieren möchten, zu suchen.

![](../images/computed-attributes/Schemas-Browse.png)

Nachdem Sie das Schema gefunden haben, klicken Sie auf seinen Namen, um das [!DNL Schema Editor] zu öffnen, in dem Sie Änderungen am Schema vornehmen können.

![](../images/computed-attributes/Schema-Editor.png)

### Erstellen eines Mixins

Um ein neues Mixin zu erstellen, klicken Sie im Abschnitt **[!UICONTROL Komposition]** auf der linken Seite des Editors neben **[!UICONTROL Mixins]** auf **[!UICONTROL Hinzufügen]**. Dadurch wird der Dialog **[!UICONTROL Mixin hinzufügen]** geöffnet, in dem vorhandene Mixins angezeigt werden. Klicken Sie auf das Optionsfeld für **[!UICONTROL Neues Mixin erstellen]**, um Ihr neues Mixin zu definieren.

Geben Sie dem Mixin einen Namen und eine Beschreibung und klicken Sie anschließend auf **[!UICONTROL Mixin hinzufügen]**.

![](../images/computed-attributes/Add-mixin.png)

### Berechnetes Attributfeld für das Schema hinzufügen

Ihr neues Mixin sollte nun im Abschnitt &quot;[!UICONTROL Mixins]&quot;unter &quot;[!UICONTROL Zusammensetzung]&quot;angezeigt werden. Klicken Sie auf den Namen des Mixins, woraufhin im Abschnitt **[!UICONTROL Struktur]** des Editors mehrere Schaltflächen vom Typ **[!UICONTROL Feld hinzufügen]** angezeigt werden.

Wählen Sie neben dem Namen des Schemas **[!UICONTROL Feld hinzufügen]**, um ein Feld der obersten Ebene hinzuzufügen. Alternativ können Sie das Feld an einer beliebigen Stelle im gewünschten Schema einfügen.

Nachdem Sie auf **[!UICONTROL Feld hinzufügen]** geklickt haben, wird ein neues Objekt mit dem Namen Ihrer Mandantenkennung geöffnet. Dies zeigt, dass sich das Feld im richtigen Namespace befindet. Innerhalb des Objekts wird ein **[!UICONTROL neues Feld]** angezeigt. Dies ist das Feld, in dem Sie das berechnete Attribut definieren werden.

![](../images/computed-attributes/New-field.png)

### Feld konfigurieren

Geben Sie im Abschnitt **[!UICONTROL Feldeigenschaften]** auf der rechten Seite des Editors die erforderlichen Daten für das neue Feld ein, einschließlich Name, Anzeigename und Typ.

>[!NOTE]
>
>Der Typ für das Feld muss mit dem Typ des berechneten Attributwerts übereinstimmen. Wenn der berechnete Attributwert beispielsweise eine Zeichenfolge ist, muss auch das im Schema definierte Feld eine Zeichenfolge sein.

Wenn Sie fertig sind, klicken Sie auf **[!UICONTROL Übernehmen]**. Daraufhin werden der Name des Felds sowie der Typ im Abschnitt **[!UICONTROL Struktur]** des Editors angezeigt.

![](../images/computed-attributes/Apply.png)

### Schema für [!DNL Profile] aktivieren

Bevor Sie fortfahren, stellen Sie sicher, dass das Schema für [!DNL Profile] aktiviert wurde. Klicken Sie im Bereich **[!UICONTROL Struktur]** des Editors auf den Namen des Schemas, um den Tab **[!UICONTROL Schemaeigenschaften]** anzuzeigen. Wenn der Schieberegler **[!UICONTROL Profil]** blau ist, wurde das Schema für [!DNL Profile] aktiviert.

>[!NOTE]
>
>Die Aktivierung eines Schemas für [!DNL Profile] kann nicht rückgängig gemacht werden. Wenn Sie also auf den Schieberegler klicken, müssen Sie nicht riskieren, es zu deaktivieren.

![](../images/computed-attributes/Profile.png)

Jetzt können Sie auf **[!UICONTROL Speichern]** klicken, um das aktualisierte Schema zu speichern und mit dem Rest des Tutorials unter Nutzung der API fortzufahren.

### Berechnetes Attribut erstellen {#create-a-computed-attribute}

Wenn Ihr berechnetes Attributfeld identifiziert und bestätigt wird, dass das Schema für [!DNL Profile] aktiviert ist, können Sie jetzt ein berechnetes Attribut konfigurieren.

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
| `expression.value` | Ein gültiger Ausdruck [!DNL Profile Query Language] (PQL). Weiterführende Informationen zu PQL und Links zu unterstützten Abfragen finden Sie in der [PQL-Übersicht](../../segmentation/pql/overview.md). |
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
| `{NEW_EXPRESSION_VALUE}` | Ein gültiger Ausdruck [!DNL Profile Query Language] (PQL). Weiterführende Informationen zu PQL und Links zu unterstützten Abfragen finden Sie in der [PQL-Übersicht](../../segmentation/pql/overview.md). |

**Antwort**

Bei erfolgreicher Aktualisierung werden der HTTP-Status 204 (Kein Inhalt) und ein leerer Antworttext zurückgegeben. Wenn Sie sich vergewissern möchten, dass die Aktualisierung erfolgreich war, können Sie eine GET-Anfrage ausführen, um das berechnete Attribut mit seiner Kennung anzuzeigen.

## Berechnetes Attribut löschen

Sie können ein berechnetes Attribut mithilfe der API auch löschen. Dies geschieht durch Richten einer DELETE-Anfrage an den `/config/computedAttributes`-Endpunkt und Einschließen der Kennung des berechneten Attributs, das Sie löschen möchten, in den Anfragepfad.

>[!NOTE]
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