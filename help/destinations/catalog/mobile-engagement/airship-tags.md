---
keywords: Luftschiff-Tags; Luftschiff-Ziel
title: Verbindung von Airship Tags
description: Nahtlose Weitergabe von Zielgruppendaten von Adobe an Airship als Zielgruppen-Tags für Targeting innerhalb von Airship.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: a765f6829f08f36010e0e12a7186bf5552dfe843
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# [!DNL Airship Tags] connection {#airship-tags-destination}

## Übersicht

[!DNL Airship] ist die führende Plattform für Kundeninteraktionen, mit der Sie Ihren Benutzern in allen Phasen des Kundenlebenszyklus sinnvolle, personalisierte Omnichannel-Nachrichten bereitstellen können.

Durch diese Integration werden Adobe Experience Platform-Segmentdaten zum Targeting oder zur Auslösung als [Tags](https://docs.airship.com/guides/audience/tags/) an [!DNL Airship] übergeben.

Weitere Informationen zu [!DNL Airship] finden Sie in den [Airship Docs](https://docs.airship.com).


>[!TIP]
>
>Diese Dokumentationsseite wurde vom [!DNL Airship]-Team erstellt. Bei Fragen oder Aktualisierungsanfragen wenden Sie sich bitte direkt an [support.airship.com](https://support.airship.com/).

## Voraussetzungen

Bevor Sie Ihre Adobe Experience Platform-Segmente an [!DNL Airship] senden können, müssen Sie Folgendes tun:

* Erstellen Sie eine Tag-Gruppe in Ihrem [!DNL Airship] -Projekt.
* Generieren Sie ein Trägertoken zur Authentifizierung.

>[!TIP]
> 
>Erstellen Sie ein [!DNL Airship]-Konto über [diesen Anmelde-Link](https://go.airship.eu/accounts/register/plan/starter/), falls noch nicht geschehen.

## Tag-Gruppen

Das Konzept der Segmente in Adobe Experience Platform ähnelt [Tags](https://docs.airship.com/guides/audience/tags/) in Airship, wobei es bei der Implementierung geringfügige Unterschiede gibt. Diese Integration ordnet den Status der [Mitgliedschaft eines Benutzers in einem Experience Platform-Segment](../../../xdm/field-groups/profile/segmentation.md) dem Vorhandensein oder Nichtvorhandensein eines [!DNL Airship]-Tags zu. Beispiel: In einem Platform-Segment, in dem `xdm:status` zu `realized` geändert wird, wird das Tag dem Kanal [!DNL Airship] hinzugefügt oder dem benannten Benutzer, dem dieses Profil zugeordnet ist. Wenn sich `xdm:status` in `exited` ändert, wird das Tag entfernt.

Um diese Integration zu aktivieren, erstellen Sie eine *Tag-Gruppe* in [!DNL Airship] mit dem Namen `adobe-segments`.

>[!IMPORTANT]
>
>Beim Erstellen Ihrer neuen Tag-Gruppe **Aktivieren Sie nicht** das Optionsfeld &quot;[!DNL Allow these tags to be set only from your server]&quot;. Andernfalls schlägt die Integration von Adobe-Tags fehl.

Anweisungen zum Erstellen der Tag-Gruppe finden Sie unter [Tag-Gruppen verwalten](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) .

## Bearer-Token generieren

Gehen Sie zu **[!UICONTROL Einstellungen]**&quot; **[!UICONTROL APIs und Integrationen]** im [Airship Dashboard](https://go.airship.com) und wählen Sie im Menü links **[!UICONTROL Tokens]** aus.

Klicken Sie auf **[!UICONTROL Token erstellen]**.

Geben Sie einen benutzerfreundlichen Namen für Ihr Token ein, z. B. &quot;Ziel für Adobe-Tags&quot;und wählen Sie &quot;Zugriff auf alle&quot;für die Rolle.

Klicken Sie auf **[!UICONTROL Token erstellen]** und speichern Sie die Details als vertraulich.

## Anwendungsfälle

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie das [!DNL Airship Tags]-Ziel verwenden sollten, finden Sie hier Beispielanwendungsfälle, die Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

### Anwendungsfall 1

Einzelhändler oder Unterhaltungsplattformen können Benutzerprofile für ihre Treuekunden erstellen und diese Segmente für Nachrichten-Targeting für mobile Kampagnen an [!DNL Airship] übergeben.

### Anwendungsfall 2

Trigger von Eins-zu-Eins-Nachrichten in Echtzeit, wenn Benutzer in bestimmte Segmente innerhalb von Adobe Experience Platform fallen oder aus diesen herausfallen.

So richtet beispielsweise ein Einzelhändler ein markenspezifisches Jeans-Segment in Platform ein. Dieser Händler kann nun eine Mobilnachricht Trigger haben, sobald jemand seine Jeans-Voreinstellung auf eine bestimmte Marke setzt.

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* **[!UICONTROL Trägertoken]**: das Inhaber-Token, das Sie über das  [!DNL Airship] Dashboard generiert haben.
* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Domäne]**: Wählen Sie entweder ein US- oder ein EU-Rechenzentrum aus, je nachdem, welches  [!DNL Airship] Rechenzentrum für dieses Ziel gilt.


## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Streaming-Segmentexportziele](../../ui/activate-segment-streaming-destinations.md) .

## Zuordnungsüberlegungen {#mapping-considerations}

[!DNL Airship] -Tags können entweder für einen Kanal festgelegt werden, der die Geräteinstanz darstellt, z. B. iPhone, oder für einen benannten Benutzer, der alle Geräte eines Benutzers einer gemeinsamen Kennung wie einer Kunden-ID zuordnet. Wenn Sie E-Mail-Adressen mit normalem Text (ungehasht) als primäre Identität in Ihrem Schema haben, wählen Sie das E-Mail-Feld in Ihrem **[!UICONTROL Quellattribute]** aus und ordnen Sie es in der rechten Spalte unter **[!UICONTROL Zielidentitäten]** dem benannten Benutzer [!DNL Airship] zu, wie unten dargestellt.

![Zuordnung von benannten Benutzern](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

Bei Kennungen, die einem Kanal zugeordnet werden sollen, d. h. einem Gerät, müssen Sie basierend auf der Quelle dem entsprechenden Kanal zuordnen. Die folgenden Abbildungen zeigen, wie Sie eine Google Advertising-ID einem Android-Kanal [!DNL Airship] zuordnen.

![Verbindung zu Airship ](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![TagsVerbindung zu Airship ](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![TagsKanalzuordnung](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Übersicht über Data Governance](../../../data-governance/home.md).
