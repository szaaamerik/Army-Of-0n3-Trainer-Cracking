# Cracking the Trainer's New API: A Deep Dive with Cheat Engine

Welcome back, fellow hackers! <br/>
Today, we're taking our cracking skills to the next level as we tackle the new API of this trainer.<br/>
No more Mr. Nice Guy – it's time to get down and dirty with Cheat Engine and some good old-fashioned breakpoint debugging.

## Prerequisites

Just like before, here's what you'll need:

- [Fiddler Classic](https://www.telerik.com/download/fiddler)
- [Cheat Engine](https://www.cheatengine.org/)
- Basic understanding of HTTP requests and responses as well as JSON
- Basic debugging knowledge
- A willingness to bend the rules

## Step 1: Setting up Cheat Engine and breakpoints

Alright, it's time to unleash the power of Cheat Engine and set some breakpoints.<br/>
This is where the real magic happens, so pay close attention.<br/>
Before we start, make sure you have the VEH Debugger checked as your debugger in the settings.<br/>

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/43edee08-d125-4068-a96a-d47ff593d08d)

### 1. Attach Cheat Engine to the Trainer
Next, you'll want to attach Cheat Engine to the trainer process.<br/>
Find the process associated with the trainer in Cheat Engine's process list and click "Open".<br/>

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/03147bf6-c502-44fd-a33d-450cdbae9a28)


### 2. Choose Your Signature

Now comes the fun part. <br/>
You get to choose which function you want to target with your breakpoints. <br/>
As I mentioned, the signatures may differ slightly, but for the purpose of this guide, it doesn't matter much.<br/>
Pick one and let's roll with it.

```
- Signatures
	* JsonReader
		"85 C0 0F 85 ? ? ? ? 80 7E 39 ? 74 ? 48 8D ? ? 48 8B ? 48 8B ? ? 48 03 ? ? 8B 47"
	* JsonCreator (?)
		"48 89 ? ? ? 4C 8D ? ? 4C 89 ? ? ? 4C 8B ? ? 4D 8B ? ? ? ? ? 48 8B ? ? 48 8B"
```

### 3. Scan for the signature

Now that we've got Cheat Engine up and running, it's time to scan for the signature of the function we want to target. <br/>
Here's how you do it:<br/>

**1. Set Scan Type to "Array of Bytes"**

In Cheat Engine, find the Scanning part and select `Scan Type` from the toolbar. <br/>
Choose `Array of Bytes` from the dropdown menu. <br/>
This allows us to search for a specific sequence of bytes in memory.<br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/702f4274-3114-491a-9759-0b940841d04f)

**2. Input the Signature**<br/>

Next, input one of the signatures provided by me into the "Value" box. <br/>
For the purpose of this tutorial, I will pick the `JsonCreator` one. <br/>
It does not really matter which one you choose as the steps are the exact same. <br/>
This signature is essentially a unique pattern of bytes that identifies the function we're interested in. <br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/335f7a13-0e9f-4774-9fe2-32e6d4c2a5e1)

**3. Configure Memory Scan Options**<br/>

Now, let's configure the memory scan options to narrow down our search:

1. Click on the combobox in the `Memory Scan Options` section.
2. Select the first option after the `All` one. This limits the scan to regions of the main exe memory.

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/17335658-f05e-4c0a-a095-a73f9d3ee36c)

**4. Start the Scan**

With everything set up, click `First Scan` to initiate the scan. <br/>
Cheat Engine will scan through the memory of the trainer and identify any locations that match the signature we provided.

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/798bc71a-08e7-4297-a3ce-62f995d9f35a)

**5. Set Breakpoints on Relevant Instructions**

With your function signature in hand, it's time to set some breakpoints. <br/>
Right-click the result from the scan, and click on `Show In Disassembler`.<br/> 
Set a breakpoint on the highlighted instruction using the F5 key to halt execution when it's hit.<br/>

