---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics-Quellverbindung in der Benutzeroberfläche
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Adobe Experience Platform-Benutzeroberfläche eine Quellverbindung mit Microsoft Dynamics erstellen.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 31%

---

# Erstellen eines Quell-Connectors für [!DNL Microsoft Dynamics] in der Benutzeroberfläche

In diesem Tutorial werden Schritte zum Erstellen eines [!DNL Microsoft Dynamics] (nachstehend &quot;genannt)[!DNL Dynamics]&quot;) Quellverbindung über die Adobe Experience Platform-Benutzeroberfläche.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [[!DNL Experience Data Model (XDM)] System](../../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
   * [Grundlagen der Schemakomposition](../../../../../xdm/schema/composition.md): Machen Sie sich mit den grundlegenden Bausteinen von XDM-Schemas vertraut, einschließlich der wichtigsten Prinzipien und Best Practices bei der Schemaerstellung.
   * [Tutorial zum Schema-Editor](../../../../../xdm/tutorials/create-schema-ui.md): Erfahren Sie, wie Sie benutzerdefinierte Schemas mithilfe der Benutzeroberfläche des Schema-Editors erstellen können.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.

Wenn Sie bereits über eine gültige [!DNL Dynamics] -Konto verwenden, können Sie den Rest dieses Dokuments überspringen und mit dem Tutorial zum [Datenfluss für eine CRM-Quelle konfigurieren](../../dataflow/crm.md).

### Sammeln erforderlicher Anmeldeinformationen

Um Ihre [!DNL Dynamics] -Quelle angeben, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics] -Instanz. |
| `username` | Der Benutzername für Ihre [!DNL Dynamics] Benutzerkonto. |
| `password` | Das Kennwort für Ihre [!DNL Dynamics] -Konto. |

>[!TAB Service-Prinzipal- und Schlüsselauthentifizierung]

| Anmeldedaten | Beschreibung |
| --- | --- |
| `servicePrincipalId` | Die Client-ID Ihrer [!DNL Dynamics] -Konto. Diese ID ist bei der Verwendung der Service-Prinzipal- und schlüsselbasierten Authentifizierung erforderlich. |
| `servicePrincipalKey` | Der Geheimschlüssel des Dienstprinzips. Diese Berechtigung ist bei der Verwendung von Dienstprinzipal und schlüsselbasierter Authentifizierung erforderlich. |

>[!ENDTABS]

Weitere Informationen zu den ersten Schritten finden Sie unter [this [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Verbinden Ihres [!DNL Dynamics]-Kontos

Wählen Sie in der Platform-Benutzeroberfläche in der linken Navigationsleiste die Option **[!UICONTROL Quellen]**, um auf den Arbeitsbereich [!UICONTROL Quellen] zuzugreifen. Die [!UICONTROL Katalog] zeigt eine Vielzahl von Quellen an, mit denen Sie ein Konto erstellen können.

Sie können die gewünschte Kategorie aus dem Katalog auf der linken Bildschirmseite auswählen. Alternativ können Sie die gewünschte Quelle mithilfe der Suchoption finden.

Unter dem [!UICONTROL CRM] category, select **[!UICONTROL Microsoft Dynamics]** und wählen Sie **[!UICONTROL Daten hinzufügen]**.

![Der Quellkatalog mit ausgewähltem Microsoft Dynamics.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Die **[!UICONTROL Microsoft Dynamics-Konto verbinden]** angezeigt. Auf dieser Seite können Sie entweder neue oder vorhandene Anmeldedaten verwenden.

### Vorhandenes Konto

Um ein vorhandenes Konto zu verwenden, wählen Sie die [!DNL Dynamics] Konto, das Sie verwenden möchten, wählen Sie **[!UICONTROL Nächste]** in der oberen rechten Ecke, um fortzufahren.

![Die vorhandene Kontoschnittstelle.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### Neues Konto

>[!TIP]
>
>Nach der Erstellung können Sie den Authentifizierungstyp eines [!DNL Dynamics] Basisverbindung. Um den Authentifizierungstyp zu ändern, müssen Sie eine neue Basisverbindung erstellen.

Um ein neues Konto zu erstellen, wählen Sie **[!UICONTROL Neues Konto]** und geben Sie dann einen Namen und eine optionale Beschreibung für Ihre neue [!DNL Dynamics] -Konto.

![Die neue Benutzeroberfläche zur Kontoerstellung.](../../../../images/tutorials/create/ms-dynamics/new.png)

Sie können beim Erstellen einer [!DNL Dynamics] -Konto.

>[!BEGINTABS]

>[!TAB Einfache Authentifizierung]

So erstellen Sie eine [!DNL Dynamics] Konto mit einfacher Authentifizierung auswählen [!UICONTROL Grundlegende Authentifizierung] und dann Werte für Ihre [!UICONTROL Dienst-URI], [!UICONTROL Benutzername], und [!UICONTROL Passwort]. **Hinweis**: Grundlegende Authentifizierung in [!DNL Dynamics] kann durch Authentifizierung mit zwei Faktoren blockiert werden, die derzeit nicht von Platform unterstützt wird. In diesem Fall wird empfohlen, die schlüsselbasierte Authentifizierung zu verwenden, um einen Quell-Connector mit [!DNL Dynamics].

Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]** und dann etwas Zeit für die Einrichtung des neuen Kontos.

![Die grundlegende Authentifizierungsschnittstelle.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB Service-Prinzipal- und Schlüsselauthentifizierung]

So erstellen Sie eine [!DNL Dynamics] Konto mit Service-Prinzipal- und Schlüsselauthentifizierung, wählen Sie **[!UICONTROL Service-Prinzipal- und Schlüsselauthentifizierung]** und dann Werte für Ihre [!UICONTROL Service Prinzipal ID] und [!UICONTROL Hauptschlüssel des Dienstes].

Wählen Sie zum Abschluss **[!UICONTROL Verbindung mit Quelle herstellen]** und dann etwas Zeit für die Einrichtung des neuen Kontos.

![Die Authentifizierungsschnittstelle für den Service-Prinzipal-Schlüssel.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## Nächste Schritte

Mithilfe dieses Tutorials haben Sie eine Verbindung zu Ihrem [!DNL Dynamics]-Konto hergestellt. Sie können jetzt mit dem nächsten Tutorial fortfahren und einen [Datenfluss konfigurieren, um Daten in Platform zu importieren](../../dataflow/crm.md).
