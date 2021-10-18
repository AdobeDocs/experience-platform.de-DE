---
keywords: Experience Platform; Startseite; beliebte Themen; Identitätsdienst-API; Entwicklerhandbuch für Identitätsdienste; Region
solution: Experience Platform
title: Identity Service API-Anleitung
topic-legacy: API guide
description: Mit der Identity Service-API können Entwickler die geräteübergreifende, kanalübergreifende und nahezu echtzeitübergreifende Identifizierung Ihrer Kunden mithilfe von Identitätsdiagrammen in Adobe Experience Platform verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: f269a7b1584a6e4a0e1820a0c587a647c0c8f7b5
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 36%

---

# [!DNL Identity Service]-API-Handbuch

Adobe Experience Platform [!DNL Identity Service] verwaltet die geräteübergreifende, kanalübergreifende und nahezu Echtzeit-Kundenidentifizierung in einem so genannten Identitätsdiagramm in Adobe Experience Platform.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Identity Service]](../home.md): Löst die grundlegende Herausforderung aus, die sich aus der Fragmentierung von Kundenprofildaten ergibt. Dies geschieht durch die Verknüpfung von Identitäten über Geräte und Systeme hinweg, in denen Kunden mit Ihrer Marke interagieren.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Platform] Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Identity Service]-API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

### regionenbasiertes Routing

The [!DNL Identity Service] API employs region-specific endpoints that require the inclusion of a `{REGION}` as part of the request path. Während der Bereitstellung Ihrer IMS-Organisation wird eine Region in Ihrem IMS-Org-Profil bestimmt und gespeichert. Using the correct region with each endpoint ensures that all requests made using the [!DNL Identity Service] API are routed to the appropriate region.

There are two regions currently supported by [!DNL Identity Service] APIs: VA7 and NLD2.

Die folgende Tabelle zeigt Beispielpfade mit Regionen:

| Service | Region: VA7 | Region: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Anfragen, die ohne Angabe einer Region durchgeführt werden, können dazu führen, dass Aufrufe an die falsche Region weitergeleitet werden oder dass Aufrufe unerwartet fehlschlagen.

Wenn Sie die Region in Ihrem IMS-Org-Profil nicht finden können, wenden Sie sich an Ihren Systemadministrator, um Unterstützung zu erhalten.

## Verwenden der [!DNL Identity Service]-API

Identitätsparameter, die in diesen Diensten verwendet werden, können auf zwei Arten ausgedrückt werden: zusammengesetzt oder XID.

Verbund-Identitäten sind Konstrukte, die sowohl den ID-Wert als auch den Namespace enthalten. Bei Verwendung von zusammengesetzten Identitäten kann der Namespace entweder mit dem Namen (`namespace.code`) oder der Kennung (`namespace.id`) angegeben werden.

Wenn eine Identität persistiert wird, generiert [!DNL Identity Service] eine Kennung, die als native ID oder XID bezeichnet wird, und weist sie dieser Identität zu. Alle Varianten von Cluster- und Mapping-APIs unterstützen sowohl zusammengesetzte Identitäten als auch XID in ihren Anfragen und Antworten. Einer der Parameter ist erforderlich - `xid` oder Kombination von [`ns` oder `nsid`] und `id` , um diese APIs zu verwenden.

Um die Payload in Antworten zu begrenzen, passen APIs ihre Antworten an den Typ des verwendeten Identitätskonstrukts an. Wenn Sie also XID übergeben, haben Ihre Antworten XIDs, wenn Sie zusammengesetzte Identitäten übergeben, folgt die Antwort der in der Anfrage verwendeten Struktur.

Die Beispiele in diesem Dokument decken nicht die gesamte Funktionalität der [!DNL Identity Service]-API ab. For the complete API, see the [Swagger API Reference](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Alle zurückgegebenen Identitäten werden im nativen XID-Formular angezeigt, wenn in der Anfrage die native XID verwendet wird. Es wird empfohlen, das Formular ID/Namespace zu verwenden. For more information, see the section on [getting the XID for an identity](./create-custom-namespace.md).

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie nun das restliche Entwicklerhandbuch lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und veranschaulicht Beispiel-API-Aufrufe zur Durchführung von CRUD-Vorgängen. Zu jedem Aufruf gehören das allgemeine API-Format, eine Beispielanfrage mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Payloads sowie eine Beispielantwort eines erfolgreichen Aufrufs.
