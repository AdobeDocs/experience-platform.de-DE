---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics Source-Verbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung mit Microsoft Dynamics erstellen.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 31%

---

# Erstellen eines Quell-Connectors für [!DNL Microsoft Dynamics] in der Benutzeroberfläche

In diesem Tutorial erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung vom Typ &quot;[!DNL Microsoft Dynamics]&quot;(im Folgenden &quot;1}&quot;) erstellen.[!DNL Dynamics]

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemata vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemata mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über ein gültiges [!DNL Dynamics] -Konto verfügen, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum Konfigurieren eines Datenflusses für eine CRM-Quelle fortfahren.](../../dataflow/crm.md)[

### Sammeln erforderlicher Anmeldeinformationen

Um Ihre [!DNL Dynamics] -Quelle zu authentifizieren, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics] -Instanz. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics] -Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics]-Konto. |

>[!TAB Service-Prinzipal- und Schlüsselauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| `servicePrincipalKey` | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |

>[!ENDTABS]

Weitere Informationen zu den ersten Schritten finden Sie in [diesem [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Verbinden Ihres [!DNL Dynamics]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Der Bildschirm [!UICONTROL Katalog] enthält verschiedene Quellen, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Wählen Sie unter der Kategorie [!UICONTROL CRM] die Option **[!UICONTROL Microsoft Dynamics]** und dann **[!UICONTROL Daten hinzufügen]** aus.

![Der Quellkatalog mit ausgewähltem Microsoft Dynamics.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Die Seite **[!UICONTROL Microsoft Dynamics-Konto verbinden]** wird angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie das gewünschte [!DNL Dynamics]-Konto aus und klicken Sie dann oben rechts auf **[!UICONTROL Weiter]** , um fortzufahren.

![Die vorhandene Kontoschnittstelle.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Neues Konto

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp einer Basis-Verbindung vom Typ [!DNL Dynamics] nicht mehr ändern. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihr neues [!DNL Dynamics]-Konto ein.

![Die neue Benutzeroberfläche zur Kontoerstellung.](../../../../images/tutorials/create/ms-dynamics/new.png)

Sie können bei der Erstellung eines [!DNL Dynamics] -Kontos entweder einfache Authentifizierung oder Service-Prinzipal- und Schlüsselauthentifizierung verwenden.

>[!BEGINTABS]

>[!TAB Grundlegende Authentifizierung]

Um ein [!DNL Dynamics] -Konto mit einfacher Authentifizierung zu erstellen, wählen Sie [!UICONTROL Grundlegende Authentifizierung] und geben Sie dann Werte für Ihren [!UICONTROL Dienst-URI], Ihren [!UICONTROL Benutzernamen] und Ihr [!UICONTROL Kennwort] an. **Hinweis**: Die grundlegende Authentifizierung in [!DNL Dynamics] kann durch eine Zwei-Faktor-Authentifizierung blockiert werden, die derzeit von Platform nicht unterstützt wird. In diesem Fall wird empfohlen, die schlüsselbasierte Authentifizierung zu verwenden, um einen Quell-Connector mit [!DNL Dynamics] zu erstellen.

Wählen Sie abschließend **[!UICONTROL Mit Quelle verbinden]** aus und lassen Sie dann etwas Zeit für die Einrichtung des neuen Kontos zu.

![ Die grundlegende Authentifizierungsschnittstelle.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Service-Prinzipal- und Schlüsselauthentifizierung]

Um ein [!DNL Dynamics] -Konto mit Dienstprinzipal- und Schlüsselauthentifizierung zu erstellen, wählen Sie **[!UICONTROL Dienstprinzipal- und Schlüsselauthentifizierung]** und geben Sie dann Werte für Ihre [!UICONTROL Dienstprinzipal-ID] und den [!UICONTROL Dienstprinzipalschlüssel] an.

Wählen Sie abschließend **[!UICONTROL Mit Quelle verbinden]** aus und lassen Sie dann etwas Zeit für die Einrichtung des neuen Kontos zu.

![Die Authentifizierungsschnittstelle für den Service-Prinzipal-Schlüssel.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Dynamics]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss konfigurieren, um Daten in Platform zu importieren](../../dataflow/crm.md).
