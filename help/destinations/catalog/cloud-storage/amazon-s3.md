---
keywords: Amazon S3; S3-Ziel; s3; amazon s3
title: Amazon S3-Verbindung
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: 8d1594aeb1d6671eec187643245d940ed3ff74cd
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 9%

---

# [!DNL Amazon S3] connection {#s3-connection}

## Übersicht {#overview}

Erstellen Sie eine ausgehende Live-Verbindung zu Ihrem S3-Speicher (AWS), um in regelmäßigen Abständen tabulatorgetrennte oder CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Behälter zu exportieren.[!DNL Amazon Web Services]

## Exporttyp {#export-type}

**Profilbasiert**  - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des  [Zielaktivierungs-Workflows](../../ui/activate-destinations.md#select-attributes) ausgewählt.

![Profilbasierter Exporttyp für Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!DNL Amazon S3]Zugriffsschlüssel** und  **[!DNL Amazon S3]geheimer Schlüssel**: Generieren Sie  [!DNL Amazon S3]in ein  `access key - secret access key` Paar, um Platform Zugriff auf Ihr  [!DNL Amazon S3] Konto zu gewähren. Weitere Informationen finden Sie in der [Dokumentation zu Amazon Web Services](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung dieses Ziels ein.
* **[!UICONTROL Bucket-Name]**: Geben Sie den Namen des  [!DNL Amazon S3] Buckets ein, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.

>[!TIP]
>
>Im Zielverbindungs-Workflow können Sie einen benutzerdefinierten Ordner in Ihrem Amazon S3-Speicher pro exportierter Segmentdatei erstellen. Lesen Sie [Verwenden Sie Makros, um einen Ordner in Ihrem Speicherort zu erstellen](overview.md#use-macros), um Anweisungen zu erhalten.

### Erforderliche [!DNL Amazon S3] Berechtigungen {#required-s3-permission}

Um Daten erfolgreich mit Ihrem [!DNL Amazon S3]-Speicherort zu verbinden und zu exportieren, erstellen Sie einen Benutzer für die Identitäts- und Zugriffsverwaltung (IAM) für [!DNL Platform] in [!DNL Amazon S3] und weisen Sie Berechtigungen für die folgenden Aktionen zu:

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

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für Ziele finden Sie unter [Aktivieren von Profilen und Segmenten für ein Ziel](../../ui/activate-destinations.md) .

## Exportierte Daten {#exported-data}

Für [!DNL Amazon S3]-Ziele erstellt [!DNL Platform] eine tabulatorgetrennte `.csv`-Datei am von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentaktivierung.
