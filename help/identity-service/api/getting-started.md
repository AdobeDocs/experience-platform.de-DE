---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Erste Schritte
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# Entwicklerhandbuch für Identitätsdienst-API

Der Identitätsdienst für Adobe Experience Platform verwaltet den geräteübergreifenden, geräteübergreifenden Kanal und die Identifikation Ihrer Kunden in Echtzeit in einem so genannten Identitätsdiagramm innerhalb der Adobe Experience Platform.

## Erste Schritte

Dieses Handbuch erfordert ein Verständnis der folgenden Komponenten der Adobe Experience Platform:

- [Identitätsdienst](../home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung der Kundendaten ergibt. Dies geschieht, indem Identitäten zwischen Geräten und Systemen, auf denen Kunden mit Ihrer Marke interagieren, überbrückt werden.
- [Echtzeit-Profil](../../profile/home.md): Bietet ein einheitliches, benutzerdefiniertes Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [Erlebnisdatenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Identitätsdienst-API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Handbuch finden Sie Beispiele für API-Aufrufe, die zeigen, wie Sie Ihre Anforderungen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anforderungs-Nutzdaten. Beispiel-JSON, die in API-Antworten zurückgegeben wird, wird ebenfalls bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Werte für erforderliche Kopfzeilen sammeln

Um Aufrufe an Plattform-APIs durchführen zu können, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen. Das Abschließen des Authentifizierungstreutorials stellt die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform API-Aufrufen bereit, wie unten dargestellt:

- Genehmigung: Träger `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle Ressourcen in Experience Platform werden zu bestimmten virtuellen Sandboxen isoliert. Für alle Anforderungen an Plattform-APIs ist ein Header erforderlich, der den Namen der Sandbox angibt, in der der Vorgang ausgeführt wird:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Weitere Informationen zu Sandboxes in Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../../sandboxes/home.md).

Für alle Anforderungen mit einer Payload (POST, PUT, PATCH) ist ein zusätzlicher Header erforderlich:

- Content-Type: application/json

### Regionales Routing

Die Identitätsdienst-API verwendet regionsspezifische Endpunkte, für die ein `{REGION}` Teil des Anforderungspfads eingefügt werden muss. Während der Bereitstellung Ihrer IMS-Organisation wird eine Region in Ihrem IMS-Org-Profil ermittelt und gespeichert. Durch Verwendung des richtigen Bereichs für jeden Endpunkt wird sichergestellt, dass alle Anforderungen, die mit der Identitätsdienst-API ausgeführt werden, an den entsprechenden Bereich weitergeleitet werden.

Derzeit werden zwei Regionen von Identitätsdienst-APIs unterstützt: VA7 und NLD2.

Die nachstehende Tabelle zeigt Beispielpfade mit Regionen:

| Service | Region: VA7 | Region: NLD2 |
| ------ | -------- |--------- |
| Identitätsdienst-API | https://</span>platform-va7.adobe.</span>io/data/core/identity/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/identity/{ENDPOINT} |
| Identitäts-Namensraum-API | https://</span>platform-va7.adobe.</span>io/data/core/idnamespace/{ENDPOINT} | https://</span>platform-nld2.adobe.</span>io/data/core/idnamespace{ENDPOINT} |

>[!NOTE] Anforderungen, die ohne Angabe einer Region ausgeführt werden, können dazu führen, dass Routing an die falsche Region gesendet werden oder dass Aufrufe unerwartet fehlschlagen.

Wenn Sie die Region nicht in Ihrem IMS Org-Profil finden können, wenden Sie sich bitte an Ihren Systemadministrator.

## Verwenden der Identitätsdienst-API

Identitätsparameter, die in diesen Diensten verwendet werden, können auf zwei Arten ausgedrückt werden: Composite oder XID.

Composite-Identitäten sind Konstrukte, die sowohl den ID-Wert als auch den Namensraum enthalten. Bei Verwendung von Composite-Identitäten kann der Namensraum entweder mit dem Namen (`namespace.code`) oder mit der ID (`namespace.id`) bereitgestellt werden.

Wenn eine Identität beibehalten wird, generiert der Identitätsdienst eine ID und weist dieser Identität eine ID zu, die als native ID oder XID bezeichnet wird. Alle Varianten von Cluster- und Zuordnungs-APIs unterstützen sowohl Composite-Identitäten als auch XID in ihren Anforderungen und Antworten. Einer der Parameter ist erforderlich - `xid` oder eine Kombination aus [`ns` oder `nsid`] und `id` für die Verwendung dieser APIs.

Um die Nutzlast in Antworten zu begrenzen, passen APIs ihre Antworten an den verwendeten Identitätskonstrukttyp an. Das heißt, wenn Sie XID übergeben Ihre Antworten werden XIDs haben, wenn Sie zusammengesetzte Identitäten übergeben, folgt die Antwort der Struktur, die in der Anforderung verwendet wird.

Die Beispiele in diesem Dokument decken nicht die gesamte Funktionalität der Identitätsdienst-API ab. Die vollständige API finden Sie in der [Swagger API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml).

>[!NOTE] Alle zurückgegebenen Identitäten werden im nativen XID-Formular zurückgegeben, wenn in der Anforderung native XID verwendet wird. Es wird empfohlen, das Formular ID/Namensraum zu verwenden. Weitere Informationen finden Sie im Abschnitt zum [Abrufen der XID für eine Identität](./create-custom-namespace.md).

## Nächste Schritte

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie jetzt den Rest des Entwicklerhandbuchs lesen. Jeder Abschnitt enthält wichtige Informationen zu ihren Endpunkten und zeigt Beispiel-API-Aufrufe für CRUD-Vorgänge. Zu jedem Aufruf gehören das allgemeine **API-Format**, eine **Musteranforderung** mit erforderlichen Kopfzeilen und ordnungsgemäß formatierten Nutzdaten sowie eine Beispielantwort **** für einen erfolgreichen Aufruf.
