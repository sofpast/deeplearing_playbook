### Training log

- When I trained a transformer model with `learning rate = 6.25e-6`, here is the training log that I got:
""
                                                            
>{'loss': 0.0026, 'learning_rate': 3.3564814814814815e-05, 'epoch': 123.38}                                                                                                  
{'loss': 0.0056, 'learning_rate': 3.240740740740741e-05, 'epoch': 129.87}                                                                                                   
{'loss': 0.0174, 'learning_rate': 3.125e-05, 'epoch': 136.36}                                                                                                               
{'loss': 0.0025, 'learning_rate': 3.0092592592592593e-05, 'epoch': 142.86}                                                                                                  
{'loss': 1.3854, 'learning_rate': 2.8935185185185186e-05, 'epoch': 149.35}                                                                                                  
{'loss': 0.0034, 'learning_rate': 2.777777777777778e-05, 'epoch': 155.84}                                                                                                   
{'loss': 0.002, 'learning_rate': 2.6620370370370372e-05, 'epoch': 162.34}                                                                                                   
{'loss': 0.0031, 'learning_rate': 2.5462962962962965e-05, 'epoch': 168.83}                                                                                                  
{'loss': 0.002, 'learning_rate': 2.4305555555555558e-05, 'epoch': 175.32}                                                                                                   
{'loss': 0.0019, 'learning_rate': 2.314814814814815e-05, 'epoch': 181.82}                                                                                                   
{'loss': 0.0039, 'learning_rate': 2.1990740740740743e-05, 'epoch': 188.31}                                                                                                  
{'loss': 0.0034, 'learning_rate': 2.0833333333333336e-05, 'epoch': 194.81}                                                                                                  
{'loss': 0.0046, 'learning_rate': 1.967592592592593e-05, 'epoch': 201.3}                                                                                                    
{'loss': 0.0073, 'learning_rate': 1.8518518518518518e-05, 'epoch': 207.79}                                                                                                  
{'loss': 0.0051, 'learning_rate': 1.736111111111111e-05, 'epoch': 214.29}                                                                                                   
{'loss': 0.0125, 'learning_rate': 1.6203703703703704e-05, 'epoch': 220.78}                                                                                                  
{'loss': 0.0147, 'learning_rate': 1.5046296296296297e-05, 'epoch': 227.27}                                                                                                  
{'loss': 0.0056, 'learning_rate': 1.388888888888889e-05, 'epoch': 233.77}                                                                                                   
{'loss': 0.0071, 'learning_rate': 1.2731481481481482e-05, 'epoch': 240.26}                                                                                                  
{'loss': 0.0049, 'learning_rate': 1.1574074074074075e-05, 'epoch': 246.75}                                                                                                  
{'loss': 0.0052, 'learning_rate': 1.0416666666666668e-05, 'epoch': 253.25}                                                                                                  
{'loss': 0.0038, 'learning_rate': 9.259259259259259e-06, 'epoch': 259.74}                                                                                                   
{'loss': 0.0037, 'learning_rate': 8.101851851851852e-06, 'epoch': 266.23}                                                                                                   
{'loss': 0.0044, 'learning_rate': 6.944444444444445e-06, 'epoch': 272.73}                                                                                                   
{'loss': 0.0046, 'learning_rate': 5.787037037037038e-06, 'epoch': 279.22}                                                                                                   
{'loss': 0.0036, 'learning_rate': 4.6296296296296296e-06, 'epoch': 285.71}                                                                                                  
{'loss': 0.0034, 'learning_rate': 3.4722222222222224e-06, 'epoch': 292.21}                                                                                                  
{'loss': 0.0026, 'learning_rate': 2.3148148148148148e-06, 'epoch': 298.7}                                                                                                   
{'loss': 0.0023, 'learning_rate': 1.1574074074074074e-06, 'epoch': 305.19}                                                                                                  
{'loss': 0.0022, 'learning_rate': 0.0, 'epoch': 311.69} 
"""

A question is that how can we read the log and is my model is fine. How can I test it.

- I am using AdamW for optimizer and what the recommendation is using learning rate for NLP problem is: `1e-1, 2e-3, 3e-3 and 5e-3`.

### Important information of the training log
- Context: I will give a litle bit about the context that i am working on:
  - I have a set of 120 invoices for training data (I could not have more)
  - I am using LayoutXLM for SER
  - Optimizer: AdamW
- When i started with `learning_rate = 1e-3`, then:
> {'loss': 1.8644, 'learning_rate': 0.00018518518518518518, 'epoch': 259.74}                                                                                                         
{'loss': 1.8648, 'learning_rate': 0.00016203703703703703, 'epoch': 266.23}                                                                                                         
{'loss': 1.8661, 'learning_rate': 0.0001388888888888889, 'epoch': 272.73}                                                                                                          
{'loss': 1.86, 'learning_rate': 0.00011574074074074075, 'epoch': 279.22}                                                                                                           
{'loss': 1.8636, 'learning_rate': 9.259259259259259e-05, 'epoch': 285.71}                                                                                                          
{'loss': 1.8703, 'learning_rate': 6.944444444444444e-05, 'epoch': 292.21}                                                                                                          
{'loss': 1.8628, 'learning_rate': 4.6296296296296294e-05, 'epoch': 298.7}                                                                                                          
{'loss': 1.8637, 'learning_rate': 2.3148148148148147e-05, 'epoch': 305.19}  

- Loss is slightly over time but it is very high. I know the model is not accuracy, and yet, the compute metrics is too low `0.33`. Those things make me think about the problem of `gradient vanishing`.
    - Loss function is not decreased as I expected
    - model is not converging
    - Model does not perform well in validation set
- Perhaps, because I am using high learning rate, and it works well with `6.25e-6`. I might decrease it a litle bit further.

- One more thing is my dataset is too small `size = 120` examples, so comparing with the typical size which is at least `1,000 examples`.

- 
