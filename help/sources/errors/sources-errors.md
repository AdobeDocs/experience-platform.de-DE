---
title: Quellen-Fehlermeldungen
description: Erfahren Sie mehr über die Fehlermeldungen, die bei Verwendung des Flow Service für Quellen auftreten können.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 9%

---

# Quellen-Fehlermeldungen

Dieses Dokument enthält einen Katalog mit Fehlermeldungen, Beschreibungen und empfohlenen Lösungen für Quellen.

## Allgemeine Fehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1000-400` | Ungültige Anfrage | Die Anfrage ist ungültig. Überprüfen Sie die Anfrage und versuchen Sie es erneut. |
| `1001-401` | Unerlaubt | Der Benutzer ist nicht autorisiert. Wenden Sie sich an Ihren Administrator, um Zugriff auf die Ressource zu erhalten. |
| `1002-403` | Verboten | Der angeforderte Vorgang ist verboten. Überprüfen Sie den angeforderten Vorgang und versuchen Sie es erneut. |
| `1003-404` | Ressource nicht gefunden | Die angeforderte Ressource wurde nicht gefunden. Überprüfen Sie die bereitgestellte Anfrage und versuchen Sie es erneut. |
| `1004-415` | Nicht unterstützter Medientyp | Das angegebene Payload-Format wird nicht unterstützt. Überprüfen Sie Ihre bereitgestellte Anfrage und versuchen Sie es erneut. |
| `1005-500` | Interner Fehler | Es ist ein interner Fehler aufgetreten. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1006-408` | Anfrage-Timeout | Bei der Verarbeitung der Anfrage ist ein Fehler aufgetreten. Die Anfrage wurde zurückgestellt. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1007-400` | Ungültiger Kopfzeilenparameter | Ein ungültiger Header-Parameter: {headerName} wurde empfangen. Überprüfen Sie die Kopfzeilenparameter und versuchen Sie es erneut. |
| `1008-401` |  | Ungültiges Autorisierungstoken | Das Autorisierungstoken hat keinen Zugriff auf diese Organisation oder die Organisation existiert nicht. Stellen Sie sicher, dass die Organisation vorhanden ist, oder kontaktieren Sie Ihren Administrator, um Zugriff zu erhalten. |
| `1009-403` | Die IMS-Organisations-ID fehlt oder ist leer | Der Anforderungsheader für die Organisations-ID fehlt oder ist leer. Aktualisieren Sie den Header-Wert und versuchen Sie es erneut. |
| `1010-500` | Ungültige detaillierte Nachricht | Der Parameter in der detaillierten Nachricht wurde nicht ordnungsgemäß bereitgestellt. Überprüfen Sie den Parameter in der detaillierten Nachricht und versuchen Sie es erneut. |
| `1011-503` | Dienst nicht verfügbar | Der Dienst ist vorübergehend nicht verfügbar. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1012-504` | Gateway-Zeitüberschreitung | Es ist ein Gateway-Timeout aufgetreten. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1013-412` | Vorbedingung fehlgeschlagen | Die von den Headern If-Unmodified-Since oder If-None-Match definierte Bedingung ist nicht erfüllt. Bitte überprüfen und versuchen Sie es erneut. |
| `1014-400` | Ungültige Anfrage - Argument | Die Anfrage konnte nicht verarbeitet werden. {detailsMessage} |

