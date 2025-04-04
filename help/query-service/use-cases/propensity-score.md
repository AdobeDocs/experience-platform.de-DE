---
title: Bestimmen eines Neigungs-Scores mithilfe eines durch maschinelles Lernen generierten prädiktiven Modells
description: Erfahren Sie, wie Sie mit Query Service Ihr prädiktives Modell auf Experience Platform-Daten anwenden können. In diesem Dokument wird gezeigt, wie mithilfe von Experience Platform-Daten die Kaufneigung eines Kunden bei jedem Besuch vorhergesagt werden kann.
exl-id: 29587541-50dd-405c-bc18-17947b8a5942
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Bestimmen eines Neigungs-Scores mithilfe eines durch maschinelles Lernen generierten prädiktiven Modells

Mit dem Abfrage-Service können Sie Prognosemodelle wie Tendenzwerte nutzen, die auf Ihrer maschinellen Lernplattform erstellt wurden, um Experience Platform-Daten zu analysieren.

In diesem Handbuch wird erläutert, wie Sie mit dem Abfrage-Service Daten an Ihre Plattform für maschinelles Lernen senden können, um ein Modell in einem Notebook zu trainieren. Das trainierte Modell kann mithilfe von SQL auf Daten angewendet werden, um die Kaufneigung eines Kunden bei jedem Besuch vorherzusagen.

## Erste Schritte

Im Rahmen dieses Prozesses müssen Sie ein Modell für maschinelles Lernen trainieren. Dieses Dokument setzt Kenntnisse über eine oder mehrere maschinelle Lernumgebungen voraus.

In diesem Beispiel wird [!DNL Jupyter Notebook] als Entwicklungsumgebung verwendet. Obwohl viele Optionen verfügbar sind, wird [!DNL Jupyter Notebook] empfohlen, da es sich um eine Open-Source-Webanwendung mit geringen Rechenanforderungen handelt. Es kann [von der offiziellen Website heruntergeladen werden](https://jupyter.org/).

Wenn Sie dies noch nicht getan haben, führen Sie die Schritte zum [Verbinden [!DNL Jupyter Notebook] mit dem Adobe Experience Platform-Abfrage-](../clients/jupyter-notebook.md) aus, bevor Sie mit diesem Handbuch fortfahren.

Zu den in diesem Beispiel verwendeten Bibliotheken gehören:

```console
python=3.6.7
psycopg2
sklearn
pandas
matplotlib
numpy
tqdm
```

## Importieren von Analytics-Tabellen aus Experience Platform in [!DNL Jupyter Notebook] {#import-analytics-tables}

Um ein Tendenz-Score-Modell zu generieren, muss eine Projektion der in Experience Platform gespeicherten Analysedaten in [!DNL Jupyter Notebook] importiert werden. Von einer [!DNL Python] 3-[!DNL Jupyter Notebook], die mit dem Abfrage-Service verbunden ist, importieren die folgenden Befehle einen Kundenverhaltensdatensatz aus Luma, einem fiktiven Bekleidungsgeschäft. Da Experience Platform-Daten im Experience-Datenmodell (XDM)-Format gespeichert werden, muss ein JSON-Beispielobjekt generiert werden, das der Schemastruktur entspricht. In der Dokumentation finden Sie Anweisungen zum Generieren [ JSON-Beispielobjekts](../../xdm/ui/sample.md).

![Das [!DNL Jupyter Notebook]-Dashboard mit mehreren hervorgehobenen Befehlen.](../images/use-cases/jupyter-commands.png)

Die Ausgabe zeigt eine tabellarische Ansicht aller Spalten aus dem Verhaltensdatensatz von Luma im [!DNL Jupyter Notebook]-Dashboard an.

![Die tabellarische Ausgabe des importierten Kundenverhaltensdatensatzes von Luma in [!DNL Jupyter Notebook].](../images/use-cases/behavioural-dataset-results.png)

## Vorbereiten der Daten für maschinelles Lernen {#prepare-data-for-machine-learning}

Zum Trainieren eines Modells für maschinelles Lernen muss eine Zielspalte identifiziert werden. Da die Kaufneigung das Ziel für diesen Anwendungsfall ist, wird die Spalte `analytic_action` als Zielspalte aus den Luma-Ergebnissen ausgewählt. Der Wert `productPurchase` ist der Indikator für einen Kundenkauf. Die Spalten `purchase_value` und `purchase_num` werden ebenfalls entfernt, da sie direkt mit der Produktkaufaktion zusammenhängen.

Die Befehle zum Ausführen dieser Aktionen lauten wie folgt:

```python
#define the target label for prediction
df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
#remove columns that are dependent on the label
df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
```

Als Nächstes müssen die Daten aus dem Luma-Datensatz in geeignete Darstellungen umgewandelt werden. Zwei Schritte sind erforderlich:

1. Transformiert die Spalten, die Zahlen darstellen, in numerische Spalten. Konvertieren Sie dazu den Datentyp im `dataframe` explizit.
1. Wandeln Sie kategoriale Spalten auch in numerische Spalten um.

```python
#convert columns that represent numbers
num_cols = ['purchase_num', 'value_cart', 'value_lifetime']
df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
```

Eine Technik namens *One-Hot* Kodierung) wird verwendet, um die kategorialen Datenvariablen zu konvertieren, damit sie mit maschinellen und Deep-Learning-Algorithmen verwendet werden können. Dies verbessert wiederum die Vorhersagen sowie die Klassifizierungsgenauigkeit eines Modells. Verwenden Sie die `Sklearn`-Bibliothek, um jeden Kategoriewert in einer separaten Spalte darzustellen.

