---
keywords: Experience Platform; Homepage; beliebte Themen; Oracle-Objektspeicher; oracle-Objektspeicher
solution: Experience Platform
title: Erstellen einer Oracle-Objektspeicherquellenverbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Oracle Object Storage-Quellverbindung erstellen.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 46%

---

# Erstellen Sie eine [!DNL Oracle Object Storage] Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Oracle Object Storage] Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Sammeln erforderlicher Anmeldeinformationen

In , um eine Verbindung herzustellen [!DNL Oracle Object Storage]müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `serviceUrl` | Die [!DNL Oracle Object Storage] Endpunkt, der für die Authentifizierung erforderlich ist. Das Endpunktformat lautet: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Die [!DNL Oracle Object Storage] Zugriffsschlüssel-ID, die für die Authentifizierung erforderlich ist. |
| `secretKey` | Die [!DNL Oracle Object Storage] Passwort, das für die Authentifizierung erforderlich ist. |
| `bucketName` | Der zulässige Behältername, der erforderlich ist, wenn der Benutzer eingeschränkten Zugriff hat. Der Behältername muss zwischen drei und 63 Zeichen lang sein, er muss entweder mit einem Buchstaben oder einer Zahl beginnen und enden und darf nur Kleinbuchstaben, Zahlen oder Bindestriche (`-`). Der Behältername kann nicht wie eine IP-Adresse formatiert werden. |
| `folderPath` | Der zulässige Ordnerpfad, der erforderlich ist, wenn der Benutzer eingeschränkten Zugriff hat. |

Weitere Informationen zum Abrufen dieser Werte finden Sie im Abschnitt [Authentifizierungshandbuch zur oracle-Objektspeicherung](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues Oracle Object Storage-Konto für die Verbindung mit Platform zu erstellen.

## Verbindung zum Oracle-Objektspeicher herstellen

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchleiste finden.

Unter dem [!UICONTROL Cloud-Speicher] category, select **[!UICONTROL Oracle-Objektspeicher]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Object Storage]-Konto, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhanden](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL Oracle Object Storage]-Anmeldedaten an. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** und warten Sie, bis die neue Verbindung hergestellt ist.

![neu](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Oracle Object Storage]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial zum [Konfigurieren eines Datenflusses, um Daten aus Ihrem Cloud-Speicher in Platform zu übertragen](../../dataflow/batch/cloud-storage.md).
