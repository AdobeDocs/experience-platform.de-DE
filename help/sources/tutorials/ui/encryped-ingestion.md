---
title: Verschlüsselte Daten in der Quellenbenutzeroberfläche von Workspace erfassen
description: Erfahren Sie, wie Sie verschlüsselte Daten im Arbeitsbereich der Quellenbenutzeroberfläche erfassen.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 18%

---

# Verschlüsselte Daten in der Quell-Benutzeroberfläche erfassen

>[!AVAILABILITY]
>
>Die Unterstützung für die verschlüsselte Datenerfassung in der Quell-Benutzeroberfläche befindet sich in der Beta-Phase und steht Ihrem Unternehmen möglicherweise nicht zur Verfügung. Die Funktion und die Dokumentation können sich ändern.

Sie können verschlüsselte Datendateien und Ordner mit Cloud-Speicher-Batch-Quellen in Adobe Experience Platform erfassen. Mithilfe der verschlüsselten Datenaufnahme können Sie asymmetrische Verschlüsselungsmechanismen nutzen, um Batch-Daten sicher in Experience Platform zu übertragen. Derzeit werden die asymmetrischen Verschlüsselungsmechanismen PGP und GPG unterstützt.

Diese Funktion steht den folgenden Quellen zur Verfügung:

* [Amazon S3]
* [Azure Blob]
* [Azure Data Lake Storage Gen2]
* [Azure-Dateispeicher]
* [Data Landing Zone]
* [FTP]
* [Google Cloud Storage]
* [HDFS]
* [Oracle Object Storage]
* [SFTP]

In diesem Handbuch erfahren Sie, wie Sie verschlüsselte Daten mit Cloud-Speicher-Batch-Quellen über die Benutzeroberfläche erfassen können.

## Erste Schritte

Es ist hilfreich, sich mit den folgenden Experience Platform-Funktionen und -Konzepten vertraut zu machen, bevor Sie mit der verschlüsselten Datenerfassung in der Benutzeroberfläche arbeiten:

* [Quellen](../../home.md): Verwenden Sie Experience Platform-Quellen, um Daten aus einer Adobe-Anwendung oder einer Datenquelle von Drittanbietern zu erfassen.
* [Datenflüsse](../../../dataflows/home.md): Datenflüsse sind Darstellungen von Datenaufträgen, die Daten über Experience Platform verschieben. Sie können den Arbeitsbereich &quot;Quellen&quot;verwenden, um Datenflüsse zu erstellen, die Daten von einer bestimmten Quelle zu Experience Platform erfassen.
* [Sandboxes](../../../sandboxes/home.md): Verwenden Sie Sandboxes in Experience Platform, um virtuelle Partitionen zwischen Ihren Experience Platform-Instanzen zu erstellen und Umgebungen für die Entwicklung oder Produktion zu erstellen.

### Allgemeine Übersicht

1. Erstellen Sie ein Verschlüsselungsschlüsselpaar mithilfe des Arbeitsbereichs &quot;Quellen&quot;in der Experience Platform-Benutzeroberfläche. Optional können Sie auch ein Schlüsselpaar für die Signaturüberprüfung erstellen, um eine zusätzliche Sicherheitsschicht für Ihre verschlüsselten Daten bereitzustellen.
2. Verwenden Sie den öffentlichen Schlüssel zum Verschlüsseln Ihrer Daten.
3. Platzieren Sie Ihre verschlüsselten Daten in Ihrem Cloud-Speicher-Provider. In diesem Schritt müssen Sie außerdem sicherstellen, dass Sie über eine Beispieldatei verfügen, die als Referenz für die Zuordnung Ihrer Quelldaten zu einem Experience-Datenmodell (XDM)-Schema verwendet werden kann.
4. Erfassen Sie Ihre verschlüsselten Daten auf Experience Platform, indem Sie eine Quellverbindung erstellen.
5. Geben Sie beim Erstellen der Quellverbindung die Schlüssel-ID an, die dem öffentlichen Schlüssel entspricht, den Sie zum Verschlüsseln Ihrer Daten verwendet haben. Wenn Sie auch den Schlüssel-Paar-Mechanismus für die Signierüberprüfung verwendet haben, müssen Sie auch die Schlüssel-ID für die Signierüberprüfung angeben, die Ihren verschlüsselten Daten entspricht.
6. Fahren Sie mit den Schritten zur Erstellung des Datenflusses fort.

## Verschlüsselungs-Schlüsselpaar erstellen {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="Verschlüsselungsschlüssel-ID"
>abstract="Geben Sie die Verschlüsselungsschlüssel-ID an, die Ihrem Verschlüsselungsschlüssel entspricht, der zum Verschlüsseln Ihrer Quelldaten verwendet wurde."

* Navigieren Sie in der Platform-Benutzeroberfläche zum Arbeitsbereich &quot;Quellen&quot;und wählen Sie dann in der oberen Kopfzeile [!UICONTROL Schlüsselpaare] aus.
* Sie gelangen zu einer Seite, auf der eine Liste der in Ihrem Unternehmen vorhandenen Verschlüsselungsschlüsselpaare angezeigt wird. Auf dieser Seite finden Sie Informationen zu Titel, Kennung, Typ, Verschlüsselungsalgorithmus, Ablauf und Status eines bestimmten Schlüssels. Um ein neues Schlüsselpaar zu erstellen, wählen Sie **[!UICONTROL Schlüssel erstellen]** aus.
* Wählen Sie als Nächstes den Schlüsseltyp aus, den Sie erstellen möchten. Um einen Verschlüsselungsschlüssel zu erstellen, wählen Sie **[!UICONTROL Verschlüsselungsschlüssel]** aus und geben Sie dann einen Titel und eine Passphrase für Ihren Verschlüsselungsschlüssel ein. Die Passphrase ist eine zusätzliche Schutzschicht für Ihre Verschlüsselungsschlüssel. Bei der Erstellung speichert Experience Platform die Passphrase in einem anderen sicheren Tresor als den öffentlichen Schlüssel. Sie müssen eine nicht leere Zeichenfolge als Passphrase angeben.

### Erstellen eines Signaturüberprüfungsschlüssels {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="Sign Verification Key ID"
>abstract="Geben Sie die Kennung des Signierüberprüfungsschlüssels an, der Ihren signierten, verschlüsselten Quelldaten entspricht."

## Aufnehmen verschlüsselter Daten {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Ist die Datei verschlüsselt?"
>abstract="Aktivieren Sie diese Option, wenn Sie eine bereits verschlüsselte Datei aufnehmen."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Auswählen einer Beispieldatei"
>abstract="Sie müssen bei der Aufnahme verschlüsselter Daten eine Beispieldatei aufnehmen, um eine Zuordnung zu erstellen."


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