An illustration of how it should look like:<br/>

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/2dc71717-ee7b-43c5-a354-dff4dd8fcc6f)


## Step 2: Setting up Fiddler and Capturing Responses

Before we jump in, make sure you've gone through Steps 1 through 3 of the [Old API Guide](OldApi.md#step-1-setup-fiddler-filters) as they are the same. <br/>
We'll be building on that foundation as we dive deeper into the rabbit hole.

## Step 3: Swapping the Response

This step is very similar to the one we've covered in the [Old API Guide](OldApi.md#step-4-swap-the-response).<br/>
You can repeat the same steps but you need to use the [new response](https://pastebin.com/LhDaLybu).<br/>

This is how properly followed steps should look like.<br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/e50f24c9-6202-4b3b-a0c4-16cf04383864)

## Step 4: Starting Debugging

Once you clicked on the `Run to Completion` button in Fiddler, it's time to kick things into gear. This is where your breakpoint hits.<br/>
Now, take a closer look at the RDX register. This register always contains a pointer to the response data, which is exactly what we're interested in.<br/>

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/e10fbf9e-3281-4b50-a717-0c2bdcf9ee9a)

Right-click it, and then select `Show in HexView`.<br/>
In the bottom part of Cheat Engine, you will be greeted with the decrypted response data. It's time to modify that.<br/>
We have two ways of cracking the trainer from here, both are equally trivial:
1. Changing `DateNow` - decrease the time.
2. Changing `ExpireDate` - increase the time.

I'll be going with changing the `ExpireDate` since it's far more amusing seeing a colossal number until expiration on the trainer.<br/>
You can just select the text on the right hand side and edit it out.<br/>

This is how you can do it:<br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/560fb9ab-9acb-4170-891c-42cffcb39eda)


After this is done, you can press run in the top left corner.

## Step 5: Letting the responses run

After you've hit run, Fiddler should catch a couple of responses.<br/>
As mentioned in the [Old API Guide](OldApi.md#step-5-let-it-flow), you just need to let them go through.

## Step 6: Starting to finalize the process

Now, that you've let the responses through, you should see a message box like this you need to press `Ok`.

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/f718e56b-5f7f-49e9-8162-b277d4ff6c15)

Then, you'll be greeted with a window like this:

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/f359f4e0-f82c-40ec-81f8-d3608507651e)

You need to input `555555` in the text box, then click `Ok`.<br/>
In Fiddler, you will see a new response pop up.<br/>
You need to `Break on Response`, then paste the [new response](https://pastebin.com/LhDaLybu) in the `Text View`.

This is how you properly do it:

![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/b132b9f7-85e6-4660-befa-74b269bbf456)

Now, your breakpoint in Cheat Engine should hit again.

### Step 6: Actually finalizing the process

For the most part, you can repeat the [4th step](#step-4-starting-debugging), but there is an additional thing that you need to do as well.<br/>
Remember the security code (`555555`) we input before? Yes, we need to modify the response in memory for that as well.<br/>

This is exactly how you do it:<br/>
![obraz](https://github.com/szaaamerik/Army-Of-0n3-Trainer-Cracking/assets/126014478/3e0b41bb-fe34-4276-9edd-5e80afad6c5f)


After that, you can hit `Run` in the top left corner of Cheat Engine again.<br/>
Then, go in Fiddler, and search for the latest HTTP Request, and let it run as well.
Now, you can lean back in your chair and see how the trainer lets you in no issue.

## Conclusion

And there you have it, folks! <br/>
With these "advanced" techniques, you're well on your way to mastering the art of cracking the trainer's new API and finding the actual login checking function. <br/><br/>
Remember, this guide is just the beginning. <br/>
As you continue to explore and experiment, you'll uncover even more devious methods to bypass security measures and bend the rules to your will. <br/><br/>
So go forth, break boundaries, and revel in the thrill of pushing the limits of what's possible. <br/>
The digital world is yours for the taking!
