## January-11
---
This morning, I got through another hour of the AI-102 learning path. More delving into the natural language processing capabilities in Azure. I do wonder, however, if a number of these capabilites are really as significant as they may have been in previous years. NLP and language understanding have taken a sharp turn with ChatGPT and transformer based models in the last couple of years. So much so that larger LLMs are able to handle many of the more discrete capabilities that are built out in PaaS capabilities like the Azure AI Services... I dunno.. just a thought.


## January-10
---
I saw some tweets this morning about how GPT-4 is getting increasingly "lazy" and some innacuracies or unfinished responses being observed more often. In response, some people suggested running LLMs like [Mistral 7B](https://mistral.ai/news/announcing-mistral-7b/) which is touted as the best 7B open source model available to date. Some people then responded that it isn't possible to run this without high vram, but that is incorrect. It's possible to run quantized versions of Mistral without any vram. As a test, I used [LM Studio](https://lmstudio.ai/) and was able to get some answers to some non-intuitive problems and the performance was quite quick when using the right version of Mistral.

Aside : What does quantization mean anyway? And how does one quantize a model? Note to self: explore this...

This evening I spent quite a bit of time playing around with LM Studio and varoius language models. Unfortunately I did not have great success. Maybe it was because I was running it from a Linux image on an sd card, but it was giving me some very strange results and then I couldn't open a model any longer.

This evenint I also spent some more time going through the AI-102 training, knocking off another module. I didn't get a chance to do much else unfortunately. The evening was busy.

## January-9
---
I took the train into Toronto today. I nearly got on the wrong train heading back home. Actually I **did** get on the wrong train heading home, but fortunately got on the right train line and was able to hop-off-hop-on to get on the right train. Phew!

During the train to the office, I managed to get through a couple of modules on the AZ-102 certification learning path. Completed the computer vision section and moved onto the language processing section.

I'm listening to a science-fiction, [Robopocalypse, by Daniel H. Wilson (2011)](https://en.wikipedia.org/wiki/Robopocalypse) and it's a pretty sweet story about a human unleashing uncontrollable AI. I'm very much enjoying it and managed to get a few chapters in as well on the train. The problem I'm having is that I end up not listening for stretches or, like last night, I fall asleep and wake up 12 further chapters into the book but no idea what happened. So I'm having to rewind quite a bit. But highly recommended if you are on the hunt for AI related science fiction.

I finished one of the Microsoft Ignite: Azure AI Vision challenge. Part of it was exploring the Image Analysis 4.0 capabilities and get a better understanding of the improvements that have been made with the use of Florence.

Got me some sweet badges.

![Azure AI Vision badges](images/20230109_azure-learn-achievements-vision_and_facialrecognition.jpg)


## January-8
---
I go for walks most mornings to kick start the day. This morning was no exception and while getting some steps in, I listened to the first 30 minutes or so of a recently puslished book - [The Coming Wave: Technology, Power and the Twenty-first Century's Greatest Dilemma, by Mustafa Suleyman and Michael Bhaskar](https://www.amazon.com/Coming-Wave-Technology-Twenty-first-Centurys/dp/0593593952). Only that far in and I'm getting quite a picture that this is a great book. It reminds me a bit of Life 3.0 mixed with Superintelligence. Definitely getting the "urgent warning" vibes and looking forward to listening to the rest. I'm headed to Toronto tomorrow so expecting that I'll get quite a bit of listening in then.

Interestingly, today starts CES 2024. There were a couple of keynotes that I caught today. Most notibly were the keynotes from both AMD and Nvidia. Both companies introduced some new tech related to AI (and gaming). Nvidia announced the much discussed RTX Super series of cards and showed off some interesting  demos, like the discussions with NPC characters in a game that uses LLM + voice synth. AMD also announced a new graphics card as well as the 8000 series APUs that will be able to run games like Cyberpunk 2077 in 1080, with all the good effects, without a dedicated GPU card. AMD also discussed a lot about their foray into AI.

The AMD keynote actually made me look into ROCm and ONNX a little more and although a few years old now, ONNX (a non-platform specific ML framework) seems to have a lot of promise. I'm interested in reading through the book, The State of Open Source AI, to get some more insight in to this and maybe other "write once run everywhere" capabilities for ML that could help boost competition in the AI silicon space.

This evening, I did a few modules in Computer Vision on the self-paced AI-102 lerning track. And once again, got a tiny bit more of the Savill study cram in while... you guessed it, lifting some weights.

## January-7
---
- Found some recent books on AI. I've read some great AI books in the past, including Life 3.0, Superintelligence. Found some books that I'll start getting into. At first, I found 2084 on Amazon with really positive ratings but then delved into the ratings on Goodreads and found some scathing reviews - "Lennox feels that he can disregard credible scientific information, quote the bible as his source of evidence for ridiculous, completely illogical arguments... And then turn around and act like he himself is a man of science." - yikes!
- Worked through the AI-102 Azure AI Service lab, using an Azure AI container. It's interesting that Microsoft makes their containers available for local runtime and are still able to apply billing back to your subscription. I ran the language detection container on an Azure Container Instance. Which took a really long time to get running. I also found that the first time I ran the service, it took a fairly long time to instantiate and run. Consecutive attempts ran pretty quickly.
- Sidenote : Azure container repo URI : https://mcr.microsoft.com/en-us/catalog?page=1
- I quickly then deleted the container instance to avoid charges.
- Started next module in AI-102 self-paced track, introducing decision support capabilities.
- Did the Analyze Images lab in the self-paced learning track
- Watched another 30 minutes of [John Savill's Azure AI-102 Study Cram](https://youtu.be/I7fdWafTcPY?si=d9l-gEwqddqYiAmx) video - again while working out in my basement gym.
 
## January-6
---
So here I go again. Trying to jam in as much learning as I can about AI. Intending to use this markdown file as a mechanism to blog about it all. Previously when I did this, I documented the whole journey in [Trello, here](https://trello.com/b/g1cS5K0O) and wrote about the top 5 insights I learned, [here in a Medium article](https://medium.com/swlh/top-5-insights-after-i-spent-100-days-learning-about-artificial-intelligence-b14b44a67134). This time, I'm just going to put it all in my github account. This has become the place where I mostly write anyway.

I'm going to commit to 30 minutes per day of learning. This doesn't include writing in the journal here. I'm hopeful to be able to spend considerable more time than that, but I have work and family and I also need to keep my Duolingo streak going 😉.

To start, between last night and this morning, I've spent roughly 1.5 hours on courses.

I have already certified in a number of Microsoft Azure certs, including AI-900, but will go for the AI-102 certification which seems a little more comprehensive than AI-900. Given my background, I expect I'll be able to do this in less than the 40 - 50 hours I've calculated as the bare minimum if you're going in cold. Will see. Certifications always catch me off guard with how much effort I really need to remember it all. I'm also going to have to spend some time brushing up in order to renew my other unrelated certs, due March, so may have to take a break from this.

Besides the AI-102 certification, I'm refreshing everything I learned in 2019 with what looks like a great review course on Udemy called [Machine Learning, Data Science and Generative AI with Python](https://www.udemy.com/share/101W9O3@VqPjR6sljJFflMO_mBMY8Uscvj2cNVU9fw6gIJ3_CPRQtxm9pkSp6Rl7etLlW3dl/) from [Frank Kane at Sundog Education](https://www.sundog-education.com/course/machine-learning-data-science-and-deep-learning-with-python/). This is to start at least, but should take a number of weeks to finish. I'll also explore some podcasts and keep up to date via the various experts I follow on Threads and the YouTube channels I subscribe to. Who knows, I may even do either of those as part of this all.

So this is my first post. If you are reading this, hopefully it all ends up helping or being interesting at least.

### Today :
- Watched 30 minutes of [John Savill's Azure AI-102 Study Cram](https://youtu.be/I7fdWafTcPY?si=d9l-gEwqddqYiAmx) video while working out in basement gym
- Listend to a couple of Practical AI podcasts (while driving with fam to Toronto and back)
- AI-102 self-paced study path (30 minutes)
- Machine Learning Udemy Course (15 minutes)
- Watched [Matt Wolfe's latest AI update](https://youtu.be/RGsZrqa2Iss?si=hAJtmaaCVzWOihUg)
- Started Microsoft Skills Challenge : [Ignite Azure Vision](https://learn.microsoft.com/training/challenges?id=bf3c5e50-6ea9-47b6-86e5-3cfe22e1e626&WT.mc_id=cloudskillschallenge_bf3c5e50-6ea9-47b6-86e5-3cfe22e1e626&ocid=ignite23_CSC_sbanner2_cnl) (20 minutes)
