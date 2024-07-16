---
keywords: Experience Platform; home; beliebte Themen; Identitätsdienst; Identity Service; freigegebene Geräte; freigegebene Geräte
title: Übersicht über freigegebene Geräte (Beta)
description: Bei der Erkennung freigegebener Geräte werden verschiedene authentifizierte Benutzer desselben Geräts identifiziert, sodass Kundendaten in Identitätsdiagrammen genauer dargestellt werden können.
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: d7c7bed74d746aba2330ecba62f9f810fbaf0d63
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 9%

---

# Übersicht über die Erkennung freigegebener Geräte (Beta)

>[!IMPORTANT]
>
>Die Funktion [!DNL Shared Device Detection] befindet sich in der Beta-Phase. Ihre Funktionen und Dokumentation können sich ändern.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, sich einen besseren Überblick über Ihre Kunden und ihr Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für effektive und persönliche digitale Erlebnisse sorgen.

[!DNL Shared Device] bezieht sich auf Geräte, die von mehr als einer Person verwendet werden. Beispiele für gemeinsam genutzte Geräte sind Tablets, Bibliothekscomputer und Kiosks. Mit der Funktion &quot;[!DNL Shared Device Detection]&quot; können unterschiedliche Benutzer desselben Geräts daran gehindert werden, in einer Identität zusammengeführt zu werden, wodurch eine genauere Darstellung einer Person ermöglicht wird.

Mit [!DNL Shared Device Detection] können Sie:

* Erstellen Sie separate Identitätsdiagramme für verschiedene Benutzer desselben Geräts.
* Verhindern der Vermischung von Daten verschiedener Personen, die dasselbe Gerät verwenden;
* Erstellen Sie eine sauberere und genauere Ansicht Ihrer Kunden.

>[!TIP]
>
>Konfigurationen für [!DNL Shared Device Detection] müssen vor der Aktivierung des Profils für den Datensatz abgeschlossen sein, da Sie die Einstellungen nach der Erstellung von Diagrammen in [!DNL Identity Service] nicht mehr ändern können.

## Erste Schritte mit [!DNL Shared Device Detection]

Die Arbeit mit [!DNL Shared Device Detection] erfordert ein Verständnis der verschiedenen beteiligten Platform-Dienste. Bevor Sie mit [!DNL Shared Device Detection] arbeiten, lesen Sie bitte die Dokumentation für die folgenden Dienste:

* [[!DNL Identity Service]](./home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kunden und ihr Verhalten, indem Sie Identitäten zwischen Geräten und Systemen überbrücken.
   * [Betrachter des Identitätsdiagramms](./features/identity-graph-viewer.md): Visualisieren Sie den Viewer für Identitätsdiagramme und interagieren Sie mit ihm, um besser zu verstehen, wie Kundenidentitäten zusammengeführt werden und auf welche Weise.
   * [Identitäts-Namespaces](./features/namespaces.md): Sehen Sie sich die Komponenten einer vollständig qualifizierten Identität an und wie Identitäts-Namespaces es Ihnen ermöglichen, den Kontext und den Typ einer Identität zu unterscheiden.

## Grundlagen zu [!DNL Shared Device Detection]

Bei der Arbeit mit
[!DNL Shared Device Detection]. Die nachstehende Tabelle enthält eine Liste der Begriffe, die für das Verständnis von [!DNL Shared Device Detection] erforderlich sind.

### Terminologie

| Begriffe | Definition |
| --- | --- |
| Freigegebenes Gerät | Ein freigegebenes Gerät ist ein Gerät, das von mehr als einer Person verwendet wird. Beispiele für gemeinsam genutzte Geräte sind Tablets, Bibliothekscomputer und Kiosks. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] bezieht sich auf eine Konfigurationseinstellung, mit der Daten verschiedener Benutzer desselben Geräts voneinander getrennt werden können. |
| Freigegebener Identity-Namespace | Der Shared Identity-Namespace stellt das Gerät dar, das von mehreren Benutzern verwendet werden kann. Der freigegebene Identitäts-Namespace ist normalerweise die ECID, kann jedoch auf andere Geräte-IDs festgelegt werden. |
| Identity-Namespace des Benutzers | Der User Identity-Namespace stellt den authentifizierten (angemeldeten) Benutzer eines gemeinsam genutzten Geräts dar. |
| Letzter authentifizierter Benutzer | Der zuletzt authentifizierte Benutzer stellt den Benutzer dar, der zuletzt bei einem Gerät angemeldet war, wenn ein Gerät von mehreren Konten angemeldet wird. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] funktioniert durch die Einrichtung von zwei Namespaces: dem **gemeinsamen Identitäts-Namespace** und dem **Benutzer-Identitäts-Namespace**.

