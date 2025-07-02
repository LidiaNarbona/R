library(readr)
setwd("D:/miscosas/UMA/UC3M/1sem/Methods/Vanessa/R/1st project")
df<-read_delim("data_1stassignment.csv",
               locale = locale(decimal_mark = "."),
               delim = ";")

num_regions= table(df$Country)
num_countries= length(unique(df$Country))
total_regions = sum(num_regions)
orden_indices_regiones <- order(num_regions, decreasing = FALSE)
orden_regions= num_regions[orden_indices_regiones]
bp1=barplot(orden_regions,las=2,
        ylab= expression(bold("Number of regions")),
        col = "#FF6450",
        main = "Regions by country according to the NUTS 2 classification", ylim = c (0,40), axes =FALSE,cex.main=1.5, cex.lab = 1.2)
axis(2, at=c(0,5, 10, 15, 20, 25, 30, 35, 40), pos = 0)

text(bp1, orden_regions -0.4, labels = orden_regions, pos = 3, cex = 0.8, col = "black")

library(tidyverse)
library(dplyr)

filterdf = filter(df,Country == "Hungary" | Country == "Greece" | Country == "Italy")
filterdf = mutate_if(filterdf,
               is.character,
               as.factor)

droplevels(filterdf)

layout(matrix(1:2, nrow = 1))
layout(1)

boxplot(filterdf$UnemploymentRate~filterdf$Country, col=c("#FF9C4F", "#4FFFD9","#38A8FC"), main= "Unemployment rate",ylab = expression(bold("% in every region")), xlab="")
boxplot(filterdf$Poverty~filterdf$Country, col=c("#FF9C4F", "#4FFFD9","#38A8FC"), main= "Poverty rate",ylab = expression(bold("% in every region")), xlab="")

stripchart(filterdf$UnemploymentRate~filterdf$Country,method ="jitter", pch=15,col=c("#FF9C4F", "#4FFFD9","#38A8FC"), main= "Unemployment rate",xlab = expression(bold("% of unemployment per region")))
stripchart(filterdf$Poverty~filterdf$Country,method ="jitter", pch=15,col=c("#FF9C4F", "#4FFFD9","#38A8FC"), main= "Poverty rate",xlab = expression(bold("% of poverty per region")))

Hungary = filter(df,Country == "Hungary")
Greece = filter(df,Country == "Greece")
Italy = filter(df,Country == "Italy")

summary (Greece$Poverty)
summary (Hungary$Poverty)
summary (Italy$Poverty)

summary (Greece$UnemploymentRate)
summary (Hungary$UnemploymentRate)
summary (Italy$UnemploymentRate)

ItalyUnemployment=data.frame(Region = Italy$Region, UnemploymentRate = Italy$UnemploymentRate)
ItalyPoverty=data.frame(Region = Italy$Region, Poverty = Italy$Poverty)
print(ItalyUnemployment)
print(ItalyPoverty)

par(mar=c(6,5,5,4))

orden_indices <- order(Italy$UnemploymentRate, decreasing = FALSE)
orden_valores= Italy$UnemploymentRate[orden_indices]
ItalyPoverty_ordenados = Italy$Poverty[orden_indices]
bp=barplot(orden_valores, las=2, names.arg = c("Bozen", "Prov. Autonoma di Trento", "Valle d’Aosta", "Lombardia", "Veneto", "Friuli-Venezia Giulia", "Emilia-Romagna", "Marche", "Toscana", "Umbria", "Liguria", "Piemonte", "Lazio", "Basilicata", "Abruzzo", "Molise", "Sardegna", "Puglia", "Sicilia", "Calabria", "Campania"),
        col = "#38A8FC",
        main = "Unemployment rate (%) per region in Italy",cex.main=1.5, cex.lab = 1.2, ylim = c (0,50), cex.names = 1, axes=FALSE)
axis(2, at=c(0,10,20,30,40,50), pos = 0)
lines(bp,ItalyPoverty_ordenados, type = "l", col = "#FF6450", lty = 1, lwd = 2)
legend("top", legend = c("Poverty rate (%)"),col="#FF6450",pch=15)
text(bp, orden_valores -1, labels = orden_valores, pos = 3, cex = 0.7, col = "black")
boxplot(Italy$UnemploymentRate, col="#38A8FC", main= "Unemployment rate (%) per region in Italy",ylab = expression(bold(" ")), xlab="")

p10_IT=quantile (Italy$Poverty,0.10)
p90_IT=quantile (Italy$Poverty,0.90)
p10_GR=quantile (Greece$Poverty,0.10)
p90_GR=quantile (Greece$Poverty,0.90)
p10_HG=quantile (Hungary$Poverty,0.10)
p90_HG=quantile (Hungary$Poverty,0.90)

Regionsp10_poverty_Italy=Italy[Italy$Poverty <p10_IT,]
Regionsp90_poverty_Italy=Italy[Italy$Poverty >p90_IT,]
Regionsp10_poverty_Hungary=Hungary[Hungary$Poverty <p10_HG,]
Regionsp90_poverty_Hungary=Hungary[Hungary$Poverty >p90_HG,]
Regionsp10_poverty_Greece=Greece[Greece$Poverty <p10_GR,]
Regionsp90_poverty_Greece=Greece[Greece$Poverty >p90_GR,]


filterdf= filterdf %>%
  mutate(Poverty_distribution = case_when(
    Country == "Italy" & Poverty < p10_IT ~ "Bottom 10%",
    Country == "Italy" & Poverty > p90_IT ~ "Top 10%",
    Country == "Hungary" & Poverty < p10_HG ~ "Bottom 10%",
    Country == "Hungary" & Poverty > p90_HG ~ "Top 10%",
    Country == "Greece" & Poverty < p10_GR ~ "Bottom 10%",
    Country == "Greece" & Poverty > p90_GR ~ "Top 10%",
    TRUE ~ "Regions between the 10% and the 90%"))
table(filterdf$Poverty_distribution)

df_new = data.frame(MyCountries = c("Greece", "Hungary", "Italy"), DaltonPolarization = c(4.3, 3.2, 3.5), CountryIdeology = c(4.7, 5.3, 6.4))
matrix_data = t(as.matrix(df_new[c("DaltonPolarization", "CountryIdeology")]))

barplot(matrix_data, beside = TRUE, names.arg = df_new$MyCountries, col=c("#FF6450", "#7eedd1"), ylim = c(0,10), pch=15, main= "Dalton Polarization and Ideology per country",ylab = expression(bold("Polarization and Ideology Index (0-10)")), xlab=expression(bold("")), cex.lab = 1, cex.main= 1.5, sub = "0 = Less polarized and far-left-oriented
10 = Most polarized and far-right-oriented")
legend("topright", legend = c("Dalton Polarization", "Ideology"),col=c("#FF6450", "#7eedd1"),pch=15)



