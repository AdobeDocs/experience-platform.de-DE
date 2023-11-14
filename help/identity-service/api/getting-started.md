---
keywords: Experience Platform;home;popular topics;identity service api;identity service developer guide;region
solution: Experience Platform
title: Identity Service API-Anleitung
description: Mit der Identity Service-API können Entwickler die geräteübergreifende, kanalübergreifende und nahezu echtzeitübergreifende Identifizierung Ihrer Kunden mithilfe von Identitätsdiagrammen in Adobe Experience Platform verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: 9f8ed1cc6460dacef7ca91b500a45c059ed1a295
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 36%

---

# [!DNL Identity Service]-API-Handbuch

Adobe Experience Platform [!DNL Identity Service] verwaltet die geräteübergreifende, kanalübergreifende und nahezu Echtzeit-Kundenidentifizierung in einem so genannten Identitätsdiagramm in Adobe Experience Platform.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Identity Service]](../home.md): Löst die grundlegende Herausforderung aus, die durch die Fragmentierung von Kundenprofildaten entsteht. Dies geschieht durch die Überbrückung von Identitäten zwischen Geräten und Systemen, auf denen Kunden mit Ihrer Marke interagieren.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Verbraucherprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich Aufrufe an die [!DNL Identity Service] API.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) lesen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

### regionenbasiertes Routing

Die [!DNL Identity Service] API verwendet regionenspezifische Endpunkte, für die die Einbeziehung einer `{REGION}` als Teil des Anfragepfads. Während der Bereitstellung Ihres Unternehmens wird eine Region bestimmt und in Ihrem Unternehmensprofil gespeichert. Die Verwendung des richtigen Bereichs für jeden Endpunkt stellt sicher, dass alle Anfragen, die mit dem [!DNL Identity Service] Die API wird an die entsprechende Region weitergeleitet.

Derzeit werden zwei Regionen unterstützt von [!DNL Identity Service] APIs: VA7 und NLD2.

Die folgende Tabelle zeigt Beispielpfade mit Regionen:

| Service | Region: VA7 | Region: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE]
>
>Anfragen, die ohne Angabe einer Region durchgeführt werden, können dazu führen, dass Aufrufe an die falsche Region weitergeleitet werden oder dass Aufrufe unerwartet fehlschlagen.

Wenn Sie die Region in Ihrem Unternehmensprofil nicht finden können, wenden Sie sich an Ihren Systemadministrator, um Unterstützung zu erhalten.

## Verwenden der [!DNL Identity Service] API

Identitätsparameter, die in diesen Diensten verwendet werden, können auf zwei Arten ausgedrückt werden: &quot;Composite&quot;oder &quot;XID&quot;.

Verbund-Identitäten sind Konstrukte, die sowohl den ID-Wert als auch den Namespace enthalten. Bei Verwendung von zusammengesetzten Identitäten kann der Namespace entweder mit einem Namen (`namespace.code`) oder ID (`namespace.id`).

Wenn eine Identität beibehalten wird, [!DNL Identity Service] generiert und weist dieser Identität eine Kennung zu, die als native ID oder XID bezeichnet wird. Alle Varianten von Cluster- und Mapping-APIs unterstützen sowohl zusammengesetzte Identitäten als auch XID in ihren Anfragen und Antworten. Einer der Parameter ist erforderlich - `xid` oder Kombination von [`ns` oder `nsid`] und `id` , um diese APIs zu verwenden.

Um die Payload in Antworten zu begrenzen, passen APIs ihre Antworten an den Typ des verwendeten Identitätskonstrukts an. Wenn Sie also XID übergeben, haben Ihre Antworten XIDs, wenn Sie zusammengesetzte Identitäten übergeben, folgt die Antwort der in der Anfrage verwendeten Struktur.

Die Beispiele in diesem Dokument decken nicht die gesamte Funktionalität der [!DNL Identity Service] API. Die vollständige API finden Sie in der [Swagger-API-Referenz](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Alle zurückgegebenen Identitäten werden im nativen XID-Formular angezeigt, wenn in der Anfrage die native XID verwendet wird. Es wird empfohlen, das Formular ID/Namespace zu verwenden. Weitere Informationen finden Sie im Abschnitt zu [Abrufen der XID für eine Identität](./create-custom-namespace.md).

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie nun das restliche Entwicklerhandbuch lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und veranschaulicht Beispiel-API-Aufrufe zur Durchführung von CRUD-Vorgängen. Zu jedem Aufruf gehören das allgemeine API-Format, eine Beispielanfrage mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Payloads sowie eine Beispielantwort eines erfolgreichen Aufrufs.
