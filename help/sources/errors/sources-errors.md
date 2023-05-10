---
title: Quellen-Fehlermeldungen
description: Erfahren Sie mehr über die Fehlermeldungen, die bei Verwendung des Flow Service für Quellen auftreten können.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 100%

---

# Quellen-Fehlermeldungen

Dieses Dokument enthält einen Katalog mit Fehlermeldungen, Beschreibungen und empfohlenen Lösungen für Quellen.

## Allgemeine Fehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1000-400` | Ungültige Anfrage | Die Anfrage ist ungültig. Bitte die Anfrage überprüfen und erneut versuchen. |
| `1001-401` | Nicht autorisiert | Die Benutzerin bzw. der Benutzer ist nicht autorisiert. Bitte Admin kontaktieren, um Zugriff auf die Ressource zu erhalten. |
| `1002-403` | Verboten | Der angeforderte Vorgang ist verboten. Bitte den angeforderten Vorgang überprüfen und erneut versuchen. |
| `1003-404` | Ressource nicht gefunden | Die angeforderte Ressource wurde nicht gefunden. Bitte die angegebene Anfrage überprüfen und erneut versuchen. |
| `1004-415` | Nicht unterstützter Medientyp | Das angegebene Payload-Format wird nicht unterstützt. Bitte die angegebene Anfrage überprüfen und erneut versuchen. |
| `1005-500` | Interner Fehler | Ein unbekannter Fehler ist aufgetreten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1006-408` | Zeitüberschreitung der Anfrage | Bei der Verarbeitung der Anfrage ist ein Fehler aufgetreten. Die Zeit für die Anfrage wurde überschritten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1007-400` | Ungültiger Kopfzeilenparameter | Ein ungültiger Kopfzeilenparameter: {headerName} wurde empfangen. Bitte die Kopfzeilenparameter überprüfen und erneut versuchen. |
| `1008-401` |  | Ungültiges Autorisierungs-Token | Das Autorisierungs-Token hat keinen Zugriff auf diese Organisation oder die Organisation existiert nicht. Bitte sicherstellen, dass die Organisation vorhanden ist, oder Admin kontaktieren, um Zugriff zu erhalten. |
| `1009-403` | Die IMS-Organisations-ID fehlt oder ist leer | Die Anfragekopfzeile für die Organisations-ID fehlt oder ist leer. Bitte den Wert der Kopfzeile aktualisieren und erneut versuchen. |
| `1010-500` | Ungültige detaillierte Nachricht | Der Parameter in der detaillierten Nachricht wurde nicht ordnungsgemäß angegeben. Bitte den Parameter in der detaillierten Nachricht überprüfen und erneut versuchen. |
| `1011-503` | Dienst nicht verfügbar | Der Dienst ist derzeit nicht verfügbar. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1012-504` | Gateway-Zeitüberschreitung | Es ist eine Gateway-Zeitüberschreitung aufgetreten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1013-412` | Vorbedingung fehlgeschlagen | Die von den Kopfzeilen „If-Unmodified-Since“ oder „If-None-Match“ definierte Bedingung ist nicht erfüllt. Bitte überprüfen und erneut versuchen. |
| `1014-400` | Ungültige Anfrage – unzulässiges Argument | Die Anfrage konnte nicht verarbeitet werden. {detailsMessage} |

