# Cracking the Trainer's Old API: A Step-by-Step Guide

Alright, buckle up, folks.<br/>
Today, we're diving deep into cracking the old API of this trainer.<br/>
We're going to tear through it like it's made of tissue paper.<br/>
And guess what? We're doing it all with just Fiddler Classic and a healthy dose of cynicism.

## Prerequisites

Before we get started, make sure you have the following:

- [Fiddler Classic](https://www.telerik.com/download/fiddler)
- Basic understanding of HTTP requests and responses as well as JSON
- A willingness to bend the rules

## Step 1: Setup Fiddler Filters

First things first, let's set up Fiddler to capture only the traffic we're interested in.

1. Launch Fiddler Classic.
2. Navigate to the Filters tab.
3. Set the filters to capture traffic from the trainer's login page only. This ensures we're focused on the API calls we need.
  - Check the "Use filters" checkbox.
  - Input `armyof0n3trainer.com;` in the hosts box.
  - In breakpoints, select: "Break on Post", "Break On Get", "Break on XML"

This is how properly setup filters should look like.<br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/535d54a2-a41f-4b82-bd8b-8fbfde56d481)

## Step 2: Input Fake Credentials

Time to play pretend.<br/>
Open up the trainer's login page and input some fake credentials - doesn't matter what it is.<br/>
We're not here to actually log in – we're here to intercept the juicy responses.<br/>

An image of how it should preferably look: <br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/009324c9-0e46-465c-8457-ea496db489f7)

## Step 3: Capture the Response

As soon as you hit that login button, Fiddler should capture the request and response.<br/> 
You will know that it's hit, when you see a blue `T` letter on red background.<br/>
Double-click it, click `Break On Response`, then navigate to `Text View`.<br/>

An illustration of the proper approach:<br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/59e6870d-5d23-4d40-8d86-3967aea699e3)

## Step 4: Swap the Response

Ah, here it comes. Now, this is where the magic happens. <br/>
Once you've got that response in your sights, swap it with [the one](https://pastebin.com/ye64JNLW) I've prepared for you.<br/>
If you are curious why is the response setup like this and not otherwise, I explain it at the end of the guide.<br/> 
This is your chance to inject some chaos into the system.<br/>
"How do I do it", you might ask. It is very straight forward.
- Once you're in the `Text View` page in Fiddler, delete everything.
- Copy the new response I provided you with on pastebin into the text box.
- Last but not least, click `Run to Completion`.

This is how properly followed steps should look like.<br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/225484f1-7544-4961-b8c2-038b861eb0e9)

## Step 5: Let It Flow

With the response swapped, let every single other one flow through.<br/>
Release the kraken, so to speak. Let every response after this point go through unimpeded.<br/>
"How do I do it", you might ask again. It is also extremely straight forward.<br/>
- Double-click the latest response.
- Click `Run to Completion`. Boom. That's it.

## Conclusion

And there you have it, folks.<br/>
You've just cracked the trainer's old API like a pro.<br/>
Now go forth, wreak havoc, and remember – with great power comes great responsibility. Or something like that.<br/>
The guide doesn't end here - we still have two points to cover over.

## The downsides of this method

As much as we'd like to claim victory and ride off into the sunset, there are a couple of downsides to this that we need to address.

1. Dependency on Fiddler: While Fiddler is our trusty sidekick in this endeavor, it comes with a catch. You'll need to keep Fiddler open in the background at all times. Why? Because the trainer will continue making web requests to ensure that your credentials are valid. So, don't go closing Fiddler just yet.
2. Exception Handling: Sometimes, things don't go according to plan. If an unsuccessful request occurs, such as a timeout, the trainer might throw an exception. It's like a hiccup in the system – annoying, but manageable. When this happens, don't panic. Just click continue and carry on with your cracking escapades.

So, while this method isn't without its quirks, it's still a powerful tool in your cracking arsenal.<br/>
Just keep these downsides in mind and soldier on.<br/>
After all, no great adventure is without its challenges.

## Promised explanation
In the 4th step of this guide, I promised to explain why the prepared response is set up the way it is. Here's a brief overview:

1. `"ExpirationDate": "6969-01-01 0:00:00"`: Set to the first of the year 6969 because it's a very far away date that never fails.
2. `"HardwareID": ""`: The HardwareID is set to null because the trainer interprets it as a new account, skipping the HWID check altogether.
3. `"userCode": 1`: This is set to 1 because the app assumes you're just logging in again, skipping the need for waiting on an email.

With these adjustments, you're effectively tricking the trainer into granting access without actually meeting its security requirements. <br/>
Clever, huh?
