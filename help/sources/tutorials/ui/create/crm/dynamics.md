---
keywords: Experience Platform;Home;beliebte Themen;Microsoft Dynamics;Mikrosoft dynamik;Dynamik;Dynamik
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics Source-Verbindung in der Benutzeroberfläche
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie eine Microsoft Dynamics-Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche erstellen.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 7%

---

# Erstellen einer [!DNL Microsoft Dynamics]-Quellverbindung in der Benutzeroberfläche

In diesem Lernprogramm werden Schritte zum Erstellen einer [!DNL Microsoft Dynamics]-Quellverbindung (nachstehend &quot;a1/>&quot;genannt) mithilfe der Adobe Experience Platform-Benutzeroberfläche beschrieben.[!DNL Dynamics]

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den Grundbausteinen von XDM-Schemas sowie den zentralen Konzepten und Best Practices rund um die Erstellung von Schemas vertraut.
   * [Schema-Editor-Lernprogramm](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie mit der Benutzeroberfläche des Schema-Editors benutzerdefinierte Schema erstellen.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches, Echtzeit-Profil für Kunden, das auf aggregierten Daten aus mehreren Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Dynamics]-Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Lernprogramm [zum Konfigurieren eines Datenverlusts für eine CRM-Quelle](../../dataflow/crm.md) fortfahren.

### Erforderliche Anmeldedaten sammeln

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics]-Instanz. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics]-Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics]-Konto. |
| `servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Dienstprinzipal- und der schlüsselbasierten Authentifizierung erforderlich. |
| `servicePrincipalKey` | Der Hauptgeheimschlüssel des Dienstes. Diese Berechtigung ist bei der Verwendung der Dienstprinzipal- und der schlüsselbasierten Authentifizierung erforderlich. |

Weitere Informationen zum Einstieg finden Sie unter [this [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Verbinden Sie Ihr [!DNL Dynamics]-Konto

Nachdem Sie die erforderlichen Anmeldeinformationen gesammelt haben, führen Sie die folgenden Schritte aus, um Ihr [!DNL Dynamics]-Konto mit der Plattform zu verknüpfen.

Melden Sie sich bei [Adobe Experience Platform](https://platform.adobe.com) an und wählen Sie dann **[!UICONTROL Quellen]** in der linken Navigationsleiste aus, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm **[!UICONTROL Katalog]** zeigt eine Reihe von Quellen an, für die Sie ein Konto erstellen können.

Sie können die entsprechende Kategorie im Katalog auf der linken Seite des Bildschirms auswählen. Alternativ können Sie die gewünschte Quelle mit der Suchoption finden.

Wählen Sie unter der Kategorie **[!UICONTROL CRM]** **[!UICONTROL Microsoft Dynamics]**. Wenn Sie diesen Connector zum ersten Mal verwenden, wählen Sie **[!UICONTROL Konfigurieren]**. Andernfalls wählen Sie **[!UICONTROL Hinzufügen Daten]** aus, um einen neuen [!DNL Dynamics]-Connector zu erstellen.

![Katalog](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Die Seite **[!UICONTROL Verbindung zu Dynamics]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldeinformationen verwenden.

### Neues Konto

Wenn Sie neue Anmeldeinformationen verwenden, wählen Sie **[!UICONTROL Neues Konto]**. Geben Sie im eingeblendeten Eingabeformular einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Dynamics]-Konto ein.

Der [!DNL Dynamics]-Connector bietet verschiedene Authentifizierungstypen für den Zugriff. Wählen Sie unter [!UICONTROL Kontoauthentifizierung] **[!UICONTROL Grundlegende Authentifizierung]** aus, um kennwortbasierte Anmeldeinformationen zu verwenden.

Wählen Sie nach Abschluss des Vorgangs **[!UICONTROL Mit Quelle]** verbinden und lassen Sie dann etwas Zeit für die Einrichtung des neuen Kontos zu.

![basic-authentication](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

Alternativ können Sie **[!UICONTROL Dienstprinzipal- und Schlüsselauthentifizierung]** auswählen und Ihr [!DNL Dynamics]-Konto mit einer Kombination aus [!UICONTROL Dienstprinzipal-ID] und [!UICONTROL Dienstprinzipalschlüssel] verbinden.

>[!IMPORTANT]
>
> Die einfache Authentifizierung in [!DNL Dynamics] kann durch Zweifaktorauthentifizierung blockiert werden, was derzeit nicht von Platform unterstützt wird. In diesem Fall wird empfohlen, mit der schlüsselbasierten Authentifizierung einen Quell-Connector mit [!DNL Dynamics] zu erstellen.

![key-based-authentication](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| [!UICONTROL Dienstprinzips-ID] | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Dienstprinzipal- und der schlüsselbasierten Authentifizierung erforderlich. |
| [!UICONTROL Hauptschlüssel des Dienstes] | Der Hauptgeheimschlüssel des Dienstes. Diese Berechtigung ist bei der Verwendung der Dienstprinzipal- und der schlüsselbasierten Authentifizierung erforderlich. |

### Vorhandenes Konto

Um ein vorhandenes Konto zu verbinden, wählen Sie das [!DNL Dynamics]-Konto, mit dem Sie eine Verbindung herstellen möchten, und klicken Sie dann in der oberen rechten Ecke auf **[!UICONTROL Weiter]**, um fortzufahren.

![existing](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Nächste Schritte

Mit diesem Tutorial haben Sie eine Verbindung zu Ihrem [!DNL Dynamics]-Konto hergestellt. Sie können nun mit dem nächsten Lernprogramm fortfahren und [einen Datendurchlauf konfigurieren, um Daten in Platform](../../dataflow/crm.md) zu importieren.