## Framework-Fehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1100-400` | Ungültige Anfrage | Die Anfrage konnte nicht verarbeitet werden. {detailsMessage} |
| `1101-500` | Interner Fehler | Ein unbekannter Fehler ist aufgetreten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1102-404` | Ressource nicht gefunden | Die angeforderte Ressource wurde nicht gefunden. {detailsMessage} |
| `1103-503` | Dienst nicht verfügbar | Der Dienst ist derzeit nicht verfügbar. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1104-504` | Gateway-Zeitüberschreitung | Es ist eine Gateway-Zeitüberschreitung aufgetreten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1105-401` | Nicht autorisiert | Die Benutzerin bzw. der Benutzer ist nicht autorisiert. {detailsMessage} |
| `1106-403` | Verboten | Der angeforderte Vorgang ist verboten. {detailsMessage} |
| `1107-412` | Vorbedingung fehlgeschlagen | Die von den Kopfzeilen „If-Unmodified-Since“ oder „If-None-Match“ definierte Bedingung ist nicht erfüllt. {detailsMessage} |

## Verschlüsselungsfehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1200-500` | Interner Fehler | Ein unbekannter Fehler ist aufgetreten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1201-400` | Ungültige Anfrage | Die flowId darf nicht null oder leer sein. Bitte in der Anfrage eine gültige flowId angeben und erneut versuchen. |
| `1202-400` | Ungültige Anfrage | Die publicKeyId fehlt in den Transformationen {transformations} des Flusses. Bitte die publicKeyId in der Anfrage angeben und erneut versuchen. |
| `1203-400` | Ungültige Anfrage | Der Verschlüsselungsschlüssel ist nicht für keyID {keyID} in den Transformationen {transformations} des Flusses vorhanden. Bitte die angegebene keyID überprüfen und erneut versuchen. |
| `1204-400` | Ungültige Anfrage | Der angegebene Verschlüsselungsalgorithmus ist ungültig. Bitte einen gültigen Verschlüsselungsalgorithmus angeben und erneut versuchen. |
| `1205-400` | Ungültige Anfrage | Die Passphrase fehlt im Abschnitt „params“ in der angegebenen Anfrage. Bitte die Passphrase unter „params“ eingeben und erneut versuchen. |

## REST-API-Fehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1300-400` | Ungültige Anfrage | Die Patch-Verbindungsanforderung wird für den {connectorType}-Connector nicht unterstützt. Bitte die angegebene Anfrage überprüfen und erneut versuchen. |
| `1301-400` | Ungültige Anfrage | Der angegebene authSpecType-Parameter {authSpecType} wird nicht unterstützt. Bitte einen gültigen Authentifizierungsspezifikationstyp angeben und erneut versuchen. |
| `1302-400` | Ungültige Anfrage | Der angegebene Authentifizierungstyp {authType} wird für den Connector {connectorType} nicht unterstützt. Bitte einen gültigen Authentifizierungstyp für den angegebenen Connector angeben. |
| `1303-400` | Ungültige Anfrage | Die URL konnte mit den angegebenen Authentifizierungsparametern nicht codiert werden, da die URL-Codierung für {value} nicht unterstützt wird. Bitte Authentifizierungsparameter überprüfen und erneut versuchen. |
| `1304-400` | Ungültige Anfrage | Das erforderliche Feld {field} ist nicht angegeben. Bitte das Feld {field} angeben und erneut versuchen. |
| `1305-400` | Ungültige Anfrage | Der bereitgestellte Connector-Typ {connectorType} wird für diesen Vorgang nicht unterstützt. |
| `1306-400` | Ungültige Anfrage | Die Zielverbindung darf beim Überprüfen der Spezifikations-ID der Zielverbindung nicht null sein. Bitte die angegebene Anfrage überprüfen und erneut versuchen. |
| `1307-400` | Ungültige Anfrage | Die Spezifikations-ID der Zielverbindung ist ungültig={targetConnectionSpecId}. Der zulässige Wert lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Ungültige Anfrage | Die Anfrage konnte nicht verarbeitet werden. Fehlermeldung: {msftErrorMessage} |
| `1309-400` | Ungültige Anfrage | Die angegebene Verschlüsselungstransformation ist ungültig, da {requiredParam} in den Parametern fehlt. Bitte {requiredParam} eingeben und erneut versuchen. |
| `1310-400` | Ungültige Anfrage | Die angegebene publicKeyId in den Parametern ist abgelaufen. Bitte eine gültige publicKeyId eingeben und erneut versuchen. |
| `1311-400` | Ungültige Anfrage | Die in den Parametern angegebene publicKeyId ist ungültig. Bitte eine gültige publicKeyId eingeben und erneut versuchen. |
| 1312-400 | Ungültige Anfrage | Der angegebene Parameterwert {paramValue} ist keine gültige Eingabe für die Eigenschaft={requestParam}. Bitte einen gültigen Parameterwert eingeben und erneut versuchen. |
| `1313-400` | Ungültige Anfrage | Das Pfadattribut {attribute} ist nicht vorhanden. Bitte sicherstellen, dass das Attribut existiert, und erneut versuchen. |
| `1314-400` | Ungültige Anfrage | Ein komplexer Pfad wurde angegeben, ist jedoch nicht zulässig. Bitte sicherstellen, dass kein komplexer Pfad angegeben ist, und erneut versuchen. |
| `1315-400` | Ungültige Anfrage | Der angegebene Pfad {path} sollte auf ein Array von Datensätzen verweisen. Bitte sicherstellen, dass der angegebene Pfad auf das Array von Datensätzen verweist, und erneut versuchen. |
| `1316-400` | Ungültige Anfrage | Die angegebenen Paginierungsparameter dürfen nicht leer sein. Bitte gültige Paginierungsparameter angeben und erneut versuchen. |
| `1317-400` | Ungültige Anfrage | Die angegebenen Zeitplanparameter sind leer, dürfen jedoch nicht leer sein. Bitte gültige Zeitplanparameter angeben und erneut versuchen. |
| `1318-400` | Ungültige Anfrage | {combinedMessage}. Bitte die angegebene Anfrage überprüfen und erneut versuchen. |
| `1319-400` | Ungültige Anfrage | {param} muss Teil der übergeordneten Sammlung sein. Bitte einen Wert für {param} in der übergeordneten Sammlung angeben und erneut versuchen. |
| `1320-400` | Ungültige Anfrage | {idType} darf weder null noch leer sein. Bitte einen gültigen Wert für {idType} angeben und erneut versuchen. |
| `1321-400` | Ungültige Anfrage | Die Länge von {idType} muss 1 sein, die angegebene Größe ist {size}. Bitte eine gültige Größe angeben und erneut versuchen. |
| `1322-400` | Ungültige Anfrage | Die Quellverbindung darf für das Erstellen der Schemareferenz nicht null sein. Bitte eine gültige Quellverbindung angeben und erneut versuchen. |
| `1323-400` | Ungültige Anfrage | {entity} darf in der Quellverbindung nicht null oder leer sein: {sourceConnection}. Bitte einen gültigen Wert für {entity} angeben und erneut versuchen. |
| `1324-400` | Ungültige Anfrage | Die Zielverbindung darf beim Extrahieren der Datensatz-ID nicht null sein. Bitte eine gültige Zielverbindung angeben und erneut versuchen. |
| `1325-400` | Ungültige Anfrage | Der dataSetId-Parameter darf in der Zielverbindung nicht null oder leer sein: {TargetConnection}. Bitte einen gültigen dataSetId-Parameter angeben und erneut versuchen. |
| `1326-400` | Ungültige Anfrage | Die Quellverbindung darf beim Abrufen des Quellformats nicht null sein. Bitte eine gültige Quellverbindung angeben und erneut versuchen. |
| `1327-400` | Ungültige Anfrage | Das Format der in SourceConnection bereitgestellten Quelldaten {sourceFormat} wird nicht unterstützt. Zulässige Werte sind: {values}. Bitte zulässige Werte angeben und erneut versuchen. |
| `1328-400` | Ungültige Anfrage | Die Zuordnungstransformation darf beim Extrahieren von {param} nicht null sein. Bitte eine gültige Zuordnungstransformation angeben und erneut versuchen. |
| `1329-400` | Ungültige Anfrage | Der Parameter {param} darf in der angegebenen Anfrage nicht null oder leer sein. Bitte einen gültigen Wert für {param} angeben und erneut versuchen. |
| `1330-400` | Ungültige Anfrage | Für die Tabelle {tableName} wurden keine Spalten gefunden. Bitte einen gültigen Tabellennamen angeben und erneut versuchen. |
| `1331-400` | Ungültige Anfrage | Das Spaltentrennzeichen darf in SourceConnection nicht mehr als ein Zeichen aufweisen: {sourceConnection}. Bitte ein gültiges Spaltentrennzeichen angeben und erneut versuchen. |
| `1332-400` | Ungültige Anfrage | Die Quellverbindungsanfrage mit der connectionSpecId: {connectionSpecId} darf keine baseConnectionId haben. Bitte die baseConnectionId entfernen und erneut versuchen. |
| `1333-400` | Fehlerhafte Anfrage | flowRunAction={flowRunAction} wird für die Quelle mit Spezifikations-ID {specId} nicht unterstützt. Bitte eine gültige Flussausführungsaktion angeben und erneut versuchen. |
| `1334-400` | Ungültige Anfrage | Der Abfrageparameter {param} darf nicht leer sein. Bitte einen gültigen Wert für {param} angeben und erneut versuchen. |
| `1335-400` | Ungültige Anfrage | Beim Serialisieren der Filterparameter für die Erkundung ist ein Fehler aufgetreten. Bitte die Filterparameteranfrage überprüfen und erneut versuchen. |
| `1336-400` | Ungültige Anfrage | Das Erkunden der Verbindung wird für die Verbindungsspezifikations-ID {connectionSpecId} nicht unterstützt. Bitte eine unterstützte Verbindungsspezifikations-ID angeben und erneut versuchen. |
| `1337-400` | Ungültige Anfrage | {QueryParam} darf für objectType={objectType} nicht leer sein. Bitte einen gültigen Wert für {QueryParam} angeben und erneut versuchen. |
| `1338-400` | Ungültige Anfrage | Die Verbindungs-ID {connectionType} darf in flowRequest nicht null sein. Bitte eine gültige {connectionType}-Verbindungs-ID in flowRequest angeben. |
| `1339-400` | Ungültige Anfrage | Das in der Anfrage angegebene Format der Organisation {imsOrg} ist ungültig. Bitte eine gültige Organisations-ID angeben und erneut versuchen. |
| `1340-400` | Ungültige Anfrage | Beim Analysieren von {time} ist ein Fehler aufgetreten. Bitte das in der Anfrage angegebene Zeitformat überprüfen und erneut versuchen. |
| `1341-400` | Ungültige Anfrage | Die angegebene ODI-JSON ist leer. Bitte eine gültige ODI-JSON angeben und erneut versuchen. |
| `1342-400` | Ungültige Anfrage | Im Segment „dls:folder“ in „odi.json“ fehlen Definitionen. Bitte die entsprechenden Definitionen in „odi.json“ eingeben und erneut versuchen. |
| `1343-400` | Ungültige Anfrage | In den Segmenten „dls:entityReferences“ und „dls:partitionSpec“ in „odi.json“ fehlen die Definitionen. Bitte die entsprechenden Definitionen in „odi.json“ eingeben und erneut versuchen. |
| `1344-400` | Ungültige Anfrage | Die Definition für „dls:partitionSpec“ in „odi.json“ ist ungültig, da mehr als eine partitionSpecs gefunden wurde. Bitte die entsprechenden Definitionen in „odi.json“ eingeben und erneut versuchen. |
| `1345-400` | Ungültige Anfrage | Definitionen fehlen in mindestens einem Segment in den Pfaden „dls:partitionSpec/dls:fileFormat“, „dls:partitionSpec/dls:partitionTemplate“, „dls:partitionSpec/dls:fileFormat/@type“, „dls:partitionSpec/dls:fileFormat/dls:csvDelimiters“ in „odi.json“. Bitte die entsprechenden Definitionen in „odi.json“ eingeben und erneut versuchen. |
| `1346-400` | Ungültige Anfrage | Die Definition „@type“, die in „dls:fileFormat“ in „odi.json“ angegeben ist, ist ungültig. Bitte die entsprechenden Definitionen in „odi.json“ eingeben und erneut versuchen. |
| `1347-400` | Ungültige Anfrage | Die Definition von „dls:csvDelimiters“ in „odi.json“ wird nicht unterstützt. Die unterstützten csvDelimiters sind: [, ]. Bitte die entsprechenden Definitionen in „odi.json“ eingeben und erneut versuchen. |
| `1348-400` | Ungültige Anfrage | Beim Deserialisieren von „dls:entityReferences“ ist ein Fehler aufgetreten. Bitte überprüfen, ob die Daten ein gültiges Format aufweisen, und erneut versuchen. |
| `1349-400` | Ungültige Anfrage | Die bereitgestellten Filterparameter sind ungültig. Bitte gültige Filterparameter angeben und erneut versuchen. |
| `1350-400` | Ungültige Anfrage | Zum Filtern an der Quelle wurde kein Operator angegeben. Bitte eine gültige Filteranfrage mit dem entsprechenden Operator angeben und erneut versuchen. |
| `1351-400` | Ungültige Anfrage | Der bereitgestellte Operator {operator} wird für den Filter an der Quelle für diesen Connector nicht unterstützt. Bitte einen gültigen Operator angeben und erneut versuchen. |
| `1352-400` | Ungültige Anfrage | Der bereitgestellte Operator {operator} kann keinem unterstützten nativen Operator für {ql} zugeordnet werden. Bitte einen gültigen Operator angeben und erneut versuchen. |
| `1353-400` | Ungültige Anfrage | Der Filter an der Quelle wird für den Connector {connectorType} noch nicht unterstützt. Bitte die unterstützten Connectoren in der Dokumentation: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html?lang=de überprüfen. |
| `1354-400` | Ungültige Anfrage | Die Abfragesprache {ql} wird für den Filter an der Quelle noch nicht unterstützt. Bitte eine gültige Abfragesprache angeben und erneut versuchen. |
| `1355-400` | Ungültige Anfrage | Der angegebene Filtertyp ist ungültig. Der unterstützte Filtertyp ist: PQL. Bitte einen gültigen Filtertyp angeben und erneut versuchen. |
| `1356-400` | Ungültige Anfrage | Das angegebene Filterformat ist ungültig. Das unterstützte Filterformat ist: pql/json. Bitte ein gültiges Filterformat angeben und erneut versuchen. |
| `1357-400` | Ungültige Anfrage | Der angegebene Filter ist ungültig. Der Wert muss mit detaillierten Filtern angegeben werden. Bitte einen gültigen Filter angeben und erneut versuchen. |
| `1358-400` | Ungültige Anfrage | Der angegebene Parameter „objectType“ ist ungültig. Bitte einen gültigen Wert für objectType angeben und erneut versuchen. |
| `1359-400` | Ungültige Anfrage | Der Parameter {param} fehlt in der Anfrage. Bitte einen gültigen Wert für {param} angeben und erneut versuchen. |
| `1360-400` | Ungültige Anfrage | Die Startzeit darf nicht in der Vergangenheit festgelegt werden. Bitte eine gültige Startzeit angeben und erneut versuchen. |
| `1361-400` | Ungültige Anfrage | Bei einer einmaligen Aufnahme ist kein Intervall zulässig. Bitte das Intervall entfernen oder die Häufigkeit ändern und dann erneut versuchen. |
| `1362-400` | Ungültige Anfrage | Das Intervall darf nicht kleiner als {minInterval} sein. Bitte einen gültigen Intervallwert angeben und erneut versuchen. |
| `1363-400` | Ungültige Anfrage | Das Intervall {interval} ist mit der Häufigkeit {frequency} nicht zulässig. Bitte einen gültigen Intervallwert angeben und erneut versuchen. |
| `1364-400` | Ungültige Anfrage | Das Aufstockungs-Flag ist nicht zulässig, wenn die Häufigkeit auf 1 festgelegt ist. Bitte das Aufstockungs-Flag entfernen, wenn die Häufigkeit auf 1 festgelegt ist, und erneut versuchen. |
| `1365-400` | Ungültige Anfrage | Der in Ops angegebene Pfad {path} ist ungültig. Bitte den gültigen Pfad {path} angeben und erneut versuchen. |
| `1366-400` | Ungültige Anfrage | Die Startzeit ist abgelaufen und der Aktualisierungsvorgang ist nicht mehr zulässig. |
| `1367-400` | Ungültige Anfrage | Die Delta-Spalte ist bei der Kopiertransformation erforderlich, wenn ein CRM-Connector erstellt wird. Bitte die Delta-Spalte angeben und erneut versuchen. |
| `1368-400` | Ungültige Anfrage | Der Modus ist in der Flussanfrage nicht zulässig. Bitte die Anfrage überprüfen und erneut versuchen. |
| `1369-400` | Ungültige Anfrage | Die Delta-Spalte in der Kopiertransformation ist nicht zulässig, wenn die Häufigkeit auf 1 festgelegt ist. Bitte die Delta-Spalte entfernen und erneut versuchen. |
| `1370-400` | Ungültige Anfrage | Die Quellspalten konnten zur Aufnahme nicht abgerufen werden, da die Zuordnungstransformation fehlt. Bitte die Zuordnungstransformation hinzufügen und erneut versuchen. |
| `1371-400` | Ungültige Anfrage | Die Erkennung der Dateieigenschaften wird für den {connectorType}-Connector nicht unterstützt. Bitte die Dateieigenschaften manuell angeben. |
| `1372-400` | Ungültige Anfrage | Der aktuelle Vorgang ist nicht zulässig. Das Suchen über die Verbindungsspezifikation ist für die Verbindungsspezifikations-ID {connectionSpecId} nicht zulässig. |
| `1373-400` | Ungültige Anfrage | Der flowSpecType fehlt in der Anfrage. Bitte einen gültigen flowSpecType angeben und erneut versuchen. |
| `1374-400` | Ungültige Anfrage | Die angegebenen Abfrageparameter sind ungültig. Das Flag „determineProperties“ und benutzerdefinierte Eigenschaften können nicht in derselben Anfrage verwendet werden. Bitte Anfrage korrigieren und erneut versuchen. |
| `1375-400` | Ungültige Anfrage | Die Erkennung der Dateieigenschaften ist fehlgeschlagen. Bitte Eigenschaften manuell eingeben. |
| `1376-400` | Ungültige Anfrage | Die Erkennung von Dateieigenschaften wird für die Verbindungsspezifikations-ID={connectionSpecId} nicht unterstützt. Bitte die Dateieigenschaften manuell angeben. |
| `1377-400` | Ungültige Anfrage | Der angegebene Wertparameter ist null und kann nicht mit dem Operator {operator} verglichen werden. Bitte einen gültigen Wertparameter angeben und erneut versuchen. |
| `1378-400` | Ungültige Anfrage | Bei der Validierung der Eingabespalte {column} für den Filter an der Quelle ist ein Fehler aufgetreten. Der Spaltenname muss eine gültige Spalte in der Tabelle sein. Bitte einen gültigen Spaltennamen angeben und erneut versuchen. |
| `1379-400` | Ungültige Anfrage | Bei der Validierung der Eingabe {value} für den Filter an der Quelle ist ein Fehler aufgetreten. Der Spalten-DataType an der Quelle lautet {columnDataType}, und der DataType [Zeichenfolge] des Werts stimmt nicht damit überein. Bitte einen gültigen Wert {value} angeben und erneut versuchen. |
| `1380-400` | Ungültige Anfrage | Workflow-Ausführung konnte nicht erstellt werden. Fehlermeldung: {message} |
| `1381-400` | Ungültige Anfrage | WindowEndTime={endTime} kann nicht vor WindowStartTime={startTime} liegen. Bitte eine gültige Endzeit angeben und erneut versuchen. |
| `1382-400` | Ungültige Anfrage | Die Delta-Spalte muss dem Wert entsprechen, der in den Kopiertransformationen des Flusses vorhanden ist. Bitte eine gültige Delta-Spalte angeben und erneut versuchen. |
| `1383-400` | Ungültige Anfrage | Die Delta-Spalte fehlt in den Parametern, die zum Erstellen einer Flussausführung empfangen wurden. Bitte die Delta-Spalte in den Parametern angeben und erneut versuchen. |
| `1384-400` | Ungültige Anfrage | Die für das Erstellen der Flussausführung angegebenen Parameter {params} sind ungültig oder leer. Bitte gültige Parameter angeben und erneut versuchen. |
| `1385-400` | Ungültige Anfrage | Der angegebene Connector-Typ {connectorType} wird zum Erstellen von Flussausführungen nicht unterstützt. Bitte einen gültigen Wert für connectorType angeben und erneut versuchen. |
| `1386-400` | Ungültige Anfrage | Die Fluss-ID {flowId} mit scheduleParams-Häufigkeit {frequency} wird für die Erstellung von Flussausführungen nicht unterstützt. Bitte eine gültige Häufigkeit angeben und erneut versuchen. |
| `1387-400` | Ungültige Anfrage | Die Flussausführungs-ID {flowRunId} befindet sich für das erneute Auslösen in einem ungültigen Status {state}. Bitte nach einiger Zeit erneut versuchen und den Support kontaktieren, falls das Problem weiterhin besteht. |
| `1388-400` | Ungültige Anfrage | Der Fluss {flow} befindet sich im Status {state} und kann nicht erneut ausgelöst werden. Der Fluss muss für die Neuauslösung in einem aktivierten Status sein. |
| `1389-400` | Ungültige Anfrage | Beim Analysieren der bereitgestellten base64-codierten Zeichenfolge ist ein Fehler aufgetreten. Bitte eine gültige codierte Filterzeichenfolge angeben und erneut versuchen. |
| `1390-400` | Ungültige Anfrage | Der Operator „nicht“ kann nicht mehr als einen Vergleich aufweisen. Bitte eine gültige Anzahl von Vergleichen angeben und erneut versuchen. |
| `1391-400` | Ungültige Anfrage | SchemaMetaData in sourceConnection konnte für die ID {sourceConnectionId} nicht analysiert werden. Bitte die schemaMetaData in der Anfrage überprüfen und erneut versuchen. |
| `1392-400` | Ungültige Anfrage | Fehler beim Analysieren von Transformationen in der Flussanfrage für Fluss-ID {flowId}. Bitte die Transformationen in Ihrer Anfrage überprüfen und erneut versuchen. |
| `1393-400` | Ungültige Anfrage | Der bereitgestellte Parameter {parameter} ist null oder leer. Bitte einen gültigen Wert für {parameter} angeben und erneut versuchen. |
| `1394-400` | Ungültige Anfrage | Der Mindestwert für den Parameter {parameter} ist eins. Bitte einen gültigen Wert für {parameter} angeben und erneut versuchen. |
| `1395-400` | Ungültige Anfrage | Die Quellverbindung im Fluss ist null oder leer. Bitte eine gültige Quellverbindung im Fluss angeben und erneut versuchen. |
| `1396-400` | Ungültige Anfrage | Es konnte kein übereinstimmendes Format gefunden werden. Bitte ein übereinstimmendes Format angeben und erneut versuchen. |
| `1397-400` | Ungültige Anfrage | Die angegebene Häufigkeit {frequency} ist ungültig. Bitte eine gültige Häufigkeit angeben und erneut versuchen. |
| `1398-400` | Ungültige Anfrage | Der angegebene Vorgang {action} wird nicht unterstützt. Bitte den angegebenen Vorgang überprüfen und erneut versuchen. |
| `1399-400` | Ungültige Anfrage | Ein gültiger requestFileType konnte nicht gefunden werden. Bitte einen gültigen requestFileType angeben und erneut versuchen. |
| `1400-400` | Ungültige Anfrage | Der bereitgestellte Parameter „templateType“ ist ungültig. Bitte einen gültigen Vorlagentyp angeben und erneut versuchen. |
| `1401-400` | Ungültige Anfrage | Die angegebene Flussausführungsaktion {flowRunAction} wird nicht unterstützt. Bitte eine gültige Flussausführungsaktion angeben und erneut versuchen. |
| `1402-500` | Interner Fehler | Ein unbekannter Fehler ist aufgetreten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1403-400` | Ungültige Anfrage | Die Startzeit ist vorüber, und die Häufigkeit kann nicht mehr in einmal geändert werden. |
| `1404-400` | Ungültige Anfrage | Die Startzeit ist vorüber, und die Aufstockung kann nicht mehr aktualisiert werden. |

## Flow Service-Ausnahmen (1600-1699)

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1600-400` | Ungültige Anfrage | Die Anfrage konnte nicht verarbeitet werden. {detailsMessage} |
| `1601-500` | Interner Fehler | Ein unbekannter Fehler ist aufgetreten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1602-404` | Ressource nicht gefunden | Die angeforderte Ressource wurde nicht gefunden. {detailsMessage} |
| `1603-503` | Dienst nicht verfügbar | Der Dienst ist derzeit nicht verfügbar. Bitte erneut versuchen. Kunden-Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1604-504` | Gateway-Zeitüberschreitung | Es ist eine Gateway-Zeitüberschreitung aufgetreten. Bitte erneut versuchen. Kunden-Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1605-401` | Nicht autorisiert | Die Benutzerin bzw. der Benutzer ist nicht autorisiert. {detailsMessage} |
| `1606-403` | Verboten | Der angeforderte Vorgang ist verboten. {detailsMessage} |
| `1607-412` | Vorbedingung fehlgeschlagen | Die von den Kopfzeilen „If-Unmodified-Since“ oder „If-None-Match“ definierte Bedingung ist nicht erfüllt. {detailsMessage} |

## Data Landing Zone-Fehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1700-500` | Interner Fehler | Ein unbekannter Fehler ist aufgetreten. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1701-400` | Ungültige Anfrage | Die bereitgestellte Landing Zone ist inaktiv. Bitte Landing Zone aktivieren und erneut versuchen. |
| `1702-400` | Ungültige Anfrage | Der für die Landing Zone angegebene SAS-Typ {sasType} ist nicht zulässig. Bitte ein gültiges SAS angeben und erneut versuchen. |
| `1703-400` | Ungültige Anfrage | Die Aktualisierung der Anmeldedaten ist nicht zulässig. |
| `1704-400` | Ungültige Anfrage | Die für storageAccountName={accountName} in subscriptionId={subscriptionId} und resourceGroupName={resourceGroupName} zurückgegebenen Schlüssel sind fehlerhaft. Bitte die Anfrage überprüfen und erneut versuchen. Bitte den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1705-400` | Ungültige Anfrage | Die bereitgestellte Data Landing Zone-Aktion wird nicht unterstützt. Bitte eine gültige Aktion angeben und erneut versuchen. |
| `1706-400` | Ungültige Anfrage | Die Konfiguration der zulässigen Aktivierungen ist für die Landing Zone {landingZoneType} nicht korrekt konfiguriert. Bitte erneut versuchen und den Support kontaktieren, wenn das Problem weiterhin besteht. |
| `1707-400` | Ungültige Anfrage | Der Service konnte nicht gestartet werden, da die Landing Zone-Konfiguration nicht null oder leer sein darf. Bitte sicherstellen, dass die Landing Zone-Konfiguration nicht null ist und erneut versuchen. |
| `1708-400` | Ungültige Anfrage | Die Container-Konfiguration darf in Landing Zone-Typ {landingZoneType} nicht null sein. Bitte sicherstellen, dass die Container-Konfiguration nicht null ist, und erneut versuchen. |
| `1709-400` | Ungültige Anfrage | Die SAS-Details können für {tokenConfig} in Landing Zone-Typ {landingZoneType} nicht null sein. Bitte in der Konfiguration ein gültiges SAS angeben und erneut versuchen. |
| `1710-400` | Ungültige Anfrage | Die angegebene Landing Zone vom Typ {landingZoneUseCase} wird nicht unterstützt. Bitte einen gültigen Landing Zone-Typ angeben und erneut versuchen. |
| `1711-400` | Ungültige Anfrage | Die SAS-Details wurden für die bereitgestellte Data Landing Zone vom Typ {landingZoneUseCase} nicht gefunden. Bitte überprüfen, ob SAS-Details für den angegebenen Landing Zone-Typ angegeben wurden. |
| `1712-400` | Ungültige Anfrage | Die angegebene Landing Zone-Aktion {actionType} ist nicht zulässig. Bitte eine gültige Landing Zone-Aktion angeben und erneut versuchen. |
| `1713-400` | Ungültige Anfrage | Der {OperationType} ist für den bereitgestellten {tokenType} nicht zulässig. Bitte die Anfrage überprüfen und erneut versuchen. |
| `1714-400` | Ungültige Anfrage | Die Client-ID {clientId} darf diesen Vorgang nicht ausführen. Bitte die Anfrage mit Berechtigungen überprüfen und erneut versuchen. |
