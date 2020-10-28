---
categories:
- Surse
date: "2020-07-24"
authors: 
- admin
description: În prezent internetul deține o cantitate din ce în ce mai mare de date. Agregarea lor necesită timp și responsabilitate, iar utilizarea acestora poate fi din ce în ce mai eficientă dacă știm de unde și cum să le preluăm. Vă voi prezenta 10 surse de date oficiale care pot fi importante cu ajutorul limbajului R, astfel evitând descărcarea, pierderea și prelucrarea ineficientă a datelor.
summary: În prezent internetul deține o cantitate din ce în ce mai mare de date. Agregarea lor necesită timp și responsabilitate, iar utilizarea acestora poate fi din ce în ce mai eficientă dacă știm de unde și cum să le preluăm. Vă voi prezenta 10 surse de date oficiale care pot fi importante cu ajutorul limbajului R, astfel evitând descărcarea, pierderea și prelucrarea ineficientă a datelor.
image:
  caption: "Imagine: [Open Data - Toronto](https://twitter.com/Open_TO/photo)"
  focal_point: "Center"
  placement: 1
  preview_only: false
tags:
- Pachete R
- Date oficiale
- Date deschise
title: 10 surse de date pentru prelucrarea datelor în limbajul de programare R
---


{{%toc%}}

Următorul articol prezintă 10 surse de date deschise care pot fi utilizate împreună cu limbajul de programare R. Datele pot fi apelate direct în R, fără a mai fi nevoie de o descărcare anterioară.
### Eurostat

