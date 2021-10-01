---
keywords: Experience Platform; Startseite; beliebte Themen; Segmentauswertung; Segmentierungsdienst; Segmentierung; Segmentierung; Segmentierung; Segmentergebnisse auswerten; Segmentergebnisse auswerten und aufrufen;
solution: Experience Platform
title: Segmentergebnisse auswerten und aufrufen
topic-legacy: tutorial
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie mithilfe der Adobe Experience Platform Segmentation Service-API Segmente auswerten und auf Segmentergebnisse zugreifen.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 18%

---

# Segmentergebnisse auswerten und aufrufen

Dieses Dokument bietet eine Anleitung zum Auswerten von Segmenten und Aufrufen von Segmentergebnissen mithilfe von [[!DNL Segmentation API]](../api/getting-started.md).

## Erste Schritte

Dieses Tutorial setzt ein grundlegendes Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste voraus, die am Erstellen von Zielgruppensegmenten beteiligt sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht das Erstellen von Zielgruppensegmenten anhand von  [!DNL Real-time Customer Profile] Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Kopfzeilen

Für dieses Tutorial müssen Sie außerdem das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abgeschlossen haben, damit Sie erfolgreich Aufrufe an [!DNL Platform]-APIs durchführen können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anforderungen an [!DNL Platform]-APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anfragen ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Bewerten eines Segments

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie das Segment entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten.

[Die geplante Auswertung](#scheduled-evaluation)  (auch als &quot;geplante Segmentierung&quot;bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt zu erstellen, während bei der  [On-Demand-](#on-demand-evaluation) Auswertung ein Segmentauftrag erstellt werden muss, um die Zielgruppe sofort zu erstellen. Die Schritte für die einzelnen Schritte sind unten beschrieben.

Wenn Sie das Tutorial [Erstellen eines Segments mithilfe der Segmentation API](./create-a-segment.md) noch nicht abgeschlossen haben oder eine Segmentdefinition mit [Segment Builder](../ui/overview.md) erstellt haben, führen Sie dies vor dem Fortfahren mit diesem Tutorial durch.

## Geplante Auswertung {#scheduled-evaluation}

Durch die geplante Auswertung kann Ihre IMS-Organisation einen wiederkehrenden Zeitplan erstellen, um Exportaufträge automatisch auszuführen.

>[!NOTE]
>
>Geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihr Unternehmen innerhalb einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anfrage an den `/config/schedules`-Endpunkt senden, können Sie einen Zeitplan erstellen und die genaue Zeit einschließen, zu der der Zeitplan ausgelöst werden soll.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#create) .

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#update-state) .

### Zeitplanaktualisierung

Der Zeitplan-Timing kann aktualisiert werden, indem eine PATCH-Anfrage an den Endpunkt `/config/schedules` gesendet wird und die Kennung des Zeitplans in den Pfad aufgenommen wird.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#update-schedule) .

## On-Demand-Evaluierung

Mit der On-Demand-Auswertung können Sie einen Segmentauftrag erstellen, um bei Bedarf ein Zielgruppensegment zu generieren. Im Gegensatz zur geplanten Auswertung erfolgt dies nur bei Anforderung und nicht wiederholt.

### Erstellen eines Segmentauftrags

Ein Segmentauftrag ist ein asynchroner Vorgang, bei dem ein neues Zielgruppensegment erstellt wird. Er verweist auf eine Segmentdefinition sowie auf alle Zusammenführungsrichtlinien, die steuern, wie [!DNL Real-time Customer Profile] überlappende Attribute über Ihre Profilfragmente hinweg zusammenführt. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen über das Segment sammeln, z. B. Fehler, die bei der Verarbeitung aufgetreten sind, oder die endgültige Größe Ihrer Zielgruppe.

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST-Anfrage an den Endpunkt `/segment/jobs` in der API [!DNL Real-time Customer Profile] stellen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Segmentaufträge](../api/segment-jobs.md#create) .


### Status des Segmentauftrags nachschlagen

Sie können den `id` für einen bestimmten Segmentauftrag verwenden, um eine Suchanfrage (GET) auszuführen, um den aktuellen Status des Auftrags anzuzeigen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Segmentaufträge](../api/segment-jobs.md#get) .

## Interpretieren von Segmentergebnissen

Wenn Segmentaufträge erfolgreich ausgeführt werden, wird die Zuordnung `segmentMembership` für jedes Profil aktualisiert, das im Segment enthalten ist. `segmentMembership` speichert auch alle vorab ausgewerteten Zielgruppensegmente, die in aufgenommen werden,  [!DNL Platform]sodass sie mit anderen Lösungen wie  [!DNL Adobe Audience Manager] integriert werden können.

Das folgende Beispiel zeigt, wie das `segmentMembership`-Attribut für jeden einzelnen Profildatensatz aussieht:

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

Wenn Sie das spezifische Profil kennen, auf das Sie zugreifen möchten, können Sie dies mit der API [!DNL Real-time Customer Profile] tun. Die vollständigen Schritte zum Zugriff auf einzelne Profile finden Sie im Tutorial [Zugriff auf Echtzeit-Kundenprofil-Daten mithilfe der Profil-API](../../profile/api/entities.md) .

## Segment exportieren {#export}

Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der Wert des `status`-Attributs lautet „SUCCEEDED“ (GELUNGEN)), können Sie Ihre Zielgruppe in einen Datensatz exportieren. In diesem Datensatz ist die Zielgruppe zugänglich und bearbeitbar.

