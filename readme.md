# Introduction
Creating Bots that integrate with Dynamics 365 has not been the easiest thing to do in the past for non-developers because it has required a lot of coding to be done, and also in order to change the conversation flows you needed to update and redeploy the code for the Bot to make it available to the users.
Recently I was introduced to a partner solution called AtBot that allows us to create Bot services through the AtBot portal that links to LUIS and Azure Bot  Services, allowing us to build conversation flows and dialogs using Flow as the authoring engine.
This allows us to build Bots with zero coding experience that also leverages the power of Flow to connect to other services seamlessly, allowing us to integrate Dynamics 365 using the standard entities.
In this walkthough we will show you how to configure and build an AtBot Bot that connects to Dynamics 365, using LUIS as the engine for discoving the users intent and deploy it out to chat platforms like Microsoft Teams.
This is gold I tell you, gold!

# Building a LUIS language model
We will start off by creating a LUIS language model that will be used by the Bot to infer what the intention of our questions are when we ask them.

# Logging into LUIS
We will start off by logging into the LUIS.

## How to do it…
To do this, all you need to do is navigate to the LUIS website by going to http://www.luis.ai and then click on the Login / Sign up link on the page.

![Image 001.png](images/c57293f5-d029-4509-aca3-11b8dc8f5aed.png)

This will allow you to authenticate with LUIS using your AD account.
And that will take you into the My Apps page within LUIS where you will be able to manage all of the different applications that you have trained within the Language Understanding system.

![Image 003.png](images/dfa8b570-98d7-4261-b9ed-5a594f261435.png)

# Creating a LUIS Application
Now that we are logged into LUIS, we can create a Language Understanding App that we will be able to train on all of the different ways that we can ask questions to our bot.

## How to do it…
Start off by clicking on the + Create new app link within the My Apps page.

![Image 003.png](images/75fa6350-4f94-4866-bc01-93a2255d97f2.png)

This will open up the Create new app form where we will be able to set up the details for our LUIS app.

![Image 004.png](images/47b94730-2d0a-4672-904a-2ae0b48b0313.png)

Start off by giving the app a Name.  Here we set the Name to Supply Chain Service.

![Image 005.png](images/410ac55a-75a9-4f48-8c42-239dab65058f.png)

And if you want, you can give your app a more detailed Description.  Here we set the Description to Supply Chain Language Domain Service.
After you have done that just click on the Done button to create the new LUIS app.

![Image 006.png](images/fc5ab2a0-74b4-416e-8a35-81c955171e2f.png)

![](images/a212f59d-5b03-4a1a-8855-d9fb739ea6a6.png)

![](images/d7e66d30-61a6-4d55-9b92-7b21d7581b06.png)

![](images/a918948d-ae32-4efc-abc8-f8b520566086.png)

![](images/acc582c3-9ef3-421c-b587-0cc267eb749a.png)

![](images/8b09ea31-6488-4efc-bd55-71bc0ff5b3a6.png)

![](images/bb5ab7f7-d004-47e5-9b41-f08aa8f49ba5.png)

![](images/a24ad6ef-1a3a-4bb6-a3dc-71bf7e704f30.png)

This will take us into the Intents page which will allow us to create groupings of intents (or general objectives) that we will be able to classify out commands though.

![Image 007.png](images/6103f64e-cf0e-4a69-bd09-fa0e7dc2afe4.png)

# Creating a LUIS Intent
Now that we have the app we can start building the different types of questions or intents that LUIS will be able to use to classify statements with.

## How to do it…
All we need to do here is click on the + Create new intent link in the header of the Intents page.

![Image 007.png](images/4332ad5a-89f6-4a70-b74b-65fb55e79c85.png)

This will open up a Create new intent dialog box.

![Image 008.png](images/cd8ec4ba-83b8-4b9a-ab2e-c122d6bc2464.png)

We just need to give the Intent and Intent name and then click on the Done button.  For this example we set the Intent name to Product Inquiry because all of the sentences that we use to train LUIS will be related to inquiring about a product and also the availability of the product.

![Image 009.png](images/db19d2eb-d45f-4720-93b4-441001072403.png)

This will take us into the Intents page within LUIS that we will use to describe all of the different ways that we are able to ask the same question.

![Image 010.png](images/19863f67-d15a-471d-a8de-17a1b6f896cd.png)

# Building an Utterance library
Now that we have the intent defined we can start building the library of different ways that we can ask the same question by defining Utterances within the Intents section of LUIS.
These will be the basis of our training model within LUIS that will help the system understand your questions.

<<<<<<< HEAD
## How to do it…
All we need to do is start typing in the different Utterances that we may use to achieve the intent that we are defining.For our first one we will type in a common way to ask about a product and enter Do we have any bricks?
=======
All we need to do is start typing in the different Utterances that we may use to achieve the intent that we are defining.
For our first one we will type in a common way to ask about a product and enter Do we have any bricks?
>>>>>>> 9a816f1f074c1b353336b9a71f8b9fe1ee264b79

![Image 011.png](images/c3928e2c-56c5-47fb-b12d-52e0ba2d6af6.png)

When we press return, the sentence will be added to the list of Utterances.  We need at least five of these utterance examples in order to start training the LUIS model.

![Image 012.png](images/a37b5b4b-6e49-45f6-8483-157cd593d22a.png)

![](images/3ef78d1d-b3bd-44b3-b94f-16884a346f97.png)

Let’s continue adding more utterances and add Are there any bricks in stock?.

![Image 013.png](images/2a09e0fa-dd6a-4a81-9e8d-e3703edf029d.png)