```python
from sklearn.preprocessing import OneHotEncoder

#get the categorical columns
cat_columns = list(set(df.columns) - set(num_cols + ['target']))

#get the dataframe with categorical columns only
df_cat = df.loc[:,cat_columns]

#initialize sklearn's OneHotEncoder
enc = OneHotEncoder(handle_unknown='ignore')

#fit the data into the encoder
enc.fit(df_cat)

#define OneHotEncoder's columns names
ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
ohc_columns = [item for sublist in ohc_columns for item in sublist]

#finalize the data input to the ML models
X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                 columns =  ohc_columns + num_cols)

#define target column
y = df['target']
```

Die als `X` definierten Daten werden tabellarisch dargestellt und wie folgt angezeigt:

![Die tabellarische Ausgabe von X innerhalb von [!DNL Jupyter Notebook].](../images/use-cases/x-output-table.png)


Nachdem die erforderlichen Daten für maschinelles Lernen verfügbar sind, können die vorkonfigurierten Modelle für maschinelles Lernen in die `sklearn`-Bibliothek von [!DNL Python] eingefügt werden. [!DNL Logistics Regression] wird verwendet, um das Tendenzmodell zu trainieren, und ermöglicht es Ihnen, die Genauigkeit der Testdaten zu sehen. In diesem Fall liegt er bei ca. 85 %.

Der [!DNL Logistic Regression] Algorithmus und die Methode zur Aufteilung des Zugversuchs, die zur Schätzung der Leistung von Algorithmen für maschinelles Lernen verwendet werden, werden in den folgenden Codeblock importiert:

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

clf = LogisticRegression(max_iter=2000, random_state=0).fit(X_train, y_train)

print("Test data accuracy: {}".format(clf.score(X_test, y_test)))
```

Die Genauigkeit der Testdaten beträgt 0,8518518518518519.

Durch die Verwendung der Logistik-Regression können Sie die Gründe für einen Kauf visualisieren und die Funktionen sortieren, die die Tendenz nach ihrer Rangfolge in absteigender Reihenfolge bestimmen. Die ersten Spalten bezeichnen eine höhere Kausalität, die zum Kaufverhalten führt. Letztere Spalten geben Faktoren an, die nicht zum Kaufverhalten führen.

Der Code zur Visualisierung der Ergebnisse als zwei Balkendiagramme lautet wie folgt:

```python
from matplotlib import pyplot as plt

