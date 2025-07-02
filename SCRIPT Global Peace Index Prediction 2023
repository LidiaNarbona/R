library(readr)
library(tidyverse)

setwd("D:/miscosas/UMA/UC3M/1sem/Methods/Vanessa/R/2nd project")
df=read_delim("data_100534996.csv", 
                 locale =  locale(decimal_mark = "."), 
                 delim = ";")

filterdf = mutate_if(df,
                     is.character,
                     as.factor)
filterdf$OECD= factor(filterdf$OECD, levels = c(0, 1), labels = c("No", "Yes"))

library(dplyr)

filterOECD = filter(filterdf,OECD == "Yes")
filterNotOECD = filter(filterdf,OECD == "No")

summary(filterOECD$GPI)
summary(filterNotOECD$GPI)

par(mar=c(6,5,5,4))
boxplot(filterdf$GPI~ filterdf$OECD, col=c("#5397DD", "#39AD44"), main= "Comparison between the GPI and the OECD membership",ylab = expression(bold("Global Peace Index (1-5)")), xlab=expression(bold("OECD")), ylim=c(1,3.5),cex.lab = 1, cex.main= 1.5)
text(x = 1.5, y = 3.4, labels = "GPI = 5 represents a high degree of violence", cex = 1, adj = c(0.5, 0), col = "black")  # Ajusta la posición según sea necesario

boxplot(filterdf$GPI~ filterdf$Division, col=c("#5397DD", "#39AD44", "#9265AD", "#AD8D27","#AD284E","#28ADAD"), main= "Comparison of the GPI per geographical division",ylab = expression(bold("Global Peace Index (1-5)")), xlab=expression(bold("")), ylim=c(1,3.5),cex.lab = 1, cex.main= 1.5)
text(x = 3.5, y = 3.4, labels = "GPI = 5 represents a high degree of violence", cex = 1, adj = c(0.5, 0), col = "black")  # Ajusta la posición según sea necesario
filterAfrica = filter(filterdf,Division == "Africa")
filterEurope = filter(filterdf,Division == "Europe")
filterAsia = filter(filterdf,Division == "Asia")
filterNamerica = filter(filterdf,Division == "North America")
filterOceania = filter(filterdf,Division == "Oceania")
filterSAMERICA = filter(filterdf,Division == "South America")

summary(filterAfrica$GPI)
summary(filterAsia$GPI)
summary(filterEurope$GPI)
summary(filterNamerica$GPI)
summary(filterOceania$GPI)
summary(filterSAMERICA$GPI)

cor(filterdf$MilitaryExpenditure, filterdf$GPI)
cor(filterdf$Inflation, filterdf$GPI)
cor(filterdf$GDPpc, filterdf$GPI)

plot(filterdf$MilitaryExpenditure, filterdf$GPI, pch = 15,
     col = "#5397DD", main= "Relationship between the GPI and the Military Expenditure",ylab = expression(bold("Global Peace Index (1-5)")), xlab=expression(bold("Military Expenditure (% of GDP)")),cex.lab = 1, cex.main= 1.5)
reg= lm(GPI ~ MilitaryExpenditure, data = filterdf)
summary(reg)
abline(a=1.92793, b=0.03247, lty = 3, col="#AD284E")


plot(filterdf$GDPpc, filterdf$GPI, pch = 15,
     col = "#9265AD",  main= "Relationship between the GPI and the GDP per capita",ylab = expression(bold("Global Peace Index (1-5)")), xlab=expression(bold("GDP per capita in US Dollars (thousands)")),cex.lab = 1, cex.main= 1.5)
reg2= lm(GPI ~ GDPpc, data = filterdf)
summary(reg2)
abline(a=2.182660, b=-0.011405, lty = 3, col="#AD284E")

plot(filterdf$Inflation, filterdf$GPI, pch = 15,
     col = "#AD8D27",  main= "Relationship between the GPI and the Inflation",ylab = expression(bold("Global Peace Index (1-5)")), xlab=expression(bold("Inflation rate (%)")),cex.lab = 1, cex.main= 1.5)
reg3= lm(GPI ~ Inflation, data = filterdf)
summary(reg3)
abline(a=1.983968, b=0.002320, lty = 3, col="#AD284E")

GDPpcNuevo= c(23.0546, 21.3953, 22.8455, 10.1758, 15.8474)

countriesNuevo = c("Armenia", "Albania", "Bosnia and Herzegovina", "India", "South Africa")

GPINuevo= 2.182660 - 0.011405 * GDPpcNuevo

results = data.frame(Country = countriesNuevo, GDPpc = GDPpcNuevo, GPI = GPINuevo)

print(results)

reg4 = lm(GPI ~ GDPpc + Division, 
           data = filterdf)
summary(reg4)

reg5 = lm(GPI ~ GDPpc + MilitaryExpenditure, 
           data = filterdf)
summary(reg5)

install.packages("scatterplot3d")
library(scatterplot3d)
scatterplot3d(filterdf$GDPpc, filterdf$MilitaryExpenditure, filterdf$GPI,
                     pch = 15, color = "#5397aD",
                     xlab = expression(bold("GDP per Capita (in thousands)")),
                     ylab = expression(bold("                                                               Military Expenditure (% of GDP)")),
                     zlab = expression(bold("Global Peace Index (1-5)")),
                     main = "Relationship between the GPI, the GDP per capita and the Military Expenditure", cex.lab = 1, cex.main= 1.5)
sqrt(0.398)

MilitaryExpenditureNuevo = c(4.3, 1.6, 0.8, 2.4, 0.7)

GPINuevo2 <- 2.103068 - 0.011225 * GDPpcNuevo + 0.031102 * MilitaryExpenditureNuevo

results2= data.frame(Country = countriesNuevo, GDPpc = GDPpcNuevo, MilitaryExpenditure = MilitaryExpenditureNuevo, GPI = GPINuevo2)
print(results2)

