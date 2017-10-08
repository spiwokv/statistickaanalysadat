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

Sloupce lze vybrat i pomocí názvu sloupce:
```R
prijmy$plat
```

Pak vyzkoušejte funkci `sort`:
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

Pokud chce uživatel seřadit celý dataframe podle jednoho sloupce, může to udělat takhle:
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

Nyní vše vyzkoušíme na výsledcích voleb do parlamentu 2013 v Praze:

```R
ifile <- read.table("https://raw.githubusercontent.com/spiwokv/statistickaanalysadat/master/lookingatdata/volby2013praha.txt",
                    sep=";", header=T, dec=",")
```

Je možné si vytisknout celý obsah napsáním `ifile`, ale protože se jedná o velký soubor,
je lepší použít funkce `head` nebo `tail`:

```R
head(ifile)
tail(ifile)
```
Seznam sloupečků získáte funkcí `names`:

```R
names(ifile)
```
Počty řádků a sloupců můžeme získat funkcemi `nrow`, `ncol` a `dim`:
```R
nrow(ifile)
ncol(ifile)
dim(ifile)
```
Nyní zkuste najít nejstaršího a nejmladšího kandidáta (věk je uložen jako `vek`).

Kromě řazení podle počtu hlasů je možné vybrat řádky, pro které platí nějaká podmínka, například abychom nalezli
kandidáty mladší třiceti let, použijeme příkaz:
```R
ifile[ifile[,5]<30,]
```
kde výraz `ifile[,5]` představuje věk kandidátů (pátý slopeček), `ifile[,5]<30` vrátí logický vektor s hodnotami `TRUE`
pro kandidáty mladší než 30 let a `FALSE` pro ostatní. Pozor na použití u sloupečků se zápornými hodnotami! Použijte
`< -` a ne `<-`, což je klasická šipka.

Byl mezi kandidáty nějaký, který nedostal ani jeden hlas (počet hlasů je v sloupečku `abs`)?

Byl mezi kandidáty nějaký, který nedostal jen jeden hlas?

Kolik kandidátů dostalo 0-10 hlasů?

Pokud bychom chtěli vypsat strany, můžeme použí:

```R
ifile[,2]
```
nebo
```R
ifile$strana
```
Pokud ale chceme každou stranu jen jednou, pak můžeme použít funkci `levels`:
```R
levels(ifile[,2])
```
Celkový počet stran získáme buď jako délku vektoru nebo funkcí `nlevels`:
```R
nlevels(ifile[,2])
```
Pokud chcete vědět počty kandidátů pro každou stranu můžete použít funkci `table`:
```R
table(ifile[,2])
```
Udělejte histogram věků pro všechny kadidáty.

Udělejte histogram věků pro kadidáty Pirátů.

Pokud chcete vizualizovat věk pro jednotlivé strany, je možné použít zápis:
```R
plot(vek~strana, data=volby)
```
Zápis `vek~strana` vyjadřuje, že zkoumáme jak závisí věk na přislušnosti ke straně. Tento zápis budeme používat často.

Když bychom chtěli spočítat hlasy pro celé strany, můžeme použít funkci `agregate`:
```R
aggregate(abs~strana, data=volby, FUN=sum)
```
Výsledek zobrazte funkcí `pie`, `plot`, nebo `barplot`.

Pokud Vám nefungují funkce `pie` a `barplot`, je to proto, že potřebují jako vstup pouze čísla (druhý sloupeček).
Názvy stran můžete dodat argumentem `names.arg` pro `barplot` nebo `labels` pro `pie`.

Jaký je průměrný věk kandidátů (funkce `mean`) jednotlivých stran? Zkuste to funkcí `aggregate` a výsledek
zobrazte jako `barplot`. Zkuste to ještě jednou, ale před tím seřaďte strany podle průměrného věku.