#get feature importance as a sorted list of columns
feature_importance = np.argsort(-clf.coef_[0])
top_10_features_purchase_names = X.columns[feature_importance[:10]]
top_10_features_purchase_values = clf.coef_[0][feature_importance[:10]]
top_10_features_not_purchase_names = X.columns[feature_importance[-10:]]
top_10_features_not_purchase_values = clf.coef_[0][feature_importance[-10:]]

#plot the figures
fig, (ax1, ax2) = plt.subplots(1, 2,figsize=(10,5))

ax1.bar(np.arange(10),top_10_features_purchase_values)
ax1.set_xticks(np.arange(10))
ax1.set_xticklabels(top_10_features_purchase_names,rotation = 90)
ax1.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax1.set_title("Top 10 features to define \n a propensity to purchase")

ax2.bar(np.arange(10),top_10_features_not_purchase_values, color='#E15750')
ax2.set_xticks(np.arange(10))
ax2.set_xticklabels(top_10_features_not_purchase_names,rotation = 90)
ax2.set_ylim([np.min(clf.coef_[0])-0.1,np.max(clf.coef_[0])+0.1])
ax2.set_title("Top 10 features to define \n a propensity to NOT purchase")

plt.show()
```

Nachfolgend finden Sie eine vertikale Balkendiagrammvisualisierung der Ergebnisse:

![Die Visualisierung der 10 wichtigsten Funktionen, die eine Kaufneigung definieren.](../images/use-cases/visualized-results.png)

Aus dem Balkendiagramm können mehrere Muster erkannt werden. Die Themen Point of Sale (POS) und Call (Anruf) des Kanals als als Kostenerstattung sind die wichtigsten Faktoren, die über ein Kaufverhalten entscheiden. Während die Themen der Anrufe wie Beschwerden und Rechnungen wichtige Rollen sind, um das Kaufverhalten nicht zu definieren. Dies sind quantifizierbare, umsetzbare Einblicke, die Marketing-Experten nutzen können, um Marketing-Kampagnen durchzuführen, um die Kaufneigung dieser Kundinnen und Kunden zu ermitteln.

## Verwenden des Abfrage-Service zum Anwenden des trainierten Modells {#use-query-service-to-apply-trained-model}

Nachdem das trainierte Modell erstellt wurde, muss es auf die in Experience Platform gespeicherten Daten angewendet werden. Dazu muss die Logik der Pipeline für maschinelles Lernen in SQL konvertiert werden. Die beiden Hauptkomponenten dieses Übergangs sind:

- Zunächst muss SQL an die Stelle des [!DNL Logistics Regression]-Moduls treten, um die Wahrscheinlichkeit einer Prognosebezeichnung zu erhalten. Das von Logistics Regression erstellte Modell erzeugte das Regressionsmodell `y = wX + c`, bei dem die Gewichtung `w` und die `c` die Ausgabe des Modells bilden. SQL-Funktionen können verwendet werden, um die Gewichtungen zu multiplizieren, um eine Wahrscheinlichkeit zu erhalten.

- Zweitens muss der in [!DNL Python] mit einer Hot-Codierung erzielte Engineering-Prozess ebenfalls in SQL integriert werden. In der ursprünglichen Datenbank befindet sich beispielsweise `geo_county` Spalte, in der die Provinz gespeichert wird. Die Spalte wird jedoch in `geo_county=Bexar`, `geo_county=Dallas` `geo_county=DeKalb` konvertiert. Die folgende SQL-Anweisung führt dieselbe Transformation durch, bei der `w1`, `w2` und `w3` durch die vom Modell in [!DNL Python] erlernten Gewichtungen ersetzt werden können:

```sql
SELECT  CASE WHEN geo_state = 'Bexar' THEN FLOAT(w1) ELSE 0 END AS f1,
        CASE WHEN geo_state = 'Dallas' THEN FLOAT(w2) ELSE 0 END AS f2,
        CASE WHEN geo_state = 'Bexar' THEN FLOAT(w3) ELSE 0 END AS f3,
