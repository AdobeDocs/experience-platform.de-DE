---
title: Flow Service-Fehlermeldungen
description: Erfahren Sie mehr über die Fehlermeldungen, die bei Verwendung des Flow Service für Quellen auftreten können.
exl-id: af79c547-25d0-459a-8de7-eb14206a8694
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 100%

---

# Flow Service-Fehlermeldungen

Flow Service wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Platform zu sammeln und zu zentralisieren. Der Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese Quell-Connectoren bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Dieses Dokument enthält einen Katalog mit Fehlermeldungen, Beschreibungen und empfohlenen Lösungen zum Flow Service.

## Interne Validierungsfehler in Flow Service

In der folgenden Tabelle sind Fehler bei der internen Validierung in Flow Service aufgeführt.

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1100-400` | Ungültige Anfrage | Die Anfrage konnte nicht verarbeitet werden. Fehler vom Anbieter des Flusses: Keine Berechtigung für diesen Vorgang. |
| `1101-404` | Ressource nicht gefunden | Die angeforderte Ressource wurde nicht gefunden. Fehler vom Anbieter des Flusses: Die Ressource mit der angegebenen ID ist nicht vorhanden. |
| `1102-500` | Interner Fehler | Ein unbekannter Fehler ist aufgetreten. Bitte erneut versuchen. Wenn das Problem weiterhin besteht, wenden Sie sich bitte an den Kunden-Support. |
| `1103-503` | Dienst nicht verfügbar | Der Dienst ist derzeit nicht verfügbar. Bitte erneut versuchen. Wenn das Problem weiterhin besteht, wenden Sie sich bitte an den Kunden-Support. |
| `1104-504` | Gateway-Zeitüberschreitung | Es ist eine Gateway-Zeitüberschreitung aufgetreten. Bitte erneut versuchen. Wenn das Problem weiterhin besteht, wenden Sie sich bitte an den Kunden-Support. |
| `1400-500` | Interner Fehler | Ein unbekannter Fehler ist aufgetreten. Bitte erneut versuchen. Wenn das Problem weiterhin besteht, wenden Sie sich bitte an den Kunden-Support. |
| `1401-400` | Ungültige Anfrage | Der Limit- und der Anzahl-Parameter können nicht zusammen in derselben Anfrage angegeben werden. Bitte geben Sie entweder nur den Limit- oder nur den Anzahl-Parameter an und versuchen Sie es erneut. |
| `1402-400` | Ungültige Anfrage | Die Aktion „Abschließen“ wird nur für Anbieteranfragen unterstützt. |
| `1403-400` | Kopfzeile fehlt | Die Kopfzeile „If-Match“ fehlt in der Anfrage. Geben Sie bitte die Kopfzeile an und versuchen Sie es erneut. |
| `1404-412` | Version stimmt nicht überein | Die bereitgestellte Version „v1“ stimmt nicht mit der aktuellen Version der Entität „cc01fc2c-0000-0200“ überein. Stellen Sie bitte sicher, dass die bereitgestellte Version mit der aktuellen Version der Entität übereinstimmt, und versuchen Sie es erneut. |
| `1405-400` | Ungültige Anfrage | Der Anfragetext darf nicht null oder leer sein. Geben Sie bitte einen Anfragetext an und versuchen Sie es erneut. |
| `1406-400` | Ungültige Anfrage | Der Untervorgang „Fortschritt“ kann nicht mit anderen Untervorgängen angewendet werden. Aktualisieren Sie bitte die Liste der Untervorgänge und versuchen Sie es erneut. |
| `1407-400` | Ungültige Anfrage | Status fehlgeschlagen kann nicht mit dem `progress`-Untervorgang verwendet werden. Entfernen Sie den `progress`-Untervorgang oder verwenden Sie Status=&#39;inProgress&#39; und versuchen Sie es erneut. |
| `1408-400` | Ungültige Anfrage | Der Prozentwert der abgeschlossenen Vorgänge sollte 100 für die abgeschlossenen oder fehlgeschlagenen Zustände betragen. Bitte aktualisieren Sie den Prozentwert und versuchen Sie es erneut. |
| `1409-400` | Ungültige Anfrage | Der Vorgang „Abschließen“ kann nicht auf den aktuellen Status „Aktiviert-Abschließen“ angewendet werden. Bitte aktualisieren Sie den Vorgang und versuchen Sie es erneut. |
| `1410-400` | Ungültige Anfrage | `State` ist in der Anfrage zur Flusserstellung nicht zulässig. |
| `1411-400` | Ungültige Anfrage | entityId kann nicht abgerufen werden. Ungültige Anfrage mit dem Pfad „baseConnections/123“ empfangen. |
| `1412-400` | Ungültige Anfrage | Ungültige Zuordnungsversion in der Anfrage. Bitte geben Sie die richtige Zuordnungsversion an. |
| `1413-400` | Ungültige Anfrage | Die angegebene Spezifikations-ID ist ungültig. Geben Sie eine gültige Spezifikations-ID ein und versuchen Sie es erneut. |
| `1414-400` | Ungültige Anfrage | Die Verbindungsspezifikation einer Verbindung kann nicht aktualisiert werden. |
| `1415-400` | Ungültige Anfrage | Die Authentifizierungsspezifikation „authConnection“ wurde für die Verbindungsspezifikations-ID ba6e206f-f233-ab16 nicht gefunden. |
| `1416-400` | Ungültige Anfrage | Löschen oder Aktualisieren kann nur bei Verbindung mit aktiviertem, deaktiviertem oder initialisierendem Status angewendet werden. |
| `1417-400` | Ungültige Anfrage | Löschen oder Aktualisieren von Verbindungen im Status `initializing` ist mit UserToken nicht zulässig. |
| `1418-400` | Ungültige Anfrage | Die Basisverbindung mit der ID 35dcaad3-122a-4278 kann nicht gelöscht werden, da sie in mindestens einem Fluss verwendet wird. Bitte stellen Sie sicher, dass entsprechende Flüsse gelöscht werden, bevor Sie eine Basisverbindung löschen. |
| `1419-400` | Ungültige Anfrage | Fehler beim Validieren der Zuordnung mit der ID 45d90285d2d249acb87a72a2f12f7401, Version 0. Dies kann auf unzureichende Berechtigungen für zugeordnete Felder zurückzuführen sein. Bitte überprüfen Sie Ihre Zuordnung oder wenden Sie sich an Ihren Admin. |
| `1420-400` | Ungültige Anfrage | Der aktuelle Status der Deaktivierung kann nicht aktualisiert werden. |
| `1421-400` | Ungültige Anfrage | Die aktuelle Statusaktualisierung kann nicht geändert werden. |
| `1422-400` | Ungültige Anfrage | Die Aktion „Deaktivieren“ kann nicht auf den aktuellen Status {state} angewendet werden. Bitte aktualisieren Sie die Aktion und versuchen Sie es erneut. |
| `1423-400` | Ungültige Anfrage | In ConnectionSpecFiltering wurde ein unbehandeltes Feld „baseSpec“ angegeben. Bitte aktualisieren Sie das Feld {field} und versuchen Sie es erneut. |
| `1424-400` | Ungültige Anfrage | OrderBy wird bei Cross-Sandbox-Abfragen nicht unterstützt. |
| `1425-400` | Ungültige Anfrage | Fehler beim Abgleich des Schemas im Zieldatensatz 64ef1a3c0ef mit dem Schema in der Zuordnung 91ac5a2c0eb. Das Schema mit derselben ID und Version muss sowohl in der Zuordnung als auch im Zieldatensatz verwendet werden. |
| `1426-400` | Ungültige Anfrage | Das Benutzer-Token ist nicht berechtigt, die Verbindungsspezifikation zu erstellen bzw. zu aktualisieren. Bitte stellen Sie sicher, dass das Benutzer-Token berechtigt ist, und versuchen Sie es erneut. |
| `1427-400` | Ungültige Anfrage | Das Benutzer-Token ist nicht berechtigt, Flussausführungen zu erstellen bzw. zu aktualisieren. Bitte stellen Sie sicher, dass das Benutzer-Token berechtigt ist, und versuchen Sie es erneut. |
| `1428-400` | Ungültige Anfrage | Vorgängerflussausführung nicht mit ID aa6a206f-f233-4c2d gefunden. |
| `1429-400` | Ungültige Anfrage | Vorgängerfluss nicht mit ID aa6a206f-f233-4c2d gefunden. |
| `1430-400` | Ungültige Anfrage | Fluss mit der ID aa6a206f-f233-4c2d nicht gefunden. |
| `1431-400` | Ungültige Anfrage | Ein leeres Array „fields“ ist in der Richtlinie nicht erlaubt. |
| `1432-400` | Ungültige Anfrage | Die angegebene Sortierreihenfolge ist nicht korrekt. Stellen Sie im Feldnamen „+“ für aufsteigende Reihenfolge und „-“ für absteigende Reihenfolge vor. |
| `1433-400` | Ungültige Anfrage | Falsches Feld= #id, das in „orderBy“ übergeben wird, z. B. +name, -name, name. |
| `1434-400` | Ungültige Anfrage | Nicht unterstützter Vorgang „move“ empfangen. Bitte verwenden Sie einen der unterstützten Vorgangstypen und versuchen Sie es erneut. |
| `1435-400` | Ungültige Anfrage | Nicht unterstützte Unteraktion „reverse“ wurde empfangen. Bitte verwenden Sie einen der unterstützten Unteraktionstypen und versuchen Sie es erneut. |
| `1436-400` | Ungültige Anfrage | Nicht unterstützter Untervorgang FORTSCHRITT wurde für Vorgang „Aktivieren“ empfangen. |
| `1437-400` | Ungültige Anfrage | Der nicht unterstützte Statuswert „started“ wurde empfangen. Bitte aktualisieren Sie den Statuswert und versuchen Sie es erneut. |
| `1438-400` | Ungültige Anfrage | Nicht unterstützter Aggregatvorgang „average“ empfangen. |
| `1439-400` | Ressource nicht gefunden | Die angeforderte Flüsse-Ressource 3f4ae131-b384-4e73 wurde nicht gefunden. Überprüfen Sie die Ressourcen-ID, bevor Sie es erneut versuchen. |
| `1440-400` | Ungültige Anfrage | Operator „~“ wurde nicht implementiert. |
| `1441-400` | Ungültige Anfrage | Aggregatfunktion „average“ nicht implementiert. |
| `1442-400` | Ungültige Anfrage | Aggregation ist für Feld-ID nicht zulässig. |
| `1443-400` | Ungültige Anfrage | Der Operator „&lt;=“ ist für mehrere Werte nicht zulässig. |
| `1444-400` | Ungültige Anfrage | Der Fluss 3f4ae131-b384-4e73 befindet sich nicht im erwarteten Status „Ausstehend“. |
| `1445-400` | Ungültige Anfrage | PATCH-Verbindungsfunktion nicht aktiviert. |
| `1446-400` | Ungültige Anfrage | Die Fluss-ID darf nicht null oder leer sein. Bitte aktualisieren Sie die Fluss-ID und versuchen Sie es erneut. |
| `1447-400` | Ungültige Anfrage | Es wurden aktive Flüsse mit der ID aa6a206f-f233-4c2d gefunden. |
| `1448-400` | Ungültige Anfrage | Operator „>=“ für Feld-ID nicht unterstützt. |
| `1449-400` | Ungültige Anfrage | Ungültige Feldverbindungen in Filterparametern. |
| `1450-400` | Ungültige Anfrage | Ungültiger Operator „!>“ in Filterparametern. |
| `1451-400` | Ungültige Anfrage | Ungültige Parameter „testParam“ in Abfrageparametern angegeben. |
| `1452-400` | Ungültige Anfrage | Ungültiger Wert 1676643256,1676643210 für das Feld „createdAt“. |
| `1453-400` | Ungültige Anfrage | Ungültiger Abfragewert „createdAt==“ im Abfrageparameter angegeben. |
| `1454-400` | Ungültige Anfrage | Unverarbeiteter Filterwerttyp angegeben. |
| `1455-400` | Ungültige Anfrage | Beim Validieren der Patch-Anweisungen ist ein Fehler aufgetreten: Fehlendes Feld „keyWhatDoesNotExist“. |
| `1456-400` | Ungültige Anfrage | Der Status „Löschen-Abschließen“ ist kein gültiger Wert. Zulässige Werte sind [aktiviert, deaktiviert, initialisieren]. |
| `1457-400` | Ungültige Anfrage | Der Vorgang „Aktualisieren“ kann nicht im Status „Löschen-Abschließen“ angewendet werden. |
| `1458-400` | Ungültige Anfrage | Der Vorgang „Löschen“ kann nicht im Status „Löschen-Abschließen“ angewendet werden. |

{style="table-layout:auto"}


## Verifizierungsfehler des Benutzer-Tokens zur Autorisierung

In der folgenden Tabelle sind Fehler bei der Verifizierung des Benutzer-Tokens zur Autorisierung aufgeführt

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `2000-401` | Ungültiges Autorisierungs-Token | Das Autorisierungs-Token hat keinen Zugriff auf diese Organisation oder die Organisation existiert nicht. Bitte sicherstellen, dass die Organisation vorhanden ist, oder Admin kontaktieren, um Zugriff zu erhalten. |
| `2001-401` | Kopfzeile fehlt oder ist leer | Die Kopfzeile „x-gw-ims-org-id“ fehlt oder ist leer. Bitte den Wert der Kopfzeile aktualisieren und erneut versuchen. |
| `2002-401` | Kopfzeile fehlt | Die Kopfzeile „x-gw-ims-org-id“ fehlt in der Anfrage. Bitte den Wert der Kopfzeile aktualisieren und erneut versuchen. |
| `2100-404` | Sandbox nicht gefunden | Die Sandbox mit dem Namen „dev“ konnte nicht gefunden werden. Stellen Sie bitte sicher, dass der Sandbox-Name korrekt ist, und versuchen Sie es erneut. |
| `2101-404` | Sandbox nicht gefunden | Die Sandbox mit dem Namen „dev“ konnte nicht gefunden werden. Fehler in Sandbox Management-API: Sandbox mit dem Namen „dev“ nicht vorhanden. Bitte überprüfen Sie, ob die Ressource vorhanden ist. |
| `2102-500` | Sandbox nach Namensfehler abrufen | Es gab ein Problem beim Abrufen einer Sandbox mit dem Namen „dev“. Fehler in der Sandbox-Management-API: Etwas ist schiefgelaufen. Bitte erneut versuchen. |
| `2103-404` | Sandbox nicht gefunden | Die Sandbox mit der ID „8da3ef09-b469-404a“ und dem Namen „dev“ wurde nicht gefunden. Stellen Sie bitte sicher, dass die ID- und Sandbox-Namenswerte korrekt sind, und versuchen Sie es erneut. |
| `2104-500` | Fehler beim Abrufen der Sandbox nach Kennung | Es gab ein Problem beim Abrufen einer Sandbox mit der ID „8da3ef09-b469-404a“ und dem Namen „dev“. Fehler in der Sandbox-Management-API: Etwas ist schiefgelaufen. Bitte erneut versuchen. |
| `2105-400` | Kopfzeile fehlt | Die Kopfzeile „x-sandbox-name“ fehlt in der Anfrage. Bitte fügen Sie in der Anfrage die Kopfzeile hinzu und versuchen Sie es erneut. |
| `2106-404` | Fehler beim Abrufen der Standard-Sandbox | Die standardmäßigen Sandbox-Informationen wurden nicht gefunden. |
| `2107-500` | Fehler beim Abrufen der Standard-Sandbox | Beim Abrufen einer Standard-Sandbox ist ein Problem aufgetreten. Fehler in der Sandbox-Management-API: Etwas ist schiefgelaufen. Bitte erneut versuchen. |
| `2108-500` | Fehler beim Abrufen aktiver Sandboxes | Beim Abrufen einer aktiven Sandbox ist ein Problem aufgetreten. Fehler in der Sandbox-Management-API: Etwas ist schiefgelaufen. Bitte erneut versuchen. |
| `2110-400` | Kopfzeilen nicht zulässig | Die Kopfzeile „x-sandbox-id“ ist mit dem Benutzer-Token nicht zulässig. Bitte aktualisieren Sie die Kopfzeile und versuchen Sie es erneut. |
| `2111-403` | Kopfzeilen mit eingeschränktem Wert | Die Kopfzeile „x-sandbox-name“ mit dem Wert „*“ ist mit dem Benutzer-Token eingeschränkt. Bitte aktualisieren Sie die Kopfzeile und den Wert und versuchen Sie es erneut. |
| `2112-400` | Kopfzeilen mit einem anderem Wert sind nicht zulässig | Die Kopfzeilen „x-sandbox-name“ und „x-sandbox-id“ müssen für eine Sandbox-übergreifende Abfrage den Wert „*“ aufweisen. Aktualisieren Sie die Kopfzeilen und versuchen Sie es erneut. |
| `2113-400` | Kopfzeilen mit Wert nicht zulässig | Die Kopfzeilen „x-sandbox-id“ und „x-sandbox-name“ mit dem Wert „*“ sind für die Anfrage nicht zulässig. Aktualisieren Sie die Kopfzeilen und versuchen Sie es erneut. |
| `2114-400` | Leeres Token | Leeres Token angegeben. Geben Sie ein Token an und versuchen Sie es erneut. |
| `2115-400` | Ungültiges Token | Ungültiges Token angegeben. Bitte geben Sie ein gültiges Token an und versuchen Sie es erneut. |
| `2116-500` | Interner Fehler | Ein interner Fehler ist während der Offline-Decodierung des Bearer-Tokens für die Bereichsauflösung aufgetreten. |
| `2117-500` | Interner Fehler | Beim Überprüfen der Berechtigungen für den Benutzer ist ein interner Fehler aufgetreten. Bitte erneut versuchen. Wenn das Problem weiterhin besteht, wenden Sie sich bitte an den Kunden-Support. |
| `2118-403` | Fehlende Berechtigung | Die Schreibberechtigung fehlt. Bitte kontaktieren Sie Ihren Administrator, um die Berechtigungen zu klären, und versuchen Sie es erneut. |
| `2119-400` | Abfrageparameter fehlt | Der Anfragekontext enthält nicht den erforderlichen Abfrageparameter „specId“. Bitte geben Sie den fehlenden Abfrageparameter an und versuchen Sie es erneut. |
| `2120-403` | Verboten | Sie verfügen nicht über ausreichende Berechtigungen zum Ausführen des Vorgangs. Bitte kontaktieren Sie Ihren Administrator, um die Berechtigungen zu klären, und versuchen Sie es erneut. |
| `2121-403` | Verboten | Die Berechtigungsverwaltung wird für die Ressource „Enterprise Source“ verweigert. Bitte kontaktieren Sie Ihren Administrator, um die Berechtigungen zu klären, und versuchen Sie es erneut. |
| `2200-500` | Fehler bei Anfrage für externen Dienst | Beim Aufrufen des Katalog-Services zur Validierung des Schemas ist ein Problem aufgetreten. |
| `2250-500` | Fehler bei Anfrage für externen Dienst | Beim Aufrufen des Datenvorbereitungs-Services zum Überprüfen der Zuordnung ist ein Problem aufgetreten. |

{style="table-layout:auto"}
