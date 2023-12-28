# Week 8

## 8(a)
```R
# Create a vector.
x <- c(12,7,3,4.2,18,2,54,-21,8,-5)

# Find Mean.
result.mean <- mean(x)
print(result.mean)

# Create a vector.
x <- c(12,7,3,4.2,18,2,54,-21,8,-5)

# Find Mean.
result.mean <- mean(x,trim=0.3)
print(result.mean)


# Create a vector.
x <- c(12,7,3,4.2,18,2,54,-21,8,-5,NA)

# Find mean.
result.mean <- mean(x)
print(result.mean)

# Find mean dropping NA values.
result.mean <- mean(x,na.rm = TRUE)
print(result.mean)

# Create the vector.
x <- c(12,7,3,4.2,18,2,54,-21,8,-5)

# Find the median.
median.result <- median(x)
print(median.result)

# Create the function.
getmode <- function(v) {
  uniqv <- unique(v)
  uniqv[which.max(tabulate(match(v, uniqv)))]
}

# Create the vector with numbers.
v <- c(2,1,2,3,1,2,3,4,1,5,5,3,2,3)

# Calculate the mode using the user function.
result <- getmode(v)
print(result)

# Create the vector with characters.
charv <- c("o","it","the","it","it")

# Calculate the mode using the user function.
result <- getmode(charv)
print(result)
```
## 8(b)
```R
input <- mtcars[,c("am","mpg","hp")]
print(head(input))

input <- mtcars
result <- aov(mpg~hp*am,data = input)
print(summary(result))

input <- mtcars
result <- aov(mpg~hp+am,data = input)
print(summary(result))

input <- mtcars
result1 <- aov(mpg~hp*am,data = input)
result2 <- aov(mpg~hp+am,data = input)
print(anova(result1,result2))
```

# Week 9

## Linear Regression

```R
# 1 lm()
a = c(100, 121, 143, 134, 145, 167, 187)
b = c(121, 123, 178, 120, 156, 133, 119)
res = lm(b~a)
print(summary(res))

# 2 predict()
a = c(100, 121, 143, 134, 145, 167, 187)
b = c(121, 123, 178, 120, 156, 133, 119)
res = lm(b~a)
f_res = data.frame(a = 60)
print(predict(res, f_res))

# 3 plot(), png()

a = c(100, 121, 143, 134, 145, 167, 187)
b = c(121, 123, 178, 120, 156, 133, 119)
res = lm(b~a)
png(file = "dummy.png")
plot(b, a, col= "red", main = "Height and Weight regression", abline(lm(a~b)), cex = 5.5, pch = 10, xlab = "Weight in kgs", ylab = "Height in cms")
dev.off()
```

## Multiple Regression

```R
input = mtcars[, c("mpg", "disp", "hp", "wt")]
model = lm(mpg~disp + hp+wt, data = input)
print(model)
a = coef(model)[1]
b = coef(model)[2]
c = coef(model)[3]
d = coef(model)[4]
print(a)
print(b)
print(c)
print(d)
```

## Logistic 
```R
<>
```
## Poisson Regression

```R
input<-warpbreaks
print(head(input))
output<-glm(formula=breaks~wool+tension,data=warpbreaks,family = poisson)
print(summary(output))
```

# Week 10

## 10(a) Time series (snowfall)

```R
snowfall_timeseries<-ts(snowfall,start=c(2013,1),frequency=12 )
snowfall <- c(790,1170.8,860.1,1330.6,630.4,911.5,683.5,996.6,783.2,982,881.8,1021)
snowfall_timeseries<- ts(snowfall,start = c(2013,1),frequency = 12)  
print(snowfall_timeseries)
dev.off()
graphics.off()
plot(snowfall_timeseries)  
```


## 10(b)

```R
xvalues <- c(1.6,2.1,2,2.23,3.71,3.25,3.4,3.86,1.19,2.21)
yvalues <- c(5.19,7.43,6.94,8.11,18.75,14.88,16.06,19.12,3.21,7.58)
png(file = "nls.png")
plot(xvalues,yvalues)
model <- nls(yvalues ~ b1*xvalues^2+b2,start = list(b1 = 1,b2 = 3))
new.data <- data.frame(xvalues = seq(min(xvalues),max(xvalues),len = 100))
lines(new.data$xvalues,predict(model,newdata = new.data))
dev.off()
print(sum(resid(model)^2))
print(confint(model))
```

## 10(c)

```R
library(party)
print(head(readingSkills))

library(party)
input.data <- readingSkills[c(1:105),]
png(file = "decision_tree.png")
output.tree <- ctree(nativeSpeaker~age + shoeSize+score,data = input.data)
plot(output.tree)
dev.off()
```

# Week 11

## 11 (a)

```R
#dnorm
x <- seq(-10, 10, by = .1)
y <- dnorm(x, mean = 2.5, sd = 0.5)
png(file = "dnorm.png")
plot(x,y)
dev.off()

#pnorm
x <- seq(-10,10,by = .2)
y <- pnorm(x, mean = 2.5, sd = 2)
png(file = "pnorm.png")
plot(x,y)
dev.off()

#qnorm
x <- seq(0, 1, by = 0.02)
y <- qnorm(x, mean = 2, sd = 1)
png(file = "qnorm.png")
plot(x,y)
dev.off()

#rnorm
y <- rnorm(50)
png(file = "rnorm.png")
hist(y, main = "Normal DIstribution")
dev.off()
```

## 11(b)

```R
#dbinom
x <- seq(0,50,by = 1)
y <- dbinom(x,50,0.5)
png(file = "dbinom.png")
plot(x,y)
dev.off()

#pbinom
x <- pbinom(26,51,0.5)
print(x)

#qbinom
x <- qbinom(0.25,51,1/2)
print(x)

#rbinom
x <- rbinom(8,150,.4)
print(x)
```

# Week 12

## 12(a)

```R
#x-test
library("MASS")  
print(str(Cars93))  
car_data<- data.frame(Cars93$AirBags, Cars93$Type)  
car_data = table(Cars93$AirBags, Cars93$Type)   
print(car_data)  
print(chisq.test(car_data))
```

## 12(b)

```R
set.seed(0)
ship_vol = c(rnorm(70, mean = 35000, sd = 2000))
t.test(ship_vol, mu = 35000)

#t-test 
x  <- c(0.593, 0.142, 0.329, 0.691, 0.231, 0.793, 0.519, 0.392, 0.418)
t.test(x, alternative="greater", mu=0.3)

# ....
# <t-test 2 more variations exists (refer record)>
# ....
```

## 12(c)

```R
#F-test 

install.packages("randomForest")
library(party)
print(head(readingSkills))
library(party)
library(randomForest)
output.forest <- randomForest(nativeSpeaker ~ age + shoeSize + score, data = readingSkills)
print(output.forest) 
```

# student.arff
```arff
@relation student
@attribute age{<=30,31-40,>40}
@attribute income{low,medium,high}
@attribute student{yes,no}
@attribute credit_rating{fair,excellent}
@attribute buys_computer{yes,no}
@data
<=30,high,no,fair,no
<=30,high,no,excellent,no
31-40,high,no,fair,yes
>40,medium,no,fair,yes
>40,low,yes,fair,yes
>40,low,yes,excellent,no
31-40,low,yes,excellent,yes
<=30,medium,no,fair,no
<=30,low,yes,fair,yes
>40,medium,yes,fair,yes
<=30,medium,yes,excellent,yes
31-40,medium,no,excellent,yes
31-40,high,yes,fair,yes
>40,medium,no,excellent,no
```