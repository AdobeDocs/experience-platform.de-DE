---
title: Überblick über den Identitäts-Namespace
description: Erfahren Sie mehr über Identitäts-Namespaces im Identity Service.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: 59ac3d8b7fee0327396c990ef309ca3a4f292a77
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 26%

---

# Übersicht über Identitäts-Namespaces

Im folgenden Dokument erfahren Sie mehr über die Möglichkeiten von Identitäts-Namespaces im Adobe Experience Platform Identity Service.

## Erste Schritte

Identitäts-Namespaces erfordern ein Verständnis verschiedener Adobe Experience Platform-Dienste. Bevor Sie Namespaces nutzen, lesen Sie bitte die Dokumentation für folgende Dienste:

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.
* [[!DNL Identity Service]](../home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kunden und ihr Verhalten, indem Sie Identitäten zwischen Geräten und Systemen überbrücken.
* [[!DNL Privacy Service]](../../privacy-service/home.md): Identitäts-Namespaces werden in Compliance-Anforderungen für gesetzliche Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) verwendet. Jede Datenschutzanfrage wird in Bezug auf einen Namespace gestellt, um zu ermitteln, welche Verbraucherdaten betroffen sein sollen.

## Identitäts-Namespaces verstehen {#understanding-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Identity-Namespaces"
>abstract="Ein Identity-Namespace ist der Kontext einer bestimmten Identität. Beispiel: ein Namespace von `Email` könnte **name<span>@acme.com** entsprechen. Gleichermaßen könnte ein Namespace von `Phone` `555-555-1234` entsprechen."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Identitätswerte"
>abstract="Ein Identitätswert ist eine Kennung, die für eine eindeutige Person, eine eindeutige Organisation oder ein eindeutiges Asset steht. Der Kontext oder der Typ der Identität, den der Wert darstellt, wird durch einen entsprechenden Identity-Namespace definiert. Bei der Zuordnung von Eintragsdaten über Profilfragmente hinweg müssen Namespace und Identitätswert übereinstimmen. Bei der Zuordnung von Eintragsdaten über Profilfragmente hinweg müssen Namespace und Identitätswert übereinstimmen."
>text="Learn more in documentation"

Eine voll qualifizierte Identität umfasst zwei Komponenten: einen **Identitätswert** und einen **Identitäts-Namespace**. Wenn der Wert einer Identität beispielsweise &quot;`scott@acme.com`&quot; lautet, liefert ein Namespace Kontext für diesen Wert, indem er ihn als E-Mail-Adresse unterscheidet. Auf ähnliche Weise kann ein Namespace `555-123-456` als Telefonnummer und `3126ABC` als CRM-ID unterscheiden. Im Grunde stellt **ein Namespace Kontext für eine bestimmte Identität bereit**. Wenn Datensatzdaten über Profilfragmente hinweg abgeglichen werden (z. B. wenn [!DNL Real-Time Customer Profile] Profildaten zusammenführt), müssen sowohl der Identitätswert als auch der Namespace übereinstimmen.

Zwei Profilfragmente können beispielsweise unterschiedliche primäre IDs enthalten, für den Namespace &quot;E-Mail&quot;jedoch denselben Wert verwenden. Daher kann Experience Platform sehen, dass diese Fragmente eigentlich dieselbe Person sind und die Daten im Identitätsdiagramm für die Person zusammenführen.

>[!BEGINSHADEBOX]

**Identitäts-Namespace erläutert**

Eine andere Möglichkeit, das Konzept des Namespace besser zu verstehen, besteht darin, reale Beispiele wie Städte und ihre jeweiligen Staaten zu berücksichtigen. Zum Beispiel sind Portland, Maine und Portland, Oregon zwei verschiedene Orte in den Vereinigten Staaten. Während die Städte denselben Namen haben, fungiert der Staat als Namespace und bietet den erforderlichen Kontext, der die beiden Städte voneinander unterscheidet.

Anwenden derselben Logik auf Identity Service:

* Auf einen Blick kann der Identitätswert von: `1-234-567-8900` wie eine Telefonnummer aussehen. Aus Sicht des Systems hätte dieser Wert jedoch als CRM-ID konfiguriert werden können. Identity Service kann ohne einen entsprechenden Namespace den erforderlichen Kontext auf diesen Identitätswert nicht anwenden.
* Ein weiteres Beispiel ist der Identitätswert: `john@gmail.com`. Dieser Identitätswert kann zwar leicht als E-Mail-Adresse betrachtet werden, es ist jedoch durchaus möglich, dass er als benutzerdefinierte Namespace-CRM-ID konfiguriert ist. Mit dem Namespace können Sie `Email:john@gmail.com` von `CRM ID:john@gmail.com` unterscheiden.

