---
keywords: Experience Platform;Startseite;beliebte Themen;Identity Service;Identity Service;freigegebene Geräte;freigegebene Geräte
title: Übersicht über freigegebene Geräte (Beta)
description: Die Erkennung freigegebener Geräte identifiziert verschiedene authentifizierte Benutzer desselben Geräts und ermöglicht so eine genauere Darstellung von Kundendaten in Identitätsdiagrammen
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 9%

---

# Übersicht über die Erkennung freigegebener Geräte (Beta)

>[!IMPORTANT]
>
>Die [!DNL Shared Device Detection] Funktion befindet sich in der Betaphase. Ihre Funktionen und Dokumentation können sich ändern.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und ihr Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für effektive und persönliche digitale Erlebnisse sorgen.

[!DNL Shared Device] bezieht sich auf Geräte, die von mehr als einer Person verwendet werden. Beispiele für ein gemeinsam genutztes Gerät sind Tablets, Bibliotheks-Computer und Computer-Terminals. Durch die [!DNL Shared Device Detection] Funktion können verschiedene Benutzer desselben Geräts daran gehindert werden, zu einer einzigen Identität zusammengeführt zu werden, was eine genauere Darstellung einer Person ermöglicht.

Mit [!DNL Shared Device Detection] können Sie:

* Erstellen Sie separate Identitätsdiagramme für verschiedene Benutzer desselben Geräts.
* Verhindern, dass Daten von verschiedenen Personen, die dasselbe Gerät verwenden, gemischt werden;
* Erstellen Sie eine sauberere und genauere Ansicht Ihrer Kunden.

>[!TIP]
>
>Die Konfigurationen für [!DNL Shared Device Detection] müssen vor der Aktivierung des Profils für den Datensatz abgeschlossen werden, da die Einstellungen nicht mehr geändert werden können, sobald in [!DNL Identity Service] Diagramme generiert wurden.

## Erste Schritte mit [!DNL Shared Device Detection]

Die Arbeit mit [!DNL Shared Device Detection] erfordert ein Verständnis der verschiedenen beteiligten Platform-Services. Bevor Sie [!DNL Shared Device Detection] nutzen, lesen Sie die Dokumentation für folgende Services:

* [[!DNL Identity Service]](./home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
   * [Identitätsdiagramm-Viewer](./features/identity-graph-viewer.md): Visualisieren Sie den Identitätsdiagramm-Viewer und interagieren Sie mit ihm, um besser zu verstehen, wie Kundenidentitäten zusammengeführt werden und auf welche Weise.
   * [Identitäts-](./features/namespaces.md): Sehen Sie sich die Komponenten einer vollqualifizierten Identität an und erfahren Sie, wie Sie mit Identitäts-Namespaces den Kontext und den Typ einer Identität unterscheiden können.

## Grundlagen zu [!DNL Shared Device Detection]

Es ist wichtig, dass Sie die folgende Terminologie verstehen, wenn Sie mit
[!DNL Shared Device Detection]. In der folgenden Tabelle finden Sie eine Liste der Begriffe, die für das Verständnis von [!DNL Shared Device Detection] wesentlich sind.

### Terminologie

| Begriffe | Definition |
| --- | --- |
| Freigegebenes Gerät | Ein gemeinsam genutztes Gerät ist jedes Gerät, das von mehr als einer Person verwendet wird. Beispiele für gemeinsam genutzte Geräte sind Tablets, Bibliotheks-Computer und Computer-Terminals. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] bezieht sich auf eine Konfigurationseinstellung, mit der Daten von verschiedenen Benutzern desselben Geräts voneinander getrennt werden können. |
| Freigegebener Identity-Namespace | Der freigegebene Identity-Namespace stellt das Gerät dar, das von mehreren Benutzern verwendet werden kann. Der freigegebene Identity-Namespace ist normalerweise die ECID, kann jedoch auf andere Geräte-IDs festgelegt werden. |
| Identity-Namespace des Benutzers | Der Benutzer-Identity-Namespace repräsentiert den authentifizierten (angemeldeten) Benutzer eines freigegebenen Geräts. |
| Letzter authentifizierter Benutzer | Der letzte authentifizierte Benutzer stellt den Benutzer dar, der zuletzt bei einem Gerät angemeldet war, wenn ein Gerät von mehreren Konten angemeldet wird. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] erstellt zwei Namespaces: den **freigegebenen Identity-Namespace** und den **Benutzer-Identity-Namespace**.

