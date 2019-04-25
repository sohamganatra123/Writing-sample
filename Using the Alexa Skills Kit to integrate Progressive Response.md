# Using the Alexa Skills Kit to integrate Progressive Response

[![Using DynamoDB in custom Alexa Skill](http://img.youtube.com/vi/xqzhNSXUvDw/0.jpg)](https://youtu.be/xqzhNSXUvDw)

#### Overview

Hey, today we are going to see how to use the progressive response API with your alexa skill. 

##### What does the Progressive Response API do? 

Progressive Response allows you to keep your users engaged while your skill is doing all the heavy lifting in the background. 
Alexa plays this response while it waits for the full skill response and avoids those silent moments between your responses. 

In this tutorial you will see, when we ask alexa 

"*How many astronauts in space?* "

It will first respond with the progressive response which in our example is *"Space is a bit far away, wait till i get back the information from the ISS* " 

And then it will respond with the number of astronauts once it receives the information from the API. 

Or say for example, you were doing a complex calculation that takes a couple of seconds or you are waiting for response from an API - well it wouldn’t be a good idea to keep your user waiting in the dark about what's happening. 

You could use the progressive response feature to keep your user engaged while you get the actual response in the meantime. But note that the progressive response does not change the actual response time. The response time is still approximately 8 seconds and you have to cover your progressive response as well as the original response within this time. 

Progressive Response helps you keep the conversation flowing and helps the user understand what is going on and provide a better voice user interface experience.

Now let's get started and setup a skill with progressive response. 

#### Prerequisites

Before you get started 

If you’re new to using skill templates check out our getting started video” and make sure you have the following:
- An Amazon Developer account. You can get that at: [developer.amazon.com](developer.amazon.com)
- An Amazon Web Services account. You can get that at: [aws.amazon.com](aws.amazon.com)
- The Alexa Skills Kit CLI (ASK CLI) installed and properly configured.


You can watch the [Setting up the Alexa Skills Kit CLI ](https://www.youtube.com/watch?time_continue=2&v=lcJ_K7dTjW0)video to set up the ASK-CLI. 

You can also find more details at [skilltemplates.com/docs/getting-started](skilltemplates.com/docs/getting-started)

#### Getting Started

#### 1. Start with downloading the skill from skilltemplates.com

1.1 So let's get into the terminal and clone the template. You can do that by using Alexa Skills kit 

```
ask new --template --url https://skilltemplates.com/templates.json
```

1.2 From the list of available templates choose the **Progressive Response Starter Alexa** template and hit enter. 

This will download the files to the folder and you can open up the editor of your choice and view the code. 

#### 2. Deploying the skill 

Let's understand how the code works by deploying it to AWS first. 

2.1 To deploy the skill, open the terminal or command prompt and move to the project directory. 

```
cd progressive-response-starter-alexa
```

2.2 Now, to deploy the skill enter the command in the terminal or command prompt. 

```
ask deploy
```

2.3 It will take a while to deploy the skill. Once you see the confirmation message move on to the next step to test it out. 

![confirm deploy](https://github.com/tingiris/tutorials/blob/master/img/2018-09-28-using-the-alexa-skill-kit-to-integrate-progressive-response/progressive-response-1.png)

#### 3. Testing the skill

3.1 Log in to your amazon developer console at https://developer.amazon.com and click **Test** in the navigation bar to open up the test simulator. 

![Click Test](https://github.com/tingiris/tutorials/blob/master/img/2018-09-28-using-the-alexa-skill-kit-to-integrate-progressive-response/progressive-response-2.png)

3.2 In this template, we are using an API which responds the number of astronauts in space. You can feel free to customize this url or use an [external API with Alexa](https://github.com/tingiris/tutorials/blob/master/2018-06-29-building-an-alexa-skill-that-uses-data-from-an-external-api.md).

3.3 In the test field, type *alexa ask progressive response starter how many astronauts are there in space right now*

![Enter the command](https://github.com/tingiris/tutorials/blob/master/img/2018-09-28-using-the-alexa-skill-kit-to-integrate-progressive-response/progressive-response-3.png)

Alexa will now respond with the progressive response which we have mentioned in the code. "Space is a bit far away, wait till I get back the information from ISS".

![confirm deploy](https://github.com/tingiris/tutorials/blob/master/img/2018-09-28-using-the-alexa-skill-kit-to-integrate-progressive-response/progressive-response-4.png)

It will then provide the actual response which is fetched from the API i.e. " There are currently 6 astronauts in space."

So you can see Alexa took the request, and then said Space is too far away, let me connect with ISS and then a few seconds later gave me the actual response. You can customize this response in the code. To do that let's head to the next step and see how the code works. 

#### 4. Understanding the code

4.1 Open up a text editor of your choice and open the *index.js* file. 

Here, you will see a function called `GetAstronautCountHandler` which is the intent handler. 

The `callDirectiveService`  is a method that has been defined below, which handles the progressive response. 

4.2 In this function we are creating a `directiveServiceClient` const which stores the data from `getDirectiveServiceClient` method which calls the Alexa directive service. 

We are also getting the requestID, endpoint and the request token from the request that is being made. 

![confirm deploy](https://github.com/tingiris/tutorials/blob/master/img/2018-09-28-using-the-alexa-skill-kit-to-integrate-progressive-response/progressive-response-5.png)

Then, we have created a directive which creates a voice player to speak the information that we want the user to hear. This information is written in the `speech` variable, feel free to customize it to what you'd want the user to hear.

![confirm deploy](https://github.com/tingiris/tutorials/blob/master/img/2018-09-28-using-the-alexa-skill-kit-to-integrate-progressive-response/progressive-response-6.png)

We then have a try catch method wherein we call the directive service to return the progressive response and once the progressive response is spoken out, we get the actual information from the API. 

4.3 You can customize the API url here to get other responses. 

![confirm deploy](https://github.com/tingiris/tutorials/blob/master/img/2018-09-28-using-the-alexa-skill-kit-to-integrate-progressive-response/progressive-response-7.png)

Congratulations! You can use this feature to avoid those awkward silence moments that happen when you are demoing a skill to your users.

You can also view a detailed video about setting up the Progressive Response in this [video](https://youtu.be/xqzhNSXUvDw). 

#### Resources 

You can find more tutorials and resources about creating Alexa skills on

[^1] Website:  https://dabblelab.com 

[^2] YouTube:  [Dabble Lab](https://www.youtube.com/channel/UCfY-LopSxGekh9LruXLjffg)

[^3] Templates: [skilltemplates.com](https://skilltemplates.com)
