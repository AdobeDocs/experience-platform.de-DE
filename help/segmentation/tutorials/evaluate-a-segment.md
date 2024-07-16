---
solution: Experience Platform
title: Segmentergebnisse auswerten und aufrufen
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie Segmentdefinitionen auswerten und mithilfe der Adobe Experience Platform Segmentation Service-API auf Segmentierungsergebnisse zugreifen können.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 15%

---

# Segmentdefinitionsergebnisse auswerten und aufrufen

Dieses Dokument bietet ein Tutorial zum Auswerten von Segmentdefinitionen und zum Zugriff auf diese Ergebnisse mithilfe von [[!DNL Segmentation API]](../api/getting-started.md).

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste voraus, die am Erstellen von Zielgruppen beteiligt sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht Ihnen das Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile] -Daten.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

### Erforderliche Kopfzeilen

Für dieses Tutorial müssen Sie außerdem das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, damit Sie erfolgreich Aufrufe an [!DNL Platform] -APIs durchführen können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Für Anfragen an [!DNL Platform] -APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anfragen ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

## Segmentdefinition bewerten {#evaluate-a-segment}

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie die Segmentdefinition entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung bewerten.

Mit der Funktion [Geplante Auswertung](#scheduled-evaluation) (auch als &quot;geplante Segmentierung&quot;bezeichnet) können Sie einen wiederkehrenden Zeitplan für die Ausführung eines Exportauftrags zu einem bestimmten Zeitpunkt erstellen, während bei der [On-Demand-Auswertung](#on-demand-evaluation) ein Segmentauftrag erstellt werden muss, um die Zielgruppe sofort zu erstellen. Die Schritte für die einzelnen Schritte sind unten beschrieben.

Wenn Sie das Tutorial [Erstellen einer Segmentdefinition mithilfe der Segmentation API](./create-a-segment.md) noch nicht abgeschlossen haben oder eine Segmentdefinition mithilfe von [Segment Builder](../ui/segment-builder.md) erstellt haben, führen Sie dies vor dem Fortfahren mit diesem Tutorial durch.

## Geplante Auswertung {#scheduled-evaluation}

Durch die geplante Auswertung kann Ihr Unternehmen einen Zeitplan für die automatische Ausführung von Exportvorgängen erstellen.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihre Organisation in einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anfrage an den `/config/schedules`-Endpunkt senden, können Sie einen Zeitplan erstellen und die genaue Zeit einschließen, zu der der Zeitplan ausgelöst werden soll.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#create) .

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#update-state) .

### Zeitplanaktualisierung

Der Zeitplan-Timing kann aktualisiert werden, indem eine PATCH-Anfrage an den `/config/schedules` -Endpunkt gesendet wird und die Kennung des Zeitplans in den Pfad aufgenommen wird.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Zeitpläne](../api/schedules.md#update-schedule) .

## On-Demand-Evaluierung

Mit der On-Demand-Auswertung können Sie einen Segmentauftrag erstellen, um bei Bedarf eine Zielgruppe zu generieren. Im Gegensatz zur geplanten Auswertung erfolgt dies nur bei Anforderung und nicht wiederholt.

### Erstellen eines Segmentauftrags

Ein Segmentauftrag ist ein asynchroner Prozess, der ein Zielgruppensegment bei Bedarf erstellt. Er verweist auf eine Segmentdefinition sowie auf alle Zusammenführungsrichtlinien, die steuern, wie [!DNL Real-Time Customer Profile] überlappende Attribute über Ihre Profilfragmente hinweg zusammenführt. Nach erfolgreichem Abschluss eines Segmentauftrags können Sie verschiedene Informationen zur Segmentdefinition sammeln, z. B. Fehler, die während der Verarbeitung aufgetreten sind, und die endgültige Größe Ihrer Zielgruppe. Ein Segmentauftrag muss jedes Mal ausgeführt werden, wenn Sie die Zielgruppe aktualisieren möchten, für die sich die Segmentdefinition derzeit qualifiziert.

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST-Anfrage an den `/segment/jobs` -Endpunkt in der [!DNL Real-Time Customer Profile] -API richten.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Segmentaufträge](../api/segment-jobs.md#create) .

### Status des Segmentauftrags nachschlagen

Sie können die `id` für einen bestimmten Segmentauftrag verwenden, um eine Suchanfrage (GET) auszuführen, um den aktuellen Status des Auftrags anzuzeigen.

Weitere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunktleitfaden für Segmentaufträge](../api/segment-jobs.md#get) .

## Interpretieren von Segmentauftragsergebnissen

Wenn Segmentaufträge erfolgreich ausgeführt werden, wird die `segmentMembership`-Zuordnung für jedes Profil aktualisiert, das in der Segmentdefinition enthalten ist. `segmentMembership` speichert auch alle vorab ausgewerteten Zielgruppen, die in [!DNL Platform] erfasst werden, sodass sie mit anderen Lösungen wie [!DNL Adobe Audience Manager] integriert werden können.

Das folgende Beispiel zeigt, wie das Attribut `segmentMembership` für jeden einzelnen Profildatensatz aussieht:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "realized"
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
| `lastQualificationTime` | Der Zeitstempel, zu dem die Bestätigung der Segmentzugehörigkeit erfolgte und das Profil die Segmentdefinition ein- oder ausstieg. |
| `status` | Der Teilnahmestatus der Segmentdefinition als Teil der aktuellen Anfrage. Muss einem der folgenden bekannten Werte entsprechen: <ul><li>`realized`: Die Entität ist für die Segmentdefinition qualifiziert.</li><li>`exited`: Die Entität beendet die Segmentdefinition.</li></ul> |

>[!NOTE]
>
>Jede Segmentzugehörigkeit, die sich basierend auf dem `lastQualificationTime` länger als 30 Tage im Status `exited` befindet, kann gelöscht werden.

## Auf Segmentauftragsergebnisse zugreifen

Auf die Ergebnisse eines Segmentauftrags kann auf zwei Arten zugegriffen werden: Sie können auf einzelne Profile zugreifen oder eine gesamte Zielgruppe in einen Datensatz exportieren.

In den folgenden Abschnitten werden diese Optionen ausführlicher beschrieben.

## Profil nachschlagen

Wenn Sie das spezifische Profil kennen, auf das Sie zugreifen möchten, können Sie dies mit der [!DNL Real-Time Customer Profile] -API tun. Die vollständigen Schritte zum Zugriff auf einzelne Profile finden Sie im Tutorial [Zugriff auf Echtzeit-Kundenprofil-Daten mithilfe der Profil-API](../../profile/api/entities.md) .

## Segment exportieren {#export}

Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der Wert des Attributs `status` lautet &quot;SUCCEEDED&quot;(GELUNGEN)), können Sie Ihre Zielgruppe in einen Datensatz exportieren, in dem sie aufgerufen und bearbeitet werden kann.

