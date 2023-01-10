---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentauswertung; Segmentierungsdienst; Segmentierung; Segmentierung; Segmentierung; Segmentergebnisse auswerten; Segmentergebnisse auswerten und aufrufen;
solution: Experience Platform
title: Segmentergebnisse auswerten und aufrufen
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie mithilfe der Adobe Experience Platform Segmentation Service-API Segmente auswerten und auf Segmentergebnisse zugreifen.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 20%

---

# Segmentergebnisse auswerten und aufrufen

Dieses Dokument bietet eine Anleitung zum Auswerten von Segmenten und Zugreifen auf Segmentergebnisse mithilfe der [[!DNL Segmentation API]](../api/getting-started.md).

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die an der Erstellung von Zielgruppensegmenten beteiligt sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht das Erstellen von Zielgruppensegmenten aus [!DNL Real-Time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten ordnet. Um die Segmentierung optimal zu nutzen, stellen Sie bitte sicher, dass Ihre Daten als Profile und Ereignisse gemäß dem [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md).
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

### Erforderliche Kopfzeilen

Für dieses Tutorial müssen Sie außerdem die [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) , um erfolgreich Aufrufe an [!DNL Platform] APIs. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anforderungen an [!DNL Platform] APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anfragen ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Bewerten eines Segments {#evaluate-a-segment}

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten.

[Geplante Auswertung](#scheduled-evaluation) (auch als &quot;geplante Segmentierung&quot;bezeichnet) ermöglicht Ihnen die Erstellung eines wiederkehrenden Zeitplans für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt, während [On-Demand-Evaluierung](#on-demand-evaluation) umfasst die Erstellung eines Segmentauftrags, um die Zielgruppe sofort zu erstellen. Die Schritte für die einzelnen Schritte sind unten beschrieben.

Wenn Sie die [Erstellen eines Segments mithilfe der Segmentation-API](./create-a-segment.md) Tutorial oder Erstellen einer Segmentdefinition mithilfe von [Segment Builder](../ui/overview.md)sollten Sie dies tun, bevor Sie mit diesem Tutorial fortfahren.

## Geplante Auswertung {#scheduled-evaluation}

Durch die geplante Auswertung kann Ihre IMS-Organisation einen wiederkehrenden Zeitplan erstellen, um Exportaufträge automatisch auszuführen.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihre Organisation in einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anfrage an den `/config/schedules`-Endpunkt senden, können Sie einen Zeitplan erstellen und die genaue Zeit einschließen, zu der der Zeitplan ausgelöst werden soll.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Zeitpläne](../api/schedules.md#create)

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Zeitpläne](../api/schedules.md#update-state)

### Zeitplanaktualisierung

Der Zeitplan kann aktualisiert werden, indem eine PATCH-Anfrage an die `/config/schedules` -Endpunkt und die Kennung des Zeitplans in den Pfad einschließen.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Zeitpläne](../api/schedules.md#update-schedule)

## On-Demand-Evaluierung

Mit der On-Demand-Auswertung können Sie einen Segmentauftrag erstellen, um bei Bedarf ein Zielgruppensegment zu generieren. Im Gegensatz zur geplanten Auswertung erfolgt dies nur bei Anforderung und nicht wiederholt.

### Erstellen eines Segmentauftrags

Ein Segmentauftrag ist ein asynchroner Prozess, der ein Zielgruppensegment bei Bedarf erstellt. Er verweist auf eine Segmentdefinition sowie auf alle Zusammenführungsrichtlinien, die steuern, wie [!DNL Real-Time Customer Profile] Führt überlappende Attribute über Ihre Profilfragmente hinweg zusammen. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen über das Segment sammeln, z. B. Fehler, die bei der Verarbeitung aufgetreten sind, oder die endgültige Größe Ihrer Zielgruppe. Ein Segmentauftrag muss jedes Mal ausgeführt werden, wenn Sie die Zielgruppe aktualisieren möchten, die sich derzeit für die Segmentdefinition qualifiziert.

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST-Anfrage an die `/segment/jobs` -Endpunkt im [!DNL Real-Time Customer Profile] API.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Segmentaufträge](../api/segment-jobs.md#create)

### Status des Segmentauftrags nachschlagen

Sie können die `id` für einen bestimmten Segmentauftrag, um eine Nachschlageanfrage (GET) auszuführen, um den aktuellen Status des Auftrags anzuzeigen.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Segmentaufträge](../api/segment-jobs.md#get)

## Interpretieren von Segmentergebnissen

Wenn Segmentaufträge erfolgreich ausgeführt werden, wird die `segmentMembership` map wird für jedes Profil aktualisiert, das im Segment enthalten ist. `segmentMembership` speichert auch alle vorab ausgewerteten Zielgruppensegmente, die in [!DNL Platform], wodurch eine Integration mit anderen Lösungen wie [!DNL Adobe Audience Manager].

Das folgende Beispiel zeigt, was die `segmentMembership` -Attribut für jeden einzelnen Profildatensatz aussieht:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `lastQualificationTime` | Der Zeitstempel, zu dem die Bestätigung der Segmentzugehörigkeit erfolgte und das Profil in das Segment eintrat oder es verließ. |
| `status` | Der Status der Segmentbeteiligung als Teil der aktuellen Anfrage. Muss einem der folgenden bekannten Werte entsprechen: <ul><li>`existing`: Die Entität befindet sich weiterhin im Segment.</li><li>`realized`: Entität gibt das Segment ein.</li><li>`exited`: Entität beendet das Segment.</li></ul> |

## Auf Segmentergebnisse zugreifen

Auf die Ergebnisse eines Segmentauftrags kann auf zwei Arten zugegriffen werden: Sie können auf einzelne Profile zugreifen oder eine gesamte Zielgruppe in einen Datensatz exportieren.

In den folgenden Abschnitten werden diese Optionen ausführlicher beschrieben.

## Profil nachschlagen

Wenn Sie das spezifische Profil kennen, auf das Sie zugreifen möchten, können Sie dies mit der [!DNL Real-Time Customer Profile] API. Die vollständigen Schritte für den Zugriff auf einzelne Profile finden Sie im Abschnitt [Zugriff auf Echtzeit-Kundenprofil-Daten mithilfe der Profil-API](../../profile/api/entities.md) Tutorial.

## Segment exportieren {#export}

Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der Wert des `status`-Attributs lautet „SUCCEEDED“ (GELUNGEN)), können Sie Ihre Zielgruppe in einen Datensatz exportieren. In diesem Datensatz ist die Zielgruppe zugänglich und bearbeitbar.

Die folgenden Schritte sind erforderlich, um Ihre Audience zu exportieren:

- [Zieldatensatz erstellen](#create-a-target-dataset) - Erstellen Sie den Datensatz, um Mitglieder der Zielgruppe aufzunehmen.
- [Generieren von Zielgruppenprofilen im Datensatz](#generate-profiles) - Füllen Sie den Datensatz mit individuellen XDM-Profilen basierend auf den Ergebnissen eines Segmentauftrags.
- [Fortschritt des Exports überwachen](#monitor-export-progress) - Überprüfen Sie den aktuellen Fortschritt des Exportvorgangs.
- [Audience-Daten lesen](#next-steps) - Rufen Sie die resultierenden individuellen XDM-Profile ab, die die Mitglieder Ihrer Audience darstellen.

### Erstellen eines Zieldatensatzes {#create-dataset}

Beim Exportieren einer Zielgruppe muss zunächst ein Zieldatensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert ist, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der API-Beispielanfrage unten). Um ein Segment zu exportieren, muss der Datensatz auf der [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`). Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas aggregiert, die dieselbe Klasse teilen, in diesem Fall die Klasse &quot;XDM Individual Profile&quot;. Weitere Informationen zu Vereinigungsansichtsschemas finden Sie im [Abschnitt &quot;Echtzeit-Kundenprofil&quot;des Entwicklerhandbuchs zur Schema Registry](../../xdm/api/getting-started.md).

Es gibt zwei Möglichkeiten, den erforderlichen Datensatz zu erstellen:

- **Verwenden von APIs:** In den in diesem Tutorial beschriebenen Schritten wird beschrieben, wie Sie einen Datensatz erstellen, der auf die [!DNL XDM Individual Profile Union Schema] mithilfe der [!DNL Catalog] API.
- **Verwenden der Benutzeroberfläche:** So verwenden Sie die [!DNL Adobe Experience Platform] -Benutzeroberfläche zum Erstellen eines Datensatzes, der auf das Vereinigungsschema verweist, führen Sie die Schritte im Abschnitt [UI-Tutorial](../ui/overview.md) und dann zu diesem Tutorial zurückkehren, um mit den Schritten für [Erstellen von Zielgruppenprofilen](#generate-profiles).

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen Kennung kennen, können Sie direkt mit dem Schritt für [Erstellen von Zielgruppenprofilen](#generate-profiles).

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Datensatz und stellt Konfigurationsparameter in der Payload bereit.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    }
}'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `name` | Ein beschreibender Name für den Datensatz. |
| `schemaRef.id` | Die ID der Vereinigungsansicht (Schema), mit der der Datensatz verknüpft wird. |

**Antwort**

Eine erfolgreiche Antwort gibt ein Array zurück, das die schreibgeschützte, systemgenerierte eindeutige ID des neu erstellten Datensatzes enthält. Eine ordnungsgemäß konfigurierte Datensatz-ID ist erforderlich, um Audience-Mitglieder erfolgreich zu exportieren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generieren von Profilen für Zielgruppenmitglieder {#generate-profiles}

Sobald Sie über einen Datensatz verfügen, der die Vereinigung beibehält, können Sie einen Exportauftrag erstellen, um die Mitglieder der Zielgruppe im Datensatz zu erhalten, indem Sie eine POST-Anfrage an die `/export/jobs` -Endpunkt im [!DNL Real-Time Customer Profile] API und die Angabe der Datensatz-ID und der Segmentinformationen für die Segmente, die Sie exportieren möchten.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Exportaufträge](../api/export-jobs.md#create)

### Fortschritt des Exports überwachen

Bei Exportvorgängen können Sie den Status überwachen, indem Sie eine GET-Anfrage an die `/export/jobs` Endpunkt und einschließlich `id` des Exportauftrags im Pfad. Der Exportvorgang ist abgeschlossen, sobald die `status` gibt den Wert &quot;SUCCEEDED&quot;zurück.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im Abschnitt [Endpunktleitfaden für Exportaufträge](../api/export-jobs.md#get)

## Nächste Schritte

Sobald der Export erfolgreich abgeschlossen wurde, stehen Ihre Daten im [!DNL Data Lake] in [!DNL Experience Platform]. Anschließend können Sie die [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) , um mithilfe der `batchId` mit dem Export verknüpft ist. Je nach Größe des Segments können die Daten in Blöcken vorliegen und der Batch kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zur Verwendung der [!DNL Data Access] API zum Zugreifen auf und Herunterladen von Batch-Dateien, folgen Sie dem [Tutorial zum Datenzugriff](../../data-access/tutorials/dataset-data.md).

Sie können auch auf erfolgreich exportierte Segmentdaten zugreifen, indem Sie [!DNL Adobe Experience Platform Query Service]. Verwenden der Benutzeroberfläche oder der RESTful-API, [!DNL Query Service] ermöglicht Ihnen das Schreiben, Validieren und Ausführen von Abfragen zu Daten im [!DNL Data Lake].

Weiterführende Informationen zur Abfrage von Zielgruppendaten finden Sie in der Dokumentation unter [[!DNL Query Service]](../../query-service/home.md).
