---
keywords: Experience Platform;home;popular topics;Query service;query service;connect;connect to query service;SSL;ssl;sslmode
title: SSL-Optionen für Query Service
description: Erfahren Sie mehr über die SSL-Unterstützung für Verbindungen von Drittanbietern mit Adobe Experience Platform Query Service und über die Verbindung mit dem verifizierbaren SSL-Modus.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 229ce98da8f1c97e421ef413826b0d23754d16df
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 1%

---

# [!DNL Query Service] SSL-Optionen

Zur Erhöhung der Sicherheit bietet Adobe Experience Platform [!DNL Query Service] native Unterstützung für SSL-Verbindungen, um Client-/Serverkommunikationen zu verschlüsseln. In diesem Dokument werden die verfügbaren SSL-Optionen für Client-Verbindungen von Drittanbietern mit [!DNL Query Service] und die Verbindung mithilfe des SSL-Parameterwerts `verify-full` beschrieben.

## Voraussetzungen

In diesem Dokument wird davon ausgegangen, dass Sie bereits eine Desktop-Client-Anwendung eines Drittanbieters zur Verwendung mit Ihren Platform-Daten heruntergeladen haben. Spezifische Anweisungen zur Integration von SSL-Sicherheit bei der Verbindung mit einem Drittanbieter-Client finden Sie in der entsprechenden Dokumentation zum Verbindungshandbuch. Eine Liste aller von [!DNL Query Service] unterstützten Clients finden Sie in der [Übersicht über Client-Verbindungen](./overview.md) .

## Verfügbare SSL-Optionen {#available-ssl-options}

Platform unterstützt verschiedene SSL-Optionen, um Ihren Datensicherheitsanforderungen gerecht zu werden und den Verarbeitungsaufwand für Verschlüsselung und Schlüsselaustausch auszugleichen.

Die verschiedenen `sslmode` -Parameterwerte bieten unterschiedliche Schutzstufen. Durch die Verschlüsselung Ihrer Daten in Bewegung mit SSL-Zertifikaten hilft es, Angriffe, Abhören und Identitätswechsel vom Typ &quot;man-in-the-Middle&quot;(MITM) zu verhindern. Die nachstehende Tabelle enthält eine Aufschlüsselung der verschiedenen verfügbaren SSL-Modi und des von ihnen gebotenen Schutzes.

>[!NOTE]
>
> Der SSL-Wert &quot;`disable`&quot; wird von Adobe Experience Platform aufgrund der erforderlichen Einhaltung von Datenschutzbestimmungen nicht unterstützt.