Die folgenden Schritte sind erforderlich, um Ihre Audience zu exportieren:

- [Erstellen eines Zieldatensatzes](#create-a-target-dataset)  - Erstellen Sie den Datensatz, um Zielgruppenmitglieder zu enthalten.
- [Generieren von Zielgruppenprofilen im Datensatz](#generate-profiles-for-audience-members)  - Füllen Sie den Datensatz mit individuellen XDM-Profilen basierend auf den Ergebnissen eines Segmentauftrags.
- [Überwachen des Exportfortschritts](#monitor-export-progress)  - Überprüfen Sie den aktuellen Fortschritt des Exportvorgangs.
- [Lesen von Zielgruppendaten](#next-steps)  - Rufen Sie die resultierenden individuellen XDM-Profile ab, die die Mitglieder Ihrer Zielgruppe darstellen.

### Zieldatensatz erstellen

Beim Exportieren einer Zielgruppe muss zunächst ein Zieldatensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert ist, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Beispielanfrage). Um ein Segment zu exportieren, muss der Datensatz auf dem [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas aggregiert, die dieselbe Klasse teilen, in diesem Fall die Klasse &quot;XDM Individual Profile&quot;. Weitere Informationen zu Vereinigungsansichtsschemas finden Sie im Abschnitt [Echtzeit-Kundenprofil des Entwicklerhandbuchs zur Schema Registry](../../xdm/api/getting-started.md).

Es gibt zwei Möglichkeiten, den erforderlichen Datensatz zu erstellen:

- **Verwenden von APIs:** In den in diesem Tutorial beschriebenen Schritten wird beschrieben, wie Sie einen Datensatz erstellen, der auf die  [!DNL XDM Individual Profile Union Schema] mithilfe der  [!DNL Catalog] API verweist.
- **Verwenden der Benutzeroberfläche:** Um mithilfe der  [!DNL Adobe Experience Platform] Benutzeroberfläche einen Datensatz zu erstellen, der auf das Vereinigungsschema verweist, führen Sie die Schritte im  [UI-](../ui/overview.md) Tutorial aus und kehren Sie dann zu diesem Tutorial zurück, um mit den Schritten zum  [Generieren von Zielgruppenprofilen](#generate-xdm-profiles-for-audience-members) fortzufahren.

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen Kennung kennen, können Sie direkt mit dem Schritt zum Generieren von Zielgruppenprofilen](#generate-xdm-profiles-for-audience-members) fortfahren.[

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

Sobald Sie über einen Datensatz mit Vereinigungspersistenz verfügen, können Sie einen Exportauftrag erstellen, um die Mitglieder der Zielgruppe im Datensatz zu erhalten, indem Sie eine POST-Anfrage an den Endpunkt `/export/jobs` in der API [!DNL Real-time Customer Profile] senden und die Datensatz-ID sowie die Segmentinformationen für die Segmente angeben, die exportiert werden sollen.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Exportaufträge](../api/export-jobs.md#create) .

### Fortschritt des Exports überwachen

Bei Exportvorgängen können Sie den Status überwachen, indem Sie eine GET-Anfrage an den Endpunkt `/export/jobs` senden und die `id` des Exportauftrags in den Pfad einschließen. Der Exportauftrag ist abgeschlossen, sobald das Feld `status` den Wert &quot;SUCCEEDED&quot;zurückgibt.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Exportaufträge](../api/export-jobs.md#get) .

## Nächste Schritte

Nach erfolgreichem Abschluss des Exports sind Ihre Daten im Ordner [!DNL Data Lake] in [!DNL Experience Platform] verfügbar. Sie können dann [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) verwenden, um mit dem mit dem Export verknüpften `batchId` auf die Daten zuzugreifen. Je nach Größe des Segments können die Daten in Blöcken vorliegen und der Batch kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Verwenden der [!DNL Data Access]-API für den Zugriff auf und den Download von Batch-Dateien finden Sie im [Tutorial zum Datenzugriff](../../data-access/tutorials/dataset-data.md).

Sie können auch mit [!DNL Adobe Experience Platform Query Service] auf erfolgreich exportierte Segmentdaten zugreifen. Mithilfe der Benutzeroberfläche oder der RESTful-API können Sie mit [!DNL Query Service] Abfragen zu Daten in [!DNL Data Lake] schreiben, validieren und ausführen.

Weiterführende Informationen zur Abfrage von Zielgruppendaten finden Sie in der Dokumentation zu [[!DNL Query Service]](../../query-service/home.md).