>[!ENDSHADEBOX]

### Komponenten eines Namespace

Ein Namespace besteht aus den folgenden Komponenten:

* **Anzeigename**: Der benutzerfreundliche Name für einen bestimmten Namespace.
* **Identitätssymbol**: Ein Code, der intern von Identity Service zur Darstellung eines Namespace verwendet wird.
* **Identitätstyp**: Die Klassifizierung eines bestimmten Namespace.
* **Beschreibung**: (Optional) Alle zusätzlichen Informationen, die Sie zu einem bestimmten Namespace bereitstellen können.

### Identitätstyp {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Angeben des Identitätstyps"
>abstract="Der Identitätstyp bestimmt, ob Daten im Identitätsdiagramm gespeichert werden oder nicht. Identitätsdiagramme werden nicht für die folgenden Identitätstypen generiert: Nicht-Personen-IDs und Partner-ID."
>text="Learn more in documentation"

Ein Element eines Identitäts-Namespace ist der **Identitätstyp**. Der Identitätstyp bestimmt:

* Ob ein Identitätsdiagramm generiert wird:
   * Identitätsdiagramme werden nicht für die folgenden Identitätstypen generiert: Nicht-Personen-IDs und Partner-ID.
   * Identitätsdiagramme werden für alle anderen Identitätstypen generiert.
* Welche Identitäten werden aus dem Identitätsdiagramm entfernt, wenn Systembeschränkungen erreicht werden. Weitere Informationen finden Sie in den [Limits für Identitätsdaten](../guardrails.md).

Die folgenden Identitätstypen sind innerhalb von Experience Platform verfügbar:

| Identitätstyp | Beschreibung |
| --- | --- |
| Cookie-ID | Cookie-IDs identifizieren Webbrowser. Diese Identitäten sind für Erweiterungen von entscheidender Bedeutung und bilden den Großteil des Identitätsdiagramms. Sie verfallen jedoch von Natur aus schnell und verlieren mit der Zeit ihren Wert. |
| Geräteübergreifende ID | Geräteübergreifende IDs identifizieren eine Person und verbinden normalerweise andere IDs miteinander. Beispiele sind eine Anmelde-ID, CRM-ID und Loyalitäts-ID. Dies ist ein Hinweis an [!DNL Identity Service], den Wert sensibel zu behandeln. |
| Geräte-ID | Geräte-IDs identifizieren Hardware-Geräte, wie IDFA (iPhone und iPad), GAID (Android) und RIDA (Roku) und können von mehreren Personen in Haushalten gemeinsam verwendet werden. |
| E-Mail-Adresse | E-Mail-Adressen sind oft mit einer einzelnen Person verknüpft und können daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. Identitäten dieser Art beinhalten personenbezogene Daten (PII). Dies ist ein Hinweis an [!DNL Identity Service], den Wert sensibel zu behandeln. |
| Nicht personenbezogene Kennung | Nicht personenbezogene IDs werden für das Speichern von Identifikatoren verwendet, die Namespaces erfordern, aber nicht mit einem Personen-Cluster verbunden sind, z. B. eine Produktnummer oder Daten, die mit Produkten, Organisationen oder Geschäften verbunden sind. |
| Partner-ID | <ul><li>Partner-IDs sind Kennungen, die von Datenpartnern zur Darstellung von Personen verwendet werden. Partner-IDs sind häufig pseudonym, sodass die wahre Identität einer Person nicht erkennbar ist und probabilistisch sein kann. In Real-time Customer Data Platform werden Partner-IDs primär für die erweiterte Zielgruppenaktivierung und Datenanreicherung und nicht zum Erstellen von Identitätsdiagrammverknüpfungen verwendet.</li><li>Identitätsdiagramme werden nicht bei der Erfassung einer Identität generiert, die einen Identitäts-Namespace enthält, der als Partner-ID-Typ angegeben wurde.</li><li>Wenn Partnerdaten nicht mit dem Identitätstyp Partner-ID erfasst werden, können für Identity Service Systemdiagrammbeschränkungen sowie unerwünschte Profilzusammenführungen auftreten.</li><ul> |
| Telefonnummer | Telefonnummern sind häufig mit einer einzelnen Person verknüpft und können daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. Identitäten dieser Art umfassen PII. Dies ist ein Hinweis auf [!DNL Identity Service], um den Wert sensibel zu behandeln. |

