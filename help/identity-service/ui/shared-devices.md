---
keywords: Experience Platform; Startseite; beliebte Themen; Identitätsdienst; Identitätsdienst; freigegebene Geräte; freigegebene Geräte
solution: Experience Platform
title: Übersicht über freigegebene Geräte (Beta)
topic-legacy: tutorial
description: Bei der Erkennung freigegebener Geräte werden verschiedene authentifizierte Benutzer desselben Geräts identifiziert, sodass Kundendaten in Identitätsdiagrammen genauer dargestellt werden können.
hide: true
hidefromtoc: true
source-git-commit: 1cdab6ce71c748ae174700ce50f50b143e46b40f
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 8%

---

# Übersicht über die Erkennung freigegebener Geräte (Beta)

>[!IMPORTANT]
>
>Die Funktion [!DNL Shared Device Detection] befindet sich in der Beta-Phase. Die Funktionen und Dokumentation können sich ändern.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und ihr Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für effektive und persönliche digitale Erlebnisse sorgen.

[!DNL Shared Device] bezeichnet Geräte, die von mehr als einer Person verwendet werden. Beispiele für gemeinsam genutzte Geräte sind Tablets, Bibliothekscomputer und Kiosks. Durch die Funktion [!DNL Shared Device Detection] können unterschiedliche Benutzer desselben Geräts daran gehindert werden, in einer Identität zusammengeführt zu werden, wodurch eine genauere Darstellung einer Person ermöglicht wird.

Mit [!DNL Shared Device Detection] können Sie:

* Erstellen Sie separate Identitätsdiagramme für verschiedene Benutzer desselben Geräts.
* Verhindern der Vermischung von Daten verschiedener Personen mit demselben Gerät;
* Erstellen Sie eine sauberere und genauere Ansicht Ihrer Kunden.

>[!TIP]
>
>Konfigurationen für [!DNL Shared Device Detection] müssen vor der Aktivierung des Profils für den Datensatz abgeschlossen sein, da Sie die Einstellungen nach der Erstellung von Diagrammen in [!DNL Identity Service] nicht mehr ändern können.

## Erste Schritte

Die Arbeit mit [!DNL Shared Device Detection] erfordert ein Verständnis der verschiedenen beteiligten Platform-Dienste. Bevor Sie mit [!DNL Shared Device Detection] arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Identity Service]](../home.md): Sorgt für eine bessere Darstellung einzelner Kunden und deren Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
   * [Identitätsdiagramm-Viewer](./identity-graph-viewer.md): Visualisieren Sie den Identitätsdiagramm-Viewer und interagieren Sie mit ihm, um besser zu verstehen, wie Kundenidentitäten zusammengeführt werden und auf welche Weise.
   * [Identitäts-Namespaces](../namespaces.md): Sehen Sie sich die Komponenten einer vollständig qualifizierten Identität an und erfahren Sie, wie Sie mithilfe von Identitäts-Namespaces den Kontext und den Typ einer Identität unterscheiden können.

### Terminologie

Die folgende Tabelle enthält eine Liste von Begriffen, die für das Verständnis von [!DNL Shared Device Detection] unerlässlich sind:

| Begriffe | Definition |
| --- | --- |
| Freigegebenes Gerät | Ein freigegebenes Gerät ist ein Gerät, das von mehr als einer Person verwendet wird. Beispiele für gemeinsam genutzte Geräte sind Tablets, Bibliothekscomputer und Kiosks. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] bezieht sich auf eine Konfigurationseinstellung, mit der Daten verschiedener Benutzer desselben Geräts voneinander getrennt werden können. |
| [!UICONTROL Freigegebener Identitäts-Namespace] | Ein [!UICONTROL Freigegebener Identitäts-Namespace] wird verwendet, um ein einzelnes Gerät darzustellen, das von mehreren verschiedenen Benutzern gemeinsam genutzt wird. |
| [!UICONTROL Benutzeridentitäts-Namespace] | Ein [!UICONTROL User Identity-Namespace] wird verwendet, um den authentifizierten oder angemeldeten Benutzer eines gemeinsam genutzten Geräts darzustellen. |

## Benutzeroberfläche für freigegebene Geräte

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Identitäten]** aus dem linken Navigationsbereich und dann **[!UICONTROL Identitätseinstellungen]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

Die Seite [!UICONTROL Einstellungen für freigegebene Geräte] wird angezeigt, auf der Sie eine Schnittstelle zum Konfigurieren freigegebener Geräteeinstellungen für Ihre Daten haben. Die Einstellungen für freigegebene Geräte sind standardmäßig deaktiviert.

Wenn diese Option aktiviert ist, können Daten von verschiedenen Benutzern desselben Geräts voneinander getrennt werden. Diese Konfigurationseinstellung ermöglicht eine sauberere und genauere Darstellung von Identitätsdiagrammen, bei denen Benutzeridentitäten desselben Geräts nicht miteinander kombiniert werden.

Wählen Sie **[!UICONTROL Aktivieren]** aus, um Ihre Einstellungen für freigegebene Geräte zu ändern.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

Die Konfigurationsoptionen [!UICONTROL Freigegebener Identity-Namespace] und [!UICONTROL User Identity-Namespace] werden angezeigt, sodass Sie die zu verwendenden Identitäts-Namespaces ändern können.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Shared Identity ] Namespaces stellen ein einzelnes Gerät dar, das von mehreren verschiedenen Benutzern verwendet wird. Dieser Namespace ist immer auf **[!UICONTROL ECID]** gesetzt, da alle Platform-Benutzer **[!UICONTROL ECID]** als Webbrowser-Kennung verwenden.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

Mit dem [!UICONTROL Benutzer-Identity-Namespace] können Sie verschiedene Benutzer desselben Geräts identifizieren und verhindern, dass Daten in demselben Identitätsdiagramm kombiniert werden.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Wählen Sie die Suchleiste **[!UICONTROL User Identity-Namespace]** aus und geben Sie entweder einen Identitäts-Namespace ein oder wählen Sie einen Identitäts-Namespace aus dem Dropdown-Menü aus.

>[!TIP]
>
>Der [!UICONTROL User Identity-Namespace] sollte dem Identitäts-Namespace zugeordnet sein, der der Anmelde-ID des Endbenutzers entspricht. Zu den Optionen gehören Kunden-ID, E-Mail und gehashte E-Mail.

![E-Mails](../images/shared-device/emails.png)

Nachdem Sie die [!UICONTROL Einstellungen für freigegebene Geräte] konfiguriert haben, wählen Sie **[!UICONTROL Speichern]** aus.

![Speichern](../images/shared-device/save.png)

In einem Popup-Fenster werden Sie aufgefordert, Ihre Auswahl zu bestätigen. Wählen Sie **[!UICONTROL Ja]** aus, um die Konfigurationseinstellung abzuschließen.

![Bestätigen](../images/shared-device/confirm.png)
