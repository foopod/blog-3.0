---
layout: post
title: Using Markov Chains to Generate President Trump's Next Tweet
description: 'Trump '
date: 2019-11-27 21:00:00 +0000

---
![](/public/images/trump-tweet.png)

### What are Markov Chains?

As per usual someone else already has an amazing example of what they are and how they work. So heck that out [here](http://setosa.io/ev/markov-chains/).

tldr;

> Markov Chains are a way of modelling states of something and using probability to determine a likely next state. For example if you are sitting, your next state might be as follows... 50% continue sitting, 30% standing, 10% lying down, 10% running.

### How do we use this to generate text?

So first we need to have a data set. Any text will do, and the bigger it is the better. In this example I use Donald Trump's last \~30,000 tweets.

> Maybe follow along with another data set, maybe the bible, new headlines, some shakespeare or a favourite poet.

Next we go through the text and for each word we have we create a list of words that came after it. This is an example of the word Fake.

    {"word":"Fake","followedBy":["News","News","News","News","Whistleblower?","Impeachment!","News","Whistleblower?","News","News","News","News","Hearing","Whistleblowers","Washington","News","News","News","News","News","News!","News","Washington","as","News!","News!","News","News","News","News.","News","News","News","News","News","News","News","News!","News!","News.","News","News","Whistleblower","News","News","News","News!","News","News","Witch","News","News","News","News","News","News","News","News","News!","News","News!","(Corrupt)","and","News!","News","News","News","News","News","and","Poll","News","News","News","News!","News","News","News","News","News","News!","News","News","News","News","News","News","they","News","or","News!","Interview","story","News!","News","News","News","News","and","News","News","News","News","News","News","News","and","and","News","News","News","News","News","News.","News","News","News","News.","Media!","News","News","News","reporting!","News","News","News.","News","News","News","News","News","News!","News","News","News.","News","News","News.","News","News","News","Polls.","News","News","News","News","News","News","News","News","News","unsourced","News","News","News","News","News","and","News","News)","News","News","News","News","Polls","News","News","News","News","News","(Corrupt)","numbers","News","Polling","(Corrupt)","numbers","News","Polling","News","News","News!","and","News","News","News","News!","News","News","News","News","News","News.","News","Stories","work","News","News","News!","Media","News","News","News","and","News","News","News","News","News","News","Dossier)","News","News","News","News","and","News)","News","News.","News","News","News","News","News!","Dossier’s","Story","Story","News","News)","News!","News","News","News","News","News","News","News","News","News","News","Dossier","News","Dossier","News","News.","Dossier","News","News","Science.","News","News!","News!","News","Dossier","News","News","Dossier","Media","News","News","News!","Fact","News","News.”","News","News","News","Media","and","News","News","News","News","News!","News","News","News","News","just","News","reporting","reporter","News","News","News","News","News","News","News","sources","News","News","News","News","News","News","News","News","News","News","News","News","News.","News","News","News","News.","News","News","News","60","Media","News","News","News","News","News.","News.","Suppression","News","News","News","News.","News","News","News","News","Story","News!","News.","News","News.","Dossier","News","News","News","News","NBC","Dossier","nothing","News.","Reporting","News!","Reporting","News!","News","Dossier)","News","News","CNN","News","CNN","New","CNN","News","News","News","News","News","Story","News","reporters","News","piece","News","as","Dossier.","News!","News","Dossier","News","News","Dossier","News","News","News","News","News","News","News","News","News","News","News","News","Dirty","News","News","News","News","News","News","News","News","News","News","News","News","News......","News","News","News","News","News","Media","News","ABC","News","News","News","News","News","News","News","News!","News","News","News","News!","News","News","News","News","News","she","News","News","News","News","News","Mainstream","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","Russia","News","News","News","News","NBC","Washington","News.","News","News","Memos?","Dossier","News","News","News","News.","News","News","News","News!","News","News","News","News","reporting","News","News","News","Book","News","News","News","Book","News","News","News","News","News","News","News","News","News","Polls","News.","News","Mainstream","News","News","News","News","News.","News","News","News","News","News","News!","News","News","News.","News","News","News","News","News","News","Dossier","News).","News","News","News","News","News","Dossier","Media","News","News","News","News","@NBCNews","News","News","News","News","News","News","most","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News","News.","News!","News","News","News","News","Media","News","News","News","News","News","News","News","News","News!","News","News","News","News","News","News","News.","News","News","News","Media","News.","News","Media","News","News","News","Media","News","News","Trump/Russia","News","News","media","news!","News","Tears","News?","Twitter"]}

So when we come to generate some new text we can start with a word, then randomly choose a word to come after it from the list, then repeat until we get bored (I like to finish on a full stop).

So in the above example the most likely word to follow "Fake" is "News". Who would have guessed.

### How accurate is it?

Not great. This solution doesn't worry about Natural Language and so the results can just be gibberish.

However in saying that a lot of the results are quite amusing.

Test it for yourself [here](https://foopod.github.io/trump/).

Source code available [here](https://github.com/foopod/trump).