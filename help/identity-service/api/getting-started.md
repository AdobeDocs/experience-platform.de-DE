---
keywords: Experience Platform;Home;beliebte Themen;Identitätsdienst-API;Identitätsdienst-Entwicklerhandbuch;Region
solution: Experience Platform
title: Identitätsdienst-API-Handbuch
topic-legacy: API guide
description: Die Identitätsdienst-API ermöglicht es Entwicklern, geräteübergreifende Kanal- und Echtzeitidentifizierungen Ihrer Kunden mithilfe von Identitätsdiagrammen in Adobe Experience Platform zu verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 29%

---

# [!DNL Identity Service] API-Handbuch

Adobe Experience Platform [!DNL Identity Service] verwaltet die geräteübergreifende, geräteübergreifende und nahezu Echtzeit-Identifizierung Ihrer Kunden in einem so genannten Identitätsdiagramm innerhalb von Adobe Experience Platform.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Identity Service]](../home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung der Kundendaten ergibt. Dies geschieht, indem Identitäten zwischen Geräten und Systemen, auf denen Kunden mit Ihrer Marke interagieren, überbrückt werden.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches, benutzerdefiniertes Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Identity Service]-API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an [!DNL Platform]-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird in:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxen in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

### Regionales Routing

Die API [!DNL Identity Service] verwendet regionsspezifische Endpunkte, für die ein `{REGION}` als Teil des Anforderungspfads eingefügt werden muss. Während der Bereitstellung Ihrer IMS-Organisation wird eine Region in Ihrem IMS-Org-Profil ermittelt und gespeichert. Durch Verwendung des richtigen Bereichs für jeden Endpunkt wird sichergestellt, dass alle Anforderungen, die mit der [!DNL Identity Service]-API ausgeführt werden, an den entsprechenden Bereich weitergeleitet werden.

Es gibt derzeit zwei Regionen, die von APIs unterstützt werden: VA7 und NLD2.[!DNL Identity Service]

Die nachstehende Tabelle zeigt Beispielpfade mit Regionen:

| Dienst | Region: VA7 | Region: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Anforderungen, die ohne Angabe einer Region ausgeführt werden, können dazu führen, dass Routing an die falsche Region gesendet werden oder dass Aufrufe unerwartet fehlschlagen.

Wenn Sie die Region nicht in Ihrem IMS Org-Profil finden können, wenden Sie sich bitte an Ihren Systemadministrator.

## Verwenden der [!DNL Identity Service]-API

Identitätsparameter, die in diesen Diensten verwendet werden, können auf zwei Arten ausgedrückt werden: Composite oder XID.

Composite-Identitäten sind Konstrukte, die sowohl den ID-Wert als auch den Namensraum enthalten. Bei Verwendung von Composite-Identitäten kann der Namensraum entweder mit dem Namen (`namespace.code`) oder mit der ID (`namespace.id`) bereitgestellt werden.

Wenn eine Identität beibehalten wird, generiert [!DNL Identity Service] eine ID und weist dieser Identität eine solche zu, die als native ID oder XID bezeichnet wird. Alle Varianten von Cluster- und Zuordnungs-APIs unterstützen sowohl Composite-Identitäten als auch XID in ihren Anforderungen und Antworten. Einer der Parameter ist erforderlich - `xid` oder Kombination von [`ns` oder `nsid`] und `id`, um diese APIs zu verwenden.

Um die Nutzlast in Antworten zu begrenzen, passen APIs ihre Antworten an den verwendeten Identitätskonstrukttyp an. Das heißt, wenn Sie XID übergeben Ihre Antworten werden XIDs haben, wenn Sie zusammengesetzte Identitäten übergeben, folgt die Antwort der Struktur, die in der Anforderung verwendet wird.

Die Beispiele in diesem Dokument decken nicht die gesamte Funktionalität der API ab. [!DNL Identity Service] Die vollständige API finden Sie in der [Swagger-API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE]
>
>Alle zurückgegebenen Identitäten werden im nativen XID-Formular zurückgegeben, wenn in der Anforderung native XID verwendet wird. Es wird empfohlen, das Formular ID/Namensraum zu verwenden. Weitere Informationen finden Sie im Abschnitt [Abrufen der XID für eine Identität](./create-custom-namespace.md).

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie nun das restliche Entwicklerhandbuch lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und veranschaulicht Beispiel-API-Aufrufe zur Durchführung von CRUD-Vorgängen. Zu jedem Aufruf gehören das allgemeine API-Format, eine Beispielanfrage mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Payloads sowie eine Beispielantwort eines erfolgreichen Aufrufs.
