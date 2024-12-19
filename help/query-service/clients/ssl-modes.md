---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;verbinden;mit Abfrage-Service verbinden;SSL;sslmode;
title: SSL-Optionen des Abfrage-Services
description: Erfahren Sie mehr über die SSL-Unterstützung für Drittanbieterverbindungen zum Adobe Experience Platform Query Service und darüber, wie Sie eine Verbindung mit dem vollständigen SSL-Überprüfungsmodus herstellen.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 37c30fc1a040efbce0c221c10b36e105d5b1a962
workflow-type: tm+mt
source-wordcount: '1008'
ht-degree: 1%

---

# SSL-Optionen [!DNL Query Service]

Zur Erhöhung der Sicherheit bietet Adobe Experience Platform [!DNL Query Service] native Unterstützung für SSL-Verbindungen zur Verschlüsselung der Client/Server-Kommunikation. In diesem Dokument werden die verfügbaren SSL-Optionen für Client-Verbindungen von Drittanbietern zu [!DNL Query Service] und die Verbindung mit dem `verify-full` SSL-Parameterwert beschrieben.

## Voraussetzungen

In diesem Dokument wird davon ausgegangen, dass Sie bereits ein Desktop-Client-Programm eines Drittanbieters zur Verwendung mit Ihren Platform-Daten heruntergeladen haben. Spezifische Anweisungen zur Integration der SSL-Sicherheit bei der Verbindung mit einem Drittanbieter-Client finden Sie in der entsprechenden Dokumentation zum Verbindungshandbuch. Eine Liste aller [!DNL Query Service] unterstützten Clients finden Sie unter [Client-Verbindungen - Übersicht](./overview.md).

## Verfügbare SSL-Optionen {#available-ssl-options}

Platform unterstützt verschiedene SSL-Optionen, um Ihre Datensicherheitsanforderungen zu erfüllen und den Verarbeitungsaufwand für Verschlüsselung und Schlüsselaustausch auszugleichen.

Die verschiedenen `sslmode`-Parameterwerte bieten unterschiedliche Schutzebenen. Durch die Verschlüsselung Ihrer Daten in Bewegung mit SSL-Zertifikaten wird verhindert, dass „Man-in-the-Middle“ (MITM)-Angriffe, Abhören und Identitätswechsel stattfinden. Die nachstehende Tabelle enthält eine Aufschlüsselung der verschiedenen verfügbaren SSL-Modi und des Schutzniveaus, das sie bieten.

>[!NOTE]
>
> Der SSL-Wert `disable` wird von Adobe Experience Platform aufgrund der erforderlichen Datenschutzkonformität nicht unterstützt.

