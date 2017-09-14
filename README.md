# Trabajo
Exposiciones de AR
#Se desea saber si el ingreso percibido por el empleado depende de la edad que tenga
#Con base a la población ocupada y que tiene edad de laborar se realizo la estimacion de los parametros
#que indicarán cual es la relacion entre estas variables
#Variables:
#x=edad laborable (entre 15 y 65 años)
#y=ingreso que percibe

install.packages("foreign")
library(foreign)
install.packages("questionr")
library(questionr) 

base_completa<-read.dbf("C:\\Users\\HP\\Desktop\\Laura Narvaez\\sdemt117.DBF")
class(base_completa$EDA)
base_completa$EDA<-as.numeric(base_completa$EDA)
class(base_completa$EDA)

#se filtra dadas las especificaciones de la base
edad_ingreso<-subset(base_completa,(EDA >= 15 & EDA <= 65) & (R_DEF == "00") & (C_RES == "1" | C_RES =="3")& (CLASE2=="1"))
edad_ingreso<-data.frame(edad_ingreso$INGOCUP,edad_ingreso$EDA) #crea una base nueva
edad_ingreso$X<-edad_ingreso$edad_ingreso.EDA
edad_ingreso$Y<-edad_ingreso$edad_ingreso.INGOCUP
View(edad_ingreso)

install.packages("stats")
library(stats)
regresion<-lm(Y~X,edad_ingreso)
summary(regresion)
plot(edad_ingreso$X,edad_ingreso$Y,xlab="edades",ylab="ingresos percibidos")
abline(regresion)

#Conclusión
#se puede ver que el ingreso esta determinado por la edad en la que se labora 
#la ecuacion para estos datos es: y=3500.641+25.333x
#el ingreso esta determinado por la edad en la que se comienza a trabajar 
#es decir que entre mas edad se tiene mayor ingreso se percibe, este factor va a compañado de los años de experiencia que se tiene
#podemos decir que el ingreso tiene un aumento del 25.33 cada vez que incrementa la edad
