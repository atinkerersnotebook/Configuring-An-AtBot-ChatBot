# Creating an AtBot ChatBot connected to Dynamics 365
Creating Bots that integrate with Dynamics 365 has not been the easiest thing to do in the past for non-developers because it has required a lot of coding to be done, and also in order to change the conversation flows you needed to update and redeploy the code for the Bot to make it available to the users.Recently I was introduced to a partner solution called AtBot that allows us to create Bot services through the AtBot portal that links to LUIS and Azure Bot  Services, allowing us to build conversation flows and dialogs using Flow as the authoring engine.This allows us to build Bots with zero coding experience that also leverages the power of Flow to connect to other services seamlessly, allowing us to integrate Dynamics 365 using the standard entities.In this walkthough we will show you how to configure and build an AtBot Bot that connects to Dynamics 365, using LUIS as the engine for discoving the users intent and deploy it out to chat platforms like Microsoft Teams.This is gold I tell you, gold!

# Building a LUIS language model
We will start off by creating a LUIS language model that will be used by the Bot to infer what the intention of our questions are when we ask them.

# Logging into LUIS
We will start off by logging into the LUIS.

## How to do it…
To do this, all you need to do is navigate to the LUIS website by going to http://www.luis.ai and then click on the Login / Sign up link on the page.

![Image 001.png](3a20d96d-3355-4290-abf8-73dabc604e43.png)

This will allow you to authenticate with LUIS using your AD account.And that will take you into the My Apps page within LUIS where you will be able to manage all of the different applications that you have trained within the Language Understanding system.

![Image 003.png](18482fd7-21af-469f-a309-dd2f1d31dfb9.png)

# Creating a LUIS Application
Now that we are logged into LUIS, we can create a Language Understanding App that we will be able to train on all of the different ways that we can ask questions to our bot.

## How to do it…
Start off by clicking on the + Create new app link within the My Apps page.

![Image 003.png](de4f2e20-ef44-4aeb-8fa5-39331c5a8dc6.png)

This will open up the Create new app form where we will be able to set up the details for our LUIS app.

![Image 004.png](e9627b46-d205-4742-b0ad-1fd771525f32.png)

Start off by giving the app a Name.  Here we set the Name to Supply Chain Service.

![Image 005.png](aae92df5-d07d-4c3f-a833-4f1c19062259.png)

And if you want, you can give your app a more detailed Description.  Here we set the Description to Supply Chain Language Domain Service.After you have done that just click on the Done button to create the new LUIS app.

![Image 006.png](47fc7b0c-a0b7-4e5d-b0bd-fd4efb3929fe.png)

![](59c4812b-0584-4fbc-97b8-8a86f439aba0.png)

![](4a4d3961-c021-4c4d-b5f3-4b2e7be4eabe.png)

![](701ec416-3c7d-4331-b09d-1745ff1c6ae8.png)

![](34281dad-2b91-422b-8fb8-eddaa1e953e1.png)

![](9d1617ae-554d-45e4-ab9a-2eb099a76dba.png)

![](ddcadc24-94da-4785-89f5-b64d2ec34aeb.png)

![](d1cfb766-f77b-421d-8fc8-e12065a4b3cd.png)

This will take us into the Intents page which will allow us to create groupings of intents (or general objectives) that we will be able to classify out commands though.

![Image 007.png](857e0761-eb8d-45d2-93e0-1f95aacf5ffb.png)

# Creating a LUIS Intent
Now that we have the app we can start building the different types of questions or intents that LUIS will be able to use to classify statements with.

## How to do it…
All we need to do here is click on the + Create new intent link in the header of the Intents page.

![Image 007.png](a17d2117-ab2f-4ea5-8e63-dec819dd85ee.png)

This will open up a Create new intent dialog box.

![Image 008.png](b38e98a9-daef-4a17-b908-58a1b6354539.png)

We just need to give the Intent and Intent name and then click on the Done button.  For this example we set the Intent name to Product Inquiry because all of the sentences that we use to train LUIS will be related to inquiring about a product and also the availability of the product.

![Image 009.png](9dcc9098-2a11-4358-ad0a-d3c5b914ebf9.png)

This will take us into the Intents page within LUIS that we will use to describe all of the different ways that we are able to ask the same question.

![Image 010.png](dca5eccc-cb55-4bd9-a2e3-e3ce19d714c1.png)

# Building an Utterance library
Now that we have the intent defined we can start building the library of different ways that we can ask the same question by defining Utterances within the Intents section of LUIS.These will be the basis of our training model within LUIS that will help the system understand your questions.

## How to do it…
All we need to do is start typing in the different Utterances that we may use to achieve the intent that we are defining.For our first one we will type in a common way to ask about a product and enter Do we have any bricks?

![Image 011.png](b181a1fd-f17e-4c4c-9d3c-6b1c1470c8db.png)

When we press return, the sentence will be added to the list of Utterances.  We need at least five of these utterance examples in order to start training the LUIS model.

![Image 012.png](a6481e4b-8e0c-40d1-818c-8a55fbf60b9e.png)

![](73df4ee5-d60d-432c-82bb-cc4825bc2026.png)

Let’s continue adding more utterances and add Are there any bricks in stock?.

![Image 013.png](20bba8fc-8cd5-4634-ab44-69eba55f828c.png)

We will add another common way of inquiring about products and add how many bricks do we have?