* Der freigegebene Identity-Namespace stellt das Gerät dar, das von mehreren Benutzern verwendet werden kann. Adobe empfiehlt Kunden, ECID als Kennung des freigegebenen Geräts zu verwenden.
* Der Benutzer-Identity-Namespace wird dem Identity-Namespace zugeordnet, der der Anmelde-ID eines Benutzers entspricht. Dabei kann es sich um die CRM-ID, E-Mail-Adresse, gehashte E-Mail-Adresse oder Telefonnummer eines Benutzers handeln.

Ein gemeinsam genutztes Gerät, wie ein Tablet, hat einen einzigen **freigegebenen Identity-Namespace**. Andererseits verfügt jeder Benutzer eines gemeinsam genutzten Geräts über einen eigenen designierten **Benutzer-Identity-Namespace** der seinen jeweiligen Anmelde-IDs entspricht. Beispielsweise verfügt ein Tablet, das Kevin und Nora für die E-Commerce-Nutzung freigeben, über eine eigene ECID von `1234`, während Kevin einen eigenen Benutzer-Identity-Namespace hat, der seinem `kevin@email.com`-Konto zugeordnet ist, und Nora einen eigenen Benutzer-Identity-Namespace hat, der ihrem `nora@email.com`-Konto zugeordnet ist.

[!DNL Shared Device Detection] kann zwischen mehreren Benutzern desselben Geräts unterscheiden, indem der freigegebene Identity-Namespace verknüpft wird (z. B. ECID) mit dem Identity-Namespace des letzten authentifizierten Benutzers (Anmelde-ID).

### So werden Identitätsdaten an ein Identitätsdiagramm gesendet

Betrachten Sie das folgende Beispiel, um die Funktionsweise von [!DNL Shared Device Detection] besser zu verstehen:

>[!NOTE]
>
>In diesem Diagramm wird der freigegebene Identity-Namespace als ECID und der Benutzer-Identity-Namespace als CRMID konfiguriert.

![Diagramm](./images/shared-device/diagram.png)

* Kevin und Nora teilen sich ein Tablet, um eine E-Commerce-Website zu besuchen. Beide Unternehmen verfügen jedoch über eigene unabhängige Accounts, mit denen sie online surfen und einkaufen können.
   * Als gemeinsam genutztes Gerät verfügt das Tablet über eine entsprechende ECID, die die Cookie-ID des Webbrowsers des Tablets darstellt.
* Angenommen, Kevin verwendet das Tablet und **meldet sich** seinem E-Commerce-Konto an, um nach Kopfhörern zu suchen. Dies bedeutet dann, dass Kevins CRMID (**User Identity Namespace**) jetzt mit der ECID des Tablets verknüpft ist (**Shared Identity Namespace**). Die Browserdaten des Tablet-PCs sind jetzt in Kevins Identitätsdiagramm integriert.
   * Wenn Kevin **sich abmeldet** und Nora das Tablet nutzt und **sich** ihrem eigenen Konto anmeldet und eine Kamera kauft, dann ist ihre CRMID jetzt mit der ECID des Tablets verknüpft. Daher werden die Browser-Daten des Tablets jetzt in das Identitätsdiagramm von Nora integriert.
   * Wenn Nora **sich nicht abmeldet** und Kevin das Tablet verwendet, **sich jedoch nicht anmeldet**, werden die Browser-Daten des Tablets weiterhin mit Nora integriert, da sie als authentifizierte Benutzerin verbleibt und ihre CRMID weiterhin mit der ECID des Tablets verknüpft ist.
   * Wenn Nora **sich abmeldet** und Kevin das Tablet verwendet, **sich aber nicht anmeldet** werden die Browser-Daten des Tablets weiterhin in Noras Identitätsdiagramm integriert, da als **letzter authentifizierter Benutzer** ihre CRMID weiterhin mit der ECID des Tablets verknüpft bleibt.
   * Wenn sich **erneut anmeldet** wird seine CRMID jetzt mit der ECID des Tablets verknüpft, da er nun der letzte authentifizierte Benutzer ist und die Browser-Daten des Tablets jetzt in sein Identitätsdiagramm integriert sind.

### Zusammenführen [!DNL Profile Service] Profilfragmenten mit aktiviertem [!DNL Shared Device Detection]

[!DNL Profile Service] nimmt Profilfragmente und zusammengeführte Profile zur Kenntnis. Jedes einzelne Kundenprofil besteht aus mehreren Profilfragmenten, die zu einer einzigen Ansicht dieses Kunden zusammengefügt wurden. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Platform aufgenommen werden, werden sie zusammengeführt, sodass ein zentrales Profil für diesen Kunden entsteht.

