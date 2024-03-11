---
title: Amazon S3-Verbindung
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem S3-Speicher in Amazon Web Services (AWS), um in regelmäßigen Abständen CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Behälter zu exportieren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8771aa0df001e8ef81d4ad712f4d1f9661b405b2
workflow-type: tm+mt
source-wordcount: '1440'
ht-degree: 51%

---

# [!DNL Amazon S3]-Verbindung {#s3-connection}

## Ziel-Änderungsprotokoll {#changelog}

+++ Änderungsprotokoll anzeigen


| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| Januar 2024 | Funktions- und Dokumentationsaktualisierung | Der Amazon S3-Ziel-Connector unterstützt jetzt einen neuen Authentifizierungstyp für Rollen. Mehr darüber erfahren Sie im Abschnitt [Authentifizierungsabschnitt](#assumed-role-authentication). |
| Juli 2023 | Funktions- und Dokumentationsaktualisierung | Mit der Experience Platform-Version vom Juli 2023 wird die [!DNL Amazon S3] Das Ziel bietet neue Funktionen, wie unten aufgeführt: <br><ul><li>[Unterstützung für den Datensatzexport](/help/destinations/ui/export-datasets.md)</li><li>Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Möglichkeit zum Festlegen benutzerdefinierter Datei-Kopfzeilen in exportierten Dateien durch den [verbesserten Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Möglichkeit zum Anpassen der Formatierung exportierter CSV-Datendateien](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Verbinden Sie Ihre [!DNL Amazon S3] Speicher über API oder Benutzeroberfläche {#connect-api-or-ui}

* So stellen Sie eine Verbindung zu Ihrer [!DNL Amazon S3] Speicherort mithilfe der Platform-Benutzeroberfläche, lesen Sie die Abschnitte . [Mit Ziel verbinden](#connect) und [Aktivieren von Zielgruppen für dieses Ziel](#activate) unten.
* So stellen Sie eine Verbindung zu Ihrer [!DNL Amazon S3] Speicherort programmgesteuert speichern, lesen Sie die Anleitung zum [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe des Tutorials zur Flow Service-API](../../api/activate-segments-file-based-destinations.md).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![In der Benutzeroberfläche hervorgehobener profilbasierter Exporttyp für Amazon S3.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Exportieren von Datensätzen {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* Anleitung [Datensätze mithilfe der Benutzeroberfläche von Platform exportieren](/help/destinations/ui/export-datasets.md).
* Anleitung [Datensätze programmgesteuert mit der Flow Service-API exportieren](/help/destinations/api/export-datasets.md).

## Dateiformat der exportierten Daten {#file-format}

Beim Exportieren *Zielgruppendaten*, erstellt Platform eine `.csv`, `parquet`oder `.json` -Datei an dem Speicherort gespeichert, den Sie bereitgestellt haben. Weitere Informationen zu den Dateien finden Sie unter [unterstützte Dateiformate für den Export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) im Tutorial zur Aktivierung der Zielgruppe.

Beim Exportieren *Datensätze*, erstellt Platform eine `.parquet` oder `.json` -Datei an dem Speicherort gespeichert, den Sie bereitgestellt haben. Weitere Informationen zu den Dateien finden Sie unter [Überprüfen des erfolgreichen Datensatzexports](../../ui/export-datasets.md#verify) im Tutorial zum Exportieren von Datensätzen .

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Öffentlicher RSA-Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Schlüssel finden Sie im folgenden Dokumentations-Link."

Füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]**. Das Amazon S3-Ziel unterstützt zwei Authentifizierungsmethoden:

* Zugriffsschlüssel und Authentifizierung mit geheimen Schlüsseln
* Authentifizierung der übernommenen Rolle

#### Zugriffsschlüssel und Authentifizierung mit geheimen Schlüsseln

Verwenden Sie diese Authentifizierungsmethode, wenn Sie Ihren Amazon S3-Zugriffsschlüssel und den geheimen Schlüssel eingeben möchten, damit Experience Platform Daten in Ihre Amazon S3-Eigenschaften exportieren kann.

![Bild der erforderlichen Felder bei Auswahl der Zugriffsschlüssel- und der geheimen Schlüsselauthentifizierung.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]-Zugriffsschlüssel** und geheimer **[!DNL Amazon S3]-Schlüssel**: Generieren Sie in [!DNL Amazon S3] ein `access key - secret access key`-Paar, um Platform Zugriff auf Ihr [!DNL Amazon S3]-Konto zu gewähren. Weitere Informationen finden Sie in der [Amazon Web Services-Dokumentation](https://docs.aws.amazon.com/de_de/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

  ![Bild, das ein Beispiel eines korrekt formatierten PGP-Schlüssels in der Benutzeroberfläche anzeigt.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Übernommene Rolle {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Authentifizierung der übernommenen Rolle"
>abstract="Verwenden Sie diese Authentifizierungstyp, wenn Sie Konto- und Geheimschlüssel nicht mit Adobe teilen möchten. Stattdessen stellt Experience Platform über einen rollenbasierten Zugriff eine Verbindung zu Ihrem Amazon S3-Speicherort her. Fügen Sie den ARN der Rolle ein, die Sie in AWS für die Adobe-Benutzerin bzw. den -Benutzer erstellt haben. Das Muster ist vergleichbar mit `arn:aws:iam::800873819705:role/destinations-role-customer` "

![Bild der erforderlichen Felder bei Auswahl der angenommenen Rollenauthentifizierung.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

Verwenden Sie diese Authentifizierungstyp, wenn Sie Konto- und Geheimschlüssel nicht mit Adobe teilen möchten. Stattdessen stellt Experience Platform über rollenbasierten Zugriff eine Verbindung zu Ihrem Amazon S3-Standort her.

Dazu müssen Sie in der AWS-Konsole einen angenommenen Benutzer für das Adobe mit der [erforderliche Berechtigungen](#required-s3-permission) , um in Ihre Amazon S3-Buckets zu schreiben. Erstellen Sie eine **[!UICONTROL Vertrauenswürdige Entität]** in AWS mit dem Adobe-Konto **[!UICONTROL 670664943635]**. Weitere Informationen finden Sie im Abschnitt [AWS-Dokumentation zum Erstellen von Rollen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).

* **[!DNL Role]**: Fügen Sie den ARN der Rolle ein, die Sie in AWS für den Adobe-Benutzer erstellt haben. Das Muster ähnelt dem `arn:aws:iam::800873819705:role/destinations-role-customer`.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Behältername"
>abstract="Muss zwischen 3 und 63 Zeichen lang sein. Muss mit einem Buchstaben oder einer Zahl beginnen und enden. Darf nur Kleinbuchstaben, Zahlen oder Bindestriche ( - ) enthalten. Darf nicht als IP-Adresse formatiert sein (z. B. 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Ordnerpfad"
>abstract="Darf nur die Zeichen A-Z, a-z, 0-9 und die folgenden Sonderzeichen enthalten: `/!-_.'()"^[]+$%.*"`. Um einen Ordner pro Zielgruppendatei zu erstellen, fügen Sie das Makro `/%SEGMENT_NAME%` oder `/%SEGMENT_ID%` oder `/%SEGMENT_NAME%/%SEGMENT_ID%` in das Textfeld ein. Makros können nur am Ende des Ordnerpfads eingefügt werden. Sehen Sie sich Beispiele für Makros in der Dokumentation an."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=de#use-macros" text="Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort"

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung dieses Ziels ein.
* **[!UICONTROL Behältername]**: Geben Sie den Namen des [!DNL Amazon S3]-Behälters ein, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL Dateityp]**: Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Wenn Sie [!UICONTROL CSV] können Sie auch [Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den Experience Platform für die exportierten Dateien verwenden soll.
* **[!UICONTROL Manifestdatei einschließen]**: Schalten Sie diese Option ein, wenn Sie möchten, dass die Exporte eine JSON-Manifestdatei mit Informationen zum Exportspeicherort, zur Exportgröße und mehr enthalten. Das Manifest wird im Format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. Anzeigen von [Beispielmanifestdatei](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Die Manifestdatei enthält die folgenden Felder:
   * `flowRunId`: Die [dataflow run](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die die exportierte Datei generiert hat.
   * `scheduledTime`: Die Uhrzeit in UTC, zu der die Datei exportiert wurde.
   * `exportResults.sinkPath`: Der Pfad in Ihrem Speicherort, unter dem die exportierte Datei abgelegt wird.
   * `exportResults.name`: Der Name der exportierten Datei.
   * `size`: Die Größe der exportierten Datei in Byte.

>[!TIP]
>
>Im Zielverbindungs-Workflow können Sie einen benutzerdefinierten Ordner in Ihrem Amazon S3-Speicher pro exportierter Zielgruppendatei erstellen. Anweisungen finden Sie unter [Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort](overview.md#use-macros).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

### Erforderliche [!DNL Amazon S3]-Berechtigungen {#required-s3-permission}

Um Daten erfolgreich mit Ihrem [!DNL Amazon S3]-Speicherort zu verbinden und dorthin zu exportieren, erstellen Sie ein Benutzerprofil für Identitäts- und Zugriffsverwaltung (IAM) für [!DNL Platform] in [!DNL Amazon S3] und weisen Berechtigungen für die folgenden Aktionen zu:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihren [!DNL Amazon S3]-Speicher überprüfen, und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Zulassungsliste von IP-Adressen {#ip-address-allow-list}

Siehe Abschnitt [IP-Adressen-Zulassungsliste](ip-address-allow-list.md) , wenn Sie Adobe-IPs zu einer Zulassungsliste hinzufügen müssen.