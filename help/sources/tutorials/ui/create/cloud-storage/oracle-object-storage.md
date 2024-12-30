---
keywords: Experience Platform;Startseite;beliebte Themen;Oracle-Objektspeicher;oracle-Objektspeicher
solution: Experience Platform
title: Erstellen einer Oracle-Objektspeicher-Source-Verbindung über die Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Benutzeroberfläche von Adobe Experience Platform eine Quellverbindung für den Oracle-Objektspeicher erstellen.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 47%

---

# Erstellen einer [!DNL Oracle Object Storage] Source-Verbindung über die Benutzeroberfläche

In diesem Tutorial finden Sie die Schritte zum Erstellen einer [!DNL Oracle Object Storage]-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldedaten

Um eine Verbindung zu [!DNL Oracle Object Storage] herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `serviceUrl` | Der für die Authentifizierung erforderliche [!DNL Oracle Object Storage]-Endpunkt. Das Endpunktformat ist: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Die [!DNL Oracle Object Storage] Zugriffsschlüssel-ID, die für die Authentifizierung erforderlich ist. |
| `secretKey` | Das [!DNL Oracle Object Storage] Kennwort, das für die Authentifizierung erforderlich ist. |
| `bucketName` | Der zulässige Behältername ist erforderlich, wenn der Benutzer eingeschränkten Zugriff hat. Der Behältername muss zwischen drei und 63 Zeichen lang sein. Er muss entweder mit einem Buchstaben oder einer Zahl beginnen und enden und darf nur Kleinbuchstaben, Zahlen oder Bindestriche (`-`) enthalten. Der Behältername kann nicht wie eine IP-Adresse formatiert werden. |
| `folderPath` | Der Pfad des zulässigen Ordners ist erforderlich, wenn der Benutzer eingeschränkten Zugriff hat. |

Weitere Informationen zum Abrufen dieser Werte finden Sie im Handbuch zur Authentifizierung beim [Oracle-Objektspeicher](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues Oracle-Objektspeicherkonto für die Verbindung mit Platform zu erstellen.

## Herstellen einer Verbindung zum Oracle-Objektspeicher

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud] die Option **[!UICONTROL Oracle-Objektspeicher]** und dann **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Object Storage]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL Oracle Object Storage]-Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Oracle Object Storage]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial [Konfigurieren eines Datenflusses, um Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/batch/cloud-storage.md) fortfahren.
