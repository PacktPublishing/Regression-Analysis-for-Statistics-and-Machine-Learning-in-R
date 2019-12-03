######################################################################
######### LASSO regression- variable selection

data(BostonHousing)
str(BostonHousing)

summary(BostonHousing)
head(BostonHousing)

library(caret)

train_control <- trainControl(method="cv", number=10)
#10 fold cv

lasso <- train(medv ~., BostonHousing,
               method='lasso',
               preProc=c('scale','center'),
               
               trControl=train_control)

lasso

# Get coef
predict.enet(lasso$finalModel, type='coefficients', s=lasso$bestTune$fraction, mode='fraction')

#coefficents are reduced to zero--> these can be discraded