| SSLMode | Abhörschutz | MITM-Schutz | Beschreibung |
|---|---|---|---|
| `allow` | Ja | Nein | Verschlüsselung ist für alle Kommunikationen erforderlich. Das Netzwerk wird für die Verbindung mit dem richtigen Server als vertrauenswürdig eingestuft. |
| `prefer` | Ja | Nein | Verschlüsselung ist für alle Kommunikationen erforderlich. Das Netzwerk wird für die Verbindung mit dem richtigen Server als vertrauenswürdig eingestuft. |
| `require` | Ja | Nein | Verschlüsselung ist für alle Kommunikationen erforderlich. Das Netzwerk wird für die Verbindung mit dem richtigen Server als vertrauenswürdig eingestuft. Die Validierung des SSL-Zertifikats des Servers ist nicht erforderlich. |
| `verify-ca` | Ja | Hängt von CA-Policy ab | Verschlüsselung ist für alle Kommunikationen erforderlich. Vor der Freigabe von Daten ist eine Validierung durch den Server erforderlich. Dazu müssen Sie ein Stammzertifikat in Ihrem [!DNL PostgreSQL] Basisverzeichnis einrichten. [Details finden Sie unten](#instructions) |
| `verify-full` | Ja | Ja | Verschlüsselung ist für alle Kommunikationen erforderlich. Vor der Freigabe von Daten ist eine Validierung durch den Server erforderlich. Dazu müssen Sie ein Stammzertifikat in Ihrem [!DNL PostgreSQL] Basisverzeichnis einrichten. [Details finden Sie unten](#instructions). |

>[!NOTE]
>
>Der Unterschied zwischen `verify-ca` und `verify-full` hängt von der Richtlinie der Stammzertifikatbehörde (CA) ab. Wenn Sie Ihre eigene lokale Zertifizierungsstelle erstellt haben, um private Zertifikate für Ihre Programme auszustellen, bietet die Verwendung von `verify-ca` oft ausreichend Schutz. Bei Verwendung einer öffentlichen Zertifizierungsstelle ermöglicht `verify-ca` Verbindungen zu einem Server, der möglicherweise von einer anderen Person bei der Zertifizierungsstelle registriert wurde. `verify-full` sollte immer mit einer öffentlichen Stamm-CA verwendet werden.

Beim Herstellen einer Drittanbieterverbindung zu einer Platform-Datenbank wird empfohlen, mindestens `sslmode=require` zu verwenden, um eine sichere Verbindung für Ihre bewegten Daten zu gewährleisten. Der `verify-full` SSL-Modus wird für die Verwendung in den meisten sicherheitsempfindlichen Umgebungen empfohlen.

## Einrichten eines Stammzertifikats für die Serverüberprüfung {#root-certificate}

>[!IMPORTANT]
>
>Die TLS/SSL-Zertifikate in Produktionsumgebungen für die interaktive Postgres-API des Abfrage-Services wurden am Mittwoch, 24. Januar 2024 aktualisiert.<br>Obwohl dies eine jährliche Anforderung ist, hat sich in diesem Fall auch das Stammzertifikat in der Kette geändert, da die Zertifikatanbieter von Adobe TLS/SSL ihre Zertifikatshierarchie aktualisiert haben. Dies kann sich auf bestimmte Postgres-Clients auswirken, wenn in ihrer Liste der Zertifizierungsstellen das Stammzertifikat fehlt. Beispielsweise müssen einem PSQL-CLI-Client die Stammzertifikate möglicherweise zu einer expliziten `~/postgresql/root.crt` hinzugefügt werden, da dies sonst zu einem Fehler führen kann. Beispiel: `psql: error: SSL error: certificate verify failed`. Weitere Informationen zu [ Problem finden Sie in ](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) offiziellen PostgreSQL-Dokumentation .<br>Das hinzuzufügende Stammzertifikat kann von [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem heruntergeladen ](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Um eine sichere Verbindung zu gewährleisten, muss die SSL-Nutzung sowohl auf dem Client als auch auf dem Server konfiguriert werden, bevor die Verbindung hergestellt wird. Wenn SSL nur auf dem Server konfiguriert ist, sendet der Client möglicherweise vertrauliche Informationen wie Passwörter, bevor festgestellt wird, dass der Server hohe Sicherheit erfordert.

Standardmäßig führt [!DNL PostgreSQL] keine Überprüfung des Serverzertifikats durch. Um die Identität des Servers zu überprüfen und eine sichere Verbindung sicherzustellen, bevor vertrauliche Daten gesendet werden (im Rahmen des SSL-`verify-full`-Modus), müssen Sie ein Stammzertifikat (selbstsigniert) auf Ihrem lokalen Computer (`root.crt`) und ein Blattzertifikat, das vom Stammzertifikat signiert ist, auf dem Server platzieren.

Wenn der `sslmode` Parameter auf `verify-full` gesetzt ist, überprüft libpq, ob der Server vertrauenswürdig ist, indem die Zertifikatskette bis zum Stammzertifikat überprüft wird, das auf dem Client gespeichert ist. Anschließend wird überprüft, ob der Hostname mit dem im Serverzertifikat gespeicherten Namen übereinstimmt.

Um die Verifizierung des Serverzertifikats zu ermöglichen, müssen Sie ein oder mehrere Stammzertifikate (`root.crt`) in der [!DNL PostgreSQL] in Ihrem Basisverzeichnis platzieren. Der Dateipfad ähnelt `~/.postgresql/root.crt`.

## Aktivieren des vollständigen SSL-Überprüfungsmodus für die Verwendung mit einer [!DNL Query Service] von Drittanbietern {#instructions}

Wenn Sie eine strengere Sicherheitskontrolle als `sslmode=require` benötigen, können Sie die hervorgehobenen Schritte ausführen, um einen Drittanbieter-Client über `verify-full` SSL-Modus mit [!DNL Query Service] zu verbinden.

>[!NOTE]
>
>Es gibt viele Möglichkeiten, ein SSL-Zertifikat zu erhalten. Aufgrund des zunehmenden Trends bei Rogue-Zertifikaten wird DigiCert in diesem Handbuch verwendet, da DigiCert ein vertrauenswürdiger globaler Anbieter von High-Assurance-TLS/SSL-, PKI-, IoT- und Signaturlösungen ist.

1. Navigieren Sie zur [Liste der verfügbaren DigiCert-Stammzertifikate](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Suchen Sie in der Liste der verfügbaren Zertifikate nach &quot;[!DNL DigiCert Global Root G2]&quot;.
1. Wählen Sie [!DNL **PEM herunterladen**], um die Datei auf Ihren lokalen Computer herunterzuladen.
   ![Die Liste der verfügbaren DigiCert-Stammzertifikate mit hervorgehobener Option „PEM herunterladen“.](../images/clients/ssl-modes/digicert.png)
1. Benennen Sie die Sicherheitszertifikatdatei in `root.crt` um.
1. Kopieren Sie die Datei in den [!DNL PostgreSQL]. Der erforderliche Dateipfad unterscheidet sich je nach Betriebssystem. Wenn der Ordner noch nicht vorhanden ist, erstellen Sie ihn.
   - Wenn Sie macOS verwenden, lautet der Pfad `/Users/<username>/.postgresql`
   - Wenn Sie Windows verwenden, lautet der Pfad `%appdata%\postgresql`

>[!TIP]
>
>Drücken Sie zum Auffinden des `%appdata%`-Speicherorts auf einem Windows-Betriebssystem ⊞ **Win + R** und geben Sie `%appdata%` in das Suchfeld ein.

Nachdem die [!DNL DigiCert Global Root G2] CRT-Datei in Ihrem [!DNL PostgreSQL]-Ordner verfügbar ist, können Sie mit der Option `sslmode=verify-full` oder `sslmode=verify-ca` eine Verbindung zu [!DNL Query Service] herstellen.

## Nächste Schritte

Durch dieses Dokument erhalten Sie ein besseres Verständnis der verfügbaren SSL-Optionen zum Verbinden eines Drittanbieter-Clients mit [!DNL Query Service] und darüber, wie Sie die `verify-full` SSL-Option aktivieren, um Ihre Daten in Bewegung zu verschlüsseln.

Wenn Sie dies noch nicht getan haben, befolgen Sie die Anweisungen unter [Verbinden eines Drittanbieter-Clients mit [!DNL Query Service]](./overview.md).
