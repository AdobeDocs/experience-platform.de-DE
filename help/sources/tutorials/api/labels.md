---
title: Anwenden von Zugriffskennzeichnungen zur Verwaltung des Benutzerzugriffs auf Datenflüsse mithilfe der -API
description: Erfahren Sie, wie Sie mit der Flow Service-API Zugriffsbeschriftungen anwenden und den Benutzerzugriff auf Ihre Quelldatenflüsse verwalten können.
exl-id: 572d6838-3e4c-4fd5-89fa-32cad6280325
source-git-commit: f57fa04e668fa9c61b9b15778e74969edffae0fa
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 11%

---

# Anwenden von Zugriffskennzeichnungen zur Verwaltung des Benutzerzugriffs auf Datenflüsse mithilfe der -API

Real-Time CDP Sie können die von der [attributbasierten Zugriffssteuerung) in &#x200B;](../../../access-control/abac/overview.md) bereitgestellten Funktionen verwenden, um Beschriftungen auf Ihre Quelldatenflüsse anzuwenden. Mit dieser Funktion können Sie sicherstellen, dass nur eine Untergruppe von Benutzern in Ihrer Organisation Zugriff auf bestimmte Quellen und Datenflüsse erhält.

Wenn Sie einem bestimmten Datenfluss eine Zugriffsbeschriftung hinzufügen, können nur Benutzer, die Zugriff auf eine Rolle haben, der diese Beschriftung zugewiesen ist, diesen Datenfluss anzeigen und bearbeiten. Wenn ein Quelldatenfluss nicht mit Beschriftungen gekennzeichnet ist, ist er für alle Benutzer sichtbar, die zu Ihrer Organisation gehören. Wenn Sie beispielsweise die Kennzeichnung C12 auf einen Datenfluss anwenden, können Benutzende, denen eine Rolle zugewiesen wurde, die nicht über die Kennzeichnung C12 verfügt, den Datenfluss nicht mit der Kennzeichnung C12 anzeigen und bearbeiten.

Lesen Sie dieses Handbuch, um Informationen zum Anwenden von Zugriffsbeschriftungen auf Ihre Quellen-Datenflüsse mithilfe der [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) zu erhalten.

## Erste Schritte

Bevor Sie mit Zugriffssteuerungsbeschriftungen arbeiten, stellen Sie sicher, dass Sie sich zunächst mit den Funktionen der attributbasierten Zugriffssteuerung vertraut machen. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Attributbasierte Zugriffssteuerung – Übersicht](../../../access-control/abac/overview.md)
* [End-to-End-Handbuch zur attributbasierten Zugriffssteuerung](../../../access-control/abac/end-to-end-guide.md)
* [Handbuch zur attributbasierten Zugriffssteuerung für die API](../../../access-control/abac/api/overview.md)
* [Glossar der Datennutzungskennzeichnungen](../../../data-governance/labels/reference.md)

## Anwenden von Zugriffskennzeichnungen auf Quellen-Datenflüsse

>[!NOTE]
>
>* Sie können keine Kennzeichnungen auf eine Flussausführung anwenden. Flussausführungen übernehmen jedoch alle Beschriftungen, die Sie auf den übergeordneten Datenfluss anwenden.
>
>* Wenn Sie keinen Ansichtszugriff auf einen Datenfluss haben, können Sie auch die entsprechenden Flussausführungen nicht anzeigen.

Um einem Datenfluss eine Kennzeichnung hinzuzufügen, stellen Sie eine PATCH-Anfrage an den `/flows`-Endpunkt und geben Sie die ID des Datenflusses an, den Sie aktualisieren möchten.

**API-Format**

```http
PATCH /flows/{FLOW_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `{FLOW_ID}` | Die ID des Datenflusses, den Sie aktualisieren möchten. |

**Anfrage**

>[!TIP]
>
>Um eine PATCH-Anfrage zu stellen, geben Sie die Version/das eTag des Datenflusses an, den Sie als `if-match`-Kopfzeilenparameter aktualisieren möchten.

Die folgende Anfrage fügt die C12-Kennzeichnung zum Datenfluss mit der ID hinzu: `84224def-1e2a-4d95-9ea2-132d697ed2aa`.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/84224def-1e2a-4d95-9ea2-132d697ed2aa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'if-match: "c5002e0e-0000-0200-0000-67a3c3b70000"'
  -d '[
    {
        "op": "add",
        "path": "/labels",
        "value": ["core/C12"]
    }
]'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `op` | Der Operationsaufruf, der verwendet wird, um die Aktion zu definieren, die zur Aktualisierung des Datenflusses erforderlich ist. Die Operationen umfassen `add`, `replace` und `remove`. |
| `path` | Der Teil des Datenflusses, der aktualisiert werden soll. |
| `value` | Der neue Wert, mit dem Sie Ihre Eigenschaft aktualisieren möchten. |



**Antwort**

Bei einer erfolgreichen Antwort werden Ihre Fluss-ID und ein aktualisiertes eTag zurückgegeben. Sie können die Aktualisierung überprüfen, indem Sie eine GET-Anfrage an die [!DNL Flow Service]-API stellen und dabei Ihre Fluss-ID angeben.

```json
{
    "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

Nachdem Sie Zugriffsbeschriftungen für Ihren Datenfluss erfolgreich konfiguriert haben, können Benutzer, die keinen Zugriff auf diese Beschriftung haben, den Datenfluss nicht mehr abrufen. Wenn beispielsweise eine Benutzerin oder ein Benutzer, die bzw. der nicht über die C12-Kennzeichnung verfügt, eine GET-Anfrage zum Abrufen des Datenflusses mit der ID `84224def-1e2a-4d95-9ea2-132d697ed2aa` stellt, erhält sie bzw. er die folgende Antwort:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-1439-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "detailed-message": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
        "id": "84224def-1e2a-4d95-9ea2-132d697ed2aa",
        "request-id": "{REQUEST_ID}",
        "type": "flows"
    },
    "errorMessage": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again.",
    "errorDetails": "The requested flows resource 84224def-1e2a-4d95-9ea2-132d697ed2aa is not found. Verify the resource ID before trying again."
}
```

Ebenso können Benutzende ohne Zugriff auf die C12-Kennzeichnung keine PATCH- oder DELETE-Anfragen für den aktualisierten Datenfluss stellen und erhalten die folgende Antwort:

```json
{
    "type": "https://ns.adobe.com/aep/errors/FLOW-2120-403",
    "title": "Forbidden",
    "status": 403,
    "report": {
        "detailed-message": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
        "request-id": "{REQUEST_ID}"
    },
    "errorMessage": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again.",
    "errorDetails": "You do not have sufficient permissions to perform the operation. Please contact your administrator to resolve permissions and try again."
}
```

## Nächste Schritte

Sie wissen jetzt, wie Sie Zugriffsbeschriftungen auf Ihre Quelldatenflüsse anwenden. Sie können jetzt sicherstellen, dass nur eine bestimmte Benutzergruppe in Ihrer Organisation auf bestimmte Datenflüsse für Quellen zugreifen kann. Weitere Informationen finden Sie in der folgenden Dokumentation:

* [Anwenden von Zugriffskennzeichnungen auf Datenflüsse von Quellen in der Benutzeroberfläche](../ui/labels.md)
* [Zugriffskontrolle – Übersicht](../../../access-control/home.md)
