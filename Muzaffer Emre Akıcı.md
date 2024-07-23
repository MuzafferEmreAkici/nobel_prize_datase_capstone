```python
import pandas as pd
```


```python
import numpy as np
```


```python
import matplotlib.pyplot as plt
```


```python
import seaborn as sns
```


```python


nobel = pd.read_csv("C:/Users/muzaf_yzoo1ti/Desktop/emre proje/nobel.csv")

nobel["birth_date"] =pd.to_datetime(nobel["birth_date"], format="%Y-%m-%d")

nobel["death_date"] = pd.to_datetime(nobel["death_date"], format="%Y-%m-%d")

nobel["age"] = nobel["death_date"].dt.year - nobel["birth_date"].dt.year

nobel["age"].fillna(nobel["age"].mean(), inplace=True)

nobel["age"] = nobel["age"].astype(int)



nobel.head(5)





```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>category</th>
      <th>prize</th>
      <th>motivation</th>
      <th>prize_share</th>
      <th>laureate_id</th>
      <th>laureate_type</th>
      <th>full_name</th>
      <th>birth_date</th>
      <th>birth_city</th>
      <th>birth_country</th>
      <th>sex</th>
      <th>organization_name</th>
      <th>organization_city</th>
      <th>organization_country</th>
      <th>death_date</th>
      <th>death_city</th>
      <th>death_country</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1901</td>
      <td>Chemistry</td>
      <td>The Nobel Prize in Chemistry 1901</td>
      <td>"in recognition of the extraordinary services ...</td>
      <td>1/1</td>
      <td>160</td>
      <td>Individual</td>
      <td>Jacobus Henricus van 't Hoff</td>
      <td>1852-08-30</td>
      <td>Rotterdam</td>
      <td>Netherlands</td>
      <td>Male</td>
      <td>Berlin University</td>
      <td>Berlin</td>
      <td>Germany</td>
      <td>1911-03-01</td>
      <td>Berlin</td>
      <td>Germany</td>
      <td>59</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1901</td>
      <td>Literature</td>
      <td>The Nobel Prize in Literature 1901</td>
      <td>"in special recognition of his poetic composit...</td>
      <td>1/1</td>
      <td>569</td>
      <td>Individual</td>
      <td>Sully Prudhomme</td>
      <td>1839-03-16</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1907-09-07</td>
      <td>Châtenay</td>
      <td>France</td>
      <td>68</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1901</td>
      <td>Medicine</td>
      <td>The Nobel Prize in Physiology or Medicine 1901</td>
      <td>"for his work on serum therapy, especially its...</td>
      <td>1/1</td>
      <td>293</td>
      <td>Individual</td>
      <td>Emil Adolf von Behring</td>
      <td>1854-03-15</td>
      <td>Hansdorf (Lawice)</td>
      <td>Prussia (Poland)</td>
      <td>Male</td>
      <td>Marburg University</td>
      <td>Marburg</td>
      <td>Germany</td>
      <td>1917-03-31</td>
      <td>Marburg</td>
      <td>Germany</td>
      <td>63</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1901</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>462</td>
      <td>Individual</td>
      <td>Jean Henry Dunant</td>
      <td>1828-05-08</td>
      <td>Geneva</td>
      <td>Switzerland</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1910-10-30</td>
      <td>Heiden</td>
      <td>Switzerland</td>
      <td>82</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1901</td>
      <td>Peace</td>
      <td>The Nobel Peace Prize 1901</td>
      <td>NaN</td>
      <td>1/2</td>
      <td>463</td>
      <td>Individual</td>
      <td>Frédéric Passy</td>
      <td>1822-05-20</td>
      <td>Paris</td>
      <td>France</td>
      <td>Male</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1912-06-12</td>
      <td>Paris</td>
      <td>France</td>
      <td>90</td>
    </tr>
  </tbody>
</table>
</div>



# Nobel Ödüllerini en çok kazanan ilk on ülkeyi bulunuz.


