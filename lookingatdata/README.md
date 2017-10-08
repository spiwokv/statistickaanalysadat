Udělejte dataframe:

```R
clovek<-c("honza","pepa","rene","klara","lucka")
plat<-c(10000,20000,25000,30000,15000)
prijmy<-data.frame(clovek,plat)
prijmy
```

vyberte řádek
```R
prijmy[1,]
```
nebo sloupec
```R
prijmy[,1]
```
nebo jednu buňku
```R
prijmy[1,1]
```
nebo použijte operátor dvojtečka pro výběr
```R
prijmy[1:3,1]
```

Pak bych ukázal funkci sort
```R
sort(clovek)
```
(jména podle abecedy)
```R
sort(plat)
```
(hodnoty podle hodnot)
```R
sort(clovek, decreasing=T)
sort(plat, decreasing=T)
```

Pokud chce uživatel seřadit celý data frame podle jednoho sloupce, může to udělat takhle:
když by chtěl vytisknou nejdřiv třeba třetí, pak pátý a pak první řádek tabulky, udělal by to
takhle:
```R
prijmy[c(3,5,1),]
```
(je to v `c()` aby to byl vektor a je to před čárkou, aby se to týkalo řádků, nikoliv sloupců).
Podobně si může pomocí funkce order vypsat pořadí pro sloupec, podle kterého chce seřadit tabulku
```R
order(plat)
order(plat, decreasing=T)
```
a ten pak použít podobným způsobem:
```R
prijmy[order(plat),]
prijmy[order(plat, decreasing=T),]
```
nebo kdyby mezi tím zapomeneme vektor plat, tak můžeme vzít sloupeček z dataframu prijmy:
```R
prijmy[order(prijmy[,2], decreasing=T),]
prijmy[order(prijmy[,2]),]
```

