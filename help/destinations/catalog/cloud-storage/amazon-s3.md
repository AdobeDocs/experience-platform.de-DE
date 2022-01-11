---
keywords: Amazon S3; S3-Ziel; s3; amazon s3
title: Amazon S3-Verbindung
description: Erstellen Sie eine aktive ausgehende Verbindung zu Ihrem Amazon Web Services (AWS) S3-Speicher, um regelmäßig CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Behälter zu exportieren.
exl-id: 6a2a2756-4bbf-4f82-88e4-62d211cbbb38
source-git-commit: bf46f4e6549fcbd975a9f0a6034040ed2e9b34e6
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# [!DNL Amazon S3] connection {#s3-connection}

## Übersicht {#overview}

Erstellen Sie eine ausgehende Live-Verbindung zu Ihrer [!DNL Amazon Web Services] (AWS) S3-Datenspeicherung , um regelmäßig CSV-Datendateien aus Adobe Experience Platform in Ihre eigenen S3-Buckets zu exportieren.

## Exporttyp {#export-type}

**Profilbasiert** - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;der [Zielaktivierungs-Workflow](../../ui/activate-segment-streaming-destinations.md#mapping).

![Profilbasierter Exporttyp für Amazon S3](../../assets/catalog/cloud-storage/amazon-s3/catalog.png)

## Mit Ziel verbinden {#connect}

Gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md).

### Verbindungsparameter {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_s3_rsa"
>title="RSA-öffentlicher Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als Base64-kodierte Zeichenfolge geschrieben werden."
>text="Learn more in documentation"

while [Einrichten](../../ui/connect-destination.md) An diesem Ziel müssen Sie die folgenden Informationen angeben:

* **[!DNL Amazon S3]Zugriffsschlüssel** und **[!DNL Amazon S3]geheimer Schlüssel**: In [!DNL Amazon S3], generieren Sie eine `access key - secret access key` , um Platform Zugriff auf Ihre [!DNL Amazon S3] -Konto. Weitere Informationen finden Sie unter [Amazon Web Services-Dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung dieses Ziels ein.
* **[!UICONTROL Bucket-Name]**: den Namen der [!DNL Amazon S3] -Bucket, der von diesem Ziel verwendet werden soll.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Zielordner ein, der die exportierten Dateien hosten soll.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.

>[!TIP]
>
>Im Zielverbindungs-Workflow können Sie einen benutzerdefinierten Ordner in Ihrem Amazon S3-Speicher pro exportierter Segmentdatei erstellen. Lesen [Verwenden Sie Makros, um einen Ordner in Ihrem Speicherort zu erstellen](overview.md#use-macros) für Anweisungen.

### Erforderlich [!DNL Amazon S3] Berechtigungen {#required-s3-permission}

So verbinden Sie Daten erfolgreich mit Ihren [!DNL Amazon S3] Speicherort speichern, erstellen Sie einen Benutzer für Identity and Access Management (IAM) für [!DNL Platform] in [!DNL Amazon S3] und weisen Berechtigungen für die folgenden Aktionen zu:

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

Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

## Exportierte Daten {#exported-data}

Für [!DNL Amazon S3] Ziele, [!DNL Platform] erstellt eine `.csv` -Datei in dem von Ihnen angegebenen Speicherort gespeichert. Weitere Informationen zu den Dateien finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) im Tutorial zur Segmentaktivierung.