![Image 014.png](2e2cddba-46a8-4001-b347-8039fef835e1.png)

![](95121698-6909-4ffb-b50e-a0b2fe43e009.png)

Next we will rephrase it and add another variation and also change the name of the product that we are looking for to give us some variation– Do we have any plates in inventory?

![Image 015.png](fbc8f55d-ff40-4ef0-bc06-93f8c17a12f1.png)

![](233d40c2-99c3-4897-a9e6-92421c04fc60.png)

And we will add one last variation of the utterance and add do we have any tiles in stock?That should give us enough to start training LUIS.

![Image 016.png](e96b1ec3-a94b-4fcc-b4a8-79249471ba63.png)

![](5e65b761-b1bf-435f-88e1-9ba11229cba7.png)

# Creating an Entity
There is another structure that we can use within LUIS called an Entity which is a way that we can mark items within a sentence that common in some way.  These entities are then passed through as additional information regarding the intent. 

## How to do it…
To start off, we will switch to the Entities page within LUIS and then click on the + Create new entity link.

![Image 017.png](4ec72607-6ac2-43ed-bc8c-5f10dba40f05.png)

![](572ccb79-47da-43ba-aa45-0ac8abeec6f9.png)

![](f99eaf63-14c4-4aa3-839b-641c1d02e16e.png)

![](5282545c-18a6-4fb7-bac5-d273e2b455a9.png)

Now we have an entity that we can use to embellish our LUIS model with.

![Image 020.png](3f83c1dd-1f93-4780-9caf-57b5da925d2c.png)

# Associating Entities with Utterances
Now that we have created our Entity we can start using it within the Intents to identify the parts of the utterances that hold the clues to what the user is asking for.

![](02a95c61-970c-497f-92b4-9fdd7e97149d.png)

![](c511df44-3a74-4490-acb9-50075e52b42f.png)

## How to do it…
On the Intent page, if we hover over any of the words within the Utterances we will see that the word gets bracketed like this – see the [tiles] on the page.

![Image 022.png](bad03e1c-5afc-4bb3-a109-54bd4b5766d9.png)

If we right-mouse-click on the word then we get other options, including the option to mark the word as an entity – in this case we can select the Product Entity.

![Image 023.png](4430c331-958c-44c2-8b87-973746d31d27.png)

![](4cbe228c-efe3-4286-9df4-8f5eb60e81f2.png)

We can continue to mark all of the other words that relate to a product name within the other four utterances.

![Image 025.png](b1a03c0c-0720-418b-937b-0207dc19f92d.png)

# Training your LUIS Application
## How to do it…
![Image 025.png](b7ec7d41-7a57-433a-9481-81a1ce22bd03.png)

This will queue the app for training.

![Image 026.png](e13731be-169d-4c8c-9e38-683df054c539.png)

And within a few seconds the training will be finished and we can start using it.

![Image 027.png](4f5087cf-516e-41e8-9f4d-4d09560073c1.png)

# Testing your LUIS Application
Before we publish this to production though we will take a little time to test the model and see if it understands what we are asking when we chat with it.

## How to do it…
To test the model we just need to click on the Test button in the menu bar.

![Image 027.png](520e600a-1860-434d-ae87-9932966e34a8.png)

This will open up the Test panel where we can start chatting with LUIS.

![Image 028.png](43fefa57-6a68-4bcb-92e5-1c99d0e13031.png)

All we need to do is type in the statement that we what LUIS to resolve.  In this case we just ask do we have any cogs in stock?

![Image 029.png](e2793b7a-b354-443a-85ff-a71a3c3297e5.png)

This will return back the result that this question is probably a Product Inquiry and LUIS is 96% certain of it.

![Image 030.png](ee02861d-427e-4436-a3a9-e5881353311d.png)

If we click on the Inspect link below the result then we can see more detail about the sentence and we can see that it has also identified that the Product that I was interested in was cogs.

![Image 031.png](41704a7d-b041-43c2-97c9-882d847e3f0e.png)

![](4fd73152-0906-43aa-ab5a-82b3ec72e404.png)

# Publishing your LUIS Application
The final step in the process is to publish the LUIS app so that we can use it within our Bot.

## How to do it…
To do this, all we need to do is click on the Publish button.

![Image 032.png](419c9ac1-615b-4d02-8412-68fdb844c892.png)

This will open up a confirmation dialog box that will allow us to choose where we want to publish the app.  In this case we will leave the environment as the default Production value and then click on the Publish button.

![Image 033.png](db7aa867-6f12-413e-9f53-bd1acf05a048.png)

![](def45d52-9fd2-4310-82f1-089c290a8b8a.png)

![](83e6c906-a042-4b08-b3e0-d1723ef6509e.png)

![](7a18131c-345f-4680-80b8-7a23e42bcf8e.png)

If we click on the Keys and Endpoints option then we will also see some more information about the app including the end points, authoring key and also the password key that we will need later on to link our bot to the LUIS app.So bookmark this page for one of the later steps.

![Image 036.png](ebc1dac0-3333-407e-af1d-c4dbf15d17b7.png)

# Review
How easy was that.  We have just created a LUIS model that will allow us to ask questions regarding the products in our inventory.  Using LUIS will make the conversation a lot easier with the bot because we don’t have to use exactly formatted phrases and it will extract the information that we need from the commands that we send it.

