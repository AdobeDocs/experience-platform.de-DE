---
title: Amazon S3-Verbindung
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem S3-Speicher in Amazon Web Services (AWS), um in regelmäßigen Abständen CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Behälter zu exportieren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 36%

---

# [!DNL Amazon S3]-Verbindung {#s3-connection}

## Ziel-Änderungsprotokoll {#changelog}

+++ Änderungsprotokoll anzeigen


| Veröffentlichungsmonat | Art der Aktualisierung | Beschreibung |
|---|---|---|
| Januar 2024 | Funktions- und Dokumentationsaktualisierung | Der Amazon S3-Ziel-Connector unterstützt jetzt einen neuen Authentifizierungstyp mit angenommener Rolle. Weitere Informationen hierzu finden Sie [ Abschnitt „Authentifizierung](#assumed-role-authentication). |
| Juli 2023 | Funktions- und Dokumentationsaktualisierung | Mit der Experience Platform-Version vom Juli 2023 bietet das [!DNL Amazon S3]-Ziel neue Funktionen, wie unten aufgeführt: <br><ul><li>[Unterstützung für den Datensatzexport](/help/destinations/ui/export-datasets.md)</li><li>Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).</li><li>Möglichkeit zum Festlegen benutzerdefinierter Datei-Kopfzeilen in exportierten Dateien durch den [verbesserten Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).</li><li>[Möglichkeit zum Anpassen der Formatierung exportierter CSV-Datendateien](/help/destinations/ui/batch-destinations-file-formatting-options.md).</li></ul> |

{style="table-layout:auto"}

+++

## Herstellen einer Verbindung zu Ihrem [!DNL Amazon S3] über API oder Benutzeroberfläche {#connect-api-or-ui}

