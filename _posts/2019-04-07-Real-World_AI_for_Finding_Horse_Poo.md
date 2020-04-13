---
layout: post
title: Real-World AI for Finding Horse Poo!
#bigimg: /img/PooDetector.gif 
#gh-repo: SubmitCode/Comparison-Of-Algorithms
#gh-badge: [star, fork, follow]
published: true
tags: [AI]
comments: true
---

![image](/img/PooDetector.gif)

My wife has a very time-consuming hobby. She has three horses. Fabiola, Herkules and Sophie. As a good husband, I, of course, help her wherever I can, but with my data science background, I’m limited in the things I can do. For instance, I cannot fix the horse panels or construct barns. But finally, my time has come. I found a use case where I can help my wife save time and money with my data science.

In this article, I describe my venture of building an AI which recognizes when a horse poos in the right spot and gives the horse a treat so that the horse learns to poo in the right place. It was quite challenging, and I learned a lot while I was working on the project. But I can prove that AI is profitable and capable of things we couldn’t have imagined before.

A side note: I call it a real-world problem because many of the data science challenges on Kaggle, OpenAI, or elsewhere have a well-defined problem with engineered data. They do 90% of the work for you. In this case, I had to come up with an idea for every aspect of the project.

# Challenge
The most time-consuming part of owning a horse is the cleaning. One should clean up after their horses at least twice a day. If you have ever cleaned a horse box, you know that there is at least one wheelbarrow (German: Schubkarre) of horse poo per day. In our case, it usually takes my wife 30 to 45 minutes to clean the horse boxes, including the sprinkling of sawdust (German: einstreuen von Sägespänen).

To solve this problem, we came up with an idea that would save us a tremendous amount of time. If we could only train our horses to always poo in the same place, and ideally just in front of the manure heap (German: Misthaufen)! Yet to attempt to train a horse in the traditional way would be quite time-consuming. One of us would have to stay in the barn to watch the horses and, whenever a horse pooed in the right spot, give it a treat. Even then, it would not be certain that the horse associates the treat with the act of pooing in the right place. This would need to be done for several days, plus we would need to teach them that the treat is actually related to pooing in the right spot and not to our presence or some other factor.

So we came up with the idea of building a robot to do this for us. The idea is quite simple. We would place an IP camera (with infrared) at the spot where the horses should poo. Then we would train some neural nets, which can detect when a horse is pooing. When pooing is detected, the horse gets a treat from a machine.

That being said, it’s actually quite challenging. But this is not because it’s hard to train a neural net or choose the right architecture. Below is a list of the main real-world challenges we encountered:

 - Horse pooing takes about 20 seconds, so in order to get enough pictures to get started, you need to capture at least one frame per second—and even then, it could be that you don’t capture the part where the poo falls on the ground. Also, we only installed one camera for detecting poo. So, by chance, the horse needs to poo in the right spot. This means we got 86,400 pics per day for, let’s say, 60 pooing pictures—and initially, we had to go through them by hand and label them.
 - We tried to label the picture based on the action that was performed. Typically, one would use a 3D Convolutional Neural Network (NN) or a recurrent NN. For now, I settled on a ResNet50 (Residual Neural Net with 50 Resnet blocks).
 - as being said we have 3 horse. One big female horse and two miniature shetland ponies one stalion and one mare and their pooing pictures actually look quite different. For instance the pooing pose of the small horse is so difficult to capture as Herkules and Sophie have a very long tail with lots of hair that we focused mainly on Fabiola, the big horse.

# Does it work?
Yes but there is still alot work to do. We still have the problem of false positives. For instance it's hard to catch the pooing action if the horse stands at a certain angle to the camera and depending on weather conditions it's sometimes hard to distinguish between pooing and peeing.

# How it works
![image](/img/solution_outline.jpg)

# Below a picture of the feeding robot
![image](/img/feeding_robot.gif)

# Is it a real world application?
Well if you do projects professionally one has to calculate the business case. So here we go. Let's assume my wife saves about 30 min a day cleaning horse box. In Switzerland the median gross income is about 6500 CHF per month. For the sake of argument I assume that the net income is 33% lower than the gross income. Which gives me an hourly rate of roughly 23 CHF per hour. The average month has about 30 days this means she is spending 15 hours per month and 180 hours per year for cleaning the horse. This gives us a saving of around 4140CHF or 4100$ per year without considering the running costs.

## Cost of the infrastructure
- IP cam 300 CHF
- LTE router 150 CHF
- Raspberry Pi + equipmnet 100 CHF
- Setup work (it takes a couple of days initially, but I expect the second project will go much faster): I will assume five days, which translates to 2,000 CHF (I assume a higher hourly rate for IT work)
- Electric engine and stuff for the feeding mechanism 100 CHF

## Running costs
- Google Cloud Linux VM 95 CHF
- Five Hour lease of graphics for 16 hours per month 7 CHF
- Internet 35 CHF
- Work per month for labeling pics and maintainance 50 CHF

All of above gives us a monthly saving of around 158 CHF and intial cost of 2750 CHF. This give us a payback period of 18 months and around 1900 CHF of savings per year.

# Summary & next steps
I have to admit, this is a special use case. But it smells like a business idea, doesn’t it? Take computer vision, add AI, and solve a real-world problem. Just think of other use cases, such as:

Do you, like most of us, hate it when you have to wait in line to pay for your groceries while the other checkouts are closed? A store could train an AI to detect long lines and automatically call a cashier.
The store could also track the performance of its salespeople. For instance, as an owner or manager, you could measure how long it takes on average until a customer gets contacted when a salesperson is in the show room.
Right now I am playing around with Retinanet, YOLO2 and FASTER RCNN architecture. In plain english. I draw bounding boxes around the horse to let the AI know which is the interesting area of the picture.
