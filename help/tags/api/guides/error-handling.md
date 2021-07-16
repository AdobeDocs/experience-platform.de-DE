---
title: Umgang mit Fehlern
description: Erfahren Sie, wie Fehler in der Reactor-API gehandhabt werden.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

---

# Umgang mit Fehlern

Wenn beim Aufrufen der Reactor-API ein Problem auftritt, kann ein Fehler auf eine der folgenden Arten zurückgegeben werden:

* **Sofortige Fehler**: Wenn eine Anfrage ausgeführt wird, die zu einem sofortigen Fehler führt, wird von der API eine Fehlerantwort zurückgegeben, wobei der HTTP-Status den allgemeinen Typ des aufgetretenen Fehlers widerspiegelt.
* **Verzögerte Fehler**: Bei der Ausführung einer API-Anfrage, die zu einem verzögerten Fehler führt (z. B. einer asynchronen Aktivität), kann von der API im  `meta.status_details` der zugehörigen Ressource ein Fehler zurückgegeben werden.

## Fehlerformat

Fehlerantworten zielen auf die Einhaltung der [JSON:API-Fehlerspezifikation](http://jsonapi.org/format/#errors) ab und halten im Allgemeinen die folgende Struktur ein:

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `id` | Eine eindeutige Kennung für dieses bestimmte Vorkommen des Problems. |
| `status` | Der für dieses Problem geltende HTTP-Status-Code, ausgedrückt als Zeichenfolgenwert. |
| `code` | Ein anwendungsspezifischer Fehlercode, ausgedrückt als Zeichenfolgenwert. |
| `title` | Eine kurze, für Menschen lesbare Zusammenfassung des Problems, das **nicht von Auftreten zu Auftreten ändern sollte**, außer zum Zwecke der Lokalisierung. |
| `detail` | Eine für Menschen lesbare Erklärung, die speziell für dieses Auftreten des Problems gilt. Wie `title` kann der Wert dieses Felds lokalisiert werden. |
| `source` | Ein Objekt, das Verweise auf die Quelle des Fehlers enthält, optional einschließlich eines der folgenden Elemente:<ul><li>`pointer`: eine  [JSON Pointer-Zeichenfolge (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) , die auf die verknüpfte Entität im Anfragedokument verweist (z. B.  `/data` für ein Primärdatenobjekt oder  `/data/attributes/title` für ein bestimmtes Attribut).</li></ul> |
| `meta` | Ein Objekt, das nicht standardmäßige Metadaten zum Fehler enthält. |

{style=&quot;table-layout:auto&quot;}

## Fehlerreferenz

In der folgenden Tabelle sind die verschiedenen Fehler aufgeführt, die die API zurückgeben kann.

| Fehlertitel | Beschreibung |
| --- | --- |
| `authentication-failure` | Ihr IMS-Zugriffstoken ist ungültig. Sie können ein neues Zugriffstoken abrufen, indem Sie sich erneut anmelden. Oder bei technischen Konten: Generieren eines neuen JWT und Tauschen durch ein IMS-Zugriffstoken. |
| `connection-refused` | Eine Verbindung zum Server konnte nicht hergestellt werden. |
| `decrypt-bad-passphrase` | Die Daten konnten nicht mit der bereitgestellten Passphrase entschlüsselt werden. |
| `decrypt-failed` | Die Daten konnten nicht mit dem bereitgestellten privaten Schlüssel entschlüsselt werden. Stellen Sie sicher, dass der Schlüssel lokal funktioniert und dass Leerzeichen abgeschnitten wurden. |
| `decrypt-no-data` | Die Daten können nicht ohne privaten Schlüssel entschlüsselt werden. Geben Sie einen verschlüsselten privaten Schlüssel an. |
| `delegate-descriptor-unresolved` | Die Erweiterung enthielt nicht die erwartete Definition dieses Delegate-Deskriptors. Die Erweiterung muss möglicherweise aktualisiert werden. |
| `deleted-resources` | Die Ressourcen, die Sie Ihrer Bibliothek hinzufügen möchten, wurden gelöscht. |
| `environment-in-use` | Eine Umgebung kann jeweils nur einer Bibliothek zugewiesen werden. Option 1 ist die Auswahl einer anderen Umgebung. Option 2 besteht darin, diese Umgebung freizugeben, indem die Bibliothek in eine andere Umgebung verschoben oder die Bibliothek gelöscht wird. |
| `environment-required` | Ihrer Bibliothek muss eine Umgebung zugewiesen sein, bevor Sie einen Build erstellen können. |
| `extension-not-found` | Die Erweiterung, die ein Datenelement oder eine Regelkomponente definiert, ist nicht in der Bibliothek enthalten. Stellen Sie sicher, dass alle erforderlichen Erweiterungen zu Ihrer Bibliothek hinzugefügt wurden. |
| `extension-package-path-error` | Ein in extension.json definierter Pfad wurde falsch erstellt. |
| `extension-package-transform-definition-error` | Sie haben eine ungültige Umwandlung für eine Objekteigenschaft definiert. Für jede Objekteigenschaft kann eine Transformation definiert werden. Dabei muss es sich um eine Dateiumwandlung oder eine Funktionstransformation handeln. |
| `extension-package-zip-error` | Beim Entpacken des ExtensionPackage oder beim Komprimieren der Dateien für die Verteilung ist ein Fehler aufgetreten. |
| `host-in-use` | Ein Host kann nicht gelöscht werden, wenn eine oder mehrere Umgebungen ihn verwenden. |
| `host-required` | Die dieser Bibliothek zugewiesene Umgebung hat keinen gültigen Host. Überprüfen Sie, welche Umgebung Ihrer Bibliothek zugewiesen ist. Weisen Sie dann dieser Umgebung einen gültigen Host zu. |
| `host-type-error` | Nur SFTP-Hosts müssen die Anmeldeinformationen überprüfen, bevor sie verwendet werden können. Daher ist der Vortest nur für diesen Hosttyp verfügbar. |
| `illegal-custom-code-transform` | Sie dürfen die Umwandlung customCode nicht verwenden. Geben Sie eine Funktion oder eine Dateiumwandlung an. |
| `ims-not-authorized` | Bei der Autorisierung Ihres Kontos ist ein unbekannter Fehler aufgetreten. Versuchen Sie es später erneut. |
| `ims-session-error` | Es gibt ein Problem mit der angemeldeten Sitzung. Melden Sie sich bitte ab und melden Sie sich erneut an. |
| `internal-error` | Es ist ein interner Fehler aufgetreten. Warten Sie einige Minuten und versuchen Sie es erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Kundendienst. |
| `invalid-data_element` | Ein ungültiges Datenelement kann einer Bibliothek nicht hinzugefügt werden. |
| `invalid-embed_code` | Entweder handelt es sich um keinen gültigen Einbettungscode oder Sie versuchen, ihn mit einer Entwicklungs- oder Staging-Umgebung zu verknüpfen. Einbettungscodes für das Dynamic Tag Management (DTM) können nur mit Produktionsumgebungen verknüpft werden. |
| `invalid-extension` | Eine ungültige Erweiterung kann einer Bibliothek nicht hinzugefügt werden. |
| `invalid-extension_package_id` | Sie können nur einige der Objekteigenschaften eines Erweiterungspakets ändern. Sie haben versucht, eine der nicht zulässigen zu ändern. |
| `invalid-new-owner-org-id` | Die Organisations-ID, die Sie zugewiesen haben, ist keine gültige Organisations-ID. |
| `invalid-org` | Ihre aktive Organisation hat keinen Zugriff auf die API. Vergewissern Sie sich, dass Sie die richtige Organisation verwenden. |
| `invalid-rule` | Eine ungültige Regel kann einer Bibliothek nicht hinzugefügt werden. |
| `invalid-settings-syntax` | Beim Analysieren der JSON-Einstellungsdatei wurde ein Syntaxfehler festgestellt. |
| `library-file-not-found` | Eine erforderliche Datei, die in extension.json definiert ist, konnte im ZIP-Paket nicht gefunden werden. |
| `minification-error` | Der Code konnte aufgrund eines ungültigen Codes oder ES6-Codes nicht kompiliert werden. |
| `multiple-revisions` | In einer Bibliothek kann nur eine Revision jeder Ressource enthalten sein. |
| `no-available-orgs` | Dieses Benutzerkonto gehört nicht zu einem Produktprofil, das Zugriff auf Tags hat. Verwenden Sie die Admin Console, um diesen Benutzer einem Produktprofil mit Tagrechten hinzuzufügen. |
| `not-authorized` | Dieses Benutzerkonto verfügt nicht über die erforderlichen Berechtigungen, um diese Aktion durchzuführen. |
| `not-found` | Der Datensatz konnte nicht gefunden werden. Überprüfen Sie die ID des Objekts, das Sie abrufen möchten. |
| `not-unique` | Der Name, den Sie verwenden möchten, wird bereits verwendet. Für diese Ressource muss die Eigenschaft &quot;name&quot;eindeutig sein. |
| `public-release-not-authorized` | Die öffentliche Veröffentlichung von Erweiterungen wird von `launch-ext-dev@adobe.com` koordiniert. Weitere Informationen finden Sie im Dokument zu [Releasedateien](../../extension-dev/submit/release.md) . |
| `read-only` | Diese Ressource ist schreibgeschützt und kann nicht geändert werden. |
| `session-timeout` | Die Benutzersitzung ist abgelaufen. Melden Sie sich bitte ab und melden Sie sich erneut an. |
| `sftp-authentication-failed` | Die Authentifizierung für die SFTP-Verbindung schlug fehl. |
| `sftp-connection-timeout` | Die SFTP-Verbindung ist abgelaufen. |
| `sftp-exception` | Bei Verwendung von SFTP zur Verbindung mit dem Server trat eine Ausnahme auf. |
| `sftp-status-exception` | Beim Versuch, mit dem Server zu kommunizieren, trat eine SFTP-Ausnahme auf. |
| `socket-error` | Beim Versuch, mit dem Server zu kommunizieren, wurde ein Socketfehler festgestellt. |
| `ssh-disconnect` | Die SSH-Sitzung wurde getrennt. |
| `timeout-error` | Die Verbindung zum Server ist abgelaufen. |
| `unknown-error` | Es ist ein unerwarteter Fehler aufgetreten. Sie können es später noch einmal versuchen oder die Kundenunterstützung anrufen und erklären, was Sie zu dem Zeitpunkt getan haben, als es passierte. |
| `unsupported-custom-code-language` | Es wurde eine benutzerdefinierte Codesprache bereitgestellt, die nicht unterstützt wird. |
| `upgraded-extension-required` | Nachdem Sie ein Erweiterungs-Upgrade installiert haben, müssen Sie es in alle Bibliotheken einbeziehen, bis das Upgrade zur Produktion erfolgt. Die einzige Ausnahme besteht, wenn die Erweiterung noch nicht veröffentlicht wurde. |
| `upstream-build-required` | Bevor Sie diesen erstellen können, ist ein erfolgreicher Build für die Upstream-Bibliothek erforderlich. |

{style=&quot;table-layout:auto&quot;}
