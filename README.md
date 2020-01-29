# LMA-Converter-
This converts LDM and Area into LMA



DF1$Area_m2<-DF1$Area/10000
DF1$LDM_kg<-DF1$LDM/1000
DF1$LMA_kg.m2<-DF1$LDM_kg/DF1$Area_m2
hist(DF1$LMA_kg.m2)
summary(DF1$LMA_kg.m2)
write.csv(DF1,"LMA_Check.csv")

good<-subset(DF1, Code != "NM3GW")
goodshit<-subset(DF1, Code == "NM3GW" & Timepoint == "1")
shit<-subset(DF1, Code == "NM3GW" & Timepoint == "2")
shit$LDM<-as.numeric(.661)

DF_new<-rbind(good, goodshit, shit)

DF_new$Area_m2<-DF_new$Area/10000
DF_new$LDM_kg<-DF_new$LDM/1000
DF_new$LMA_kg.m2<-DF_new$LDM_kg/DF1$Area_m2
hist(DF_new$LMA_kg.m2, breaks = 100)
summary(DF_new$LMA_kg.m2)

quantile(DF_new$LMA_kg.m2, seq(0,1,0.05))

rm(shit, good, goodshit)
shit<-subset(DF_new, LMA_kg.m2 < 0.067)