```python
top_countries = nobel["birth_country"].value_counts().head(10)
print(top_countries)

```

    birth_country
    United States of America    259
    United Kingdom               85
    Germany                      61
    France                       51
    Sweden                       29
    Japan                        24
    Canada                       18
    Netherlands                  18
    Italy                        17
    Russia                       17
    Name: count, dtype: int64
    

# Nobel Ödüllerini kazanan ilk kadınları listeleyiniz.


```python
import pandas as pd


women = nobel[nobel["sex"] == "Female"]


for award in nobel["category"].unique():
    first_woman = women[women["category"] == award].iloc[0]
    print(f"{award}: {first_woman['year']} - {first_woman['full_name']}")


```

    Chemistry: 1911 - Marie Curie, née Sklodowska
    Literature: 1909 - Selma Ottilia Lovisa Lagerlöf
    Medicine: 1947 - Gerty Theresa Cori, née Radnitz
    Peace: 1905 - Baroness Bertha Sophie Felicita von Suttner, née Countess Kinsky von Chinic und Tettau
    Physics: 1903 - Marie Curie, née Sklodowska
    Economics: 2009 - Elinor Ostrom
    

# Nobel Ödüllerini kazanan ilk erkekleri listeleyiniz.


```python

men = nobel[nobel["sex"] == "Male"]


for award in nobel["category"].unique():
    first_men = men[men["category"] == award].iloc[0]
    print(f"{award}: {first_men['year']} - {first_men['full_name']}")

```

    Chemistry: 1901 - Jacobus Henricus van 't Hoff
    Literature: 1901 - Sully Prudhomme
    Medicine: 1901 - Emil Adolf von Behring
    Peace: 1901 - Jean Henry Dunant
    Physics: 1901 - Wilhelm Conrad Röntgen
    Economics: 1969 - Ragnar Frisch
    

# Nobel ödülünü en çok kazanan ülkenin hangi yıldan itibaren hakimiyet sağladığını görselleştirip bu hakimiyette rol oynayan şeyler nelerdir? İçgörülerinizi paylaşır mısınız?


```python

us_data = nobel[nobel['birth_country'] == 'United States of America']
year_counts = us_data['year'].value_counts().sort_index()


plt.figure(figsize=(12, 6))
plt.plot(year_counts.index, year_counts.values, marker='o')
plt.xlabel('Yıl')
plt.ylabel('Ödül Sayısı')
plt.title('Nobel Ödülü - Amerika Birleşik Devletleri\'nin Yıllara Göre Dağılımı')
plt.xticks(rotation=45)
plt.show()

```


    
![png](output_12_0.png)
    

# Amerikanın ilk sıçarıyışın 2. Dünya Savaşı yıllarında olduğunu görüyoruz. Bu yıllarda Amerikanın özellikle Almanya
'dan göç aldığı biliniyor. Almanya, İtalya gibi faşizim ile yönetilen ülkelerden aldığı göç ve işgal altındaki Avrupa ülkerinden aldığı beyin göçü bu sıçramanın önemli sebebleriden biri olabilir.Ayrıca yine 1 dünya savaşı sırasında savaş kıtasından uzakta oldukları için aldıkalrı beyin göçünün meymesini yemiş olabililer. 1970'lı yıllardan sonrada Amerika'nın ödül sayılarında yine yükselme görüyoruz. Bunun sebebleri sahip oldukları geniş ar-ge , yüksek finans gücü, bağımsız akedemik çalışma ortamları olabilir. Dünyanın en iyi en iyi ünüversiteleri Amerika'da  ve en en iyi imkanları yine burada. Tüm bunları yükselenen kapitalzm ve Amerikan'ın dünyanın en yerindeki ve kurumundaki hakimiyeti ile birleştirince  Amerika'nın ödüllerideki yükselişine yorumlayabiliriz. 
# Nobel Ödülü kazananların cinsiyetlerini, yaşlarını, ödül kategorisi ve yılları kullanarak görselleştiriniz.(Her bir ödül kategorisi için ayrı grafik gösteriniz) Çıkan sonuçlara göre görseli yorumlayınız.