* Der Shared Identity-Namespace stellt das Gerät dar, das von mehreren Benutzern verwendet werden kann. Adobe empfiehlt Kunden die Verwendung von ECID als gemeinsam genutzte Gerätekennung.
* Der Benutzer-Identitäts-Namespace wird dem Identitäts-Namespace zugeordnet, der der Anmelde-ID eines Benutzers entspricht. Dabei kann es sich um die CRM-ID eines Benutzers, die E-Mail-Adresse, die gehashte E-Mail-Adresse oder Telefonnummer handeln.

Ein freigegebenes Gerät, wie ein Tablet, hat einen einzelnen **gemeinsamen Identitäts-Namespace**. Andererseits hat jeder Benutzer eines gemeinsam genutzten Geräts seinen eigenen festgelegten **Benutzer-Identitäts-Namespace**, der seinen jeweiligen Anmelde-IDs entspricht. Beispielsweise verfügt ein Tablet, das Kevin und Nora für die E-Commerce-Verwendung freigeben, über eine eigene ECID von `1234`, während Kevin über einen eigenen Benutzer-Identitäts-Namespace verfügt, der seinem `kevin@email.com`-Konto zugeordnet ist, und Nora über einen eigenen Benutzer-Identitäts-Namespace, der ihrem `nora@email.com`-Konto zugeordnet ist.

[!DNL Shared Device Detection] kann Unterscheidungen zwischen mehreren Benutzern desselben Geräts vornehmen, indem der freigegebene Identitäts-Namespace (z. B. ECID) mit dem zuletzt authentifizierten Benutzer-Identitäts-Namespace (Anmelde-ID).

### Senden von Identitätsdaten an ein Identitätsdiagramm

Sehen Sie sich das folgende Beispiel an, um zu verstehen, wie [!DNL Shared Device Detection] funktioniert:

>[!NOTE]
>
>In diesem Diagramm ist der Freigegebene Identitäts-Namespace für ECID und der Benutzer-Identitäts-Namespace für CRM-ID konfiguriert.

![Diagramm](./images/shared-device/diagram.png)

* Kevin und Nora teilen sich ein Tablet, um eine E-Commerce-Website zu besuchen. Sie verfügen jedoch beide über eigene unabhängige Konten, die sie jeweils verwenden, um online zu surfen und einzukaufen.
   * Als freigegebenes Gerät verfügt das Tablet über eine entsprechende ECID, die die Cookie-ID des Tablet-Webbrowsers darstellt.
* Angenommen, Kevin verwendet das Tablet und **meldet sich in** bei seinem E-Commerce-Konto an, um nach Kopfhörern zu suchen. Dies bedeutet, dass die CRM-ID von Kevin (**Benutzer-Identitäts-Namespace**) jetzt mit der ECID des Tablets (**Freigegebener Identitäts-Namespace**) verknüpft ist. Die Browserdaten des Tablets sind jetzt in Kevins Identitätsdiagramm integriert.
   * Wenn sich Kevin **abmeldet** und Nora das Tablet verwendet und sich **in** bei ihrem eigenen Konto anmeldet und eine Kamera kauft, dann ist ihre CRM-ID jetzt mit der ECID des Tablets verknüpft. Daher sind die Browserdaten des Tablets jetzt in das Identitätsdiagramm von Nora integriert.
   * Wenn Nora **sich nicht abmeldet** und Kevin das Tablet verwendet, sich jedoch nicht bei **anmeldet, sind die Browserdaten des Tablets weiterhin in Nora integriert, da sie als authentifizierter Benutzer verbleiben und ihre CRM-ID weiterhin mit der ECID des Tablets verknüpft ist.**
   * Wenn Nora **sich abmeldet** und Kevin das Tablet verwendet, sich jedoch nicht bei **3} anmeldet, sind die Browserdaten des Tablets weiterhin in das Identitätsdiagramm von Nora integriert, da als** zuletzt authentifizierter Benutzer **ihre CRM-ID mit der ECID des Tablets verknüpft bleibt.**
   * Wenn sich Kevin **erneut in** anmeldet, wird seine CRM-ID jetzt mit der ECID des Tablets verknüpft, da er nun der letzte authentifizierte Benutzer ist und die Browserdaten des Tablets jetzt in sein Identitätsdiagramm integriert sind.

### Zusammenführen von Profilfragmenten mit aktiviertem [!DNL Shared Device Detection][!DNL Profile Service]