We will add another common way of inquiring about products and add how many bricks do we have?

![Image 014.png](images/6b423894-1fc2-4afa-b9bf-8fdb83e22128.png)

![](images/37a5d7e0-57e5-4df8-9b0c-3f7f50c7ccdd.png)

Next we will rephrase it and add another variation and also change the name of the product that we are looking for to give us some variation– Do we have any plates in inventory?

![Image 015.png](images/e8545c30-2a1f-4a47-8626-06f207ecaaee.png)

![](images/52e19c43-9305-49ac-ab5c-9128571b8c8f.png)

And we will add one last variation of the utterance and add do we have any tiles in stock?
That should give us enough to start training LUIS.

![Image 016.png](images/68cd1de1-db9f-4677-a948-0fbfadaa2cde.png)

![](images/24a2e9c5-af37-4c75-9fb0-3b81282081d4.png)

# Creating an Entity
There is another structure that we can use within LUIS called an Entity which is a way that we can mark items within a sentence that common in some way.  These entities are then passed through as additional information regarding the intent. 

## How to do it…
To start off, we will switch to the Entities page within LUIS and then click on the + Create new entity link.

![Image 017.png](images/5dd09961-7046-4728-b10b-2191021c91aa.png)

![](images/ebd73314-420f-4fa5-9bdf-2083bdb6b0a3.png)

![](images/65b48de2-02fe-43a6-9b45-95aa0e503221.png)

![](images/3c1abd47-4403-48cd-9e66-cab8517bdf51.png)

Now we have an entity that we can use to embellish our LUIS model with.

![Image 020.png](images/3de266d9-594e-4c5a-affa-6cae33dddad4.png)

# Associating Entities with Utterances
Now that we have created our Entity we can start using it within the Intents to identify the parts of the utterances that hold the clues to what the user is asking for.

![](images/b552c56f-dc48-4d38-a096-644209d2aaa6.png)

![](images/773073ea-cc7a-411e-8d28-97ad21531be9.png)

## How to do it…
On the Intent page, if we hover over any of the words within the Utterances we will see that the word gets bracketed like this – see the [tiles] on the page.

![Image 022.png](images/191a897a-d5e4-481a-8f47-0ed861b1cc72.png)

If we right-mouse-click on the word then we get other options, including the option to mark the word as an entity – in this case we can select the Product Entity.

![Image 023.png](images/78d00e78-d4d6-4784-ae00-a112ab999023.png)

![](images/65f4a330-c39c-4795-80db-99ef96fd6156.png)

We can continue to mark all of the other words that relate to a product name within the other four utterances.

![Image 025.png](images/eee12345-7b57-433b-88dc-92b8ec0e4446.png)

# Training your LUIS Application
## How to do it…
![Image 025.png](images/b128f5d7-6d55-4832-bc29-e22846763e89.png)

This will queue the app for training.

![Image 026.png](images/b487ae5e-5b7c-42e2-a943-e54d10d2e1a7.png)

And within a few seconds the training will be finished and we can start using it.

![Image 027.png](images/3b7d6069-15c8-4dfc-a5bd-7a3f5c2529ad.png)

# Testing your LUIS Application
Before we publish this to production though we will take a little time to test the model and see if it understands what we are asking when we chat with it.

## How to do it…
To test the model we just need to click on the Test button in the menu bar.

![Image 027.png](images/4f4259f1-c7ac-47d3-a397-724d8e0d386f.png)

This will open up the Test panel where we can start chatting with LUIS.

![Image 028.png](images/0ebbd21f-d2f9-4e05-811f-139a0d5044a8.png)

All we need to do is type in the statement that we what LUIS to resolve.  In this case we just ask do we have any cogs in stock?

![Image 029.png](images/631a8e8f-dfe2-42f6-bce1-b976f3d27493.png)

This will return back the result that this question is probably a Product Inquiry and LUIS is 96% certain of it.

![Image 030.png](images/8b039537-b6f4-450c-af2a-e0a36138db30.png)

If we click on the Inspect link below the result then we can see more detail about the sentence and we can see that it has also identified that the Product that I was interested in was cogs.

![Image 031.png](images/acb27491-e4d6-4f4a-b373-e6a2060f5894.png)

![](images/1d7780e4-3235-4a32-ae36-207510c20c0d.png)

# Publishing your LUIS Application
The final step in the process is to publish the LUIS app so that we can use it within our Bot.

## How to do it…
To do this, all we need to do is click on the Publish button.

![Image 032.png](images/5ae46839-82c6-4eda-bb17-41bcf8d06f6a.png)

This will open up a confirmation dialog box that will allow us to choose where we want to publish the app.  In this case we will leave the environment as the default Production value and then click on the Publish button.

![Image 033.png](images/22e9a5a6-68ee-4dfe-b484-fdadcdef956c.png)

![](images/4a96cd6e-4764-4fa0-a3fb-1224439c5b15.png)

![](images/1bd01653-d0ec-47bb-9ac2-669958fcddf3.png)

![](images/3fdca03d-c921-4606-8cbb-f60263adbfaa.png)

If we click on the Keys and Endpoints option then we will also see some more information about the app including the end points, authoring key and also the password key that we will need later on to link our bot to the LUIS app.
So bookmark this page for one of the later steps.

![Image 036.png](images/acf00e86-956f-4150-be11-2513ca958601.png)

# Review
How easy was that.  We have just created a LUIS model that will allow us to ask questions regarding the products in our inventory.  Using LUIS will make the conversation a lot easier with the bot because we don’t have to use exactly formatted phrases and it will extract the information that we need from the commands that we send it.

