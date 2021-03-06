title=My experience in Refugal
date=2017-03-06
type=post
tags=hackathon,event,coding
status=published
~~~~~~

This weekend I've participated in the [Refugal](http://refu.gal/), a hackathon for refugees. It isn't the fist time I participate in a hackathon but this one has been special in some way. Do you know those videos of strangers who doesn't know each other but they start to play together in the middle of the station?. Something like this one:

<iframe width="560" height="315" src="https://www.youtube.com/embed/5Y39CwHfOHM" frameborder="0" allowfullscreen></iframe>



Well, this is exactly what I felt some times during the weekend.

Let me start in the beginning. I arrived soon and started to speak with people. A nice introduction to the hackathon by [David](https://twitter.com/dvilchez) and [Edo](https://twitter.com/edosadikovic), a game to improve creativity and we started with the ideas.

I know I'm more a doer than a thinker. But I like to collaborate so I proposed two ideas: a bot to help communicated refugees and volunteers and a network of home webcams interconnected to provide real-time information to the refugees and also to people at home. My presentation of the ideas was quite bad, mainly I was speaking about a bot... but not all people were developers so later some people told me they didn't know what a bot is. Big fail.

My "bot" idea was the third one with more votes. It was another one I liked a lot more (the first one) but I stayed with the bot. Very soon the team was formed: four developers (2 web, 1 mobile and myself) and one designer. It was the more technical team, probably because of my bad explanation of the idea.

We moved to a room. We discussed the idea for a while in front of a whiteboard and we separated the bot in different sections: Facebook Connector, Telegram Connector, Bot Logic, Design (logo, web, slides, etc.) and DevOps (my part: server, docker, Apache Kafka, etc.). In less than 30 minutes, everything was ready and we were working on the project.

Hard to explain what happened after that, four guys and a designer working like one person. Lines of code, commands, systems, drawings... everything happening so fast, [133 commits in less than 10 hours](https://github.com/refu-gal/refubot/graphs/commit-activity). I remember the designer stopping her drawing and asking: "Ey, guys, I know some development but I'm not understanding what are you are talking about. Is it complex what you are doing?". The four developers in the room said Yes! at the same time. You may take a look to [github repo](https://github.com/refu-gal/refubot): Docker, Docker Compose, AWS, Apache Kafka, four nodeJS and one SQLLite... Everything integrated and working!. And the designer, what a great work she did. You may have the best backend in the world, but without a good designer, people isn't going to appreciate it. [The bot web](http://refubot.refu.gal/) is done by her, nice work!

![Working as a team](https://lh3.googleusercontent.com/a5r3LdOYsH4W6qW3F-wyOAzsaVI5Mgqim6yF64Qeq9zw4K-FRPzQMyVe4QmR-EU4Lwk3HO0I4aDFGyz8a8zfG3a1hZ0nFpHM-cAbJH2YkGm9h8GNFcSa9Dtf-2795D6Avn96gF43keZVLGeqAROMOUlG4Orf-D_n26pbPG5lv9xNWT6Po62hqWMW9WDOobBX1rn0Cv3mjqn7-Yu5l1lCuRTANOrv6U-4DwCD-sKpmFinUYPl8y3y-veH6nB9NORgf0yjBQpr7RO5KSKRrc9fiAOvP63O8_FCpcdV1Zb5U-_DrPPbYtAMwbk50YyhSiaXghcQpJglHlqx7O-NAxZHDxAfoHyVE70w1so_af6v_KZfJBKzdEDUCZQ8rYJuCCQ4CBeK4u-Xe62U598F15e5x3Wb0lYSzSj-M_JBC6-qyqErio9NOKj4_akItup6Vp3_iDy5emavrNr9fuPa7p1lSOqBIg31LkR1Gz5y_skIV5iitaJS9HXa8D_NJS17gnUngIgCrI2s0vsbVZ753AhZFFOXdEqYwsI6LOuMhhwntmHdQa7Jcf1nmn5ybkt9qwSwYf7YNRy1iugRpg7DMIQOR6iffrQklAXfRSIbdeUKV0ytCKlftlk8UFR4DlN4JaZU0WbnMz4upj8mkK5xFzZE51o8NIbQEsCWwEH6vEXR=w1287-h965-no)



From time to time someone proposing something: always accepted or postponed to the end if there was time for that. And back to work, not even a discussion in the whole weekend. Sometimes we even forget go to eat (but a great organization and [the impacthub Vigo is so cool](http://vigo.impacthub.net/en/)!). Also we had some funny moments, smiles and lot of complicity.

I even had time to add a SMS connector using Nexmo, the best 15 euros spent in my life. First time I develop something using nodejs. I don't like it yet but I have to say it was a good decision for the project: lot of libraries and SDKs, easy to deploy and fast to develop.

Of course, we run the demo during the presentation, it was great to see people sending messages from different networks and speaking with our bot. So fun!. I will pay good money for a video of that moment but everybody was too busy sending messages.

![RefuBot presentation](https://lh3.googleusercontent.com/wEfS8qxIqm0Jg01y6C3t6wDnZslQz4-FsHs1gPuzqXxR51gH_xkSu7wZCAJ_9JYYZUteo0FvF2ThF_8XBuLcDtS0zKrnpz2AdARMVps7eCHgnaFxzKnyMp5KPerV7KOzhlJg1wX8avgpu7injwgz_0oiYLO7VIRs-uYDW8s_GavTiafJ3EpwftWJqP6sH-o9KmQRntwBuZt8QbggBhF7HWw4377Soc9GKm3mNsocqALa6Sl9Zwa5BFlZ-LnPQjp8Y2WA8_FVVq_KJdV0EzF8U4yEgcSkOlzZsiEShfcyfAwIF_NShDlOH-qYz8o22hF1rFP303zfoBfdSzuddIyD1jpMP9oRRAoQMEu7EuGEejp28Rz-GvzvbmgsJyvD3XzmuJgU-vJcq_es2D4PXabR9oHR_xQJXku2ip697ZiKrIhSlc0ye3oLFpANwC_Od_CiLp1m3NUG7KZ-vsf0BvfwYLrj1MURv2cRjChTXNTZ62LXXFbQv2uqUPWIdUlNVYcGrYoSg3lhWsCqzl3xm_80T5DDQOxyMavjJ7T4KwK-vN5CoFSiB3HSuy0NA__nUXYhhk6fudr1cw5myfyURuicvGjg1J9LD2NkbgSusyjPSgqVJqhBW4L84Q3cwMBJmcdFl921U-kD_iFRBG7VWYarTsWPPZ1i1mA_eoQCt8BRww=w1448-h965-no)




This morning, when I terminated the EC2 instance hosting the bot, I felt some type of sadness. Yet it has been great to meet such great team this weekend. And who knows?. RefuBot works and it scales. I can assure that. Maybe someone will discover it in the future and RefuBot becomes real. If it's really useful, that would be fair.

*Photos are from [this Picassa album](https://photos.google.com/share/AF1QipMDKf-GpnBzjFBII47B_Yoy5jOUpFqM1_agHANPrlG3CcKsbba09EcMIeZNP_R3sA?key=cllPNDJFMjlTYWtybXNIZ01PT1RMSWpabU5LVFF3)*.