{style="table-layout:auto"}

### Standard-Namespaces {#standard}

Experience Platform bietet mehrere Identitäts-Namespaces, die für alle Organisationen verfügbar sind. Diese werden als Standard-Namespaces bezeichnet und sind über die [!DNL Identity Service] -API oder die Platform-Benutzeroberfläche sichtbar.

Die folgenden Standard-Namespaces stehen allen Organisationen in Platform zur Verfügung:

| Anzeigename | Beschreibung |
| ------------ | ----------- |
| AdCloud | Ein Namespace, der Adobe AdCloud darstellt. |
| Adobe Analytics (veraltete ID) | Ein Namespace, der Adobe Analytics darstellt. Weitere Informationen finden Sie im folgenden Dokument zu [Adobe Analytics-Namespaces](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html#namespaces) . |
| Apple IDFA (ID für Advertiser) | Ein Namespace, der die Apple ID für Advertiser darstellt. Weiteführende Informationen finden Sie im folgenden Dokument zu [Interessensbasierten Anzeigen](https://support.apple.com/de-de/HT202074). |
| Apple Push Notification Service | Ein Namespace, der Identitäten darstellt, die mit dem Apple Push Notification Service erfasst wurden. Weitere Informationen finden Sie im folgenden Dokument zu [Apple Push Notification Service](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) . |
| ECID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument zu [ECID](./ecid.md) . |
| E-Mail | Ein Namespace, der eine E-Mail-Adresse darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |
| E-Mails (SHA256, in Kleinbuchstaben) | Ein Namespace für vorab gehashte E-Mail-Adressen. In diesem Namespace angegebene Werte werden vor dem Hashing mit SHA256 in Kleinbuchstaben umgewandelt. Vor der Normalisierung einer E-Mail-Adresse müssen vorangestellte und nachfolgende Leerzeichen abgeschnitten werden. Diese Einstellung kann nachträglich nicht mehr geändert werden. Weitere Informationen finden Sie im folgenden Dokument zur [SHA256-Hashing-Unterstützung](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html#hashing-support) . |
| Firebase Cloud Messaging | Ein Namespace, der Identitäten darstellt, die mit Google Firebase Cloud Messaging für Push-Benachrichtigungen erfasst wurden. Weitere Informationen finden Sie im folgenden Dokument zu [Google Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging) . |
| Google Ad ID (GAID) | Ein Namespace, der eine Google Advertising ID darstellt. Weiterführende Informationen finden Sie im folgenden Dokument zu [Google Advertising IDs](https://support.google.com/googleplay/android-developer/answer/6048248?hl=de). |
| Telefon | Ein Namespace, der eine Telefonnummer darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |
| Telefon (E.164) | Ein Namespace, der rohe Telefonnummern darstellt, die im E.164-Format gehasht werden müssen. Das E.164-Format enthält ein Pluszeichen (`+`), eine internationale Rufnummer, einen lokalen Gebietscode und eine Telefonnummer. Beispiel: `(+)(country code)(area code)(phone number)`. |
| Telefon (SHA256) | Ein Namespace, der Telefonnummern darstellt, die mit SHA256 gehasht werden müssen. Sie müssen Symbole, Buchstaben und alle führenden Nullen entfernen. Sie müssen auch den Länderaufrufscode als Präfix hinzufügen. |
| Phone (SHA256_E.164) | Ein Namespace, der unformatierte Telefonnummern darstellt, die mit dem SHA256- und E.164-Format gehasht werden müssen. |
| TNTID | Ein Namespace, der Adobe Target darstellt. Weitere Informationen finden Sie im folgenden Dokument zu [Target](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=de) . |
| Windows AID | Ein Namespace, der eine Windows Advertising ID darstellt. Weitere Informationen finden Sie im folgenden Dokument unter [Windows Advertising ID](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) . |

### Anzeigen von Identitäts-Namespaces {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="Anzeigen von Integrationsidentitäten"
>abstract="Integrationsidentitäten sind Namespaces, die zur Verbindung mit anderen Systemen verwendet werden. Sie werden nicht bei der Identitätsauflösung oder zum Zusammenfügen von Identitäten verwendet. <br> Diese Identitäten sind standardmäßig ausgeblendet. Mit dem Umschalter können Sie Integrations-Namespaces anzeigen."

Um Identitäts-Namespaces in der Benutzeroberfläche anzuzeigen, wählen Sie im linken Navigationsbereich **[!UICONTROL Identitäten]** und dann **[!UICONTROL Durchsuchen]** aus.

Es wird ein Verzeichnis der Namespaces in Ihrer Organisation angezeigt, in dem Informationen zu ihren Namen, Identitätssymbolen, zuletzt aktualisierten Daten, entsprechenden Identitätstypen und Beschreibungen angezeigt werden.

![Ein Verzeichnis der benutzerdefinierten Identitäts-Namespaces in Ihrem Unternehmen.](../images/namespace/browse.png)

## Benutzerdefinierte Namespaces erstellen {#create-namespaces}

Je nach Ihren Organisationsdaten und Anwendungsfällen benötigen Sie möglicherweise benutzerdefinierte Namespaces. Benutzerdefinierte Namespaces können mit der [[!DNL Identity Service]](../api/create-custom-namespace.md) -API oder über die Benutzeroberfläche erstellt werden.

Um einen benutzerdefinierten Namespace zu erstellen, wählen Sie **[!UICONTROL Identitäts-Namespace erstellen]** aus.

>[!TIP]
>
>Integrationsidentitäten sind Namespaces, die zur Verbindung mit anderen Systemen verwendet werden. Sie werden weder in der Identitätsauflösung noch zum Zuordnen von Identitäten verwendet. Wählen Sie **[!UICONTROL Integrationsidentitäten anzeigen]** aus, um die Liste zu aktualisieren und Integrationsidentitäten einzuschließen. Integrations-Identitäten sind jedoch standardmäßig ausgeblendet, da sie schreibgeschützt sind und Sie sie nicht konfigurieren müssen.

![Die Schaltfläche zum Erstellen eines Identitäts-Namespace im Arbeitsbereich &quot;Identitäten&quot;.](../images/namespace/create-identity-namespace.png)

Das Fenster [!UICONTROL Identitäts-Namespace erstellen] wird angezeigt. Zunächst müssen Sie einen Anzeigenamen und ein Identitätssymbol für den benutzerdefinierten Namespace angeben, den Sie erstellen möchten. Sie können optional auch eine Beschreibung angeben, um dem benutzerdefinierten Namespace, den Sie erstellen, mehr Kontext hinzuzufügen.

![Ein Popup-Fenster, in das Sie Informationen zu Ihrem benutzerdefinierten Identitäts-Namespace eingeben können.](../images/namespace/name-and-symbol.png)

Wählen Sie anschließend den Identitätstyp aus, den Sie dem benutzerdefinierten Namespace zuweisen möchten. Klicken Sie abschließend auf **[!UICONTROL Erstellen]**.

![Eine Auswahl von Identitätstypen, aus denen Sie einen benutzerdefinierten Identitäts-Namespace auswählen und ihn zuweisen können.](../images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* Die von Ihnen definierten Namespaces sind für Ihre Organisation privat und erfordern ein eindeutiges Identitätssymbol, damit sie erfolgreich erstellt werden können.
>
>* Nachdem ein Namespace erstellt wurde, kann er nicht mehr gelöscht werden und sein Identitätssymbol und Typ können nicht mehr geändert werden.
>
>* Doppelte Namespaces werden nicht unterstützt. Sie können beim Erstellen eines neuen Namespace keinen vorhandenen Anzeigenamen und kein Identitätssymbol verwenden.

## Namespaces in Identitätsdaten

Die Angabe des Namespace für eine Identität hängt von der Methode ab, mit der Sie Identitätsdaten bereitstellen. Einzelheiten zur Bereitstellung von Identitätsdaten finden Sie im [[!DNL Identity Service] Implementierungshandbuch](../implementation.md).

## Nächste Schritte

Nachdem Sie nun die Schlüsselkonzepte von Identitäts-Namespaces verstehen, können Sie beginnen zu lernen, wie Sie mit Ihrem Identitätsdiagramm mit dem [Identitätsdiagramm-Viewer](../features/identity-graph-viewer.md) arbeiten.