[Eurostat](https://ec.europa.eu/eurostat/home?) este o entitate publică care adună, gestionează și prelucrează toate datele statistice raportate de către țările membre Uniunii Europene către Comisia Europeană.

Eurostat prezintă o bază de date publică, internațională care poate fi accesată prin siteul propriu Eurostat - Database. 

Secretul acestei baze de date este acela că întreaga arhitectură are la bază un [API](https://ro.wikipedia.org/wiki/Application_Programming_Interface) (application interface), prin urmare toate informațiile pot fi accesate prin intermediul protocoalelor de transfer sau pe scurt, adresa http pe care o vedeți în bara de adrese a Google.

Pentru accesarea datelor într-un format cât mai simplu, a fost dezvoltat un pachet R care permite preluarea datelor foarte simplu și eficient printr-o serie de funcții. Pachetul se numește [eurostat](https://cran.r-project.org/web/packages/eurostat/index.html), și este disponibil în [CRAN](https://cran.r-project.org/).

``` R
# instalăm pachetul eurostat prin funcția install.packages()
install.packages("eurostat")
# apelăm pachetul
library(eurostat)
test<-get_eurostat("sdg_01_10")
# unde sdg_01_10 este codul setului de date conform bazei de date
# vizualizăm primele rânduri din setul de date (funcția head())
head(test)
```

### Institutul Național de Statistică

[Institutul Național de Statistică](https://insse.ro/cms/) din România colectează, prelucrează și stochează date care privesc o arie largă de subiecte.

Toate aceste date au fost inițial prelucrate și prezentate în mediul online prin intermediul platformei [TEMPO](http://statistici.insse.ro:8077/tempo-online/). Această platformă permite vizualizarea seturilor de date și salvarea acestora în diverse formate, fie ele .csv sau .xlsx. 

De curând, platforma a fost refăcută în special din punct de vedere estetic. La fel ca baza de date Eurostat, și cea a INS are în spate un API. Acest API a dus la crearea ulterioară în 2017 și în 2019 a pachetelor rTEMPO, respectiv [TEMPO](https://github.com/RProjectRomania/TEMPO).

Pachetul TEMPO permite apelarea seturilor de date din baza de date INS și stocarea acestora în consola R. O astfel de acțiune permite sărirea pașilor privind căutarea setului de date în platforma online, filtrarea datelor, descărcarea acestora, salvarea și ulterior procesarea acestora.

Pachetul TEMPO este disponibil pe CRAN și poate fi descărcat desigur în mod gratuit. 

``` R
# instalăm pachetul TEMPO prin funcția install.packages()
install.packages("TEMPO")
# apelăm pachetul
library(TEMPO)
# salvăm un set de date local pentru a fi utilizat direct prin funcția read.csv()
tempo_bulk("CDP102D")
# citim setul de date pentru a putea fi prelucrat
test<-read.csv("CDP102D.csv")
# vizualizăm primele rânduri
head(test)
```

### Banca Mondială

[Banca Mondială](https://databank.worldbank.org/Databases.aspx) gestionează și actualizează lunar, trimestrial și anual o serie largă de indicatori socio-economici la nivel internațional. 

Aceasta dispune de o bază de date comprehensibilă, densă și stufoasă. Accesarea ei se realizează în mod direct prin accesarea paginii web. În momentul accesării, utilizatorul poate descărca setul de date pentru prelucrare proprie sau îl poate vizualiza direct pe site.

Având în vedere că analiza de date, prin prelucrarea informațiilor și supunerea acestora mai multor teste statistice (sau altele) necesită un mediu de lucru unic, eficient și ușor de manipulat, accesarea acestor baze de date prin pachete dedicate eficientizează întregul proces.

[Pachetul R wbstats](https://cran.r-project.org/web/packages/wbstats/vignettes/Using_the_wbstats_package.html) vine în ajutorul utilizatorilor limbajului de programare R și a datelor deschise, pentru a stabili o conexiune directă între seturile de date și mediul de lucru.

Pachetul R wbstats este dezvoltat de Jesse Piburn și este pus la dispoziția utilizatorilor atât prin GitHub, cât și prin CRAN.

``` R
# instalăm pachetul wbstats prin funcția install.packages()
install.packages("wbstats")
# apelăm pachetul
library(wbstats)
# căutăm seturile de date care conțin cuvântul cheie population
search_index<-wbsearch(pattern="population")
# vizualizăm primele rânduri din rezultatul căutării
head(search_index)
# preluăm un set de date pentru România
test<-wb(country="RO",indicator="SI.DST.02ND.20")
# vizualizăm primele rânduri
head(test)
```

### DBNomics

[DB Nomics - the world's economic database](https://db.nomics.world/) este un portal online care permite accesul liber la seturi de date din surse distincte, atât oficiale, cât și neoficiale. 

Pe platformă pot fi accesate, vizualizate și descărcate seturi de date cu un caracter economic în majoritatea situațiilor, însă, pot fi utilizate și alte seturi de date care nu au neapărat o latură economică. 

Platforma gestionează date din surse precum, BIS - Bank for International Settlements, ECB - European Central Bank, Eurostat, ILO - International Labour Organization, OECD - Organisation for Economic Co-operation and Development, IMF - International Monetary Fund ș.a.

[Pachetul rdbnomics](https://cran.r-project.org/web/packages/rdbnomics/index.html) a fost dezvoltat de [Sebastien Galais](https://github.com/s915) și este disponibil atât pe GitHub, cât și pe CRAN.

``` R
# instalăm pachetul rdbnomics prin funcția install.packages()
install.packages("rdbnomics")
```
Pentru a descărca diferite seturi de date acestea ori pot fi căutate online pe site și descărcate individual sau în paralel cu un alt set de date pentru comparare, ori pot fi descărcate prin link-ul API aferent fiecărui set de date care poate fi găsit pe site.

``` R
# apelăm pachetul
library(rdbnomics)
# vom prelua un set de date pentru cod furnizor AMECO, cod dataset - ZUTN, cod serie - EA19.1.0.0.0.ZUTN
test<-rdb(ids="AMECO/ZUTN/EA19.1.0.0.0.ZUTN")
# vizualizăm primele rânduri
head(test)
# preluăm un set de date prin link-ul API
test <- rdb(api_link = "https://api.db.nomics.world/v22/series/WB/DB?dimensions=%7B%22country%22%3A%5B%22FR%22%2C%22IT%22%2C%22ES%22%5D%7D&q=IC.REG.PROC.FE.NO&observations=1&format=json&align_periods=1&offset=0&facets=0")
# vizualizăm primele rânduri
head(test)
```


### Organizația Mondială a Sănătății

[Organizația Mondială a Sănătății](https://www.who.int/) deține seturi de date privind sanătatea la nivel internațional pentru fiecare țară în parte, cel puțin acolo unde acestea există.

Pachetul WHO a fost dezvoltat de Eric (GitHub: [expersso](https://github.com/expersso)) și este disponibil pe GitHub.

Pentru a utiliza [pachetul WHO](https://github.com/expersso/WHO) este nevoie de preluarea acestuia de pe GitHub deoarece nu mai este vizibil în CRAN. Pentru acest pachet este nevoie de funcția install_github() din pachetul devtools, care ne permite să preluăm un pachet R direct dintr-un repositoriu GitGub.

``` R
# instalăm pachetul devtools
install.packages("devtools")
# apelăm pachetul
library(devtools)
# instalăm pachetul prin install_github()
install_github("expersso/WHO")
# apelăm librăria WHO
library(WHO)
# preluăm toate codurile din baza de date și seturile de date aferente
search_index<-get_codes()
# având codurile, preluăm datele pentru un set de date în funcție de cod
test<-get_data("MDG_0000000006")
# vizualizăm primele rânduri
head(test)
```

### OECD

[OECD - Organisation for Economic Co-operation and Development](https://www.oecd.org/) deține seturi de date socio-economice și nu numai la nivelul țărilor membre. Aceste seturi de date pot fi accesate prin pachetul R OECD și prelucrate în consola R.

Pentru [pachetul OECD](https://github.com/expersso/OECD) lucrurile sunt un pic mai dichisite dar nu foarte complitate. După ce căutăm setul de date, trebuie creat un filtru pentru a putea prelua datele ulterior în funcție de filtru.

``` R
# instalăm pachetul OECD
install.packages("OECD")
# apelăm pachetul
library(OECD)
# căutăm și salvăm seturile de date din OECD
search_index<-get_datasets()
# preluăm structura unui set de date, acesta va fi salvat într-o listă care la rândul ei deține mai multe variabile.
dataset_structure<-get_data_structure("DUR_D")
# vizualizăm primele rânduri
head(dataset_structure)
# salvăm un filtru
filter_values<-list(c("DEU", "FRA"), "MW", "2024")
# preluăm datele prin setul de date DUR_D și aplicăm filtrul de mai sus
test<-get_dataset(dataset = "DUR_D",filter=filter_values)
# vizualizăm primele rânduri
head(test)
```


### Gapminder

[Fundația Gapminder](https://www.gapminder.org/) este rezultatul fondatorului [Hans Rosling](https://en.wikipedia.org/wiki/Hans_Rosling) care a reușit să vizualizeze prin intermediul graficelor de tip bubble (bubble charts=scatter plots unde valorile punctelor sunt direct proporționale cu dimensiunea acestora ) PIB-ul pe cap de locuitor și speranța la viață pentru țările de pe mapamond.

[Gapminder](https://cran.r-project.org/web/packages/gapminder/index.html) este o librărie care ne permite să descărcăm seturile de date din celebra publicație pentru a fi utilizate în R. Acestea sunt stocate în mod direct ca un set de date. Printre variabile se numără țara, continentul, anul, speranța de viață, populația și PIB-ul pe cap de locuitor.

``` R
# instalăm pachetul gapminder
install.packages("gapminder")
# apelăm librăria
library(gapminder)
# filtrăm datele pentru România
gapminder[gapminder$country=="Romania",]
# vizualiză primele rânduri
head(gapminder)
```

### UNData

[UNdata](https://data.un.org/) reprezintă baza de date a Națiunilor Unite. Aceasta poate fi accesată prin intermediul platformei web sau a API-ului existent.

### Kaggle

[Kaggle](https://www.kaggle.com/) este unul dintre cele mai interesante și competitive centre de analiză a datelor la nivel internațional. Platforma dispune de seturi de date bine definite, standardizate și eficiente pentru a fi puse în practică în inteligență artificială și data science, precum și seturi de date noi care nu au fost încă prelucrate.

Analiști de date, dezvoltatori software, data scientists (încă nu știu care este traducerea în limba română a acestei profesii) din jurul lumii se strâng și analizează seturile de date, le vizualizează, le aranjează astfel încât să susțină modele de machine learning ș.a.

Puteți accesa toate seturile de date, le puteți analiza online direct pe platformă și puteți câștiga competiții, care la rândul lor sunt organizate periodic, având desigur și premii în bani($).

### Date guvernamentale România - data.gov.ro 

Platforma [data.gov.ro](http://data.gov.ro/) este desvoltată de guvernul României în urma recomandărilor Comisiei Europene cu privire la datele deschise ale țării. 

Puteți accesa seturi de date din toate instituțiile țării, în funcție de cum sunt acestea raportate (nu foarte eficient și în niciun caz sub formă agregată). 

Formatul seturilor de date diferă, unele sunt în .csv, altele în .xlsx, iar altele în .xml. Rămâne la latitudinea noastră de a reuși să scoatem ceva interesant din ele deoarece multe nu sunt standardizate și nici foarte ușor de prelucrat.