```python

physics_data = nobel[nobel['category'] == 'Physics'].copy()

physics_data['birth_date'] = pd.to_datetime(physics_data['birth_date'], format='%Y-%m-%d', errors='coerce').dt.year
physics_data['Age'] = physics_data['year'] - physics_data['birth_date']

gender_counts = physics_data['sex'].value_counts()


age_counts = physics_data['Age'].value_counts().sort_index()

year_counts = physics_data['year'].value_counts().sort_index()


plt.figure(figsize=(6, 6))
plt.pie(gender_counts, labels=gender_counts.index, autopct='%1.1f%%')
plt.title('Fizik Cinsiyet Dağılımı')
plt.show()

plt.figure(figsize=(8, 4))
plt.hist(physics_data['Age'], bins=20, edgecolor='black')
plt.xlabel('Yaş')
plt.ylabel('Kazanan Sayısı')
plt.title('Fizik: Kazananların Yaş Dağılımı')
plt.show()


plt.figure(figsize=(8, 4))
plt.plot(year_counts.index, year_counts.values, marker='o')
plt.xlabel('Yıl')
plt.ylabel('Ödül Sayısı')
plt.title('Fizik Yıllara Göre Dağılım')
plt.xticks(rotation=45)
plt.show()
```


    
![png](output_15_0.png)
    



    
![png](output_15_1.png)
    



    
![png](output_15_2.png)
    



```python

chemistry_data = nobel[nobel['category'] == 'Chemistry'].copy()


chemistry_data['birth_date'] = pd.to_datetime(chemistry_data['birth_date'], format='%Y-%m-%d', errors='coerce').dt.year
chemistry_data['Age'] = chemistry_data['year'] - chemistry_data['birth_date']


gender_counts = chemistry_data['sex'].value_counts()


age_counts = chemistry_data['Age'].value_counts().sort_index()


year_counts = chemistry_data['year'].value_counts().sort_index()

plt.figure(figsize=(6, 6))
plt.pie(gender_counts, labels=gender_counts.index, autopct='%1.1f%%')
plt.title('Kimya: Cinsiyet Dağılımı')
plt.show()


plt.figure(figsize=(8, 4))
plt.hist(chemistry_data['Age'], bins=20, edgecolor='black')
plt.xlabel('Yaş')
plt.ylabel('Kazanan Sayısı')
plt.title('Kimya: Kazananların Yaş Dağılımı')
plt.show()


plt.figure(figsize=(8, 4))
plt.plot(year_counts.index, year_counts.values, marker='o')
plt.xlabel('Yıl')
plt.ylabel('Ödül Sayısı')
plt.title('Kimya: Yıllara Göre Dağılım')
plt.xticks(rotation=45)
plt.show()
```


    
![png](output_16_0.png)
    



    
![png](output_16_1.png)
    



    
![png](output_16_2.png)
    



```python

literature_data = nobel[nobel['category'] == 'Literature'].copy()


literature_data['birth_date'] = pd.to_datetime(literature_data['birth_date'], format='%Y-%m-%d', errors='coerce').dt.year
literature_data['Age'] = literature_data['year'] - literature_data['birth_date']


gender_counts = literature_data['sex'].value_counts()


age_counts = literature_data['Age'].value_counts().sort_index()


year_counts = literature_data['year'].value_counts().sort_index()


plt.figure(figsize=(6, 6))
plt.pie(gender_counts, labels=gender_counts.index, autopct='%1.1f%%')
plt.title('Edebiyat Cinsiyet Dağılımı')
plt.show()


plt.figure(figsize=(8, 4))
plt.hist(literature_data['Age'], bins=20, edgecolor='black')
plt.xlabel('Yaş')
plt.ylabel('Kazanan Sayısı')
plt.title('Edebiyat: Kazananların Yaş Dağılımı')
plt.show()

plt.figure(figsize=(8, 4))
plt.plot(year_counts.index, year_counts.values, marker='o')
plt.xlabel('Yıl')
plt.ylabel('Ödül Sayısı')
plt.title('Edebiyat Yıllara Göre Dağılım')
plt.xticks(rotation=45)
plt.show()
```


    
![png](output_17_0.png)
    



    
![png](output_17_1.png)
    



    
![png](output_17_2.png)
    



