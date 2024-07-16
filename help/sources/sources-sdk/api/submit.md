---
keywords: Experience Platform;Startseite;beliebte Themen;Quellen;Connectoren;Quell-Connectoren;Quellen-SDK;SDK
title: Übermitteln Ihrer Source
description: Das folgende Dokument enthält Schritte zum Testen und Überprüfen einer neuen Quelle mithilfe der Flow Service-API und zur Integration einer neuen Quelle über Self-Serve-Quellen (Batch SDK).
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 16%

---

# Übermitteln Ihrer Quelle

Der letzte Schritt bei der Integration Ihrer neuen Quelle in Adobe Experience Platform mithilfe von Self-Serve-Quellen (Batch SDK) besteht darin, Ihre Quelle zur Verifizierung zu testen. Nach erfolgreichem Abschluss können Sie Ihre neue Quelle senden, indem Sie sich an Ihren Adobe-Support-Mitarbeiter wenden.

Das folgende Dokument enthält Schritte zum Testen und Debuggen Ihrer Quelle mit der [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

* Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../landing/api-guide.md).
* Informationen zum Generieren Ihrer Anmeldeinformationen für Platform-APIs finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md).
* Informationen zum Einrichten von [!DNL Postman] für Platform-APIs finden Sie im Tutorial zum [Einrichten der Entwicklerkonsole und  [!DNL Postman]](../../../landing/postman.md).
* Laden Sie zur Unterstützung Ihres Test- und Debugging-Prozesses die Überprüfungssammlung und -umgebung für Self-Serve-Quellen hier herunter ](../assets/sdk-verification.zip) und führen Sie die unten beschriebenen Schritte aus.[

## Testen der Quelle

Um Ihre Quelle zu testen, müssen Sie die Überprüfungssammlung für Self-Serve-Quellen und die Umgebung ](../assets/sdk-verification.zip) auf [!DNL Postman] ausführen und dabei die entsprechenden Umgebungsvariablen für Ihre Quelle angeben.[

Um den Test zu starten, müssen Sie zunächst die Sammlung und Umgebung auf [!DNL Postman] einrichten. Geben Sie als Nächstes die Verbindungsspezifikations-ID an, die Sie testen möchten.

### `authSpecName` angeben

Nachdem Sie Ihre Verbindungsspezifikations-ID eingegeben haben, müssen Sie die `authSpecName` angeben, die Sie für Ihre Basisverbindung verwenden. Je nach Wahl kann dies entweder `OAuth 2 Refresh Code` oder `Basic Authentication` sein. Nachdem Sie Ihren `authSpecName` angegeben haben, müssen Sie die erforderlichen Anmeldeinformationen in Ihre Umgebung einfügen. Wenn Sie beispielsweise `authSpecName` als `OAuth 2 Refresh Code` angeben, müssen Sie die erforderlichen Anmeldeinformationen für OAuth 2 bereitstellen, nämlich `host` und `accessToken`.

### `sourceSpec` angeben

Nachdem Sie die Authentifizierungs-Spezifizierungsparameter hinzugefügt haben, müssen Sie als Nächstes die erforderlichen Eigenschaften aus Ihrer Quellspezifikation hinzufügen. Sie finden die erforderlichen Eigenschaften in &quot;`sourceSpec.spec.properties`&quot;. Im folgenden Beispiel für [!DNL MailChimp Members] ist die einzige erforderliche Eigenschaft `listId`, was `listId` bedeutet und der entsprechende ID-Wert für Ihre [!DNL Postman]-Umgebung ist.

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

Nachdem Sie die Authentifizierungs- und Quellspezifizierungsparameter angegeben haben, können Sie mit dem Ausfüllen der übrigen Umgebungsvariablen beginnen. Die nachstehende Tabelle enthält eine Referenz:

>[!NOTE]
>
>Alle folgenden Beispielvariablen sind Platzhalterwerte, die Sie aktualisieren müssen, mit Ausnahme von `flowSpecificationId` und `targetConnectionSpecId`, bei denen es sich um feste Werte handelt.

| Parameter | Beschreibung | Beispiel |
| --- | --- | --- |
| `x-api-key` | Eine eindeutige Kennung, mit der Aufrufe an Experience Platform-APIs authentifiziert werden. Informationen zum Abrufen Ihrer `x-api-key` finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md) . | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | Eine Unternehmenseinheit, die Produkte und Dienste besitzen oder lizenzieren und Zugriff auf ihre Mitglieder gewähren kann. Anweisungen zum Abrufen Ihrer `x-gw-ims-org-id` -Informationen finden Sie im Tutorial zum Einrichten der Entwicklerkonsole mit [und  [!DNL Postman]](../../../landing/postman.md) . | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Das Autorisierungstoken, das zum Abschließen von Aufrufen an Experience Platform-APIs erforderlich ist. Informationen zum Abrufen Ihrer `authorizationToken` finden Sie im Tutorial zum [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md) . | `Bearer authorizationToken` |
| `schemaId` | Damit die Quelldaten in Platform verwendet werden können, muss ein Zielschema erstellt werden, das die Quelldaten entsprechend Ihren Anforderungen strukturiert. Ausführliche Schritte zum Erstellen eines XDM-Zielschemas finden Sie im Tutorial zum [Erstellen eines Schemas mithilfe der API](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | Die eindeutige Version, die Ihrem Schema entspricht. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | Die `meta:altId`, die beim Erstellen eines neuen Schemas neben dem `schemaId` zurückgegeben wird. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Ausführliche Anweisungen zum Erstellen eines Zieldatensatzes finden Sie im Tutorial zu [Erstellen eines Datensatzes mithilfe der API](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | Mit Zuordnungssätzen lässt sich definieren, wie Daten in einem Quellschema den Daten eines Zielschemas zugeordnet werden sollen. Ausführliche Anweisungen zum Erstellen einer Zuordnung finden Sie im Tutorial zum Erstellen eines Zuordnungssatzes mit der API](../../../data-prep/api/mapping-set.md).[ | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | Die eindeutige ID, die Ihrem Zuordnungssatz entspricht. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | Die Verbindungsspezifikations-ID, die Ihrer Quelle entspricht. Dies ist die ID, die Sie nach dem [Erstellen einer neuen Verbindungsspezifikation](./create.md) generiert haben. | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | Die Flussspezifikations-ID `RestStorageToAEP`. **Dies ist ein fester Wert**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | Die Zielverbindungs-ID des Data Lake, in dem die erfassten Daten landen. **Dies ist ein fester Wert**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | Das festgelegte Zeitintervall, das bei der Überprüfung auf den Abschluss eines Flusslaufs eingehalten werden soll. | `40` |
| `startTime` | Die vorgesehene Startzeit für Ihren Datenfluss. Die Startzeit muss in Unix-Zeit formatiert sein. | `1597784298` |

Nachdem Sie alle Umgebungsvariablen bereitgestellt haben, können Sie mit der Ausführung der Sammlung über die [!DNL Postman] -Oberfläche beginnen. Wählen Sie in der Benutzeroberfläche [!DNL Postman] die Auslassungszeichen (**...**) neben [!DNL Sources SSSs Verification Collection] und dann **Sammlung ausführen** aus.

![runner](../assets/runner.png)

Die Oberfläche [!DNL Runner] wird angezeigt, über die Sie die Ausführungsreihenfolge Ihres Datenflusses konfigurieren können. Wählen Sie **Ausführen der SSS Verification Collection** aus, um die Sammlung auszuführen.

>[!NOTE]
>
>Sie können **Fluss löschen** in der Checkliste für die Ausführungsreihenfolge deaktivieren, wenn Sie das Dashboard für die Quellenüberwachung in der Platform-Benutzeroberfläche bevorzugen. Sobald Sie jedoch mit dem Test fertig sind, müssen Sie sicherstellen, dass Ihre Testflüsse gelöscht werden.

![run-collection](../assets/run-collection.png)

## Übermitteln Ihrer Quelle

Sobald Ihre Quelle den gesamten Workflow abschließen kann, können Sie sich an Ihren Adobe-Support-Mitarbeiter wenden und Ihre Quelle zur Integration übermitteln.
