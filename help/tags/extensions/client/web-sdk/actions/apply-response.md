---
title: Antwort anwenden
description: Durchführen einer Aktion basierend auf einer Antwort von Edge Network.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# Antwort anwenden

Mit dem Aktionstyp **[!UICONTROL Apply response]** können basierend auf einer Antwort von Edge Network verschiedene Aktionen ausgeführt werden. Dieser Aktionstyp wird normalerweise in Hybridbereitstellungen verwendet, bei denen der Server einen ersten Aufruf an die Edge Network sendet. Dieser Aktionstyp nimmt die Antwort aus diesem Aufruf entgegen und initialisiert die Web-SDK im Browser. Durch die Verwendung dieses Aktionstyps können die Client-Ladezeiten für Anwendungsfälle der hybriden Personalisierung reduziert werden.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Rules]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Actions] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das Dropdown-Feld [!UICONTROL Extension] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und dann den [!UICONTROL Action type] auf **[!UICONTROL Apply response]** fest.

![Abbildung der Experience Platform-Benutzeroberfläche mit dem Aktionstyp „Antwort anwenden“.](../assets/apply-response.png)

## Anwendungsfälle

* Trigger **Manuelle Aufteilung zwischen Datenerfassung und Personalisierung**: Sie können eine Aktion [Ereignis senden](send-event.md) mit Render-Entscheidungen auf `false` setzen und dann eine Regel „Ereignis senden abgeschlossen“ anwenden, um das Versprechen einzufangen. Die erste Aktion innerhalb dieser Regel kann „Antwort anwenden“ sein. Dieser Workflow ermöglicht es, die DOM-Manipulation zu verzögern, bis der Code Ihres Unternehmens andere Arbeiten abgeschlossen hat.
* **Edge-Antwort, die von außerhalb der Web-SDK empfangen wurde**: Wenn Sie eine andere Bibliothek für die Kommunikation mit der Edge Network verwenden, können Sie der Web-SDK erlauben, die Antwort der Edge Network mithilfe dieser Aktion weiterhin zu verarbeiten.

## Verfügbare Felder

Dieser Aktionstyp unterstützt die folgenden Konfigurationsoptionen:

* **[!UICONTROL Instance]**: Die SDK-Instanz, für die die Aktion gilt. Dieses Dropdown-Menü ist deaktiviert, wenn Ihre Implementierung eine einzige SDK-Instanz verwendet.
* **[!UICONTROL Response headers]**: Wählen Sie das Datenelement aus, das ein Objekt mit den Kopfzeilenschlüsseln und den vom Edge Network-Server-Aufruf zurückgegebenen Werten zurückgibt.
* **[!UICONTROL Response body]**: Wählen Sie das Datenelement aus, das das -Objekt mit der JSON-Payload zurückgibt, die von der Edge Network-Antwort bereitgestellt wird.
* **[!UICONTROL Render visual personalization decisions]**: Aktivieren Sie diese Option, um den von Edge Network bereitgestellten Personalisierungsinhalt automatisch zu rendern und den Inhalt vorab auszublenden, um ein Flackern zu verhindern.
