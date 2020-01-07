# Creating an AtBot ChatBot connected to Dynamics 365
Creating Bots that integrate with Dynamics 365 has not been the easiest thing to do in the past for non-developers because it has required a lot of coding to be done, and also in order to change the conversation flows you needed to update and redeploy the code for the Bot to make it available to the users.Recently I was introduced to a partner solution called AtBot that allows us to create Bot services through the AtBot portal that links to LUIS and Azure Bot  Services, allowing us to build conversation flows and dialogs using Flow as the authoring engine.This allows us to build Bots with zero coding experience that also leverages the power of Flow to connect to other services seamlessly, allowing us to integrate Dynamics 365 using the standard entities.In this walkthough we will show you how to configure and build an AtBot Bot that connects to Dynamics 365, using LUIS as the engine for discoving the users intent and deploy it out to chat platforms like Microsoft Teams.This is gold I tell you, gold!

# Building a LUIS language model
We will start off by creating a LUIS language model that will be used by the Bot to infer what the intention of our questions are when we ask them.

# Logging into LUIS
We will start off by logging into the LUIS.

To do this, all you need to do is navigate to the LUIS website by going to http://www.luis.ai and then click on the Login / Sign up link on the page.

![Image 001.png](images/a019531d-8d05-45ce-bacf-b258ab74a356.png)

This will allow you to authenticate with LUIS using your AD account.And that will take you into the My Apps page within LUIS where you will be able to manage all of the different applications that you have trained within the Language Understanding system.

![Image 003.png](images/9180c841-bf48-4f35-9263-488d5f5e77b5.png)

# Creating a LUIS Application
Now that we are logged into LUIS, we can create a Language Understanding App that we will be able to train on all of the different ways that we can ask questions to our bot.

Start off by clicking on the + Create new app link within the My Apps page.

![Image 003.png](images/e0ac8868-b6ce-4242-9d7c-a374f2d113d9.png)

This will open up the Create new app form where we will be able to set up the details for our LUIS app.

![Image 004.png](images/73db3a7e-625b-4b70-9d1c-74a1755281a0.png)

Start off by giving the app a Name.  Here we set the Name to Supply Chain Service.

![Image 005.png](images/0107fb89-015c-4b00-b165-f72dd402830e.png)

And if you want, you can give your app a more detailed Description.  Here we set the Description to Supply Chain Language Domain Service.After you have done that just click on the Done button to create the new LUIS app.

![Image 006.png](images/335a9acc-2295-4cef-8d82-71e06f885245.png)

![](images/9d5b05e8-cc4c-43cf-9dc2-7cb5df7e9ed4.png)

![](images/d19173fa-090b-40fb-8253-bb23b6ac1300.png)

![](images/a08a4ec2-0aca-4725-97d9-08a5d0f41c63.png)

![](images/ed354194-4404-466a-8694-28ab6b8943a8.png)

![](images/e23c2f1c-ef06-4593-8750-13e6d6a17940.png)

![](images/9e797f3d-ae78-4f1f-9f76-576ede76a94d.png)

![](images/fe521709-7eb6-45df-bb14-5870c2072abc.png)

This will take us into the Intents page which will allow us to create groupings of intents (or general objectives) that we will be able to classify out commands though.

![Image 007.png](images/6761fed9-e758-487b-9d14-77bfd68c3f57.png)

# Creating a LUIS Intent
Now that we have the app we can start building the different types of questions or intents that LUIS will be able to use to classify statements with.

All we need to do here is click on the + Create new intent link in the header of the Intents page.

![Image 007.png](images/6ccd5efc-3dcb-4159-9a08-577f5b79e3c1.png)

This will open up a Create new intent dialog box.

![Image 008.png](images/1111dc85-7f4e-42fd-9b96-b4967c5454eb.png)

We just need to give the Intent and Intent name and then click on the Done button.  For this example we set the Intent name to Product Inquiry because all of the sentences that we use to train LUIS will be related to inquiring about a product and also the availability of the product.

![Image 009.png](images/48963c59-f96b-451a-a400-ee2b6ddeeaac.png)

This will take us into the Intents page within LUIS that we will use to describe all of the different ways that we are able to ask the same question.

![Image 010.png](images/92013c22-de2e-4f21-9255-b8c63f00a55a.png)

# Building an Utterance library
Now that we have the intent defined we can start building the library of different ways that we can ask the same question by defining Utterances within the Intents section of LUIS.These will be the basis of our training model within LUIS that will help the system understand your questions.

All we need to do is start typing in the different Utterances that we may use to achieve the intent that we are defining.For our first one we will type in a common way to ask about a product and enter Do we have any bricks?

![Image 011.png](images/c6aac6dd-1ee9-4dae-805e-232f05d445bb.png)

When we press return, the sentence will be added to the list of Utterances.  We need at least five of these utterance examples in order to start training the LUIS model.

![Image 012.png](images/5b7c2b64-1f5e-4935-8ccc-4c066394efb8.png)

![](images/d60f427a-69a6-4428-91a0-ce148b911b73.png)

Let’s continue adding more utterances and add Are there any bricks in stock?.

![Image 013.png](images/4be0f304-a70c-4303-b0bf-7b29081b50c2.png)

We will add another common way of inquiring about products and add how many bricks do we have?

![Image 014.png](images/551131bf-5e42-459e-a60e-06f13bb94744.png)