| sslmode | Abhörschutz | MITM-Schutz | Beschreibung |
|---|---|---|---|
| `allow` | Teilweise | Nein | Sicherheit ist keine Priorität, Schnelligkeit und ein geringer Verarbeitungsaufwand sind wichtiger. Dieser Modus entscheidet sich nur dann für die Verschlüsselung, wenn der Server darauf besteht. |
| `prefer` | Teilweise | Nein | Verschlüsselung ist nicht erforderlich, die Kommunikation wird jedoch verschlüsselt, wenn der Server sie unterstützt. |
| `require` | Ja | Nein | Verschlüsselung ist bei allen Kommunikationen erforderlich. Das Netzwerk ist vertrauenswürdig, um eine Verbindung zum richtigen Server herzustellen. Die Überprüfung des SSL-Zertifikats des Servers ist nicht erforderlich. |
| `verify-ca` | Ja | Abhängig von CA-Richtlinien | Verschlüsselung ist bei allen Kommunikationen erforderlich. Vor der Datenfreigabe ist eine Servervalidierung erforderlich. Dazu müssen Sie ein Stammzertifikat im Basisverzeichnis von [!DNL PostgreSQL] einrichten. [Details werden unter ](#instructions) angegeben. |
| `verify-full` | Ja | Ja | Verschlüsselung ist bei allen Kommunikationen erforderlich. Vor der Datenfreigabe ist eine Servervalidierung erforderlich. Dazu müssen Sie ein Stammzertifikat im Basisverzeichnis von [!DNL PostgreSQL] einrichten. [Details werden unter ](#instructions) angegeben. |

>[!NOTE]
>
>Der Unterschied zwischen `verify-ca` und `verify-full` hängt von der Richtlinie der Stammzertifikatbehörde (CA) ab. Wenn Sie Ihre eigene lokale Zertifizierungsstelle für die Ausgabe privater Zertifikate für Ihre Anwendungen erstellt haben, bietet die Verwendung von `verify-ca` oft genug Schutz. Bei Verwendung einer öffentlichen Zertifizierungsstelle erlaubt `verify-ca` Verbindungen zu einem Server, die möglicherweise von einer anderen Person bei der Zertifizierungsstelle registriert wurden. `verify-full` sollte immer mit einer öffentlichen Stamm-CA verwendet werden.

Bei der Herstellung einer Drittanbieter-Verbindung zu einer Platform-Datenbank wird empfohlen, mindestens `sslmode=require` zu verwenden, um eine sichere Verbindung für Ihre in Bewegung befindlichen Daten sicherzustellen. Der SSL-Modus `verify-full` wird für die Verwendung in den meisten sicherheitskritischen Umgebungen empfohlen.

## Einrichten eines Stammzertifikats für die Serverüberprüfung {#root-certificate}

>[!IMPORTANT]
>
>Die TLS/SSL-Zertifikate für Produktionsumgebungen für die Query Service Interactive Postgres API wurden am Mittwoch, 24. Januar 2024 aktualisiert.<br>Obwohl dies eine jährliche Anforderung ist, hat sich in diesem Fall auch das Stammzertifikat in der Kette geändert, da der Adobe TLS/SSL-Zertifikatanbieter seine Zertifikathierarchie aktualisiert hat. Dies kann sich auf bestimmte Postgres-Clients auswirken, wenn in ihrer Liste der Zertifizierungsstellen das Stammzertifikat fehlt. Beispielsweise muss einem PSQL-CLI-Client möglicherweise die Root-Zertifikate zu einer expliziten Datei `~/postgresql/root.crt` hinzugefügt werden, da dies andernfalls zu einem Fehler führen kann. Beispiel: `psql: error: SSL error: certificate verify failed`. Weitere Informationen zu diesem Problem finden Sie in der [offiziellen PostgreSQL-Dokumentation](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) .<br>Das Stammzertifikat, das hinzugefügt werden soll, kann von [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem) heruntergeladen werden.

Um eine sichere Verbindung sicherzustellen, muss die SSL-Nutzung sowohl auf dem Client als auch auf dem Server konfiguriert werden, bevor die Verbindung hergestellt wird. Wenn die SSL-Verschlüsselung nur auf dem Server konfiguriert ist, sendet der Client möglicherweise vertrauliche Informationen wie Passwörter, bevor festgestellt wird, dass der Server hohe Sicherheit erfordert.

Standardmäßig führt [!DNL PostgreSQL] keine Überprüfung des Serverzertifikats durch. Um die Identität des Servers zu überprüfen und sicherzustellen, dass eine sichere Verbindung besteht, bevor vertrauliche Daten gesendet werden (im SSL-Modus `verify-full` ), müssen Sie ein Stammzertifikat (selbstsigniert) auf Ihrem lokalen Computer (`root.crt`) und ein vom Stammzertifikat auf dem Server signiertes Blattzertifikat platzieren.

Wenn der Parameter `sslmode` auf `verify-full` gesetzt ist, überprüft libpq, ob der Server vertrauenswürdig ist, indem die Zertifikatskette bis zum Stammzertifikat überprüft wird, das auf dem Client gespeichert ist. Anschließend wird überprüft, ob der Hostname mit dem im Serverzertifikat gespeicherten Namen übereinstimmt.

Um die Überprüfung des Serverzertifikats zu ermöglichen, müssen Sie mindestens ein Stammzertifikat (`root.crt`) in der Datei [!DNL PostgreSQL] in Ihrem Basisverzeichnis ablegen. Der Dateipfad ähnelt `~/.postgresql/root.crt`.

## Aktivieren Sie den Verifizierung-vollständigen SSL-Modus für die Verwendung mit einer [!DNL Query Service]-Verbindung eines Drittanbieters {#instructions}

Wenn Sie eine strengere Sicherheitskontrolle als `sslmode=require` benötigen, können Sie die hervorgehobenen Schritte ausführen, um einen Drittanbieter-Client mit dem SSL-Modus `verify-full` mit [!DNL Query Service] zu verbinden.

>[!NOTE]
>
>Zum Erzielen eines SSL-Zertifikats stehen viele Optionen zur Verfügung. Aufgrund des wachsenden Trends bei Schurkenzertifikaten wird DigiCert in diesem Handbuch verwendet, da sie ein vertrauenswürdiger globaler Anbieter von TLS/SSL-, PKI-, IoT- und Signaturlösungen mit hoher Sicherheit sind.

1. Navigieren Sie zur Liste der verfügbaren DigiCert-Stammzertifikate ](https://www.digicert.com/kb/digicert-root-certificates.htm).[
1. Suchen Sie in der Liste der verfügbaren Zertifikate nach &quot;[!DNL DigiCert Global Root G2]&quot;.
1. Wählen Sie [!DNL **PEM herunterladen**] aus, um die Datei auf Ihren lokalen Computer herunterzuladen.
   ![Die Liste der verfügbaren DigiCert-Stammzertifikate mit hervorgehobenem Download-PEM.](../images/clients/ssl-modes/digicert.png)
1. Benennen Sie die Sicherheitszertifikatdatei in &quot;`root.crt`&quot;um.
1. Kopieren Sie die Datei in den Ordner &quot;[!DNL PostgreSQL]&quot;. Der erforderliche Dateipfad unterscheidet sich je nach Betriebssystem. Wenn der Ordner noch nicht vorhanden ist, erstellen Sie den Ordner.
   - Wenn Sie macOS verwenden, lautet der Pfad `/Users/<username>/.postgresql`
   - Wenn Sie Windows verwenden, lautet der Pfad `%appdata%\postgresql`

>[!TIP]
>
>Um Ihren `%appdata%`-Dateispeicherort auf einem Windows-Betriebssystem zu finden, drücken Sie ⊞ **Win + R** und geben Sie `%appdata%` in das Suchfeld ein.

Nachdem die CRT-Datei [!DNL DigiCert Global Root G2] im Ordner [!DNL PostgreSQL] verfügbar ist, können Sie mit der Option `sslmode=verify-full` oder `sslmode=verify-ca` eine Verbindung zu [!DNL Query Service] herstellen.

## Nächste Schritte

Durch Lesen dieses Dokuments erhalten Sie ein besseres Verständnis der verfügbaren SSL-Optionen zum Verbinden eines Drittanbieter-Clients mit [!DNL Query Service] sowie darüber, wie Sie die SSL-Option `verify-full` aktivieren können, um Ihre in Bewegung befindlichen Daten zu verschlüsseln.

Wenn Sie dies noch nicht getan haben, folgen Sie den Anweisungen unter [Verbinden eines Drittanbieter-Clients mit  [!DNL Query Service]](./overview.md).