* Um über die Experience Platform-Benutzeroberfläche eine Verbindung zu Ihrem [!DNL Amazon S3]-Speicherort herzustellen, lesen Sie die Abschnitte [Mit dem Ziel verbinden](#connect) und [Zielgruppen für dieses Ziel aktivieren](#activate).
* Um programmgesteuert eine Verbindung zu Ihrem [!DNL Amazon S3]-Speicherort herzustellen, lesen Sie das Handbuch zum [ von Zielgruppen für dateibasierte Ziele mithilfe des Tutorials zur Flow Service-API](../../api/activate-segments-file-based-destinations.md).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![Auf dem Amazon S3-Profil basierender Exporttyp, der in der Benutzeroberfläche hervorgehoben ist.](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Datensätze exportieren {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* So [ Sie Datensätze mithilfe der Benutzeroberfläche von Experience Platform ](/help/destinations/ui/export-datasets.md).
* So [ Sie Datensätze mithilfe der Flow Service-API programmgesteuert ](/help/destinations/api/export-datasets.md).

## Dateiformat der exportierten Daten {#file-format}

Beim Exportieren *Zielgruppendaten* erstellt Experience Platform eine `.csv`-, `parquet`- oder `.json`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Unterstützte Dateiformate für den Export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) im Tutorial zur Zielgruppenaktivierung.

Beim Exportieren *Datensätze* erstellt Experience Platform eine `.parquet`- oder `.json`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Überprüfen eines erfolgreichen Datensatzexports](../../ui/export-datasets.md#verify) im Tutorial zum Exportieren von Datensätzen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. ](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Zielkonfigurations-Workflow die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="Öffentlicher RSA-Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Schlüssel finden Sie im folgenden Dokumentations-Link."

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Connect to destination]** aus. Das Amazon S3-Ziel unterstützt zwei Authentifizierungsmethoden:

* Authentifizierung mit Zugriffsschlüssel und Geheimschlüssel
* Authentifizierung der übernommenen Rolle

#### Authentifizierung mit S3-Zugriffsschlüssel und geheimen Schlüssel

Verwenden Sie diese Authentifizierungsmethode, wenn Sie Ihren Amazon S3-Zugriffsschlüssel und geheimen Schlüssel eingeben möchten, damit Experience Platform Daten in Ihre Amazon S3-Eigenschaften exportieren kann.

![Abbildung der erforderlichen Felder bei der Auswahl von Zugriffsschlüssel und Authentifizierung mit geheimen Schlüsseln.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/access-key-secret-key-authentication.png)

* **[!DNL Amazon S3]-** und **[!DNL Amazon S3]geheimer Schlüssel**: Generieren Sie [!DNL Amazon S3] ein `access key - secret access key`, um Experience Platform Zugriff auf Ihr [!DNL Amazon S3]-Konto zu gewähren. Weitere Informationen finden Sie in der [Amazon Web Services-Dokumentation](https://docs.aws.amazon.com/de_de/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Encryption key]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

  ![Abbildung mit einem Beispiel für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

#### Authentifizierung mit der übernommenen S3-Rolle {#assumed-role-authentication}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_assumed_role"
>title="Authentifizierung der übernommenen Rolle"
>abstract="Verwenden Sie diese Authentifizierungstyp, wenn Sie Konto- und Geheimschlüssel nicht mit Adobe teilen möchten. Stattdessen stellt Experience Platform über einen rollenbasierten Zugriff eine Verbindung zu Ihrem Amazon S3-Speicherort her. Fügen Sie den ARN der Rolle ein, die Sie in AWS für die Adobe-Benutzerin bzw. den -Benutzer erstellt haben. Das Muster ist vergleichbar mit `arn:aws:iam::800873819705:role/destinations-role-customer` "

Verwenden Sie diese Authentifizierungstyp, wenn Sie Konto- und Geheimschlüssel nicht mit Adobe teilen möchten. Stattdessen stellt Experience Platform mithilfe des rollenbasierten Zugriffs eine Verbindung zu Ihrem Amazon S3-Speicherort her.

![Bild der erforderlichen Felder bei der Auswahl der angenommenen Rollenauthentifizierung.](/help/destinations/assets/catalog/cloud-storage/amazon-s3/assumed-role-authentication.png)

* **[!DNL Role]**: Fügen Sie den ARN der Rolle ein, die Sie in AWS für den Adobe-Benutzer erstellt haben. Das Muster ähnelt `arn:aws:iam::800873819705:role/destinations-role-customer`. Detaillierte Anleitungen zum korrekten Konfigurieren des S3-Zugriffs finden Sie in den folgenden Schritten.
* **[!UICONTROL Encryption key]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

Dazu müssen Sie in der AWS-Konsole eine zugewiesene Rolle für Adobe mit den [erforderlichen Berechtigungen) erstellen, ](#minimum-permissions-iam-user) in Ihre Amazon S3-Buckets zu schreiben.

**Erstellen Sie eine Richtlinie mit den erforderlichen Berechtigungen**

1. Öffnen Sie die AWS-Konsole und navigieren Sie zu IAM > Richtlinien > Richtlinie erstellen .
2. Wählen Sie Richtlinien-Editor > JSON aus und fügen Sie unten die Berechtigungen hinzu.

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "VisualEditor0",
               "Effect": "Allow",
               "Action": [
                   "s3:PutObject",
                   "s3:GetObject",
                   "s3:DeleteObject",
                   "s3:GetBucketLocation",
                   "s3:ListMultipartUploadParts"
               ],
               "Resource": "arn:aws:s3:::bucket/folder/*"
           },
           {
               "Sid": "VisualEditor1",
               "Effect": "Allow",
               "Action": [
                   "s3:ListBucket"
               ],
               "Resource": "arn:aws:s3:::bucket"
           }
       ]
   }
   ```

3. Geben Sie auf der nächsten Seite einen Namen für Ihre Richtlinie ein und speichern Sie sie als Referenz. Sie benötigen diesen Richtliniennamen, wenn Sie im nächsten Schritt die Rolle erstellen.

**Benutzerrolle in Ihrem S3-Kundenkonto erstellen**

1. Öffnen Sie die AWS-Konsole und gehen Sie zu IAM > Rollen > Neue Rolle erstellen .
2. Wählen Sie **Vertrauenswürdiger Entitätstyp** > **AWS-Konto**
3. Wählen Sie **Ein AWS-Konto** > **Ein anderes AWS-** aus und geben Sie die Adobe-Konto-ID ein: `670664943635`
4. Hinzufügen von Berechtigungen mithilfe der zuvor erstellten Richtlinie
5. Geben Sie einen Rollennamen ein (z. B. `destinations-role-customer`). Der Rollenname sollte wie ein Kennwort vertraulich behandelt werden. Er kann bis zu 64 Zeichen lang sein und alphanumerische Zeichen sowie die folgenden Sonderzeichen enthalten: `+=,.@-_`. Überprüfen Sie dann, ob:
   * Die Adobe-Konto-ID `670664943635` ist im Abschnitt **[!UICONTROL Select trusted entities]** vorhanden
   * Die zuvor erstellte Richtlinie ist in **[!UICONTROL Permissions policy summary]** vorhanden

**Geben Sie die Rolle an, die Adobe übernehmen soll**

Nachdem Sie die Rolle in AWS erstellt haben, müssen Sie Adobe die Rolle ARN zuweisen. Der ARN folgt diesem Muster: `arn:aws:iam::800873819705:role/destinations-role-customer`

Den ARN finden Sie auf der Hauptseite, nachdem Sie die Rolle in der AWS-Konsole erstellt haben. Sie werden dieses ARN beim Erstellen des Ziels verwenden.

**Überprüfen von Rollenberechtigungen und Vertrauensbeziehungen**

Stellen Sie sicher, dass Ihre Rolle über die folgende Konfiguration verfügt:

* **Berechtigungen**: Die Rolle sollte über Berechtigungen für den Zugriff auf S3 verfügen (entweder Vollzugriff oder die minimalen Berechtigungen, die im Schritt **Erstellen einer Richtlinie mit den erforderlichen Berechtigungen“** oben bereitgestellt wurden)
* **Vertrauensbeziehungen**: Die Rolle sollte in ihren Vertrauensbeziehungen das Adobe-Stammkonto (`670664943635`) haben

**Alternative: Auf bestimmte Adobe-Benutzende beschränken (optional)**

Wenn Sie es vorziehen, nicht das gesamte Adobe-Konto zuzulassen, können Sie den Zugriff nur auf bestimmte Adobe-Benutzende beschränken. Bearbeiten Sie dazu die Vertrauensrichtlinie mit der folgenden Konfiguration:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::670664943635:user/destinations-adobe-user"
            },
            "Action": "sts:AssumeRole",
            "Condition": {}
        }
    ]
}
```