![](images/1c31150f-f8bb-404e-9470-54c80ee8e5b0.png)

Next we will rephrase it and add another variation and also change the name of the product that we are looking for to give us some variation– Do we have any plates in inventory?

![Image 015.png](images/4e70e99a-1566-4c5b-9adf-93b85b19f0d9.png)

![](images/7319b3a0-967b-4538-8ea6-1ed38e508ae5.png)

And we will add one last variation of the utterance and add do we have any tiles in stock?That should give us enough to start training LUIS.

![Image 016.png](images/fe008c4b-44d2-4a1b-b3be-278fe07d7f12.png)

![](images/8a915f39-7c0b-425d-9b14-2f3bcb382e9f.png)

# Creating an Entity
There is another structure that we can use within LUIS called an Entity which is a way that we can mark items within a sentence that common in some way.  These entities are then passed through as additional information regarding the intent. 

To start off, we will switch to the Entities page within LUIS and then click on the + Create new entity link.

![Image 017.png](images/5708c1df-bdbe-4371-a8bd-b44bb6e45694.png)

![](images/5a61d601-1f06-4d9c-8808-e8fb05ba1531.png)

![](images/3aafc712-7792-419d-8327-2f3321a01d01.png)

![](images/8ff393d0-f436-4021-88a1-25f87e8a730b.png)

Now we have an entity that we can use to embellish our LUIS model with.

![Image 020.png](images/284cfe97-fbea-49bd-baf4-03b18e9eeadf.png)

# Associating Entities with Utterances
Now that we have created our Entity we can start using it within the Intents to identify the parts of the utterances that hold the clues to what the user is asking for.

![](images/8ff5c826-cabc-43ea-b76e-20205f35c8a4.png)

![](images/01b765a6-26fd-4dc2-b6b9-95eb8671568c.png)

On the Intent page, if we hover over any of the words within the Utterances we will see that the word gets bracketed like this – see the [tiles] on the page.

![Image 022.png](images/f2963bf8-58a6-4632-8dee-304a65c08457.png)

If we right-mouse-click on the word then we get other options, including the option to mark the word as an entity – in this case we can select the Product Entity.

![Image 023.png](images/8f748531-6f5a-4ed7-adf1-0ecf309ef2b8.png)

![](images/b6fdb5db-d5be-40e8-8ce5-bf3963b40034.png)

We can continue to mark all of the other words that relate to a product name within the other four utterances.

![Image 025.png](images/30ba50d7-ab75-4e57-860b-eceb2c170345.png)

# Training your LUIS Application
![Image 025.png](images/4862e12b-3400-4fd3-9c54-4c40bc81301f.png)

This will queue the app for training.

![Image 026.png](images/cdb9ed82-bba2-4df1-9df9-c4176944a129.png)

And within a few seconds the training will be finished and we can start using it.

![Image 027.png](images/dd07c7ae-cac2-4271-bfd4-02040065ac27.png)

# Testing your LUIS Application
Before we publish this to production though we will take a little time to test the model and see if it understands what we are asking when we chat with it.

To test the model we just need to click on the Test button in the menu bar.

![Image 027.png](images/c13dda28-5f40-4fdc-a3fd-d9f11848004a.png)

This will open up the Test panel where we can start chatting with LUIS.

![Image 028.png](images/5cdac83a-887c-4ca6-9230-b2361c0d125e.png)

All we need to do is type in the statement that we what LUIS to resolve.  In this case we just ask do we have any cogs in stock?

![Image 029.png](images/66fa305f-d329-4292-806d-e1ffe5b3bfc5.png)

This will return back the result that this question is probably a Product Inquiry and LUIS is 96% certain of it.

![Image 030.png](images/d83952ec-7ddb-4823-8d71-99d920fc35b3.png)

If we click on the Inspect link below the result then we can see more detail about the sentence and we can see that it has also identified that the Product that I was interested in was cogs.

![Image 031.png](images/cc34e46e-f078-44c3-9721-1ea5db80202b.png)

![](images/ebe57354-a596-4c79-80e1-dc7784d3ba69.png)

# Publishing your LUIS Application
The final step in the process is to publish the LUIS app so that we can use it within our Bot.

To do this, all we need to do is click on the Publish button.

![Image 032.png](images/0159b24d-8082-470e-9fd4-020d17d58e9f.png)

This will open up a confirmation dialog box that will allow us to choose where we want to publish the app.  In this case we will leave the environment as the default Production value and then click on the Publish button.

![Image 033.png](images/5393de9c-2d8c-48a0-96cc-558769f2a300.png)

![](images/228df9c9-9808-493e-942d-39194d539a6b.png)

![](images/9a95fc5c-cbd3-4f55-a1c6-91154be46ec0.png)

![](images/81b07f34-3cd1-43de-981a-da814a02a45d.png)

If we click on the Keys and Endpoints option then we will also see some more information about the app including the end points, authoring key and also the password key that we will need later on to link our bot to the LUIS app.So bookmark this page for one of the later steps.

![Image 036.png](images/63097400-5a5d-43f8-9712-e3bfad126604.png)

# Review
How easy was that.  We have just created a LUIS model that will allow us to ask questions regarding the products in our inventory.  Using LUIS will make the conversation a lot easier with the bot because we don’t have to use exactly formatted phrases and it will extract the information that we need from the commands that we send it.