```python

peace_data = nobel[nobel['category'] == 'Peace'].copy()


peace_data['birth_date'] = pd.to_datetime(peace_data['birth_date'], format='%Y-%m-%d', errors='coerce').dt.year
peace_data['Age'] = peace_data['year'] - peace_data['birth_date']


gender_counts = peace_data['sex'].value_counts()


age_counts = peace_data['Age'].value_counts().sort_index()


year_counts = peace_data['year'].value_counts().sort_index()

plt.figure(figsize=(6, 6))
plt.pie(gender_counts, labels=gender_counts.index, autopct='%1.1f%%')
plt.title('Barış: Cinsiyet Dağılımı')
plt.show()


plt.figure(figsize=(8, 4))
plt.hist(peace_data['Age'], bins=20, edgecolor='black')
plt.xlabel('Yaş')
plt.ylabel('Kazanan Sayısı')
plt.title('Barış: Kazananların Yaş Dağılımı')
plt.show()

plt.figure(figsize=(8, 4))
plt.plot(year_counts.index, year_counts.values, marker='o')
plt.xlabel('Yıl')
plt.ylabel('Ödül Sayısı')
plt.title('Barış: Yıllara Göre Dağılım')
plt.xticks(rotation=45)
plt.show()
```


    
![png](output_18_0.png)
    



    
![png](output_18_1.png)
    



    
![png](output_18_2.png)
    



```python

medicine_data = nobel[nobel['category'] == 'Medicine'].copy()


medicine_data['birth_date'] = pd.to_datetime(medicine_data['birth_date'], format='%Y-%m-%d', errors='coerce').dt.year
medicine_data['Age'] = medicine_data['year'] - medicine_data['birth_date']


gender_counts = medicine_data['sex'].value_counts()

age_counts = medicine_data['Age'].value_counts().sort_index()


year_counts = medicine_data['year'].value_counts().sort_index()


plt.figure(figsize=(6, 6))
plt.pie(gender_counts, labels=gender_counts.index, autopct='%1.1f%%')
plt.title('Tıp Cinsiyet Dağılımı')
plt.show()


plt.figure(figsize=(8, 4))
plt.hist(medicine_data['Age'], bins=20, edgecolor='black')
plt.xlabel('Yaş')
plt.ylabel('Kazanan Sayısı')
plt.title('Tıp: Kazananların Yaş Dağılımı')
plt.show()

plt.figure(figsize=(8, 4))
plt.plot(year_counts.index, year_counts.values, marker='o')
plt.xlabel('Yıl')
plt.ylabel('Ödül Sayısı')
plt.title('Tıp: Yıllara Göre Dağılım')
plt.xticks(rotation=45)
plt.show()
```


    
![png](output_19_0.png)
    



    
![png](output_19_1.png)
    



    
![png](output_19_2.png)
    



```python

economics_data = nobel[nobel['category'] == 'Economics'].copy()


economics_data['birth_date'] = pd.to_datetime(economics_data['birth_date'], format='%Y-%m-%d', errors='coerce').dt.year
economics_data['Age'] = economics_data['year'] - economics_data['birth_date']


gender_counts = economics_data['sex'].value_counts()

age_counts = economics_data['Age'].value_counts().sort_index()


year_counts = economics_data['year'].value_counts().sort_index()

plt.figure(figsize=(6, 6))
plt.pie(gender_counts, labels=gender_counts.index, autopct='%1.1f%%')
plt.title(' Ekonomi: Cinsiyet Dağılımı')
plt.show()


plt.figure(figsize=(8, 4))
plt.hist(economics_data['Age'], bins=20, edgecolor='black')
plt.xlabel('Yaş')
plt.ylabel('Kazanan Sayısı')
plt.title(' Ekonomi: Kazananların Yaş Dağılımı')
plt.show()

plt.figure(figsize=(8, 4))
plt.plot(year_counts.index, year_counts.values, marker='o')
plt.xlabel('Yıl')
plt.ylabel('Ödül Sayısı')
plt.title('Ekonomi: Yıllara Göre Dağılım')
plt.xticks(rotation=45)
plt.show()
```


    
![png](output_20_0.png)
    



    
![png](output_20_1.png)
    



    
![png](output_20_2.png)
    

