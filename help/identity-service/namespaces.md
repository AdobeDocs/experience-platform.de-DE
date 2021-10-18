---
keywords: Experience Platform;Startseite;beliebte Themen;Namespace;Namespace;Namespaces;Namespaces;Identitäts-Namespace;Identitäts-Namespace;Identität;Identity Service;Identitätsdienst
solution: Experience Platform
title: Identity Namespace - Überblick
topic-legacy: overview
description: Identity-Namespaces sind Komponenten des Identity Service, die als Indikatoren für den Kontext dienen, auf den sich eine Identität bezieht. Sie unterscheiden beispielsweise den Wert "name@email.com"als E-Mail-Adresse oder "443522"als numerische CRM-ID.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 5373b8fcd84cee749a85bdb755a23eb7292cf352
workflow-type: tm+mt
source-wordcount: '1598'
ht-degree: 21%

---

# Übersicht über Identitäts-Namespaces

Identitäts-Namespaces sind eine Komponente des [[!DNL Identity Service]](./home.md), die als Indikatoren für den Kontext dient, auf den sich eine Identität bezieht. Sie unterscheiden beispielsweise den Wert von „name<span>@email.com“ als E-Mail-Adresse oder „443522“ als numerische CRM-ID.

## Erste Schritte

Das Verwenden von Identitäts-Namespaces setzt ein Verständnis der verschiedenen beteiligten Adobe Experience Platform-Dienste voraus. Bevor Sie Namespaces nutzen, lesen Sie bitte die Dokumentation für folgende Dienste:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
- [[!DNL Identity Service]](./home.md): Sorgt für eine bessere Darstellung einzelner Kunden und deren Verhalten, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
- [[!DNL Privacy Service]](../privacy-service/home.md): Identitäts-Namespaces werden zur Einhaltung der Datenschutz-Grundverordnung (DSGVO) verwendet, laut der DSGVO-Anfragen für einen Namespace gestellt werden können.

## Identitäts-Namespaces verstehen

Eine vollqualifizierte Identität umfasst einen ID-Wert und einen Namespace. Wenn Datensatzdaten über Profilfragmente hinweg abgeglichen werden (z. B. wenn [!DNL Real-time Customer Profile] Profildaten zusammenführt), müssen sowohl der Identitätswert als auch der Namespace übereinstimmen.

Beispielsweise können zwei Profilfragmente unterschiedliche primäre IDs enthalten, für den Namespace &quot;E-Mail&quot;jedoch denselben Wert verwenden. [!DNL Platform] kann daher sehen, dass diese Fragmente eigentlich dieselbe Person sind und die Daten im Identitätsdiagramm für die Person zusammenführen.

![](images/identity-service-stitching.png)

### Identitätstypen

Daten können anhand verschiedener Identitätstypen identifiziert werden. Der Identitätstyp wird zum Zeitpunkt der Erstellung des Identitäts-Namespace angegeben und steuert, ob die Daten im Identitätsdiagramm persistiert werden oder nicht. Außerdem gibt es spezielle Anweisungen zum Umgang mit diesen Daten. Alle Identitätstypen mit Ausnahme von **Nicht-Personen-ID** folgen demselben Verhalten beim Zuordnen eines Namespace und des zugehörigen ID-Werts zu einem Identitätsdiagramm-Cluster. Daten werden bei Verwendung von **Personen-Kennung** nicht zugeordnet.

Die folgenden Identitätstypen sind innerhalb von [!DNL Platform] verfügbar:

| Identitätstyp | Beschreibung |
| --- | --- |
| Cookie ID | Cookie-IDs identifizieren Webbrowser. Diese Identitäten sind für Erweiterungen von entscheidender Bedeutung und bilden den Großteil des Identitätsdiagramms. Sie verfallen jedoch naturgemäß schnell und verlieren mit der Zeit ihren Wert. |
| Geräteübergreifende ID | Geräteübergreifende IDs identifizieren eine Person und verbinden normalerweise andere IDs miteinander. Beispiele sind eine Anmelde-ID, CRM-ID und Loyalitäts-ID. Dies ist ein Hinweis für [!DNL Identity Service], den Wert sensibel zu behandeln. |
| Geräte-ID | Geräte-IDs identifizieren Hardwaregeräte wie IDFA (iPhone und iPad), GAID (Android) und RIDA (Roku) und können von mehreren Personen in Haushalten gemeinsam genutzt werden. |
| E-Mail  Adresse | E-Mail-Adressen sind oft mit einer einzelnen Person verknüpft und können daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. Identitäten dieser Art beinhalten personenbezogene Daten (PII). Dies ist ein Hinweis für [!DNL Identity Service], den Wert sensibel zu behandeln. |
| Personenidentifizierung | Nicht-Personen-IDs werden zum Speichern von Kennungen verwendet, die Namespaces erfordern, aber nicht mit einem Personen-Cluster verbunden sind. Beispielsweise eine Produkt-SKU, Daten, die sich auf Produkte, Organisationen oder Geschäfte beziehen. |
| Telefonnummer | Telefonnummern sind häufig mit einer einzelnen Person verknüpft und können daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. Identitäten dieser Art umfassen PII. Dies ist ein Hinweis auf [!DNL Identity Service], den Wert sensibel zu behandeln. |

