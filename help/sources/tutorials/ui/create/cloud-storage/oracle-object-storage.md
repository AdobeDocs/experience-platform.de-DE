---
keywords: Experience Platform; Homepage; beliebte Themen; Oracle-Objektspeicher; oracle-Objektspeicher
solution: Experience Platform
title: Erstellen einer Oracle-Objektspeicherquellenverbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Oracle Object Storage-Quellverbindung erstellen.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 10%

---

# Erstellen einer [!DNL Oracle Object Storage] Quellverbindung in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen einer [!DNL Oracle Object Storage]-Quellverbindung mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Platform-Diensten zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Erforderliche Anmeldedaten sammeln

Um eine Verbindung zu [!DNL Oracle Object Storage] herzustellen, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUrl` | Der für die Authentifizierung erforderliche [!DNL Oracle Object Storage]-Endpunkt. Das Endpunktformat lautet: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Die für die Authentifizierung erforderliche Zugriffsschlüssel-ID [!DNL Oracle Object Storage]. |
| `secretKey` | Das für die Authentifizierung erforderliche [!DNL Oracle Object Storage]-Kennwort. |
| `bucketName` | Der zulässige Behältername, der erforderlich ist, wenn der Benutzer eingeschränkten Zugriff hat. Der Behältername muss zwischen drei und 63 Zeichen lang sein. Er muss entweder mit einem Buchstaben oder einer Zahl beginnen und enden und darf nur Kleinbuchstaben, Zahlen oder Bindestriche (`-`) enthalten. Der Behältername kann nicht wie eine IP-Adresse formatiert werden. |
| `folderPath` | Der zulässige Ordnerpfad, der erforderlich ist, wenn der Benutzer eingeschränkten Zugriff hat. |

Weitere Informationen zum Abrufen dieser Werte finden Sie im [Handbuch zur Authentifizierung bei der Oracle-Objektspeicherung](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, können Sie die folgenden Schritte ausführen, um ein neues Oracle Object Storage-Konto für die Verbindung mit Platform zu erstellen.

## Verbindung zum Oracle-Objektspeicher herstellen

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Quellen]** aus dem linken Navigationsbereich aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält eine Vielzahl von Quellen, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle über die Suchleiste finden.

Wählen Sie unter der Kategorie [!UICONTROL Cloud-Speicher] die Option **[!UICONTROL Oracle-Objektspeicher]** und klicken Sie dann auf **[!UICONTROL Daten hinzufügen]**.

![Katalog](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das [!DNL Oracle Object Storage]-Konto aus, mit dem Sie einen neuen Datenfluss erstellen möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**, um fortzufahren.

![vorhandene](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Neues Konto

Wenn Sie ein neues Konto erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen, eine optionale Beschreibung und Ihre [!DNL Oracle Object Storage]-Anmeldedaten ein. Wenn Sie fertig sind, wählen Sie **[!UICONTROL Mit Quelle verbinden]** aus und lassen Sie dann etwas Zeit für die Einrichtung der neuen Verbindung zu.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Nächste Schritte

In diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Oracle Object Storage]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial zum Konfigurieren eines Datenflusses fortfahren, um Daten aus Ihrem Cloud-Speicher in Platform](../../dataflow/batch/cloud-storage.md) zu übertragen.[