Die folgenden Schritte sind erforderlich, um Ihre Audience zu exportieren:

- [Erstellen eines Zieldatensatzes](#create-a-target-dataset) - Erstellen Sie den Datensatz, in dem Zielgruppenmitglieder gespeichert werden sollen.
- [Generieren von Zielgruppenprofilen im Datensatz](#generate-profiles) - Füllen Sie den Datensatz mit individuellen XDM-Profilen basierend auf den Ergebnissen eines Segmentauftrags.
- [Überwachen des Exportfortschritts](#monitor-export-progress) - Überprüfen Sie den aktuellen Fortschritt des Exportvorgangs.
- [Lesen von Zielgruppendaten](#next-steps) - Rufen Sie die resultierenden individuellen XDM-Profile ab, die die Mitglieder Ihrer Zielgruppe darstellen.

### Erstellen eines Zieldatensatzes {#create-dataset}

Beim Exportieren einer Zielgruppe muss zunächst ein Zieldatensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert ist, um sicherzustellen, dass der Export erfolgreich ist.

Eine der wichtigsten Überlegungen ist das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Beispielanfrage). Um eine Segmentdefinition zu exportieren, muss der Datensatz auf dem [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas aggregiert, die dieselbe Klasse teilen, in diesem Fall die Klasse &quot;XDM Individual Profile&quot;. Weitere Informationen zu Vereinigungsansichtsschemas finden Sie im Abschnitt [Echtzeit-Kundenprofil des Entwicklerhandbuchs zur Schema Registry](../../xdm/api/getting-started.md).

Es gibt zwei Möglichkeiten, den erforderlichen Datensatz zu erstellen:

- **Verwenden von APIs:** In den in diesem Tutorial beschriebenen Schritten wird beschrieben, wie Sie einen Datensatz erstellen, der mithilfe der [!DNL Catalog] -API auf [!DNL XDM Individual Profile Union Schema] verweist.
- **Verwenden der Benutzeroberfläche:** Um mithilfe der Benutzeroberfläche von [!DNL Adobe Experience Platform] einen Datensatz zu erstellen, der auf das Vereinigungsschema verweist, führen Sie die Schritte im Tutorial [UI-Tutorial](../ui/overview.md) aus und kehren Sie dann zu diesem Tutorial zurück, um mit den Schritten zum Generieren von Zielgruppenprofilen [fortzufahren.](#generate-profiles)

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen Kennung kennen, können Sie direkt mit dem Schritt zum Generieren von [Zielgruppenprofilen](#generate-profiles) fortfahren.

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

Sobald Sie über einen Datensatz verfügen, der Vereinigungspersistenz speichert, können Sie einen Exportauftrag erstellen, um die Zielgruppenmitglieder im Datensatz zu behalten, indem Sie eine POST-Anfrage an den `/export/jobs` -Endpunkt in der [!DNL Real-Time Customer Profile] -API richten und die Datensatz-ID sowie die Segmentdefinitionsinformationen für die Segmentdefinitionen angeben, die Sie exportieren möchten.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkthandbuch zu Exportvorgängen](../api/export-jobs.md#create) .

### Fortschritt des Exports überwachen

Bei der Verarbeitung eines Exportauftrags können Sie dessen Status überwachen, indem Sie eine GET-Anfrage an den `/export/jobs` -Endpunkt senden und die `id` des Exportauftrags in den Pfad einschließen. Der Exportauftrag ist abgeschlossen, sobald das Feld `status` den Wert &quot;SUCCEEDED&quot;zurückgibt.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Endpunkthandbuch zu Exportvorgängen](../api/export-jobs.md#get) .

## Nächste Schritte

Nach erfolgreichem Abschluss des Exports sind Ihre Daten im Bereich [!DNL Data Lake] in [!DNL Experience Platform] verfügbar. Anschließend können Sie mit dem [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) auf die Daten zugreifen, indem Sie den mit dem Export verknüpften `batchId` verwenden. Je nach Größe der Segmentdefinition können die Daten in Blöcken vorliegen und der Batch kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Verwenden der [!DNL Data Access]-API für den Zugriff auf und den Download von Batch-Dateien finden Sie im [Tutorial zum Datenzugriff](../../data-access/tutorials/dataset-data.md) .

Sie können auch mit [!DNL Adobe Experience Platform Query Service] auf erfolgreich exportierte Segmentdefinitionsdaten zugreifen. Mithilfe der Benutzeroberfläche oder der RESTful-API können Sie mit [!DNL Query Service] Abfragen zu Daten innerhalb des [!DNL Data Lake] schreiben, validieren und ausführen.

Weitere Informationen zum Abfragen von Zielgruppendaten finden Sie in der Dokumentation zu [[!DNL Query Service]](../../query-service/home.md).