[!DNL Profile Service] berücksichtigt Profilfragmente und zusammengeführte Profile. Jedes einzelne Kundenprofil besteht aus mehreren Profilfragmenten, die zu einer einzigen Ansicht dieses Kunden zusammengefügt wurden. Wenn ein Kunde beispielsweise über mehrere Kanäle mit Ihrer Marke interagiert, verfügt Ihr Unternehmen über mehrere Profilfragmente, die sich auf diesen einzelnen Kunden beziehen und in mehreren Datensätzen enthalten sind. Wenn diese Fragmente in Platform aufgenommen werden, werden sie zusammengeführt, sodass ein zentrales Profil für diesen Kunden entsteht.

Wenn [!DNL Shared Device Detection] aktiviert ist, definiert [!DNL Profile] die primäre Identität des Profilfragments basierend darauf, ob das Erlebnisereignis authentifiziert oder nicht authentifiziert ist.

Ein **authentifiziertes Erlebnisereignis** ist eine Aktion, die von einem Benutzer bei der Anmeldung auf einem Gerät abgeschlossen wird. Bei authentifizierten Erlebnisereignissen ist die primäre Identität der **Benutzer-Identitäts-Namespace** (Anmelde-ID). Ein **nicht authentifiziertes Erlebnisereignis** ist eine Aktion, die von einem Benutzer abgeschlossen wird, der nicht bei einem Gerät angemeldet ist. Bei nicht authentifizierten Erlebnisereignissen ist die primäre Identität der **Shared Identity Namespace** (ECID).

Weitere Informationen finden Sie in der [[!DNL Real-Time Customer Profile] Übersicht](../profile/home.md).

## Benutzeroberfläche für freigegebene Geräte

Wählen Sie in der Platform-Benutzeroberfläche im linken Navigationsbereich **[!UICONTROL Identitäten]** und dann **[!UICONTROL Identitätseinstellungen]** aus.

![identity-dashboard](./images/shared-device/identity-dashboard.png)

Die Seite [!UICONTROL Einstellungen für freigegebene Geräte] wird angezeigt, auf der Sie eine Schnittstelle zum Konfigurieren der Einstellungen für freigegebene Geräte für Ihre Daten haben. Die Einstellungen für freigegebene Geräte sind standardmäßig deaktiviert.

Wenn diese Option aktiviert ist, können Daten von verschiedenen Benutzern desselben Geräts voneinander getrennt werden. Diese Konfigurationseinstellung ermöglicht eine sauberere und genauere Darstellung von Identitätsdiagrammen, bei denen Benutzeridentitäten desselben Geräts nicht miteinander kombiniert werden.

Wählen Sie **[!UICONTROL Aktivieren]** aus, um mit der Änderung Ihrer Einstellungen für freigegebene Geräte zu beginnen.

![enable-shared-device](./images/shared-device/enable-shared-device.png)

Die Konfigurationsoptionen [!UICONTROL Freigegebener Identitäts-Namespace] und [!UICONTROL Benutzer-Identitäts-Namespace] werden angezeigt, sodass Sie die gewünschten Identitäts-Namespaces ändern können.

![set-namespaces](./images/shared-device/set-namespaces.png)

[!UICONTROL Freigegebener Identitäts-Namespace] stellt ein einzelnes Gerät dar, das von mehreren verschiedenen Benutzern verwendet wird. Dieser Namespace wird immer auf **[!UICONTROL ECID]** gesetzt, da alle Platform-Benutzer **[!UICONTROL ECID]** als Webbrowser-Kennung verwenden.

![shared-identity-namespace](./images/shared-device/shared-identity-namespace.png)

Mit dem [!UICONTROL Benutzer-Identitäts-Namespace] können Sie verschiedene Benutzer desselben Geräts identifizieren und verhindern, dass Daten in demselben Identitätsdiagramm kombiniert werden.

![user-identity-namespace](./images/shared-device/user-identity-namespace.png)

Wählen Sie die Suchleiste **[!UICONTROL User Identity Namespace]** aus und geben Sie entweder einen Identitäts-Namespace ein oder wählen Sie einen Identitäts-Namespace aus dem Dropdown-Menü aus.

>[!TIP]
>
>Der [!UICONTROL Benutzer-Identitäts-Namespace] sollte dem Identitäts-Namespace zugeordnet sein, der der Anmelde-ID des Endbenutzers entspricht. Zu den Optionen gehören Kunden-ID, E-Mail und gehashte E-Mail.

![E-Mails](./images/shared-device/emails.png)

Nachdem Sie die [!UICONTROL Einstellungen für freigegebene Geräte] konfiguriert haben, wählen Sie **[!UICONTROL Speichern]** aus.

![save](./images/shared-device/save.png)

In einem Popup-Fenster werden Sie aufgefordert, Ihre Auswahl zu bestätigen. Wählen Sie **[!UICONTROL Ja]** aus, um die Konfigurationseinstellung abzuschließen.

![confirm](./images/shared-device/confirm.png)