# Yorum:Ödüllerin dağılımına genel olarak baktığımız zaman ciddi bir cinsiyet eşitisizliğini görmek mümkün. Nobel ödülerinde erkek egemen kültürünün olduğunu rahatlıkla  söyleyebilriz. Tabi bunun sebebi sadece nobel değil akedemilerdeki erkek hakimiyeti olabilir. 
Kategorilere tek tek bakacak olursak ise Fizik kategorisinde ödülü kazanaların daha genç isimler olduğunu gözlemliyoruz. Ödül sayısında ki ilk yükselişler 1920'lerde ve 1960'larda  nu yıllarda dünyada önemli buluşlar oldu hatta önemli bombalar yapıldı. Bu yükselişin sebepleri bunlar olabilir.

#Kimya  kategorsine geldiğimizde ise ödül kazanma yaş aralığını Fizik'e göre biraz yükseldiğini gözlemliyoruz. Yinede genç insanlara veriliyor ikinci dünya savaşı ve soğuk savaş döneminde verilen ödül sayısının yükseldiğini görüyoruz. Bu tıpkı Fizikteki gibi savaşın ve soğuk savaşın ittiği yarıştan ötürü olabilir.

#Edebiyat kategorsinde ise cinsiyet eşitisizliği her ne kadar devam etsede kadınların oranında bir artış söz konusu. Yaş olarak ise Edebiyatın  55- 75  yaş aralığında yogunlaştığını görüyoruz. Ayrıca 1900 - 1920 'li yıllarda ödül sayısı daha yüksek bunun sebebi bu dönemlerde yazılan  Dünya Eserleri olabilir. 60'larda ve 80'lerde ödül sayısının artmasının sebebi globeleşen dünya ile birlikte sanata olan ilginin artması olabilir.
# Barış Kategorisinde erkek hegomanyasının sebebi direk olarak dünya siyasetindeki erkek hegomanyası ile bağlantılı olduğunu söyleyebiliriz. Bu kategoride ödüllerin yaşlılara gittiğini gözlemliyoruz. Bunun nedeni barış getirecek diplomatik birikime sahip olmanın deneyim gerektiren bir şey olmasıdır. Barış ödülelerinin ortlama dağılımıa baktığımız zaman 2'dir. Birinci dünya savaşı, ikinci dünya savaşı, soğuk savaş bunda etkildir. 90' yıllarda ki artışının savaşı ise ortadoğu'da çıkan savaşlar olabilir.
# Tıp alanında ödüllerin ağırklı olarak gençlere gittiğini görüyoruz. Ama yaşlıların da geri kaldığını söylenemez. Tıp ödülün daha sık verildiğini söylemek mümkün sürekli gelişen bir alan. 1900- 1910 yıllarda ki ödül sayısının fazla olmasının sebebi modern anlamdaki adımlar olabilir. 1945 - 55 yıllarda ise yine yaşanan önemli gelişmler, yapılan deneyler vb. ödül saysunı tetiklemiş olabilir
# Ekonomi alanında ise kadın dağılımı Fizik'ten sonraki en kötü alan. Yaş dağılımına baktığımız zaman daha orta yaşlı ve yaşlı insanlaar verildiğini söylemek mümkün. 1970'lı ve 80'lı yıllarda ödülün daha sık verilme sebebi bu yıllardaki ekenomik gelişmeler kapitlzm yükselişi olabilir. 2000'ler sonrası artış ise ekonomik krizler ve yeni programlar olabilir.