```

Bei numerischen Funktionen können Sie die Spalten direkt mit den Gewichtungen multiplizieren, wie in der folgenden SQL-Anweisung dargestellt.

```sql
SELECT FLOAT(purchase_num) * FLOAT(w4) AS f4,
```

Nachdem die Zahlen ermittelt wurden, können sie in eine Sigmoid-Funktion portiert werden, wo der Logistics Regression Algorithmus die endgültigen Prognosen erzeugt. In der folgenden Anweisung ist `intercept` die Nummer des Abschnitts in der Regression.
        

```sql
SELECT CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + f4 + FLOAT(intercept)))) > 0.5 THEN 1 ELSE 0 END AS Prediction;
```
 
### Ein Beispiel von Anfang bis Ende

Wenn Sie zwei Spalten (`c1` und `c2`) haben und `c1` zwei Kategorien hat, wird der [!DNL Logistic Regression] Algorithmus mit der folgenden Funktion trainiert:
 

```python
y = 0.1 * "c1=category 1"+ 0.2 * "c1=category 2" +0.3 * c2+0.4
```
 
Die Entsprechung in SQL lautet wie folgt:

```sql
SELECT
  CASE WHEN 1 / (1 + EXP(- (f1 + f2 + f3 + FLOAT(0.4)))) > 0.5 THEN 1 ELSE 0 END AS Prediction
FROM
  (
    SELECT
      CASE WHEN c1 = 'Cateogry 1' THEN FLOAT(0.1) ELSE 0 END AS f1,
      CASE WHEN c1 = 'Cateogry 2' THEN FLOAT(0.2) ELSE 0 END AS f2,
      FLOAT(c2) * FLOAT(0.3) AS f3
    FROM TABLE
  )
```
 
Der [!DNL Python] Code zur Automatisierung des Übersetzungsprozesses lautet wie folgt:

```python
def generate_lr_inference_sql(ohc_columns, num_cols, clf, db):
    features_sql = []
    category_sql_text = "case when {col} = '{val}' then float({coef}) else 0 end as f{name}"
    numerical_sql_text = "float({col}) * float({coef}) as f{name}"
    for i, (column, coef) in enumerate(zip(ohc_columns+num_cols, clf.coef_[0])):
        if i < len(ohc_columns):
            col,val = column.split('=')
            val = val.replace("'","%''%")
            sql = category_sql_text.format(col=col,val=val,coef=coef,name=i+1)
        else:
            sql = numerical_sql_text.format(col=column,coef=coef,name=i+1)
        features_sql.append(sql)
    features_sum = '+'.join(['f{}'.format(i) for i in range(1,len(features_sql)+1)])
    final_sql = '''
    select case when 1/(1 + EXP(-({features} + float({intercept})))) > 0.5 then 1 else 0 end as Prediction
    from
        (select {cols}
        from {db})
    '''.format(features=features_sum,cols=",".join(features_sql),intercept=clf.intercept_[0],db=db)
    return final_sql