### Standard-Namespaces

 Experience Platform bietet verschiedene Identitäts-Namespaces, die für alle Organisationen verfügbar sind. Diese werden als Standard-Namespaces bezeichnet und sind über die [!DNL Identity Service]-API oder die Platform-Benutzeroberfläche sichtbar.

Folgende Standard-Namespaces stehen allen Organisationen in Platform zur Verfügung:

| Anzeigename | Beschreibung |
| ------------ | ----------- |
| AdCloud | Ein Namespace, der die Adobe AdCloud darstellt. |
| Adobe Analytics (Legacy-ID) | Ein Namespace, der Adobe Analytics darstellt. Weitere Informationen finden Sie im folgenden Dokument zu [Adobe Analytics-Namespaces](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=en#namespaces) . |
| Apple IDFA (ID für Advertiser) | Ein Namespace, der die Apple ID für Advertiser darstellt. Weitere Informationen finden Sie im folgenden Dokument zu [Interessensbasierte Anzeigen](https://support.apple.com/de-de/HT202074) . |
| Apple Push Notification Service | Ein Namespace, der Identitäten darstellt, die mit dem Apple Push Notification Service erfasst wurden. Weitere Informationen finden Sie im folgenden Dokument zu [Apple Push Notification Service](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) . |
| CORE | Ein Namespace, der Adobe Audience Manager darstellt. Dieser Namespace kann auch durch seinen alten Namen referenziert werden: &quot;Adobe AudienceManager&quot;. Weitere Informationen finden Sie im folgenden Dokument zu [Audience Manager-IDs](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-reference/data-privacy-ids.html?lang=en#aam-ids) . |
| ECID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Alias referenziert werden: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Weitere Informationen finden Sie im folgenden Dokument zu [ECID](./ecid.md). |
| E-Mail  | Ein Namespace, der eine E-Mail-Adresse darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |
| E-Mails (SHA256, in Kleinbuchstaben) | Ein Namespace für eine E-Mail-Adresse mit vorab gehashten Nachrichten. Die in diesem Namespace bereitgestellten Werte werden vor dem Hashing mit SHA256 in Kleinbuchstaben umgewandelt. Vor der Bereinigung einer E-Mail-Adresse müssen die Leerstellen am Anfang und am Ende abgeschnitten werden. Diese Einstellung kann nicht rückwirkend geändert werden. Weitere Informationen finden Sie im folgenden Dokument zu [SHA256-Hashing-Unterstützung](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) . |
| Firebase Cloud Messaging | Ein Namespace, der Identitäten darstellt, die mit Google Firebase Cloud Messaging für Push-Benachrichtigungen erfasst wurden. Weitere Informationen finden Sie im folgenden Dokument zu [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging). |
| Google Ad ID (GAID) | Ein Namespace, der eine Google Advertising-ID darstellt. Weitere Informationen finden Sie im folgenden Dokument zu [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en). |
| Google-Klick-ID | Ein Namespace, der eine Google-Klick-ID darstellt. Weitere Informationen finden Sie im folgenden Dokument zu [Klick-Tracking in Google Ads](https://developers.google.com/adwords/api/docs/guides/click-tracking) . |
| Telefon | Ein Namespace, der eine Telefonnummer darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |
| Telefon (E.164) | Ein Namespace, der rohe Telefonnummern darstellt, die im E.164-Format gehasht werden müssen. Das E.164-Format enthält ein Pluszeichen (`+`), einen internationalen Telefoncode, einen lokalen Gebietscode und eine Telefonnummer. Beispiel: `(+)(country code)(area code)(phone number)`. |
| Telefon (SHA256) | Ein Namespace, der Telefonnummern darstellt, die mit SHA256 gehasht werden müssen. Sie müssen Symbole, Buchstaben und alle führenden Nullen entfernen. Sie müssen auch den Länderaufrufscode als Präfix hinzufügen. |
| Telefon (SHA256_E.164) | Ein Namespace, der rohe Telefonnummern darstellt, die im SHA256- und E.164-Format gehasht werden müssen. |
| TNTID | Ein Namespace, der Adobe Target darstellt. Weitere Informationen finden Sie im folgenden Dokument zu [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=en) . |
| Windows AID | Ein Namespace, der eine Windows Advertising-ID darstellt. Weitere Informationen finden Sie im folgenden Dokument unter [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) . |

### Anzeigen von Identitäts-Namespaces

Um Identitäts-Namespaces in der Benutzeroberfläche anzuzeigen, wählen Sie im linken Navigationsbereich **[!UICONTROL Identitäten]** und dann **[!UICONTROL Durchsuchen]** aus.

![durchsuchen](./images/browse.png)

Auf der Hautoberfläche der Seite wird eine Liste von Identitäts-Namespaces angezeigt, die Informationen zu ihren Namen, Identitätssymbolen, dem letzten aktualisierten Datum und dazu enthalten, ob es sich um einen Standard- oder einen benutzerdefinierten Namespace handelt. Die rechte Leiste enthält Informationen zu [!UICONTROL Stärke des Identitätsdiagramms].

![identities](./images/identities.png)

Platform bietet auch Namespaces für Integrationszwecke. Diese Namespaces sind standardmäßig ausgeblendet, da sie zur Verbindung mit anderen Systemen verwendet werden und nicht zum Zuordnen von Identitäten verwendet werden. Um Integrations-Namespaces anzuzeigen, wählen Sie **[!UICONTROL Integrations-Identitäten anzeigen]** aus.

![view-integration-identities](./images/view-integration-identities.png)

Wählen Sie einen Identitäts-Namespace aus der Liste aus, um Informationen zu einem bestimmten Namespace anzuzeigen. Bei Auswahl eines Identitäts-Namespace wird die Anzeige in der rechten Leiste aktualisiert, um Metadaten zum ausgewählten Identitäts-Namespace anzuzeigen, einschließlich der Anzahl der aufgenommenen Identitäten und der Anzahl fehlgeschlagener und übersprungener Datensätze.

![select-namespace](./images/select-namespace.png)

## Verwalten benutzerdefinierter Namespaces {#manage-namespaces}

Je nach den Daten und Anwendungsfällen in Ihrer Organisation benötigen Sie möglicherweise benutzerdefinierte Namespaces. Benutzerdefinierte Namespaces können mit der API [[!DNL Identity Service]](./api/create-custom-namespace.md) oder über die Benutzeroberfläche erstellt werden.

Um mithilfe der Benutzeroberfläche einen benutzerdefinierten Namespace zu erstellen, navigieren Sie zum Arbeitsbereich **[!UICONTROL Identitäten]**, wählen Sie **[!UICONTROL Durchsuchen]** und klicken Sie dann auf **[!UICONTROL Identitäts-Namespace erstellen]**.

![select-create](./images/select-create.png)

Das Dialogfeld **[!UICONTROL Identitäts-Namespace erstellen]** wird angezeigt. Geben Sie einen eindeutigen **[!UICONTROL Anzeigenamen]** und **[!UICONTROL Identitätssymbol]** an und wählen Sie dann den Identitätstyp aus, den Sie erstellen möchten. Sie können auch eine optionale Beschreibung hinzufügen, um weitere Informationen zum Namespace hinzuzufügen. Alle Identitätstypen mit Ausnahme von **Non-People-Kennung** folgen demselben Verhalten beim Stitching. Wenn Sie beim Erstellen eines Namespace die Kennung **Nicht-Personen** als Identitätstyp auswählen, erfolgt die Zuordnung nicht. Spezifische Informationen zu den einzelnen Identitätstypen finden Sie in der Tabelle unter [Identitätstypen](#identity-types).

Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

>[!IMPORTANT]
>
>Die von Ihnen definierten Namespaces sind für Ihre Organisation privat und erfordern ein eindeutiges Identitätssymbol, damit sie erfolgreich erstellt werden können.

![create-identity-namespace](./images/create-identity-namespace.png)

Ähnlich wie bei Standard-Namespaces können Sie auf der Registerkarte **[!UICONTROL Durchsuchen]** einen benutzerdefinierten Namespace auswählen, um dessen Details anzuzeigen. Mit einem benutzerdefinierten Namespace können Sie jedoch auch dessen Anzeigenamen und Beschreibung im Detailbereich bearbeiten.

>[!NOTE]
>
>Nachdem ein Namespace erstellt wurde, kann er nicht mehr gelöscht werden und sein Identitätssymbol und Typ können nicht mehr geändert werden.

## Namespaces in Identitätsdaten

Die Angabe des Namespace für eine Identität hängt von der Methode ab, mit der Sie Identitätsdaten bereitstellen. Einzelheiten zur Bereitstellung von Identitätsdaten finden Sie im Abschnitt zum [Bereitstellen von Identitätsdaten](./home.md#supplying-identity-data-to-identity-service) in der Übersicht über den [!DNL Identity Service]

## Nächste Schritte

Nachdem Sie nun die Schlüsselkonzepte von Identitäts-Namespaces verstehen, können Sie beginnen zu lernen, wie Sie mit Ihrem Identitätsdiagramm mit dem [Identitätsdiagramm-Viewer](./ui/identity-graph-viewer.md) arbeiten.