# 1938-1945 yılı arasında Nobel Ödülü kazananların kategorilerini ve ülkelerini görselleştirip yorumlayınız


```python


filtered_nobel = nobel[(nobel['year'] >= 1938) & (nobel['year'] <= 1945)]


plt.figure(figsize=(12, 6))
filtered_nobel['category'].value_counts().plot.pie(autopct='%1.1f%%')
plt.title('1938-1945 Yılları Arasında Nobel Ödülü Kazananların Kategorileri')
plt.ylabel('')
plt.show()


country_counts = filtered_nobel['birth_country'].value_counts()


plt.figure(figsize=(12, 6))
plt.bar(country_counts.index, country_counts.values)
plt.xlabel('Ülke')
plt.ylabel('Kazanan Sayısı')
plt.title('1938-1945 yılları arasında Nobel Ödülü Kazananların Ülkeleri')
plt.xticks(rotation=90)
plt.show()

```


    
![png](output_23_0.png)
    



    
![png](output_23_1.png)
    

Bu yıllarda ödülün 5 kategoride verildiğini görüyoruz. ikinci dünya savaşı yıllarına denk gelen bu yıllarda ödülün kimya, fizi ve tıp ağırlklı gitmesi  savaşı hızlandıracak olan bilimsel çalışmalardan ötürü olabilir Örneğin atom bombası,nükleer enerji çalışmaları gibi. Ödülelerin Amerika ve Almanya'da yogunlaşmasının sebebi dönemin siyasi olayları olabilir. Bu iki ülke her türlü alanda bu yıllarda atılım yaptı ve ööncü oldukları konular oldu. Ayrıca faşizim ile yönetilen dönemin Alamanya'sından kaçan bilim adamların bir kısmı Amerika'ya ödül getirmiştir.

# 1947-1991 yılları arasında Nobel Ödülü kazananların kategorilerini ve ülkelerini görselleştirip yorumlayınız.(Her kategori için ayrı bir grafik olması istenmektedir)


```python

category_counts = nobel[(nobel['year'] >= 1947) & (nobel['year'] <= 1991)]['category'].value_counts()


for category in category_counts.index:
    category_data = nobel[(nobel['year'] >= 1947) & (nobel['year'] <= 1991) & (nobel['category'] == category)]
    country_counts = category_data['birth_country'].value_counts()
    
    plt.figure(figsize=(8, 4))
    plt.bar(country_counts.index, country_counts.values)
    plt.xlabel('Ülke')
    plt.ylabel('Kazanan Sayısı')
    plt.title(f'1947-1991 yılları arasında Nobel Ödülü Kazananların Ülkeleri - {category} Kategorisi')
    plt.xticks(rotation=90)
    plt.show()
```


    
![png](output_26_0.png)
    



    
![png](output_26_1.png)
    



    
![png](output_26_2.png)
    



    
![png](output_26_3.png)
    



    
![png](output_26_4.png)
    



    
![png](output_26_5.png)
    

Yorum: Amerika'nın her kategoride üstünlük kurduğunu gözlemliyoruz. En çok ödül verilen kategorilerin fizik ve kimya kategorileridir. Bunun sebebi bu yıllardaki savaş odaklı buluşlar ve soğuk savaş zamanında ki üstüblik kurma çabaları olabilir. Amerika'yı , İngiltere ve Almaanya takip etmektedir. Amerika'nın ekonmik kategorisnde kurduğu üstünlük getirdiği dünya düzeninin bir göstergesidir.  Barış kategorisine baktığımız zaman ise Novreç ve İsveç gibi ülkeler  göze çarpıyor. Bu ülkeler gerek dünya'nın parasını bankalarında bulundurma gerekse yaptıkları  ev sahiplikleri ile barişa katkı sağlamış olabilir. Edebiyat kategorisinde diğer kategorilere göre daha yarışçıl ve düzenli bir dağılım var. Edebiyat kategorisinin dünya siyasetinden daha bağımsız şekilde ödül aldığı söylenebilir.
# Kimya, Edebiyat, Barış, Fizik ve Tıp kategorilerindeki 2000 sonrasındaki kişilerin ülkelerini, yaşlarını görselleştirin.(Her bir Kategori için ayrı görselleştirme yapılması istenmektedir) Veriyi yorumlayınız.