```

Wenn SQL zum Ableiten der Datenbank verwendet wird, wird folgende Ausgabe ausgegeben:

```python
sql = generate_lr_inference_sql(ohc_columns, num_cols, clf, "fdu_luma_raw")
cur.execute(sql)    
samples = [r for r in cur]
colnames = [desc[0] for desc in cur.description]
pd.DataFrame(samples,columns=colnames)
```

Die tabellarischen Ergebnisse zeigen die Kauftendenz für jede Kundensitzung mit `0` Bedeutung: keine Kauftendenz und `1` bestätigte Kauftendenz.

![Die tabellarischen Ergebnisse des Datenbankabschlusses mithilfe von SQL.](../images/use-cases/inference-results.png)

## Arbeiten mit Stichprobendaten: Bootstrapping {#working-on-sampled-data}

Falls die Datengrößen für Ihren lokalen Computer zum Speichern der Daten für das Modell-Training zu groß sind, können Sie anstelle der vollständigen Daten aus dem Abfrage-Service Stichproben nehmen. Um zu erfahren, wie viele Daten zum Stichprobenverfahren aus dem Abfrage-Service benötigt werden, können Sie eine Technik namens Bootstrapping anwenden. In dieser Hinsicht bedeutet Bootstrapping, dass das Modell mehrmals mit verschiedenen Stichproben trainiert wird und die Varianz der Modellgenauigkeiten zwischen verschiedenen Stichproben überprüft wird. Um das oben angegebene Beispiel für das Tendenzmodell anzupassen, kapseln Sie zunächst den gesamten Workflow für maschinelles Lernen in eine Funktion. Der Code lautet wie folgt:

```python
def end_to_end_pipeline(df):
    
    #define the target label for prediction
    df['target'] = (df['analytic_action'] == 'productPurchase').astype(int)
    #remove columns that are dependent on the label
    df.drop(['analytic_action','purchase_value'],axis=1,inplace=True)
    
    num_cols = ['purchase_num','value_cart','value_lifetime']
    df[num_cols] = df[num_cols].apply(pd.to_numeric, errors='coerce')
    
    #get the categorical columns
    cat_columns = list(set(df.columns) - set(num_cols + ['target']))

    #get the dataframe with categorical columns only
    df_cat = df.loc[:,cat_columns]

    #initialize sklearn's One Hot Encoder
    enc = OneHotEncoder(handle_unknown='ignore')

    #fit the data into the encoder
    enc.fit(df_cat)

    #define one hot encoder's columns names
    ohc_columns = [[c+'='+c_ for c_ in cat] for c,cat in zip(cat_columns,enc.categories_)]
    ohc_columns = [item for sublist in ohc_columns for item in sublist]

    #finalize the data input to the ML models
    X = pd.DataFrame( np.concatenate((enc.transform(df_cat).toarray(),df[num_cols]),axis=1),
                     columns =  ohc_columns + num_cols)

    #define target column
    y = df['target']
    
    X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.33, random_state=42)

    clf = LogisticRegression(max_iter=2000,random_state=0).fit(X_train, y_train)

    return clf.score(X_test, y_test)
```

Diese Funktion kann dann mehrmals in einer Schleife ausgeführt werden, beispielsweise 10-mal. Der Unterschied zum vorherigen Code besteht darin, dass das Beispiel jetzt nicht aus der gesamten Tabelle, sondern nur aus einer Reihe von Zeilen entnommen wird. Der folgende Beispiel-Code benötigt beispielsweise nur 1.000 Zeilen. Die Genauigkeiten für jede Iteration können gespeichert werden.

```python
from tqdm import tqdm

bootstrap_accuracy = []
for i in tqdm(range(100)):
    
    #sample data from QS
    cur.execute('''SELECT *
    FROM fdu_luma_raw
    ORDER BY random()
    LIMIT 1000
    ''')    
    samples = [r for r in cur]
    colnames = [desc[0] for desc in cur.description]
    df_samples = pd.DataFrame(samples,columns=colnames)
    df_samples.fillna(0,inplace=True)
    
    #train the propensity model with sampled data and output its accuracy
    bootstrap_accuracy.append(end_to_end_pipeline(df_samples))
    
bootstrap_accuracy = np.sort(bootstrap_accuracy)
```

Die Genauigkeit des Bootstrapping-Modells wird dann sortiert. Danach werden die 10. und 90. Quantile der Modellgenauigkeiten zu einem Konfidenzintervall von 95 % für die Genauigkeit des Modells bei der angegebenen Stichprobengröße.

![Der Druckbefehl zum Anzeigen des Konfidenzintervalls des Tendenzwerts.](../images/use-cases/confidence-interval.png)

Die obige Abbildung zeigt, dass Sie, wenn Sie Ihre Modelle nur in 1000 Zeilen trainieren, mit einer Genauigkeit zwischen etwa 84 % und 88 % rechnen können. Sie können die `LIMIT`-Klausel in Abfragen des Abfrage-Service Ihren Anforderungen entsprechend anpassen, um die Leistung der Modelle sicherzustellen.