Weitere Informationen finden Sie in der [AWS-Dokumentation zum Erstellen von Rollen](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html).



### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_bucket"
>title="Behältername"
>abstract="Muss zwischen 3 und 63 Zeichen lang sein. Muss mit einem Buchstaben oder einer Zahl beginnen und enden. Darf nur Kleinbuchstaben, Zahlen oder Bindestriche ( - ) enthalten. Darf nicht als IP-Adresse formatiert sein (z. B. 192.100.1.1)."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_folderpath"
>title="Ordnerpfad"
>abstract="Darf nur die Zeichen A-Z, a-z, 0-9 und die folgenden Sonderzeichen enthalten: `/!-_.'()"^[]+$%.*"`. Um einen Ordner pro Zielgruppendatei zu erstellen, fügen Sie das Makro `/%SEGMENT_NAME%` oder `/%SEGMENT_ID%` oder `/%SEGMENT_NAME%/%SEGMENT_ID%` in das Textfeld ein. Makros können nur am Ende des Ordnerpfads eingefügt werden. Sehen Sie sich Beispiele für Makros in der Dokumentation an."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/cloud-storage/overview.html?lang=de#use-macros" text="Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort"

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Description]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Bucket name]**: Geben Sie den Namen des [!DNL Amazon S3]-Behälters ein, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Folder path]**: Geben Sie den Pfad zum Zielordner ein, in dem die exportierten Dateien gespeichert werden.
* **[!UICONTROL File type]**: Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Bei Auswahl der Option [!UICONTROL CSV] können Sie auch [die Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Wählen Sie den Komprimierungstyp aus, den Experience Platform für die exportierten Dateien verwenden soll.
* **[!UICONTROL Include manifest file]**: Schalten Sie diese Option ein, wenn die Exporte eine JSON-Manifestdatei enthalten sollen, die Informationen zum Exportspeicherort, zur Exportgröße und mehr enthält. Das Manifest wird mit dem Format `manifest-<<destinationId>>-<<dataflowRunId>>.json` benannt. Anzeigen einer [Beispielmanifestdatei](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Die Manifestdatei enthält die folgenden Felder:
   * `flowRunId`: Die [Datenflussausführung](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die die exportierte Datei generiert hat.
   * `scheduledTime`: Die Zeit in UTC, zu der die Datei exportiert wurde.
   * `exportResults.sinkPath`: Der Pfad an Ihrem Speicherort, an dem die exportierte Datei abgelegt wird.
   * `exportResults.name`: Der Name der exportierten Datei.
   * `size`: Die Größe der exportierten Datei in Byte.

>[!TIP]
>
>Im Zielverbindungs-Workflow können Sie für jede exportierte Zielgruppendatei einen benutzerdefinierten Ordner im Amazon S3-Speicher erstellen. Anweisungen finden Sie unter [Verwenden von Makros zum Erstellen eines Ordners an Ihrem Speicherort](overview.md#use-macros).

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

### Erforderliche [!DNL Amazon S3]-Berechtigungen {#required-s3-permission}

Um Daten erfolgreich mit Ihrem [!DNL Amazon S3]-Speicherort zu verbinden und dorthin zu exportieren, erstellen Sie ein Benutzerprofil für Identitäts- und Zugriffsverwaltung (IAM) für [!DNL Experience Platform] in [!DNL Amazon S3] und weisen Berechtigungen für die folgenden Aktionen zu:

* `s3:DeleteObject`
* `s3:GetBucketLocation`
* `s3:GetObject`
* `s3:ListBucket`
* `s3:PutObject`
* `s3:ListMultipartUploadParts`

#### Erforderliche Mindestberechtigungen für die Authentifizierung der vom IAM übernommenen Rolle {#minimum-permissions-iam-user}

Stellen Sie bei der Konfiguration der IAM-Rolle als Kundin oder Kunde sicher, dass die mit der Rolle verknüpfte Berechtigungsrichtlinie die erforderlichen Aktionen für den Zielordner im Bucket und die `s3:ListBucket` Aktion für den Stamm des Buckets enthält. Nachfolgend finden Sie ein Beispiel für die Richtlinie mit den Mindestberechtigungen für diesen Authentifizierungstyp:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "VisualEditor0",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:DeleteObject",
                "s3:GetBucketLocation",
                "s3:ListMultipartUploadParts"
            ],
            "Resource": "arn:aws:s3:::bucket/folder/*"
        },
        {
            "Sid": "VisualEditor1",
            "Effect": "Allow",
            "Action": [
                "s3:ListBucket"
            ],
            "Resource": "arn:aws:s3:::bucket"
        }
    ]
}  
```

<!--

Commenting out this note, as write permissions are assigned through the s3:PutObject permission.

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [ Aktivieren von Zielgruppen für dieses Ziel finden Sie ](../../ui/activate-batch-profile-destinations.md)Aktivieren von Zielgruppendaten für Batch-Profil-).

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Überprüfen Sie, ob die Daten erfolgreich exportiert wurden, indem Sie Ihren [!DNL Amazon S3]-Speicher überprüfen, und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Zulassungsliste von IP-Adressen {#ip-address-allow-list}

Siehe den Artikel [IP-Adresse](ip-address-allow-list.md) , wenn Sie einer Zulassungsliste Adobe auf die Zulassungsliste setzen-IPs hinzufügen müssen.