Wenn [!DNL Shared Device Detection] aktiviert ist, definiert [!DNL Profile] die primäre Identität des Profilfragments in Abhängigkeit davon, ob das Erlebnisereignis authentifiziert oder nicht authentifiziert ist

Ein **authentifiziertes Erlebnisereignis** ist eine Aktion, die von einem Benutzer ausgeführt wird, während er bei einem Gerät angemeldet ist. Bei authentifizierten Erlebnisereignissen ist die primäre Identität der **User Identity-Namespace** (Anmelde-ID). Ein **nicht authentifiziertes Erlebnisereignis** ist eine Aktion, die von einem Benutzer ausgeführt wird, der nicht bei einem Gerät angemeldet ist. Bei nicht authentifizierten Erlebnisereignissen ist die primäre Identität der **Shared Identity Namespace** (ECID).

Weitere Informationen finden Sie unter [[!DNL Real-Time Customer Profile] Übersicht](../profile/home.md).

## Benutzeroberfläche für freigegebene Geräte

Wählen Sie in der Platform-Benutzeroberfläche **[!UICONTROL Identitäten]** im linken Navigationsbereich und anschließend **[!UICONTROL Identitätseinstellungen]** aus.

![identity-dashboard](./images/shared-device/identity-dashboard.png)

Die Seite [!UICONTROL Freigegebene Geräteeinstellungen] wird angezeigt und bietet Ihnen eine Schnittstelle zum Konfigurieren von freigegebenen Geräteeinstellungen für Ihre Daten. Freigegebene Geräteeinstellungen sind standardmäßig deaktiviert.

Wenn diese Option aktiviert ist, können Daten von verschiedenen Benutzern desselben Geräts voneinander getrennt werden. Diese Konfigurationseinstellung ermöglicht eine sauberere und genauere Darstellung von Identitätsdiagrammen, bei denen Benutzeridentitäten desselben Geräts nicht kombiniert werden.

Wählen Sie **[!UICONTROL Aktivieren]** aus, um mit der Änderung Ihrer Einstellungen für freigegebene Geräte zu beginnen.

![enable-shared-device](./images/shared-device/enable-shared-device.png)

Die Konfigurationsoptionen [!UICONTROL Freigegebener Identity]Namespace und [!UICONTROL Benutzer-Identity-Namespace] werden angezeigt, sodass Sie die Identity-Namespaces ändern können, die Sie verwenden möchten.

![set-namespaces](./images/shared-device/set-namespaces.png)

[!UICONTROL Freigegebener Identity-Namespace] stellt ein einzelnes Gerät dar, das von mehreren verschiedenen Benutzern verwendet wird. Dieser Namespace ist immer auf **[!UICONTROL ECID]** festgelegt, da alle Platform-Benutzer **[!UICONTROL ECID]** als Webbrowser-Kennung verwenden.

![shared-identity-namespace](./images/shared-device/shared-identity-namespace.png)

Mit [!UICONTROL User Identity-Namespace] können Sie verschiedene Benutzer desselben Geräts identifizieren und verhindern, dass Daten in demselben Identitätsdiagramm kombiniert werden.

![user-identity-namespace](./images/shared-device/user-identity-namespace.png)

Wählen Sie die **[!UICONTROL Benutzer-Identity-Namespace]** Suchleiste aus und geben Sie entweder einen Identity-Namespace ein oder wählen Sie einen Identity-Namespace aus dem Dropdown-Menü aus.

>[!TIP]
>
>Der [!UICONTROL Benutzer-Identity]Namespace) sollte dem Identity-Namespace zugeordnet werden, der der Anmelde-ID des Endbenutzers entspricht. Zu den Optionen gehören Kunden-ID, E-Mail und gehashte E-Mail.

![E-Mails](./images/shared-device/emails.png)

Nachdem Sie Ihre [!UICONTROL Einstellungen für freigegebene Geräte] konfiguriert haben, klicken Sie auf **[!UICONTROL Speichern]**.

![Speichern](./images/shared-device/save.png)

Ein Popup-Fenster erscheint, in dem Sie aufgefordert werden, Ihre Auswahl zu bestätigen. Wählen Sie **[!UICONTROL Ja]** aus, um die Konfigurationseinstellung abzuschließen.

![Bestätigen](./images/shared-device/confirm.png)