```python


selected_categories = ['Medicine', 'Literature', 'Peace', 'Physics', 'Chemistry']
selected_data = nobel[(nobel['category'].isin(selected_categories)) & (nobel['year'] > 2000)].copy()


selected_data['birth_date'] = pd.to_datetime(selected_data['birth_date'], format='%Y-%m-%d', errors='coerce').dt.year
selected_data['Age'] = selected_data['year'] - selected_data['birth_date']

for category in selected_categories:
    category_data = selected_data[selected_data['category'] == category]


    plt.figure(figsize=(8, 4))
    country_counts = category_data['birth_country'].value_counts().head(10).astype(int)  
    country_counts.plot(kind='bar', color='skyblue')
    plt.xlabel('Ülkeler')
    plt.ylabel('Kazanan Sayısı')
    plt.title(f'{category} Kategorisinde Nobel Kazananların Ülkeleri (2000 Sonrası)')
    plt.xticks(rotation=45)
    plt.yticks(range(country_counts.max() + 1))  
    plt.show()

    plt.figure(figsize=(8, 4))
    plt.hist(category_data['Age'], bins=20, edgecolor='black', color='lightgreen')
    plt.xlabel('Yaş')
    plt.ylabel('Kazanan Sayısı')
    plt.title(f'{category} Kategorisinde Nobel Kazananların Yaş Dağılımı (2000 Sonrası)')
    plt.yticks(range(category_data['Age'].value_counts().max() + 1))  

```


    
![png](output_29_0.png)
    



    
![png](output_29_1.png)
    



    
![png](output_29_2.png)
    



    
![png](output_29_3.png)
    



    
![png](output_29_4.png)
    



    
![png](output_29_5.png)
    



    
![png](output_29_6.png)
    



    
![png](output_29_7.png)
    



    
![png](output_29_8.png)
    



    
![png](output_29_9.png)
    

Yorum:Genel olarak baktığımız zaman ödüller finasman ve akedemi alanlarında güçlü olan ülkelere gidiyor. Genel olarak akademik olarak genç diyebileceğimiz 55 - 65 aralığında dağıldığını görüyoruz. Bununla birlilte daha uzun soluklu çalışmalar yaptığını söylenebilecek yaşlı bilim adamlarda ödüllerde yine etkili.

Tıp kategorsine baktığımız zaman. Amerika ve İngiltere başı çekiyor. Dünyanın en güçlü akedemileri ve finasman gücünün karşığını alıyorlar. Tıp alanında alınan ödüllerin yaş dağılımı daha düzenli gözüküyor. Gerek daha kısa soluklu gerek daha uzun soluklu araştırmalara  ödül gitmiş oalbilir.

Edebiyat alanında ise ödüllerin ülkere daha düzenli dağıldığını söyleyebilriz.Yaş aralığında ise 65'ten sonra sıklaştığını söylemek mümkün.

Barış alanına baktığımız zaman genel olarak ödül Amerika'ya gitmiştir ve daha deneyimli siyasetçiler ve politikacılara gittiğini söylemek mümkün.

Fizik kategorisinde ise ödül yibe refah seviyesi yüksek ülkere gidiyor ve ödülük kzanların yaş ortalamasının 55 - 60 olduğunu söylenebilir. Kimya alanına yine araştırmaların daha genç insanlar taafından yapıldığını söylemek mümkün ve gelişmiş ülkeler yine ağırlığını koyuyor. Özellike Amerika üstümlüğü göze çarpıyor.

```python

```
