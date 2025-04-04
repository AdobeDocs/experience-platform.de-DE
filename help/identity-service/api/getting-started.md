---
keywords: Experience Platform;Startseite;beliebte Themen;Identity Service-API;Identity Service-Entwicklerhandbuch;Region
solution: Experience Platform
title: Identity Service-API-Handbuch
description: Mit der Identity Service-API können Entwickler die geräte- und kanalübergreifende, nahezu in Echtzeit ausgeführte Identifizierung Ihrer Kunden mithilfe von Identitätsdiagrammen in Adobe Experience Platform verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
role: Developer
exl-id: d612af38-4648-4c3e-8cfd-3f306c9370e1
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 35%

---

# [!DNL Identity Service]-API-Handbuch

Adobe Experience Platform [!DNL Identity Service] verwaltet die geräte- und kanalübergreifende, nahezu in Echtzeit ausgeführte Identifizierung Ihrer Kunden in einem so genannten Identitätsdiagramm innerhalb von Adobe Experience Platform.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [[!DNL Identity Service]](../home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenprofildaten ergibt. Dies erfolgt durch die Überbrückung von Identitäten zwischen Geräten und Systemen, in denen Kunden mit Ihrer Marke interagieren.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten von [!DNL Experience Platform] organisiert werden.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die [!DNL Identity Service]-API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Experience Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

- Authorization: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform] sind auf bestimmte virtuelle Sandboxes beschränkt. Bei allen Anfragen an [!DNL Experience Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in [!DNL Experience Platform] finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Bei allen Anfragen mit einer Payload (POST, PUT, PATCH) ist eine zusätzliche Kopfzeile erforderlich:

- Content-Type: application/json

### Regionsbasiertes Routing

Die [!DNL Identity Service]-API verwendet regionsspezifische Endpunkte, für die ein `{REGION}` als Teil des Anfragepfads eingeschlossen werden muss. Bei der Bereitstellung Ihrer Organisation wird eine Region innerhalb Ihres Unternehmensprofils bestimmt und gespeichert. Durch die Verwendung der richtigen Region für jeden Endpunkt wird sichergestellt, dass alle Anforderungen, die mithilfe der [!DNL Identity Service]-API gestellt werden, an die entsprechende Region weitergeleitet werden.

Derzeit werden zwei Regionen von [!DNL Identity Service] APIs unterstützt: VA7 und NLD2.

Die folgende Tabelle zeigt Beispielpfade mit Regionen:

| Service | Region: VA7 | Region: NLD2 |
| ------ | -------- |--------- |
| [!DNL Identity Service] API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| [!DNL Identity Namespace] API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idNamespace{ENDPOINT} |

>[!NOTE]
>
>Anfragen, die ohne Angabe einer Region gesendet werden, können dazu führen, dass -Aufrufe an die falsche Region weitergeleitet werden oder -Aufrufe unerwartet fehlschlagen.

Wenn Sie die Region in Ihrem Unternehmensprofil nicht finden können, wenden Sie sich an Ihren Systemadministrator, um Unterstützung zu erhalten.

## Verwenden der [!DNL Identity Service]-API

Identitätsparameter, die in diesen Services verwendet werden, können auf zwei Arten ausgedrückt werden: zusammengesetzte oder XID.

Zusammengesetzte Identitäten sind Konstrukte, die sowohl den ID-Wert als auch den Namespace enthalten. Bei Verwendung von zusammengesetzten Identitäten kann der Namespace entweder nach Name (`namespace.code`) oder ID (`namespace.id`) bereitgestellt werden.

Wenn eine Identität beibehalten wird, generiert [!DNL Identity Service] und weist dieser Identität eine ID zu, die als native ID oder XID bezeichnet wird. Alle Varianten von Cluster- und Mapping-APIs unterstützen in ihren Anfragen und Antworten sowohl zusammengesetzte Identitäten als auch XID. Einer der Parameter ist erforderlich - `xid` oder Kombination aus [`ns` oder `nsid`] und `id`, um diese APIs zu verwenden.

Um die Payload in Antworten zu begrenzen, passen APIs ihre Antworten an den Typ des verwendeten Identitätskonstrukts an. Das heißt, wenn Sie eine XID übergeben, enthalten Ihre Antworten XIDs. Wenn Sie zusammengesetzte Identitäten übergeben, folgt die Antwort der in der Anfrage verwendeten Struktur.

Die Beispiele in diesem Dokument decken nicht die vollständige Funktionalität der [!DNL Identity Service]-API ab. Die vollständige API finden Sie in der [Swagger-API-Referenz](https://www.adobe.io/experience-platform-apis/references/identity-service).

>[!NOTE]
>
>Alle zurückgegebenen Identitäten werden im nativen XID-Formular angezeigt, wenn in der Anfrage eine native XID verwendet wird. Es wird empfohlen, das Formular ID/Namespace zu verwenden. Weitere Informationen finden Sie im Abschnitt zum [ der XID für eine Identität](./create-custom-namespace.md).

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldedaten gesammelt haben, können Sie nun das restliche Entwicklerhandbuch lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und veranschaulicht Beispiel-API-Aufrufe zur Durchführung von CRUD-Vorgängen. Zu jedem Aufruf gehören das allgemeine API-Format, eine Beispielanfrage mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Payloads sowie eine Beispielantwort eines erfolgreichen Aufrufs.
