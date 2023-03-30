---
title: Flussdienst-Fehlermeldungen
description: Erfahren Sie mehr über die Fehlermeldungen, die bei Verwendung des Flow Service für Quellen auftreten können.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 5%

---

# Flussdienstfehlermeldungen

Mit Flow Service können Kundendaten aus verschiedenen Quellen innerhalb von Platform erfasst und zentralisiert werden. Der Service bietet eine Benutzeroberfläche und eine RESTful-API, mit der Sie auf einfache Weise Quellverbindungen zu verschiedenen Datenanbietern einrichten können. Diese sogenannten „Quell-Connectoren“ bieten eine Schnittstelle zur Authentifizierung bei Systemen von Drittanbietern und ermöglichen die Einrichtung von Zeitplänen für die Datenaufnahme sowie die Steuerung des Aufnahmedurchsatzes.

Dieses Dokument enthält einen Katalog mit Fehlermeldungen, Beschreibungen und empfohlenen Lösungen zum Flow Service.

## Interne Validierungsfehler im Flussdienst

In der folgenden Tabelle sind Fehler bei der internen Validierung in Flow Service aufgeführt.

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1100-400` | Ungültige Anfrage | Die Anfrage konnte nicht verarbeitet werden. Fehler beim Flussanbieter: Kein Anspruch auf diesen Vorgang. |
| `1101-404` | Ressource nicht gefunden | Die angeforderte Ressource wurde nicht gefunden. Fehler beim Flussanbieter: Die Ressource mit der angegebenen ID ist nicht vorhanden. |
| `1102-500` | Interner Fehler | Es ist ein interner Fehler aufgetreten. Bitte versuchen Sie es erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Support. |
| `1103-503` | Dienst nicht verfügbar | Der Dienst ist vorübergehend nicht verfügbar. Bitte versuchen Sie es erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Support. |
| `1104-504` | Gateway-Zeitüberschreitung | Es ist ein Gateway-Timeout aufgetreten. Bitte versuchen Sie es erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Support. |
| `1400-500` | Interner Fehler | Es ist ein interner Fehler aufgetreten. Bitte versuchen Sie es erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Support. |
| `1401-400` | Ungültige Anfrage | Die Parameter limit und count können nicht in derselben Anfrage zusammen angegeben werden. Geben Sie entweder nur den Grenzwert oder den Zählerparameter an und versuchen Sie es erneut. |
| `1402-400` | Ungültige Anfrage | Die Aktion &quot;Finalize&quot;wird nur für Provider-Anforderungen unterstützt. |
| `1403-400` | Kopfzeile fehlt | Die Kopfzeile &quot;If-Match&quot;fehlt in der Anfrage. Geben Sie die Kopfzeile an und versuchen Sie es erneut. |
| `1404-412` | Version stimmt nicht überein | Die bereitgestellte Version &quot;v1&quot;stimmt nicht mit der aktuellen Version der Entität &quot;cc01fc2c-0000-0200&quot;überein. Stellen Sie sicher, dass die bereitgestellte Version mit der aktuellen Version auf der Entität übereinstimmt, und versuchen Sie es erneut. |
| `1405-400` | Ungültige Anfrage | Der Anfrageinhalt darf nicht null oder leer sein. Geben Sie einen Anfragetext an und versuchen Sie es erneut. |
| `1406-400` | Ungültige Anfrage | Der Untervorgang &quot;progress&quot;kann nicht mit anderen Untervorgängen angewendet werden. Aktualisieren Sie die Liste der Unteroperationen und versuchen Sie es erneut. |
| `1407-400` | Ungültige Anfrage | Der Status fehlgeschlagen kann nicht mit der Variablen `progress` subOp. Entfernen Sie die `progress` subOp oder verwenden Sie den Status=&#39;inProgress&#39; und versuchen Sie es erneut. |
| `1408-400` | Ungültige Anfrage | Der prozentuale Anteil der ausgefüllten Werte sollte für die abgeschlossenen oder fehlgeschlagenen Status 100 betragen. Bitte aktualisieren Sie die Anzahl der ausgefüllten Datensätze und versuchen Sie es erneut. |
| `1409-400` | Ungültige Anfrage | Der Vorgang &quot;finalize&quot;kann nicht auf die aktuelle Status-Aktivierung angewendet werden. Aktualisieren Sie den Vorgang und versuchen Sie es erneut. |
| `1410-400` | Ungültige Anfrage | `State` ist in der Workflow-Anfrage zum Erstellen nicht zulässig. |
| `1411-400` | Ungültige Anfrage | entityId kann nicht abgerufen werden. Ungültige Anfrage mit dem Pfad &#39;baseConnections/123&#39; empfangen. |
| `1412-400` | Ungültige Anfrage | Ungültige Zuordnungsversion in Anfrage. Bitte geben Sie die korrekte Zuordnungsversion an. |
| `1413-400` | Ungültige Anfrage | Die angegebene Spezial-ID ist ungültig. Geben Sie eine gültige Spezifikations-ID ein und versuchen Sie es erneut. |
| `1414-400` | Ungültige Anfrage | Die Verbindungsspezifikation einer Verbindung kann nicht aktualisiert werden. |
| `1415-400` | Ungültige Anfrage | Die auth spec &#39;authConnection&#39; konnte für die Verbindungsspezifikations-ID ba6e206f-f233-ab16 nicht gefunden werden. |
| `1416-400` | Ungültige Anfrage | Löschen oder Aktualisieren kann nur bei Verbindung mit aktiviertem, deaktiviertem oder initialisierendem Status angewendet werden. |
| `1417-400` | Ungültige Anfrage | Löschen oder Aktualisieren von Verbindungen in `initializing` -Status sind bei UserToken nicht zulässig. |
| `1418-400` | Ungültige Anfrage | Die Basisverbindung mit der ID 35dcaad3-122a-4278 kann nicht gelöscht werden, da die Basisverbindung in einem oder mehreren Flüssen verwendet wird. Stellen Sie sicher, dass die entsprechenden Flüsse gelöscht werden, bevor Sie eine Basisverbindung löschen. |
| `1419-400` | Ungültige Anfrage | Fehler beim Validieren der Zuordnung mit der ID 45d90285d2d249acb87a72a2f12f7401, Version 0. Dies kann an unzureichenden Berechtigungen für zugeordnete Felder liegen. Überprüfen Sie Ihr Mapping oder kontaktieren Sie Ihren Administrator. |
| `1420-400` | Ungültige Anfrage | Die aktuelle Status-Deaktivierung kann nicht aktualisiert werden. |
| `1421-400` | Ungültige Anfrage | Die aktuelle Statusaktualisierung kann nicht geändert werden. |
| `1422-400` | Ungültige Anfrage | Die Aktionsdeaktiviert kann nicht auf den aktuellen Status {state} angewendet werden. Aktualisieren Sie die Aktion und versuchen Sie es erneut. |
| `1423-400` | Ungültige Anfrage | In ConnectionSpecFiltering wurde ein unbehandeltes Feld baseSpec bereitgestellt. Aktualisieren Sie das Feld {field} und versuchen Sie es erneut. |
| `1424-400` | Ungültige Anfrage | OrderBy wird bei Cross-Sandbox-Abfragen nicht unterstützt. |
| `1425-400` | Ungültige Anfrage | Fehler beim Abgleich des Schemas im Zieldatensatz 64ef1a3c0ef mit dem Schema in der Zuordnung 91ac5a2c0eb. Das Schema mit derselben ID und Version muss sowohl in der Zuordnung als auch im Zieldatensatz verwendet werden. |
| `1426-400` | Ungültige Anfrage | Das Benutzer-Token ist nicht berechtigt, die Verbindungsspezifikation zu erstellen/zu aktualisieren. Stellen Sie sicher, dass das Benutzer-Token autorisiert ist, und versuchen Sie es erneut. |
| `1427-400` | Ungültige Anfrage | Das Benutzer-Token ist nicht berechtigt, Fluss-Läufe zu erstellen/zu aktualisieren. Stellen Sie sicher, dass das Benutzer-Token autorisiert ist, und versuchen Sie es erneut. |
| `1428-400` | Ungültige Anfrage | Vorgängerfluss wird nicht mit id aa6a206f-f233-4c2d gefunden. |
| `1429-400` | Ungültige Anfrage | Vorgängerfluss mit id aa6a206f-f233-4c2d nicht gefunden. |
| `1430-400` | Ungültige Anfrage | Fluss mit der ID aa6a206f-f233-4c2d nicht gefunden. |
| `1431-400` | Ungültige Anfrage | Leeres Array &quot;fields&quot;ist in der Richtlinie nicht zulässig. |
| `1432-400` | Ungültige Anfrage | Die angegebene Sortierreihenfolge ist nicht korrekt. Setzen Sie das Präfix + für aufsteigende Reihenfolge und - für absteigende Reihenfolge im fieldName. |
| `1433-400` | Ungültige Anfrage | Falsches Feld= #id, das in orderBy übergeben wird, z. B. +name, -name, name. |
| `1434-400` | Ungültige Anfrage | Nicht unterstützter Vorgang &quot;Verschieben&quot;empfangen. Verwenden Sie einen der unterstützten Vorgangstypen und versuchen Sie es erneut. |
| `1435-400` | Ungültige Anfrage | Nicht unterstützte Unteraktion &quot;Reverse&quot;wurde empfangen. Bitte verwenden Sie einen der unterstützten Unteraktionstypen und versuchen Sie es erneut. |
| `1436-400` | Ungültige Anfrage | Nicht unterstützte Unteroperation Die Aktivierung von PROGRESS, das für den Betrieb empfangen wurde. |
| `1437-400` | Ungültige Anfrage | Der nicht unterstützte Statuswert &#39;started&#39; wurde empfangen. Aktualisieren Sie den Statuswert und versuchen Sie es erneut. |
| `1438-400` | Ungültige Anfrage | Nicht unterstützte Aggregat-Operation &quot;Durchschnitt&quot;empfangen. |
| `1439-400` | Ressource nicht gefunden | Die angeforderte Flüsse-Ressource 3f4ae131-b384-4e73 wurde nicht gefunden. Überprüfen Sie die Ressourcen-ID, bevor Sie es erneut versuchen. |
| `1440-400` | Ungültige Anfrage | Operator &quot;~&quot;wurde nicht implementiert. |
| `1441-400` | Ungültige Anfrage | Aggregatfunktion &quot;Durchschnitt&quot;nicht implementiert. |
| `1442-400` | Ungültige Anfrage | Aggregation ist für Feld-ID nicht zulässig. |
| `1443-400` | Ungültige Anfrage | Der Operator &#39;&lt;=&#39; ist für mehrere Werte nicht zulässig. |
| `1444-400` | Ungültige Anfrage | Der Fluss 3f4ae131-b384-4e73 befindet sich nicht im erwarteten Status ausstehend. |
| `1445-400` | Ungültige Anfrage | PATCH-Verbindungsfunktion nicht aktiviert. |
| `1446-400` | Ungültige Anfrage | Die Fluss-ID darf nicht null oder leer sein. Aktualisieren Sie die Fluss-ID und versuchen Sie es erneut. |
| `1447-400` | Ungültige Anfrage | Es wurden aktive Flüsse mit der ID aa6a206f-f233-4c2d gefunden. |
| `1448-400` | Ungültige Anfrage | Operator >= für Feld-ID nicht unterstützt. |
| `1449-400` | Ungültige Anfrage | Ungültige Feldverbindungen in Filterparametern. |
| `1450-400` | Ungültige Anfrage | Ungültiger Operator !> in Filterparametern. |
| `1451-400` | Ungültige Anfrage | Ungültige params testParam in Abfrageparametern bereitgestellt. |
| `1452-400` | Ungültige Anfrage | Ungültiger Wert 1676643256,1676643210 für das Feld createdAt. |
| `1453-400` | Ungültige Anfrage | Ungültiger Abfragewert createdAt== wird im Abfrageparameter bereitgestellt. |
| `1454-400` | Ungültige Anfrage | Unbehandelter Filterwerttyp bereitgestellt. |
| `1455-400` | Ungültige Anfrage | Beim Überprüfen der Patch-Anweisungen ist ein Fehler aufgetreten: Fehlendes Feld &quot;keyWhatDoesNotExist&quot;. |
| `1456-400` | Ungültige Anfrage | Das Löschen und Fertigstellen von Status ist kein gültiger Wert. Zulässige Werte sind [aktiviert, deaktiviert, initialisieren]. |
| `1457-400` | Ungültige Anfrage | Die Aktualisierung von Vorgängen kann nicht bei der Fertigstellung der Statuslöschung angewendet werden. |
| `1458-400` | Ungültige Anfrage | Das Löschen von Vorgängen kann nicht bei der Fertigstellung des Status angewendet werden. |

{style="table-layout:auto"}


## Überprüfungsfehler des Benutzer-Tokens zur Autorisierung

In der folgenden Tabelle sind Fehler bei der Überprüfung des Benutzer-Tokens zur Autorisierung aufgeführt

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `2000-401` | Ungültiges Autorisierungstoken | Das Autorisierungstoken hat keinen Zugriff auf diese Organisation oder die Organisation existiert nicht. Stellen Sie sicher, dass die Organisation vorhanden ist, oder kontaktieren Sie Ihren Administrator, um Zugriff zu erhalten. |
| `2001-401` | Kopfzeile fehlt oder leer | Die Kopfzeile x-gw-ims-org-id fehlt oder ist leer. Aktualisieren Sie den Header-Wert und versuchen Sie es erneut. |
| `2002-401` | Kopfzeile fehlt | Die Kopfzeile x-gw-ims-org-id fehlt in der Anfrage. Aktualisieren Sie den Header-Wert und versuchen Sie es erneut. |
| `2100-404` | Sandbox nicht gefunden | Die Sandbox mit dem Namen &quot;dev&quot;konnte nicht gefunden werden. Vergewissern Sie sich, dass der Sandbox-Name korrekt ist, und versuchen Sie es erneut. |
| `2101-404` | Sandbox nicht gefunden | Die Sandbox mit dem Namen &quot;dev&quot;konnte nicht gefunden werden. Fehler bei der Sandbox Management-API: Sandbox mit dem Namen &quot;dev&quot;nicht vorhanden. Überprüfen Sie, ob die Ressource vorhanden ist. |
| `2102-500` | Sandbox nach Namensfehler abrufen | Es gab ein Problem beim Abrufen einer Sandbox mit dem Namen &quot;dev&quot;. Fehler bei der Sandbox Management-API: Etwas ist schiefgelaufen. Bitte versuchen Sie es erneut. |
| `2103-404` | Sandbox nicht gefunden | Die Sandbox mit der ID 8da3ef09-b469-404a und dem Namen dev konnte nicht gefunden werden. Vergewissern Sie sich, dass die ID- und Sandbox-Namenswerte korrekt sind, und versuchen Sie es erneut. |
| `2104-500` | Sandbox anhand eines ID-Fehlers abrufen | Es gab ein Problem beim Abrufen einer Sandbox mit der ID &#39;8da3ef09-b469-404a&#39; und dem Namen &#39;dev&#39;. Fehler bei der Sandbox Management-API: Etwas ist schiefgelaufen. Bitte versuchen Sie es erneut. |
| `2105-400` | Kopfzeile fehlt | Der Header x-sandbox-name fehlt in der Anfrage. Fügen Sie den Header in die Anfrage ein und versuchen Sie es erneut. |
| `2106-404` | Standard-Sandbox-Fehler abrufen | Die standardmäßigen Sandbox-Informationen konnten nicht gefunden werden. |
| `2107-500` | Standard-Sandbox-Fehler abrufen | Beim Abrufen einer Standard-Sandbox trat ein Problem auf. Fehler bei der Sandbox Management-API: Etwas ist schiefgelaufen. Bitte versuchen Sie es erneut. |
| `2108-500` | Fehler &quot;Aktive Sandboxes abrufen&quot; | Beim Abrufen einer aktiven Sandbox trat ein Problem auf. Fehler bei der Sandbox Management-API: Etwas ist schiefgelaufen. Bitte versuchen Sie es erneut. |
| `2110-400` | Kopfzeilen nicht zulässig | Die Header x-sandbox-id ist mit dem Benutzer-Token nicht zulässig. Bitte aktualisieren Sie die Kopfzeile und versuchen Sie es erneut. |
| `2111-403` | Kopfzeilen mit eingeschränktem Wert | Die Kopfzeile x-sandbox-name mit dem Wert * ist mit dem Benutzer-Token eingeschränkt. Bitte aktualisieren Sie die Kopfzeile und den Wert und versuchen Sie es erneut. |
| `2112-400` | Header mit anderem Wert sind nicht zulässig | Die Header x-sandbox-name und x-sandbox-id müssen für eine Sandbox-übergreifende Abfrage den Wert * aufweisen. Aktualisieren Sie die Header und versuchen Sie es erneut. |
| `2113-400` | Header mit Wert nicht zulässig | Die Header x-sandbox-id und x-sandbox-name mit dem Wert * sind für die Anfrage nicht zulässig. Aktualisieren Sie die Header und versuchen Sie es erneut. |
| `2114-400` | Leeres Token | Leeres Token bereitgestellt. Geben Sie ein Token an und versuchen Sie es erneut. |
| `2115-400` | Ungültiges Token | Ungültiges Token bereitgestellt. Geben Sie ein gültiges Token ein und versuchen Sie es erneut. |
| `2116-500` | Interner Fehler | Während der Offline-Dekodierung des Trägertokens für die Perimeterauflösung ist ein interner Fehler aufgetreten. |
| `2117-500` | Interner Fehler | Beim Überprüfen der Berechtigungen für den Benutzer ist ein interner Fehler aufgetreten. Bitte versuchen Sie es erneut. Wenn das Problem weiterhin besteht, wenden Sie sich an den Support. |
| `2118-403` | Fehlende Berechtigung | Das Berechtigungsschreiben fehlt. Wenden Sie sich an Ihren Administrator, um die Berechtigungen zu beheben und es erneut zu versuchen. |
| `2119-400` | Abfrageparameter fehlt | Der Anfragekontext enthält nicht den erforderlichen Abfrageparameter specId. Geben Sie den fehlenden Abfrageparameter an und versuchen Sie es erneut. |
| `2120-403` | Verboten | Sie verfügen nicht über ausreichende Berechtigungen zum Ausführen des Vorgangs. Wenden Sie sich an Ihren Administrator, um die Berechtigungen zu beheben und es erneut zu versuchen. |
| `2121-403` | Verboten | Die Berechtigungsverwaltung wird für die Ressource Enterprise Source verweigert. Wenden Sie sich an Ihren Administrator, um die Berechtigungen zu beheben und es erneut zu versuchen. |
| `2200-500` | Fehler bei Anforderung für externen Dienst | Beim Aufrufen des Catalog-Dienstes zur Validierung des Schemas trat ein Problem auf. |
| `2250-500` | Fehler bei Anforderung für externen Dienst | Beim Aufrufen des Data Prep-Dienstes für die Validierung der Zuordnung trat ein Problem auf. |

{style="table-layout:auto"}