## Framework-Fehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1100-400` | Ungültige Anfrage | Die Anfrage konnte nicht verarbeitet werden. {detailsMessage} |
| `1101-500` | Interner Fehler | Es ist ein interner Fehler aufgetreten. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1102-404` | Ressource nicht gefunden | Die angeforderte Ressource wurde nicht gefunden. {detailsMessage} |
| `1103-503` | Dienst nicht verfügbar | Der Dienst ist vorübergehend nicht verfügbar. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1104-504` | Gateway-Zeitüberschreitung | Es ist ein Gateway-Timeout aufgetreten. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1105-401` | Unerlaubt | Der Benutzer ist nicht autorisiert. {detailsMessage} |
| `1106-403` | Verboten | Der angeforderte Vorgang ist verboten. {detailsMessage} |
| `1107-412` | Vorbedingung fehlgeschlagen | Die von den Headern If-Unmodified-Since oder If-None-Match definierte Bedingung ist nicht erfüllt. {detailsMessage} |

## Verschlüsselungsfehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1200-500` | Interner Fehler | Es ist ein interner Fehler aufgetreten. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1201-400` | Ungültige Anfrage | Die flowId darf nicht null oder leer sein. Geben Sie in der Anfrage eine gültige flowId an und versuchen Sie es erneut. |
| `1202-400` | Ungültige Anfrage | Die publicKeyId fehlt in den transformations={transformations} des Flusses. Geben Sie publicKeyId in der Anfrage ein und versuchen Sie es erneut. |
| `1203-400` | Ungültige Anfrage | Der Verschlüsselungsschlüssel ist nicht für keyID={keyID} in den transformations={transformations} des Flusses vorhanden. Überprüfen Sie Ihre bereitgestellte keyID und versuchen Sie es erneut. |
| `1204-400` | Ungültige Anfrage | Der bereitgestellte Verschlüsselungsalgorithmus ist ungültig. Geben Sie einen gültigen Verschlüsselungsalgorithmus an und versuchen Sie es erneut. |
| `1205-400` | Ungültige Anfrage | Die Passphrase fehlt im Abschnitt &quot;params&quot;in der angegebenen Anfrage. Bitte geben Sie passPhrase in params an und versuchen Sie es erneut. |

## REST-API-Fehler

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1300-400` | Ungültige Anfrage | Die Patch-Verbindungsanforderung wird für den {connectorType}-Connector nicht unterstützt. Überprüfen Sie die bereitgestellte Anfrage und versuchen Sie es erneut. |
| `1301-400` | Ungültige Anfrage | Der bereitgestellte Parameter authSpecType : {authSpecType} wird nicht unterstützt. Bitte geben Sie einen gültigen Authentifizierungstyp an und versuchen Sie es erneut. |
| `1302-400` | Ungültige Anfrage | Der angegebene Authentifizierungstyp = {authType} wird für connector={connectorType} nicht unterstützt. Bitte geben Sie einen gültigen Authentifizierungstyp für den angegebenen Connector an. |
| `1303-400` | Ungültige Anfrage | Die URL konnte nicht mit den angegebenen Authentifizierungsparametern kodiert werden, da die URL-Kodierung für {value} nicht unterstützt wird. Überprüfen Sie Ihre Authentifizierungsparameter und versuchen Sie es erneut. |
| `1304-400` | Ungültige Anfrage | Das erforderliche Feld {field} wird nicht angegeben. Geben Sie das Feld ein und versuchen Sie es erneut. |
| `1305-400` | Ungültige Anfrage | Der bereitgestellte Connector-Typ = {connectorType} wird für diesen Vorgang nicht unterstützt. |
| `1306-400` | Ungültige Anfrage | Die Zielverbindung kann beim Überprüfen der Ziel-Verbindungsspezifikations-ID nicht null sein. Überprüfen Sie die bereitgestellte Anfrage und versuchen Sie es erneut. |
| `1307-400` | Ungültige Anfrage | Die Kennung der Zielverbindungsspezifikation ist ungültig={targetConnectionSpecId}. Der zulässige Wert lautet: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Ungültige Anfrage | Die Anfrage konnte nicht verarbeitet werden. Fehlermeldung: {msftErrorMessage} |
| `1309-400` | Ungültige Anfrage | Die bereitgestellte Verschlüsselungsumwandlung ist ungültig, da {requiredParam} in den Parametern fehlt. Geben Sie {requiredParam} ein und versuchen Sie es erneut. |
| `1310-400` | Ungültige Anfrage | Die bereitgestellte publicKeyId in den Parametern ist abgelaufen. Geben Sie eine gültige publicKeyId ein und versuchen Sie es erneut. |
| `1311-400` | Ungültige Anfrage | Die in params bereitgestellte publicKeyId ist ungültig. Geben Sie eine gültige publicKeyId ein und versuchen Sie es erneut. |
| 1312-400 | Ungültige Anfrage | Der angegebene Parameterwert {paramValue} ist keine gültige Eingabe für property={requestParam}. Geben Sie einen gültigen Parameterwert ein und versuchen Sie es erneut. |
| `1313-400` | Ungültige Anfrage | Das Pfadattribut {attribute} ist nicht vorhanden. Vergewissern Sie sich, dass das Attribut vorhanden ist, und versuchen Sie es erneut. |
| `1314-400` | Ungültige Anfrage | Ein komplexer Pfad wurde bereitgestellt, ist jedoch nicht zulässig. Stellen Sie sicher, dass kein komplexer Pfad angegeben ist, und versuchen Sie es erneut. |
| `1315-400` | Ungültige Anfrage | Der bereitgestellte Pfad {path} sollte auf ein Array von Datensätzen verweisen. Stellen Sie sicher, dass der angegebene Pfad auf das Array von Datensätzen verweist, und versuchen Sie es erneut. |
| `1316-400` | Ungültige Anfrage | Die bereitgestellten Paginierungsparameter sollten nicht leer sein. Geben Sie gültige Paginierungsparameter an und versuchen Sie es erneut. |
| `1317-400` | Ungültige Anfrage | Die bereitgestellten Zeitplanparameter sind leer, sollten jedoch nicht leer sein. Geben Sie gültige Zeitplanparameter an und versuchen Sie es erneut. |
| `1318-400` | Ungültige Anfrage | {linkedMessage}. Überprüfen Sie die bereitgestellte Anfrage und versuchen Sie es erneut. |
| `1319-400` | Ungültige Anfrage | {param} sollte Teil der übergeordneten Sammlung sein. Geben Sie {param} in der übergeordneten Sammlung an und versuchen Sie es erneut. |
| `1320-400` | Ungültige Anfrage | {idType} darf nicht null oder leer sein. Geben Sie einen gültigen {idType} an und versuchen Sie es erneut. |
| `1321-400` | Ungültige Anfrage | Die Länge von {idType} sollte 1 betragen, die bereitgestellte Größe ist {size}. Bitte geben Sie eine gültige Größe an und versuchen Sie es erneut. |
| `1322-400` | Ungültige Anfrage | Die Quellverbindung kann beim Erstellen der Schemareferenz nicht null sein. Geben Sie eine gültige Quellverbindung an und versuchen Sie es erneut. |
| `1323-400` | Ungültige Anfrage | Die {entity} darf in der Quellverbindung nicht null oder leer sein: {sourceConnection}. Geben Sie gültige {entity} ein und versuchen Sie es erneut. |
| `1324-400` | Ungültige Anfrage | Die Zielverbindung kann beim Extrahieren der Datensatz-ID nicht null sein. Geben Sie eine gültige Zielverbindung an und versuchen Sie es erneut. |
| `1325-400` | Ungültige Anfrage | Der Parameter dataSetId darf in der Zielverbindung nicht null oder leer sein: {TargetConnection}. Geben Sie einen gültigen dataSetId-Parameter an und versuchen Sie es erneut. |
| `1326-400` | Ungültige Anfrage | Die Quellverbindung kann beim Abrufen des Quellformats nicht null sein. Geben Sie eine gültige Quellverbindung an und versuchen Sie es erneut. |
| `1327-400` | Ungültige Anfrage | Das Format der in SourceConnection bereitgestellten Quelldaten ={sourceFormat} wird nicht unterstützt. Zulässige Werte sind: {values}. Geben Sie die zulässigen Werte an und versuchen Sie es erneut. |
| `1328-400` | Ungültige Anfrage | Die Mapping-Umwandlung kann beim Extrahieren von {param} nicht null sein. Bitte geben Sie eine gültige Mapping-Transformation an und versuchen Sie es erneut. |
| `1329-400` | Ungültige Anfrage | Der -Parameter: {param} darf in der angegebenen Anfrage nicht null oder leer sein. Geben Sie gültige {param} ein und versuchen Sie es erneut. |
| `1330-400` | Ungültige Anfrage | Für die Tabelle {tableName} wurden keine Spalten gefunden. Geben Sie einen gültigen Tabellennamen ein und versuchen Sie es erneut. |
| `1331-400` | Ungültige Anfrage | Das Spalten-Trennzeichen darf in SourceConnection nicht mehr als ein Zeichen sein: {sourceConnection}. Geben Sie ein gültiges Spaltentrennzeichen ein und versuchen Sie es erneut. |
| `1332-400` | Ungültige Anfrage | Die Anfrage zur Quellverbindung mit der connectionSpecId: {connectionSpecId} darf keine baseConnectionId haben. Entfernen Sie die baseConnectionId und versuchen Sie es erneut. |
| `1333-400` | Ungültige Anforderungen | Die flowRunAction={flowRunAction} wird für die Quelle mit spec id={specId} nicht unterstützt. Geben Sie eine gültige Flusslaufaktion an und versuchen Sie es erneut. |
| `1334-400` | Ungültige Anfrage | Der Abfrageparameter : {param} darf nicht leer sein. Geben Sie gültige {param} ein und versuchen Sie es erneut. |
| `1335-400` | Ungültige Anfrage | Beim Serialisieren der Filterparameter für die Erforschung ist ein Fehler aufgetreten. Überprüfen Sie Ihre Filterparam-Anfrage und versuchen Sie es erneut. |
| `1336-400` | Ungültige Anfrage | Die Verbindung durchsuchen wird für die Verbindungsspezifikations-ID nicht unterstützt: {connectionSpecId} Bitte geben Sie die unterstützte Verbindungsspezifikations-ID an und versuchen Sie es erneut. |
| `1337-400` | Ungültige Anfrage | Der {QueryParam}-Wert darf für objectType={objectType} nicht leer sein. Geben Sie gültige {QueryParam} an und versuchen Sie es erneut. |
| `1338-400` | Ungültige Anfrage | Die Verbindungs-ID {connectionType} darf in flowRequest nicht null sein. Bitte geben Sie eine gültige {connectionType}-Verbindungs-ID in flowRequest an. |
| `1339-400` | Ungültige Anfrage | Das in der Anfrage angegebene Format von organization={imsOrg} ist ungültig. Bitte geben Sie eine gültige Organisations-ID ein und versuchen Sie es erneut. |
| `1340-400` | Ungültige Anfrage | Beim Analysieren von {time} ist ein Fehler aufgetreten. Überprüfen Sie das in der Anfrage angegebene Zeitformat und versuchen Sie es erneut. |
| `1341-400` | Ungültige Anfrage | Das bereitgestellte ODI-JSON ist leer. Bitte geben Sie gültige ODI Json an und versuchen Sie es erneut. |
| `1342-400` | Ungültige Anfrage | Im Segment &quot;dls:folder&quot;in &quot;odi.json&quot;fehlen Definitionen. Geben Sie die entsprechenden Definitionen in &quot;odi.json&quot;ein und versuchen Sie es erneut. |
| `1343-400` | Ungültige Anfrage | Bei den Segmenten &quot;dls:entityReferences&quot;und &quot;dls:partitionSpec&quot;in &quot;odi.json&quot;fehlen beide Definitionen. Bitte geben Sie die entsprechenden Definitionen in &quot;odi.json&quot;ein und versuchen Sie es erneut. |
| `1344-400` | Ungültige Anfrage | Die Definition für &#39;dls:partitionSpec&#39; in &#39;odi.json&#39; ist ungültig, da mehr als eine partitionSpecs gefunden wurden. Geben Sie die entsprechenden Definitionen in &quot;odi.json&quot;ein und versuchen Sie es erneut. |
| `1345-400` | Ungültige Anfrage | Definitionen fehlen in einem oder mehreren Segmenten in Pfaden: &#39;dls:partitionSpec/dls:fileFormat&#39;, &#39;dls:partitionSpec/dls:partitionTemplate&#39;,&#39;dls:partitionSpec/dls:fileFormat/@type&#39;, &#39;dls:partitionSpec/dls:fileFormat/dls:csvDelimiters&#39; in &#39;odi.json&#39;. Geben Sie die entsprechenden Definitionen in &quot;odi.json&quot;ein und versuchen Sie es erneut. |
| `1346-400` | Ungültige Anfrage | Die Definition &#39;@type&#39;, die in &#39;dls:fileFormat&#39; in &#39;odi.json&#39; angegeben ist, ist ungültig. Geben Sie die entsprechenden Definitionen in &quot;odi.json&quot;ein und versuchen Sie es erneut. |
| `1347-400` | Ungültige Anfrage | Die Definition von dls:csvDelimiters in &quot;odi.json&quot;wird nicht unterstützt. Die unterstützten csvDelimiters sind: [&#39;,&#39;]. Geben Sie die entsprechenden Definitionen in &quot;odi.json&quot;ein und versuchen Sie es erneut. |
| `1348-400` | Ungültige Anfrage | Beim Deserialisieren von &#39;dls:entityReferences&#39; ist ein Fehler aufgetreten. Überprüfen Sie, ob die Daten ein gültiges Format aufweisen, und versuchen Sie es erneut. |
| `1349-400` | Ungültige Anfrage | Die bereitgestellten Filterparameter sind ungültig. Geben Sie gültige Filterparameter an und versuchen Sie es erneut. |
| `1350-400` | Ungültige Anfrage | Für die Filterung an der Quelle wurde kein Operator angegeben. Geben Sie eine gültige Filteranfrage mit dem entsprechenden Operator an und versuchen Sie es erneut. |
| `1351-400` | Ungültige Anfrage | Der bereitgestellte Operator {operator} wird für den Filter an der Quelle für diesen Connector nicht unterstützt. Geben Sie einen gültigen Operator ein und versuchen Sie es erneut. |
| `1352-400` | Ungültige Anfrage | Der bereitgestellte Operator {operator} kann keinem unterstützten nativen Operator für {ql} zugeordnet werden. Geben Sie einen gültigen Operator ein und versuchen Sie es erneut. |
| `1353-400` | Ungültige Anfrage | Der Filter an der Quelle wird für den Connector {connectorType} noch nicht unterstützt. Überprüfen Sie die unterstützten Connectoren in der Dokumentation: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html |
| `1354-400` | Ungültige Anfrage | Die Abfragesprache {ql} wird für den Quellfilter noch nicht unterstützt. Bitte geben Sie eine gültige Abfragesprache an und versuchen Sie es erneut. |
| `1355-400` | Ungültige Anfrage | Der angegebene Filtertyp ist ungültig. Der unterstützte Filtertyp ist: PQL. Geben Sie einen gültigen Filtertyp an und versuchen Sie es erneut. |
| `1356-400` | Ungültige Anfrage | Das angegebene Filterformat ist ungültig. Das unterstützte Filterformat lautet : pql/json. Geben Sie ein gültiges Filterformat an und versuchen Sie es erneut. |
| `1357-400` | Ungültige Anfrage | Der bereitgestellte Filter ist ungültig. Der Wert muss mit detaillierten Filtern angegeben werden. Geben Sie einen gültigen Filter an und versuchen Sie es erneut. |
| `1358-400` | Ungültige Anfrage | Der bereitgestellte Parameter &quot;objectType&quot;ist ungültig. Geben Sie einen gültigen objectType ein und versuchen Sie es erneut. |
| `1359-400` | Ungültige Anfrage | Der Parameter {param} fehlt in der Anfrage. Geben Sie einen gültigen {param} ein und versuchen Sie es erneut. |
| `1360-400` | Ungültige Anfrage | Die Startzeit kann nicht in der Vergangenheit festgelegt werden. Geben Sie eine gültige Startzeit an und versuchen Sie es erneut. |
| `1361-400` | Ungültige Anfrage | Bei einmaliger Erfassung ist kein Intervall zulässig. Entfernen Sie das Intervall oder ändern Sie die Häufigkeit und versuchen Sie es dann erneut. |
| `1362-400` | Ungültige Anfrage | Das Intervall darf nicht kleiner als {minInterval} sein. Geben Sie einen gültigen Intervallwert an und versuchen Sie es erneut. |
| `1363-400` | Ungültige Anfrage | Intervall {interval} ist mit der Häufigkeit nicht zulässig: {frequency}. Geben Sie einen gültigen Intervallwert an und versuchen Sie es erneut. |
| `1364-400` | Ungültige Anfrage | Das Aufstockungsflag ist nicht zulässig, wenn die Häufigkeit auf 1 gesetzt ist. Entfernen Sie die Aufstockungskennzeichnung, wenn die Häufigkeit auf ein einziges Mal eingestellt ist, und versuchen Sie es erneut. |
| `1365-400` | Ungültige Anfrage | Der in ops angegebene Pfad {path} ist ungültig. Geben Sie den gültigen Pfad {path} an und versuchen Sie es erneut. |
| `1366-400` | Ungültige Anfrage | Die Startzeit ist vorüber und der Aktualisierungsvorgang ist nicht mehr zulässig. |
| `1367-400` | Ungültige Anfrage | Die Delta-Spalte ist bei der Kopierumwandlung bei der Erstellung eines CRM-Connectors erforderlich. Geben Sie die Delta-Spalte ein und versuchen Sie es erneut. |
| `1368-400` | Ungültige Anfrage | Der Modus ist in der Flussanforderung nicht zulässig. Überprüfen Sie Ihre Anfrage und versuchen Sie es erneut. |
| `1369-400` | Ungültige Anfrage | Die Delta-Spalte in der Copy-Umwandlung ist nicht zulässig, wenn die Häufigkeit auf einmal eingestellt ist. Entfernen Sie die Delta-Spalte und versuchen Sie es erneut. |
| `1370-400` | Ungültige Anfrage | Die Quellspalten konnten nicht zur Aufnahme abgerufen werden, da die Zuordnungsverwandlung fehlt. Fügen Sie die Mapping-Umwandlung hinzu und versuchen Sie es erneut. |
| `1371-400` | Ungültige Anfrage | Die Erkennung der Dateieigenschaften wird für den Connector {connectorType} nicht unterstützt. Bitte geben Sie die Dateieigenschaften manuell an. |
| `1372-400` | Ungültige Anfrage | Der aktuelle Vorgang ist nicht zulässig. Durchsuchen der Verbindungsspezifikation ist für die Verbindungsspezifikations-ID={connectionSpecId} nicht zulässig. |
| `1373-400` | Ungültige Anfrage | Der flowSpecType fehlt in der Anfrage. Geben Sie einen gültigen flowSpecType ein und versuchen Sie es erneut. |
| `1374-400` | Ungültige Anfrage | Die angegebenen Abfrageparameter sind ungültig. Sie können nicht das Flag &quot;defineProperties&quot;und benutzerdefinierte Eigenschaften in derselben Anforderung verwenden. Korrigieren Sie Ihre Anfrage und versuchen Sie es erneut. |
| `1375-400` | Ungültige Anfrage | Die Erkennung der Dateieigenschaften ist fehlgeschlagen. Geben Sie die Eigenschaften manuell ein. |
| `1376-400` | Ungültige Anfrage | Die Erkennung der Dateieigenschaften wird für Verbindungsspezifikations-ID={connectionSpecId} nicht unterstützt. Bitte geben Sie die Dateieigenschaften manuell an. |
| `1377-400` | Ungültige Anfrage | Der angegebene Wertparameter ist null und kann nicht mit dem Operator {operator} verglichen werden. Geben Sie einen gültigen Wertparameter an und versuchen Sie es erneut. |
| `1378-400` | Ungültige Anfrage | Bei der Validierung der Eingabespalte {column} für den Quellfilter ist ein Fehler aufgetreten. Der Spaltenname sollte eine gültige Spalte in der Tabelle sein. Geben Sie einen gültigen Spaltennamen ein und versuchen Sie es erneut. |
| `1379-400` | Ungültige Anfrage | Bei der Validierung der Eingabe {value} für den Filter an der Quelle ist ein Fehler aufgetreten. Die Spalte DataType an der Quelle lautet {columnDataType} und Wert DataType [Zeichenfolge] stimmt nicht überein. Geben Sie einen gültigen {Wert} ein und versuchen Sie es erneut. |
| `1380-400` | Ungültige Anfrage | Workflow-Ausführung konnte nicht erstellt werden. Fehlermeldung: {message} |
| `1381-400` | Ungültige Anfrage | WindowEndTime={endTime} kann nicht vor Window StartTime={startTime} liegen. Geben Sie eine gültige Endzeit an und versuchen Sie es erneut. |
| `1382-400` | Ungültige Anfrage | Die Delta-Spalte sollte mit dem Wert übereinstimmen, der in den Copy-Transformationen des Flusses vorhanden ist. Bitte geben Sie eine gültige Delta-Spalte ein und versuchen Sie es erneut. |
| `1383-400` | Ungültige Anfrage | Die Delta-Spalte fehlt in den Parametern, die zum Erstellen eines Flusslaufs empfangen wurden. Geben Sie die Delta-Spalte in den Parametern ein und versuchen Sie es erneut. |
| `1384-400` | Ungültige Anfrage | Die params={params}, die zum Erstellen des Fluss-Laufs bereitgestellt werden, sind ungültig oder leer. Geben Sie gültige Parameter an und versuchen Sie es erneut. |
| `1385-400` | Ungültige Anfrage | Der bereitgestellte connectorType={connectorType} wird nicht für die Erstellung von Flussläufen unterstützt. Geben Sie einen gültigen ConnectorType an und versuchen Sie es erneut. |
| `1386-400` | Ungültige Anfrage | Die flowId={flowId} mit scheduleParams frequency={frequency} wird für die Erstellung von Flussläufen nicht unterstützt. Bitte geben Sie eine gültige Häufigkeit ein und versuchen Sie es erneut. |
| `1387-400` | Ungültige Anfrage | Die flowRunId={flowRunId} befindet sich zum erneuten Auslösen in einem ungültigen Status={state}. Versuchen Sie es nach einiger Zeit erneut und wenden Sie sich an den Support, falls das Problem weiterhin besteht. |
| `1388-400` | Ungültige Anfrage | Der Fluss={flow} befindet sich im Status={state} und kann nicht erneut ausgelöst werden. Der Fluss muss für die Neuauslösung aktiviert sein. |
| `1389-400` | Ungültige Anfrage | Beim Analysieren der bereitgestellten base64-kodierten Zeichenfolge ist ein Fehler aufgetreten. Geben Sie eine gültige kodierte Filterzeichenfolge an und versuchen Sie es erneut. |
| `1390-400` | Ungültige Anfrage | Der Operator &quot;nicht&quot;kann nicht mehr als einen Vergleich aufweisen. Bitte geben Sie eine gültige Anzahl der Vergleiche an und versuchen Sie es erneut. |
| `1391-400` | Ungültige Anfrage | SchemaMetaData konnte nicht in sourceConnection für Id={sourceConnectionId} analysiert werden. Überprüfen Sie die schemaMetaData in Ihrer Anfrage und versuchen Sie es erneut. |
| `1392-400` | Ungültige Anfrage | Fehler beim Analysieren von Umwandlungen in der Flussanfrage für flowId={flowId}. Überprüfen Sie die Umwandlungen in Ihrer Anforderung und versuchen Sie es erneut. |
| `1393-400` | Ungültige Anfrage | Der bereitgestellte Parameter {parameter} ist null oder leer. Geben Sie einen gültigen {Parameter} ein und versuchen Sie es erneut. |
| `1394-400` | Ungültige Anfrage | Der Mindestwert für den Parameter {parameter} ist eins. Geben Sie einen gültigen {Parameter} ein und versuchen Sie es erneut. |
| `1395-400` | Ungültige Anfrage | Die Quellverbindung im Fluss ist entweder null oder leer. Geben Sie eine gültige Quellverbindung im Fluss an und versuchen Sie es erneut. |
| `1396-400` | Ungültige Anfrage | Es konnte kein passendes Format gefunden werden. Bitte geben Sie ein entsprechendes Format an und versuchen Sie es erneut. |
| `1397-400` | Ungültige Anfrage | Die bereitgestellte Häufigkeit : {frequency} ist ungültig. Bitte geben Sie eine gültige Häufigkeit ein und versuchen Sie es erneut. |
| `1398-400` | Ungültige Anfrage | Der bereitgestellte Vorgang : {action} wird nicht unterstützt. Überprüfen Sie den angegebenen Vorgang und versuchen Sie es erneut. |
| `1399-400` | Ungültige Anfrage | Ein gültiger requestFileType konnte nicht gefunden werden. Geben Sie einen gültigen requestFileType ein und versuchen Sie es erneut. |
| `1400-400` | Ungültige Anfrage | Der bereitgestellte Parameter &#39;templateType&#39; ist ungültig. Geben Sie einen gültigen Vorlagentyp an und versuchen Sie es erneut. |
| `1401-400` | Ungültige Anfrage | Die angegebene Flusslaufaktion action={flowRunAction} wird nicht unterstützt. Geben Sie eine gültige Flusslaufaktion an und versuchen Sie es erneut. |
| `1402-500` | Interner Fehler | Es ist ein interner Fehler aufgetreten. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1403-400` | Ungültige Anfrage | Die Startzeit ist vorbei und Sie können die Häufigkeit nicht mehr auf einmal ändern. |
| `1404-400` | Ungültige Anfrage | Die Startzeit ist vorbei und Sie können die Aufstockung nicht mehr aktualisieren. |

## Flussdienstausnahmen (1600-1699)

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1600-400` | Ungültige Anfrage | Die Anfrage konnte nicht verarbeitet werden. {detailsMessage} |
| `1601-500` | Interner Fehler | Es ist ein interner Fehler aufgetreten. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1602-404` | Ressource nicht gefunden | Die angeforderte Ressource wurde nicht gefunden. {detailsMessage} |
| `1603-503` | Dienst nicht verfügbar | Der Dienst ist vorübergehend nicht verfügbar. Bitte versuchen Sie es erneut. Wenden Sie sich an den Support, wenn das Problem weiterhin besteht. |
| `1604-504` | Gateway-Zeitüberschreitung | Es ist ein Gateway-Timeout aufgetreten. Bitte versuchen Sie es erneut. Wenden Sie sich an den Support, wenn das Problem weiterhin besteht. |
| `1605-401` | Unerlaubt | Der Benutzer ist nicht autorisiert. {detailsMessage} |
| `1606-403` | Verboten | Der angeforderte Vorgang ist verboten. {detailsMessage} |
| `1607-412` | Vorbedingung fehlgeschlagen | Die von den Headern If-Unmodified-Since oder If-None-Match definierte Bedingung ist nicht erfüllt. {detailsMessage} |

## Fehler in der Dateneinstiegszone

| Fehler-Code | Titel | Detaillierte Nachricht |
| --- | --- | --- |
| `1700-500` | Interner Fehler | Es ist ein interner Fehler aufgetreten. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1701-400` | Ungültige Anfrage | Die bereitgestellte Landingzone ist inaktiv. Bitte aktivieren Sie die Landingzone und versuchen Sie es erneut. |
| `1702-400` | Ungültige Anfrage | Der für die Landingzone angegebene SAS-Typ={sasType} ist nicht zulässig. Geben Sie ein gültiges SAS an und versuchen Sie es erneut. |
| `1703-400` | Ungültige Anfrage | Die Aktualisierung der Anmeldedaten ist nicht zulässig. |
| `1704-400` | Ungültige Anfrage | Die für storageAccountName={accountName} in subscriptionId={subscriptionId} und resourceGroupName={resourceGroupName} zurückgegebenen Schlüssel sind fehlerhaft. Überprüfen Sie Ihre Anfrage und versuchen Sie es erneut. Wenden Sie sich an den Support, wenn das Problem weiterhin besteht. |
| `1705-400` | Ungültige Anfrage | Die bereitgestellte Aktion für Daten-Landingzonen wird nicht unterstützt. Geben Sie eine gültige Aktion an und versuchen Sie es erneut. |
| `1706-400` | Ungültige Anfrage | Die Konfiguration der zulässigen Aktivierungen ist für landing zone={landingZoneType} nicht korrekt konfiguriert. Versuchen Sie es erneut und kontaktieren Sie den Support , falls das Problem weiterhin besteht. |
| `1707-400` | Ungültige Anfrage | Der Dienst konnte nicht gestartet werden, da die Landingzone-Konfiguration nicht null oder leer sein kann. Vergewissern Sie sich, dass die Landingzone-Konfiguration nicht null ist, und versuchen Sie es erneut. |
| `1708-400` | Ungültige Anfrage | Die Containerkonfiguration kann in landingZoneType={landingZoneType} nicht null sein. Stellen Sie sicher, dass die Container-Konfiguration nicht null ist, und versuchen Sie es erneut. |
| `1709-400` | Ungültige Anfrage | Die SAS-Details können für {tokenConfig} in landingZoneType={landingZoneType} nicht null sein. Geben Sie in der Konfiguration ein gültiges SAS an und versuchen Sie es erneut. |
| `1710-400` | Ungültige Anfrage | Die bereitgestellte Landingzone des Typs: {landingZoneUseCase} wird nicht unterstützt. Bitte geben Sie einen gültigen Landingzonentyp an und versuchen Sie es erneut. |
| `1711-400` | Ungültige Anfrage | Die SAS-Details wurden für die bereitgestellte Data Landingzone des Typs nicht gefunden: {landingZoneUseCase}. Überprüfen Sie, ob SAS-Details für den angegebenen Landingzonentyp angegeben wurden. |
| `1712-400` | Ungültige Anfrage | Die bereitgestellte Aktion für die Landingzone : {actionType} ist nicht zulässig. Bitte geben Sie eine gültige Landingzone-Aktion an und versuchen Sie es erneut. |
| `1713-400` | Ungültige Anfrage | Der {OperationType} ist für den bereitgestellten {tokenType} nicht zulässig. Überprüfen Sie Ihre Anfrage und versuchen Sie es erneut. |
| `1714-400` | Ungültige Anfrage | clientId={clientId} darf diesen Vorgang nicht ausführen. Überprüfen Sie Ihre Anfrage mit Berechtigungen und versuchen Sie es erneut. |