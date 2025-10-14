---
solution: Experience Platform
title: Auswerten und Zugreifen auf Segmentergebnisse
type: Tutorial
description: In diesem Tutorial erfahren Sie, wie Sie Segmentdefinitionen auswerten und mithilfe der Segmentierungs-Service-API von Adobe Experience Platform auf Segmentierungsergebnisse zugreifen können.
exl-id: 47702819-f5f8-49a8-a35d-034ecac4dd98
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1594'
ht-degree: 15%

---

# Auswerten und Zugreifen auf Ergebnisse der Segmentdefinition

Dieses Dokument enthält ein Tutorial zum Auswerten von Segmentdefinitionen und zum Zugriff auf diese Ergebnisse mithilfe der [[!DNL Segmentation API]](../api/getting-started.md).

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der verschiedenen [!DNL Adobe Experience Platform]-Services voraus, die bei der Erstellung von Zielgruppen zum Einsatz kommen. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Ermöglicht das Erstellen von Zielgruppen aus [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von Platform organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.
- [Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Experience Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln können.

### Erforderliche Kopfzeilen

Für dieses Tutorial müssen Sie auch das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abgeschlossen haben, um [!DNL Experience Platform] APIs erfolgreich aufrufen zu können. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Anfragen an [!DNL Experience Platform]-APIs erfordern eine Kopfzeile, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle POST-, PUT- und PATCH-Anfragen ist eine zusätzliche -Kopfzeile erforderlich:

- Content-Type: application/json

## Auswerten einer Segmentdefinition {#evaluate-a-segment}

Nachdem Sie Ihre Segmentdefinition entwickelt, getestet und gespeichert haben, können Sie die Segmentdefinition entweder durch eine geplante Auswertung oder eine On-Demand-Auswertung auswerten.

[Geplante Auswertung](#scheduled-evaluation) (auch als „geplante Segmentierung“ bezeichnet) ermöglicht es Ihnen, einen wiederkehrenden Zeitplan für die Ausführung eines Exportvorgangs zu einem bestimmten Zeitpunkt zu erstellen, während [On-Demand-](#on-demand-evaluation) die Erstellung eines Segmentvorgangs umfasst, um die Zielgruppe sofort zu erstellen. Die einzelnen Schritte sind unten beschrieben.

Wenn Sie das Tutorial [Erstellen einer Segmentdefinition mit der Segmentierungs-API](./create-a-segment.md) noch nicht abgeschlossen haben oder eine Segmentdefinition mit [Segment Builder](../ui/segment-builder.md) erstellt haben, tun Sie dies, bevor Sie mit diesem Tutorial fortfahren.

## Geplante Auswertung {#scheduled-evaluation}

Durch eine geplante Auswertung kann Ihr Unternehmen einen wiederkehrenden Zeitplan erstellen, um Exportaufträge automatisch auszuführen.

>[!NOTE]
>
>Die geplante Auswertung kann für Sandboxes mit maximal fünf (5) Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] aktiviert werden. Wenn Ihre Organisation in einer Sandbox-Umgebung über mehr als fünf Zusammenführungsrichtlinien für [!DNL XDM Individual Profile] verfügt, können Sie keine geplante Auswertung verwenden.

### Zeitplan erstellen

Wenn Sie eine POST-Anfrage an den `/config/schedules`-Endpunkt senden, können Sie einen Zeitplan erstellen und die genaue Zeit einschließen, zu der der Zeitplan ausgelöst werden soll.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Endpunkten für Zeitpläne](../api/schedules.md#create)

### Zeitplan aktivieren

Standardmäßig ist ein Zeitplan bei der Erstellung inaktiv, es sei denn, die `state`-Eigenschaft ist im Text der POST-Anfrage (Erstellen) auf `active` gesetzt. Sie können einen Zeitplan aktivieren (setzen Sie `state` auf `active`), indem Sie eine PATCH-Anfrage an den `/config/schedules`-Endpunkt senden und die Kennung des Zeitplans in den Pfad einschließen.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Endpunkten für Zeitpläne](../api/schedules.md#update-state)

### Zeitplandauer aktualisieren

Die Zeitplanung kann aktualisiert werden, indem eine PATCH-Anfrage an den `/config/schedules`-Endpunkt gesendet und die Kennung des Zeitplans in den Pfad aufgenommen wird.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Endpunkten für Zeitpläne](../api/schedules.md#update-schedule)

## On-Demand-Evaluierung

Mit der On-Demand-Auswertung können Sie einen Segmentauftrag erstellen, um bei Bedarf eine Zielgruppe zu generieren. Im Gegensatz zur geplanten Auswertung erfolgt dies nur auf Anfrage und nicht wiederkehrend.

### Erstellen eines Segmentauftrags

Ein Segmentauftrag ist ein asynchroner Prozess, der bei Bedarf ein Zielgruppensegment erstellt. Es verweist auf eine Segmentdefinition sowie auf alle Zusammenführungsrichtlinien, die steuern, wie [!DNL Real-Time Customer Profile] überlappende Attribute über Ihre Profilfragmente hinweg zusammenführt. Wenn ein Segmentauftrag erfolgreich abgeschlossen wurde, können Sie verschiedene Informationen zur Segmentdefinition erfassen, z. B. alle Fehler, die während der Verarbeitung aufgetreten sind, und die endgültige Größe Ihrer Zielgruppe. Ein Segmentauftrag muss jedes Mal ausgeführt werden, wenn Sie die Zielgruppe aktualisieren möchten, für die die Segmentdefinition derzeit qualifiziert ist.

Sie können einen neuen Segmentauftrag erstellen, indem Sie eine POST-Anfrage an den `/segment/jobs`-Endpunkt in der [!DNL Real-Time Customer Profile]-API stellen.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Segmentvorgängen](../api/segment-jobs.md#create)

### Status von Segmentvorgängen nachschlagen

Sie können die `id` für einen bestimmten Segmentauftrag verwenden, um eine Suchanfrage (GET) durchzuführen, um den aktuellen Status des Auftrags anzuzeigen.

Detailliertere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Segmentvorgängen](../api/segment-jobs.md#get)

## Interpretieren der Segmentauftragsergebnisse

Wenn Segmentaufträge erfolgreich ausgeführt werden, wird die `segmentMembership` für jedes Profil aktualisiert, das in der Segmentdefinition enthalten ist. `segmentMembership` speichert auch alle vorab ausgewerteten Zielgruppen, die in [!DNL Experience Platform] aufgenommen werden, sodass sie in andere Lösungen wie [!DNL Adobe Audience Manager] integriert werden können.

Das folgende Beispiel zeigt, wie das `segmentMembership`-Attribut für jeden einzelnen Profildatensatz aussieht:

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
| `lastQualificationTime` | Der Zeitstempel, zu dem die Bestätigung der Segmentzugehörigkeit erfolgte und das Profil in die Segmentdefinition eingetreten ist oder diese verlassen hat. |
| `status` | Der Teilnahmestatus der Segmentdefinition als Teil der aktuellen Anfrage. Muss einem der folgenden bekannten Werte entsprechen: <ul><li>`realized`: Entität qualifiziert sich für die Segmentdefinition.</li><li>`exited`: Entität beendet die Segmentdefinition.</li></ul> |

>[!NOTE]
>
>Jede Segmentzugehörigkeit, die sich basierend auf dem `lastQualificationTime` für mehr als 30 Tage im `exited` befindet, wird gelöscht.

## Zugreifen auf Ergebnisse von Segmentvorgängen

Der Zugriff auf die Ergebnisse eines Segmentvorgangs ist auf zwei Arten möglich: Sie können auf einzelne Profile zugreifen oder eine gesamte Audience in einen Datensatz exportieren.

In den folgenden Abschnitten werden diese Optionen detaillierter beschrieben.

## Profil nachschlagen

Wenn Sie das spezifische Profil kennen, auf das Sie zugreifen möchten, können Sie dies mithilfe der [!DNL Real-Time Customer Profile]-API tun. Die vollständigen Schritte für den Zugriff auf einzelne Profile finden Sie im Tutorial [Zugriff auf Echtzeit-Kundenprofildaten über die Profil-API](../../profile/api/entities.md) .

## Segment exportieren {#export}

Nachdem ein Segmentierungsauftrag erfolgreich abgeschlossen wurde (der Wert des `status` ist „SUCCEEDED„), können Sie Ihre Zielgruppe in einen Datensatz exportieren, wo sie aufgerufen und bearbeitet werden kann.

Die folgenden Schritte sind erforderlich, um Ihre Zielgruppe zu exportieren:

- [Erstellen eines Zieldatensatzes](#create-a-target-dataset) - Erstellen Sie den Datensatz für Mitglieder der Audience.
- [Generieren von Zielgruppenprofilen im Datensatz](#generate-profiles) - Füllen des Datensatzes mit individuellen XDM-Profilen basierend auf den Ergebnissen eines Segmentauftrags.
- [Exportfortschritt überwachen](#monitor-export-progress) - Überprüfen Sie den aktuellen Fortschritt des Exportvorgangs.
- [Zielgruppendaten lesen](#next-steps) - Ruft die resultierenden individuellen XDM-Profile ab, die die Mitglieder Ihrer Zielgruppe darstellen.

### Erstellen eines Zieldatensatzes {#create-dataset}

Beim Exportieren einer Zielgruppe muss zunächst ein Zieldatensatz erstellt werden. Es ist wichtig, dass der Datensatz korrekt konfiguriert ist, um sicherzustellen, dass der Export erfolgreich war.

Eine der wichtigsten Überlegungen betrifft das Schema, auf dem der Datensatz basiert (`schemaRef.id` in der unten stehenden API-Beispielanfrage). Um eine Segmentdefinition zu exportieren, muss der Datensatz auf dem [!DNL XDM Individual Profile Union Schema] (`https://ns.adobe.com/xdm/context/profile__union`) basieren. Ein Vereinigungsschema ist ein systemgeneriertes, schreibgeschütztes Schema, das die Felder von Schemas aggregiert, die dieselbe Klasse aufweisen, in diesem Fall die Klasse „XDM Individual Profile“. Weitere Informationen zu Vereinigungsansichtsschemata finden Sie im Abschnitt [Echtzeit-Kundenprofil“ des Entwicklerhandbuchs zur Schemaregistrierung](../../xdm/api/getting-started.md).

Es gibt zwei Möglichkeiten, den erforderlichen Datensatz zu erstellen:

- **Verwenden von APIs:** In den Schritten, die in diesem Tutorial folgen, wird beschrieben, wie Sie mithilfe der [!DNL Catalog]-API einen Datensatz erstellen, der auf die [!DNL XDM Individual Profile Union Schema] verweist.
- **Verwenden der Benutzeroberfläche:** Um die [!DNL Adobe Experience Platform]-Benutzeroberfläche zum Erstellen eines Datensatzes zu verwenden, der auf das Vereinigungsschema verweist, führen Sie die Schritte im [Benutzeroberflächen-Tutorial](../ui/overview.md) aus und kehren Sie dann zu diesem Tutorial zurück, um mit den Schritten zum [Generieren von Zielgruppenprofilen](#generate-profiles).

Wenn Sie bereits über einen kompatiblen Datensatz verfügen und dessen ID kennen, können Sie direkt mit dem Schritt zum [&#x200B; von Zielgruppenprofilen &#x200B;](#generate-profiles).

**API-Format**

```http
POST /dataSets
```

**Anfrage**

Die folgende Anfrage erstellt einen neuen Datensatz, der Konfigurationsparameter in der Payload bereitstellt.

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

Eine erfolgreiche Antwort gibt ein -Array zurück, das die schreibgeschützte, systemgenerierte eindeutige ID des neu erstellten Datensatzes enthält. Eine ordnungsgemäß konfigurierte Datensatz-ID ist erforderlich, um Zielgruppenmitglieder erfolgreich zu exportieren.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generieren von Profilen für Zielgruppenmitglieder {#generate-profiles}

Sobald Sie über einen Vereinigungs-persistierten Datensatz verfügen, können Sie einen Exportvorgang erstellen, um die Zielgruppenmitglieder im Datensatz zu persistieren, indem Sie eine POST-Anfrage an den `/export/jobs`-Endpunkt in der [!DNL Real-Time Customer Profile]-API stellen und die Datensatz-ID und die Segmentdefinitionsinformationen für die Segmentdefinitionen angeben, die Sie exportieren möchten.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Exportvorgängen](../api/export-jobs.md#create)

### Überwachen des Exportfortschritts

Während der Verarbeitung von Exportvorgängen können Sie den Status überwachen, indem Sie eine GET-Anfrage an den `/export/jobs`-Endpunkt senden und die `id` des Exportvorgangs in den Pfad aufnehmen. Der Exportvorgang ist abgeschlossen, sobald das `status` den Wert „SUCCEEDED“ zurückgibt.

Ausführlichere Informationen zur Verwendung dieses Endpunkts finden Sie im [Handbuch zu Exportvorgängen](../api/export-jobs.md#get)

## Nächste Schritte

Nachdem der Export erfolgreich abgeschlossen wurde, sind Ihre Daten im [!DNL Data Lake] in [!DNL Experience Platform] verfügbar. Anschließend können Sie die [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) verwenden, um auf die Daten zuzugreifen, indem Sie die mit dem Export verknüpfte `batchId` verwenden. Je nach Größe der Segmentdefinition können die Daten in Blöcken vorliegen und der Batch kann aus mehreren Dateien bestehen.

Eine schrittweise Anleitung zum Zugreifen auf und Herunterladen von Batch-Dateien mit der [!DNL Data Access]-API finden Sie im [Datenzugriffs-Tutorial](../../data-access/tutorials/dataset-data.md).

Sie können über [!DNL Adobe Experience Platform Query Service] auch auf erfolgreich exportierte Segmentdefinitionsdaten zugreifen. Mithilfe der Benutzeroberfläche oder RESTful-API können Sie mit [!DNL Query Service] Abfragen zu Daten in der [!DNL Data Lake] schreiben, validieren und ausführen.

Weitere Informationen zum Abfragen von Zielgruppendaten finden Sie in der Dokumentation zu [[!DNL Query Service]](../../query-service/home.md).
