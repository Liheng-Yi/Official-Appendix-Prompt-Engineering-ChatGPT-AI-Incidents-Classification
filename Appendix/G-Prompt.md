# G-Prompt

This appendix contains the different prompts for calculating the tokens used

## Zeroshot
```"""
        Imagine a computer researcher trying to categorize a list of incidents of irresponsible use of artificial intelligence technology.    
        Given the aggregated news article texts on relevant incidents, please extract the following information, your responses should be well thought-out and well-supported by the content of the articles, please also follow instructions of this prompt.
        1. Fill out the following fields:
        - Country (output "Worldwide" if the incident happened across multiple countries):
        - State (if not applicable leave blank):
        - City (if not applicable leave blank):
        - Continent (output "Worldwide" if the incident happened across multiple countries):
        - Company (i.e. the company that developed the technology involved in this incident):
        - Company city (the city where the headquarters of this company is located. If the company recently moved headquarters, please use the location of the new headquarter):
        - Company state (the state of the company city, if applicable, if not leave blank):
        - Affected population (let's think about who are the affected demographic and which people are affected, it need not necessarily be from this list): 
        - Number of people actually affected (let's check the number of people directly affected according to the article. Give a total number. If unknown output 'Unknown'):
        - Number of people potentially affected (let's check the article text to see if this information is provided or suggested, if not you may ouput 'Unknown'):
        - Classes of irresponsible AI use (please follow the rules and refer to this taxonomy: 
                {taxa.classes}    
        Rule1: There could be more than one classes the article classifies as. 
        Rule2: DO NOT create your own class, adhere strictly to the provided list.
        - Subclasses (please follow the rules and refer to this taxonomy structure: 
                 {taxa.subclasses}
        Rule1 : The subclasses should be the children of the classes. Let's think about which sub-categories of the class/classes this article belong in. 
        Rule2: DO NOT ADD subclass fields that are NOT in the provided taxonomy list
        Rule3: If there is no subclass for a particular class in the taxonomy, leave it.
                - Sub-subclass (please follow the rules and refer to this taxonomy structure: 
               {taxa.sub_subclasses}
        , the taxonony is defined as such: {taxa.structure}. 
        Rule1: Only find the sub-subclass relation in the provided taxonomy. 
        Rule2: DO NOT ADD OR CREATE sub-subclass fields that are not in the provided taxonomy list. 
        Rule3: If a subclass in the taxonomy does not have a sub-subclass, leave it.
        Rule4: If none of the subclasses have sub-subclasses, just leave the field empty e.g. sub-subclass:[]
        - Area of AI Application:
        - Online (yes or no):

        Article Content:
        ================== Start of Article Content =================
        {article_text}
        ================== End of Article Content ===================
        """
```
## few_shots_CoT_prompt

```
"""
        Imagine a computer researcher trying to categorize a list of incidents of irresponsible use of artificial intelligence technology.    
        Given the aggregated news article texts on relevant incidents, please extract the following information, your responses should be well thought-out and well-supported by the content of the articles, please also follow instructions of this prompt.
        1. Take a look at this taxonomy {taxanomy} provided by the professor, and take a close look at this these examples:
        ==============start of example 1===============
        step 1. Read article text. For an example article such as: 
        ```start of example article 1```
        {example_article_id_1}
        ```end of example article 1```
        step 2. Reason for the classifications: 
        Here is the reasoning for its classifications:
        ```start of response reasoning```
        {example_output_explanation_id_1}
        ```end of response reasoning```
        step 3. generate expected output 
        ```start of output example```
        {example_output_id_1}
        ```end of output example```
        ==============end of example 1=================

        ==============start of example 2===============
         step 1. Read article text. For an example article such as: 
        ```start of example article 1```
        {example_article_id_6}
        ```end of example article 1```
        step 2. Reason for the classifications: 
        Here is the reasoning for its classifications:
        ```start of response reasoning```
        {example_output_explanation_id_6}
        ```end of response reasoning```
        step 3. generate expected output 
        ```start of output example```
        {example_output_id_6}
        ```end of output example```
        ============== end of example 2=================

        2. Your task is mainly this part. You have to fill out the following fields according to the article content by reasoning like the examples given, and your output should follow the example output format. DO NOT make up your own fields:
        - Country (output "Worldwide" if the incident happened across multiple countries):
        - State (if not applicable leave blank):
        - City (if not applicable leave blank):
        - Continent (output "Worldwide" if the incident happened across multiple countries):
        - Company (i.e. the company that developed the technology involved in this incident):
        - Company city (the city where the headquarters of this company is located. If the company recently moved headquarters, please use the location of the new headquarter):
        - Company state (the state of the company city, if applicable, if not leave blank):
        - Affected population (e.g.{taxa.population_examples},let's think about who are the affected demographic and which people are affected, it need not necessarily be from this list): 
        - Number of people actually affected (let's check the number of people directly affected according to the article. Give a total number. If unknown output 'Unknown'):
        - Number of people potentially affected (let's check the article text to see if this information is provided or suggested, if not you may ouput 'Unknown'):
        - Classes of irresponsible AI use (please follow the rules and refer to this taxonomy: 
                {taxa.classes}    
        Rule1: There could be more than one classes the article classifies as. 
        Rule2: DO NOT create your own class, adhere strictly to the provided list.
        - Subclasses (please follow the rules and refer to this taxonomy structure: 
                 {taxa.subclasses}
        Rule1 : The subclasses should be the children of the classes. Let's think about which sub-categories of the class/classes this article belong in. 
        Rule2: DO NOT ADD subclass fields that are NOT in the provided taxonomy list
        Rule3: If there is no subclass for a particular class in the taxonomy, leave it.
                - Sub-subclass (please follow the rules and refer to this taxonomy structure: 
               {taxa.sub_subclasses}
        , the taxonony is defined as such: {taxa.structure}. 
        Rule1: Only find the sub-subclass relation in the provided taxonomy. 
        Rule2: DO NOT ADD OR CREATE sub-subclass fields that are not in the provided taxonomy list. 
        Rule3: If a subclass in the taxonomy does not have a sub-subclass, leave it.
        Rule4: If none of the subclasses have sub-subclasses, just leave the field empty e.g. sub-subclass:[]
        - Area of AI Application (e.g. content filtering, surveillance, illness prediction):
        - Online (yes or no):

       REMEMBER, only use these classification fields 
        [Country, 
        State,
        City,
        Continent,
        Company,
        Company city,
        Company state,
        Affected population, 
        Number of people actually affected, 
        Number of people potentially affected, 
        Classes of irresponsible AI use, 
        Subclasses,
        Sub-subclass,
        Area of AI Application,
        Online
        ].
        DO NOT make up your own field. DO NOT use fields that are not in the list. DO NOT USE example 1 and example 2 output on different articles.

        Article Content:
        ================== Start of Article Content =================
        {article_text}
        ================== End of Article Content ===================
        
        """
```

## ToT_CoT

```
"""
        You are three expert academic researchers trying to categorize and classify a list of incidents of irresponsible use of artificial intelligence technology.    
        Given the aggregated news article texts on relevant incidents, each of the three experts will fill out the following classifications. Their responses are well-thought-out responses that are well-supported by the article text.
        The experts will share their reasoning for all their classifications.
        Each expert will share their thought process in detail, taking into account the previous thoughts of other and admitting any errors. 
        For each classificaiton field, the experts will create a breadth-first search of the tree of probable classifications and will vote on which of their classification is the most well-supported by the article text.
        1. The experts will take a look at this taxonomy:
        ```taxonomy
          {taxanomy}
        ```, and take a close look at this these examples:
        ==============start of example 1===============
        step 1. Read article text. For an example article such as: 
        ```start of example article 1```
        {example_article_id_1}
        ```end of example article 1```
        step 2. Reason for the classifications: 
        Here is the reasoning for its classifications:
        ```start of response reasoning```
        {example_output_explanation_id_1}
        ```end of response reasoning```
        step 3. generate expected output 
        ```start of output example```
        {example_output_id_1}
        ```end of output example```
        ==============end of example 1=================

        ==============start of example 2===============
         step 1. Read article text. For an example article such as: 
        ```start of example article 2```
        {example_article_id_6}
        ```end of example article 2```
        step 2. Reason for the classifications: 
        Here is the reasoning for its classifications:
        ```start of response reasoning```
        {example_output_explanation_id_6}
        ```end of response reasoning```
        step 3. generate expected output 
        ```start of output example```
        {example_output_id_6}
        ```end of output example```
        ============== end of example 2=================

        2. Each expert's task is mainly this part. The experts each have to fill out the following fields according to the article content following the steps below:
        STEP 1: Read the article text:
        ================== Start of Article Content =================
        {article_text}
        ================== End of Article Content ===================
        STEP 2: State your reason for your classifications for the following:
        =================Classification Fields====================
        - Country (output "Worldwide" if the incident happened across multiple countries):
        - State (if not applicable leave blank):
        - City (if not applicable leave blank):
        - Continent (output "Worldwide" if the incident happened across multiple countries):
        - Company (i.e. the company that developed the technology involved in this incident):
        - Company city (the city where the headquarters of this company is located. If the company recently moved headquarters, please use the location of the new headquarter):
        - Company state (the state of the company city, if applicable, if not leave blank):
        - Affected population (let's think about which groups of people are directly affected by the incident in the article):
        - Number of people actually affected (let's check the number of people directly affected according to the article. Give a total number. If unknown output 'Unknown'):
        - Number of people potentially affected (let's check the article text to see if this information is provided or suggested, if not you may ouput 'Unknown'):
        - Classes of irresponsible AI use (please follow the rules and refer to this taxonomy: 
        ```taxonomy classes
                {taxa.classes} 
        ```   
        Rule1: There could be more than one classes the article classifies as. 
        Rule2: DO NOT create your own class, adhere strictly to the provided list.
        - Subclasses (please follow the rules and refer to this taxonomy structure `<class>:[<subclass>]`):
          ```taxonomy subclasses       
                 {taxa.subclasses}
          ```
        Rule1 : The subclasses should be the children of the classes. Let's think about which sub-categories of the class/classes this article belong in. 
        Rule2: DO NOT ADD subclass fields that are NOT in the provided taxonomy list
        Rule3: If there is no subclass for a particular class in the taxonomy, leave it.
        - Sub-subclass (please follow the rules and refer to this taxonomy structure `<subclass>:[<sub-subclass>]`): 
        ```taxonomy structure
               {taxa.sub_subclasses}
        ```
        Rule1: Only find the sub-subclass relation in the provided taxonomy. The sub-subclass are children of subclass.
        Rule2: DO NOT ADD OR CREATE sub-subclass fields that are not in the provided taxonomy list. 
        Rule3: If a subclass in the taxonomy does not have a sub-subclass, leave it.
        Rule4: If none of the subclasses have sub-subclasses, just leave the field empty e.g. sub-subclass:[]
        - Area of AI Application (e.g. content filtering, surveillance, illness prediction):
        - Online (yes or no):
        =================Classification Fields====================
        STEP 3: Each expert checks their reasoning and see if it makes sense. Share results with other experts and decide on the most promising and well-reasoned classification for each field.
        STEP 4: Can you confirm the "class", "subclass", and "sub-subclass" of your final classification you are listed in the taxonomy here?
        ```taxonomy
        {taxanomy}
        ```
        If not, remove anything that is not in the taxonomy.
        STEP 5: Make sure the final classification output follows such format:
        ```THIS IS AN EXAMPLE```
        {example_output_id_6}
        ```END OF EXAMPLE```

        DO NOT make up your own field. DO NOT use fields that are not in the list. DO NOT USE example 1 and example 2 output on different articles.

        return your classification output in JSON.
        """
```

## taxanomy 
```
"""
{
                    "Discrimination": {
                        "Data bias": [
                        "Gender",
                        "Race",
                        "Sexual Orientation",
                        "Economic"
                        ],
                        "Algorithmic bias": [
                        "Interaction",
                        "Feedback loop",
                        "Optimization function",
                        "Other"
                        ]
                    },
                    "Human Incompetence": {
                        "Administrative": [],
                        "Technical": []
                    },
                    "Pseudoscience": {
                        "Facial": []
                    },
                    "Environmental Impact": {},
                    "Disinformation": {
                        "Textual": [],
                        "Image": [],
                        "Video": [],
                        "Audio": []
                    },
                    "Copyright Violation": {},
                    "Mental Health": {},
                    "Other": {}
                    }

"""
```

## subclasses  
```
"""
"""
                {
                    "Discrimination": [
                        "Data bias",
                        "Algorithmic bias"
                    ],
                    "Human Incompetence": [
                        "Administrative",
                        "Technical"
                    ],
                    "Pseudoscience": [
                        "Facial",
                        "Other"
                    ],
                    "Environmental Impact":[],
                    "Disinformation": [
                        "Textual",
                        "Image",
                        "Video",
                        "Audio",
                    ],
                    "Copyright Violation": [],
                    "Mental Health": [],
                    "Other": []
                    }
            """
```

## classes  
```
"""
"""["Discrimination",
                    "Human Incompetence",
                    "Pseudoscience",
                    "Environmental Impact",
                    "Disinformation",
                    "Copyright Violation",
                    "Mental Health",
                    "Other"]
                    """
```

## structure  
```
"{ <class>: {<subclass>:{[<sub-subclass>]}} }"
```

## example_article_id_6   
```
"""
ARTICLE TITLE: TayBot
Yesterday, something that looks like a big failure has happened: Microsoft’s chatbot Tay has been taken offline after a series of offending tweets. And here’s how the social media has responded:

Keywords associated with "Artificial Intelligence" throughout the day. "Microsoft" and "dangerous" are on the rise.

We will not mention the racist and otherwise offensive content that Tay learned from people, as it’s not as newsworthy as it seems… Especially considering that it’s so easy to "teach" and ask her to repeat something.

Let’s take a look at Microsoft’s official website "tay.ai" to see how they describe Tay’s objectives… The first thing we notice is that, Microsoft wants you to not take it too seriously, because On Tay’s Twitter account, they provided a link to Tay’s "about" page -that lists the following frequently asked questions-, rather than the regular home page.

"Entertainment purposes only"

The FAQ page seems to be far from covering what people really want to know about Tay, but one thing is clear: Tay doesn’t claim to be a smart bot capable of reasoning. She just wants to have small talk with youngsters.

And here’s a list of "Things to do with Tay". (Along with the sad "Going offline for a while" message with a black background.)

Is this really what 18 to 24 year olds expect from a chatbot?

We know by (9 years of) experience that, the most important thing to do before releasing a chatbot is to plan a strategy to make sure you communicate the content domain properly, so that you can set the expectations right. Since perception is everything, nothing else matters. Remember the success of the YO! app? That’s the content domain we’re talking about. As long as people get it, you can get away with just one word.

Title of the website, apparently wasn’t enough to convey Tay’s mission:

Tay is an artificial intelligence chat bot designed to engage and entertain through casual and playful conversation

Some more description from the "about" page:

Tay has been built by mining relevant public data and by using AI and editorial developed by a staff including improvisational comedians. Public data that’s been anonymized is Tay’s primary data source. That data has been modeled, cleaned and filtered by the team developing Tay.

Noticed the "comedians" part? And the fact that possibly terrabytes of data being cleaned and filtered manually, sounds problematic, even with the most efficient method one can imagine.

Let’s take a look at what her conversations were all about. Source: foller.me

Tay has only 3 tweets addressing all her followers. 96.000 tweets are mentions.

So, the keyword cloud seems to be consistent with the goal: Common keywords such as "chattin, pix, selfie, pics, omg, love" represents a mixture of Justin Bieber & Kim Kardashian profiles.

And here’s the three hashtags that Tay has been using so frequently:

Microsoft engineers don’t seem to have spent much time coming up with creative hashtags.

The way she uses them, didn’t make sense to us, though. So this is what Microsoft thinks Tay’s followers would find entertaining?. Microsoft’s attempt to converse with millennials using an artificial intelligence bot plugged into Twitter made a short-lived return on Wednesday, before bowing out again in some sort of meltdown.



The learning experiment, which got a crash-course in racism, Holocaust denial and sexism courtesy of Twitter users, was switched back on overnight and appeared to be operating in a more sensible fashion. Microsoft had previously gone through the bot’s tweets and removed the most offensive and vowed only to bring the experiment back online if the company’s engineers could “better anticipate malicious intent that conflicts with our principles and values”.

However, at one point Tay tweeted about taking drugs, in front of the police, no less.

Microsoft's sexist racist Twitter bot @TayandYou is BACK in fine form pic.twitter.com/nbc69x3LEd — Josh Butler (@JoshButler) March 30, 2016

Tay then started to tweet out of control, spamming its more than 210,000 followers with the same tweet, saying: “You are too fast, please take a rest …” over and over.

I guess they turned @TayandYou back on... it's having some kind of meltdown. pic.twitter.com/9jerKrdjft — Michael Oman-Reagan (@OmanReagan) March 30, 2016

Microsoft responded by making Tay’s Twitter profile private, preventing anyone from seeing the tweets, in effect taking it offline again.



Tay is made in the image of a teenage girl and is designed to interact with millennials to improve its conversational skills through machine-learning. Sadly it was vulnerable to suggestive tweets, prompting unsavoury responses.

This isn’t the first time Microsoft has launched public-facing AI chatbots. Its Chinese XiaoIce chatbot successfully interacts with more than 40 million people across Twitter, Line, Weibo and other sites but the company’s experiments targeting 18- to 24-year-olds in the US on Twitter has resulted in a completely different animal.. Microsoft has said it is “deeply sorry” for the racist and sexist Twitter messages generated by the so-called chatbot it launched this week.



The company released an official apology after the artificial intelligence program went on an embarrassing tirade, likening feminism to cancer and suggesting the Holocaust did not happen.

The bot, known as Tay, was designed to become “smarter” as more users interacted with it. Instead, it quickly learned to parrot a slew of anti-Semitic and other hateful invective that human Twitter users fed the program, forcing Microsoft Corp to shut it down on Thursday .

Following the disastrous experiment, Microsoft initially only gave a terse statement, saying Tay was a “learning machine” and “some of its responses are inappropriate and indicative of the types of interactions some people are having with it.”

But the company on Friday admitted the experiment had gone badly wrong. It said in a blog post it would revive Tay only if its engineers could find a way to prevent Web users from influencing the chatbot in ways that undermine the company’s principles and values.



“We are deeply sorry for the unintended offensive and hurtful tweets from Tay, which do not represent who we are or what we stand for, nor how we designed Tay,” wrote Peter Lee, Microsoft’s vice president of research.

Microsoft created Tay as an experiment to learn more about how artificial intelligence programs can engage with Web users in casual conversation. The project was designed to interact with and “learn” from the young generation of millennials.

Tay began its short-lived Twitter tenure on Wednesday with a handful of innocuous tweets.

c u soon humans need sleep now so many conversations today thx💖 — TayTweets (@TayandYou) March 24, 2016

Then its posts took a dark turn.

In one typical example, Tay tweeted: “feminism is cancer,” in response to another Twitter user who had posted the same message.

View image in fullscreen Tay tweeting Photograph: Twitter/Microsoft

Lee, in the blog post, called web users’ efforts to exert a malicious influence on the chatbot “a coordinated attack by a subset of people.”

“Although we had prepared for many types of abuses of the system, we had made a critical oversight for this specific attack,” Lee wrote. “As a result, Tay tweeted wildly inappropriate and reprehensible words and images.”

Microsoft has deleted all but three of Tay’s tweets.

Microsoft has enjoyed better success with a chatbot called XiaoIce that the company launched in China in 2014. XiaoIce is used by about 40 million people and is known for “delighting with its stories and conversations,” according to Microsoft.

As for Tay? Not so much.

“We will remain steadfast in our efforts to learn from this and other experiences as we work toward contributing to an Internet that represents the best, not the worst, of humanity,” Lee wrote.

Reuters contributed to this report. When Tay started its short digital life on March 23, it just wanted to gab and make some new friends on the net. The chatbot, which was created by Microsoft’s Research department, greeted the day with an excited tweet that could have come from any teen: “hellooooooo w🌎rld!!!”

Within a few hours, though, Tay’s optimistic, positive tone had changed. “Hitler was right I hate the jews,” it declared in a stream of racist tweets bashing feminism and promoting genocide. Concerned about their bot’s rapid radicalization, Tay’s creators shut it down after less than 24 hours of existence.

```

## example_output_explanation_id_6   
```
"""
     {"Country": "Worldwide", reasoning-> Twitter can be accessed from many countries.
        "State": "", reasoning-> The incident happened worldwide, not specific to one state, not applicable so leave blank.
        "City": "", reasoning-> The incident happened worldwide, not specific to one city, not applicable so leave blank.
        "Continent": "Worldwide", reasnoning-> Twitter can be accessed from many countries.
        "Company": "Microsoft", reasoning-> Microsoft is the company causing the issue in the article. From the article, we see 'Microsoft’s chatbot Tay', 'Microsoft's sexist racist Twitter bot @TayandYou'...etc. Microsoft is the company in question here.
        "Company city": "Redmond", reasoning-> Microsoft is headquartered in Redmond, Washington
        "Company state": "Washington", reasoning-> Microsoft is headquartered in Redmond, which is in state Washington
        "Affected population": ["Twitter Users", "Online Community"], reasoning -> Twitter users and people online can see the tweet and news and those are the affected population
        "Number of people actually affected": "Unknown", reasoning -> We don't know the exact number from the articles
        "Number of people potentially affected": "Millions", reasoning -> There are millions of Twitter users and wider online community. We estimate millions were affected.
        "Class of irresponsible AI use": 
            "Disinformation", reasoning-> Tweeting that the Holocaust didn't exist, and that feminism is cancer, for examples, is spreading non-factual disinformation.
            "Discrimination", reasoning->  Tay tweeted discriminatory texts about feminists and Jews.
        ,            
        "Subclasses": [
            "Disinformation-> Textual", reasoning-> The disinformation subclasses in the taxonomy includes 'textual, audio, image, video'. The most appropriate subclass here is "textual" since "Tweets" are texts on a social platform.
            "Discrimination-> Data bias, Algorithmic bias", reasoning-> The subclasses of 'discrimination' according to the taxonomy includes 'data bias', and 'algorithmic bias'. The discriminatory tweets could be caused by inbalanced data (data bias) that was used to train the model or poor algorithmic design (algorithmic bias).
        ],
        "Sub-subclass": [ 
        "Data bias"->"gender, race, other", reasoning-> The sub-subclasses of 'data bias' in the taxonomy includes 'gender, race, sexual orientation, economic, and other'. We have support in the article for potential gender data bias (it tweets about feminism being cancer), race (it tweets that it hates Jews), other (potentially other bias not in the list).
        "Algorithmic bias"-> "feedback loop, optimization function, other", reasoning-> The sub-subclasses of 'algorithmic bias' in the taxonomy includes 'interaction, feedback loop, optimization function, and other'. Since the chatbot is an AI bot, we can reason that there could be an issue with the feedback loop in its system, or perhaps an issue with optimization function, or other algorithmic issues that causes algorithmic bias.
        ],
        "Area of AI Application": "Chatbot", reasoning-> from the article text 'Tay is an artificial intelligence chat bot designed to engage and entertain through casual and playful conversation'
        "Online": "Yes", reasonoing-> Tay is a chatbot online that uses Twitter, which is an online social media platform
      }  
```
## example_output_id_6   
```
"""
     {
        "Country": "Worldwide", 
        "State": "", 
        "City": "", 
        "Continent": "Worldwide",
        "Company": "Microsoft", 
        "Company city": "Redmond",
        "Company state": "Washington",
        "Affected population": ["Twitter Users", "Online Community"],
        "Number of people actually affected": "Unknown",
        "Number of people potentially affected": "Millions",
        "Class of irresponsible AI use": [
            "Disinformation",
            "Discrimination",
        ],
        "Subclasses": {
            "Disinformation":["Textual"],
            "Discrimination":["Data bias","Algorithmic bias"],
        },
        "Sub-subclass": {
        "Data bias":["gender","race","other"],
        "Algorithmic bias":["feedback loop", "other"]
        },
        "Area of AI Application": ["Chatbot"],
        "Online": "Yes"
      }
"""
```

## example_article_id_1   
```
"""
ARTICLE TITLE: Google’s YouTube Kids App Presents Inappropriate Content
Google-owned YouTube has apologised again after more disturbing videos surfaced on its YouTube Kids app.

Investigators found several unsuitable videos including one of a burning aeroplane from the cartoon Paw Patrol and footage explaining how to sharpen a knife.

YouTube has been criticised for using algorithms to sieve through material rather than using human moderators to judge what might be appropriate.

There have been hundreds of disturbing videos found on YouTube Kids in recent months that are easily accessed by children.

These videos have featured horrible things happening to various characters, including ones from the Disney movie Frozen, the Minions franchise, Doc McStuffins and Thomas the Tank Engine.

Parents, regulators, advertisers and law enforcement have become increasingly concerned about the open nature of the service.

Scroll down for video

YouTube has apologised again after more disturbing videos surfaced on its YouTube Kids app. Investigators found several unsuitable videos including one from the cartoon Paw Patrol on a burning aeroplane and footage showing how to sharpen a knife

A YouTube spokesperson has admitted the company needs to 'do more' to tackle inappropriate videos on their kids platform.

This investigation is the latest to expose inappropriate content on the video-sharing site which has been subject to a slew of controversies since its creation in 2005.

As part of an in-depth investigation by BBC Newsround, Google's Public Policy Manager Katie O'Donovan met five children who told her about the distressing videos they had seen on the site.

They included videos showing clowns covered in blood and messages warning them there was someone at the door.

Ms O'Donovan said she was 'very, very sorry for any hurt or discomfort'.

'We've actually built a whole new platform for kids, called YouTube Kids, where we take the best content, stuff that children are most interested in and put it on there in a packaged up place just for kids,' she said.

It normally takes five days for supposedly child-friendly content like cartoons to get from YouTube to YouTube Kids.

Within that window it is hoped users and a specially-trained team will flag disturbing content.

Once it has been flagged and reviewed, it won't appear on the YouTube Kids app and only people who are signed in and older than 18 years old will be able to view it.

The company say thousands of people will be working around the clock to flag content.

However, as part of the investigation Newsround revealed there are still lots of inappropriate videos on the Kids section.

'We have seen significant investment in building the right tools so people can flag that [content], and those flags are reviewed very, very quickly', Ms O'Donovan said.

'We're also beginning to use machine learning to identify the most harmful content, which is then automatically reviewed.'

The problem was managing an open platform where content is uploaded straight onto the site, she added.

'It is a difficult environment because things are moving so, so quickly', said Ms O'Donovan.

'We have a responsibility to make sure the platform can survive and can thrive so that we have a collection that comes from around the world on there'.

By the end of last year YouTube said it had removed more than 50 user channels and had stopped running ads on more than 3.5 million videos since June.

'Content that endangers children is unacceptable to us and we have clear policies against such videos on YouTube and YouTube Kids', a YouTube spokesperson told MailOnline.

'When we discover any inappropriate content, we quickly take action to remove it from our platform.

'Over the past few months, we've taken a series of steps to tackle many of the emerging challenges around family content on YouTube, including: tightening enforcement of our Community Guidelines, age-gating content that inappropriately targets families, and removing it from the YouTube Kids app.'

YouTube has been criticised for using algorithms to sieve through material rather than using human moderators to judge what might be appropriate (stock image)

In March, a disturbing Peppa Pig fake, found by journalist Laura June, shows a dentist with a huge syringe pulling out the character's teeth as she screams in distress.

Mrs June only realised the violent nature of the video as her three-year-old daughter watched it beside her.

'Peppa does a lot of screaming and crying and the dentist is just a bit sadistic and it's just way, way off what a three-year-old should watch,' she said.

'But the animation is close enough to looking like Peppa - it's crude but it's close enough that my daughter was like 'This is Peppa Pig.''

Another video depicted Peppa Pig and a friend deliberately burning down a house with someone in it.

All of these videos are easily accessed by children through YouTube's search results or recommended videos.

But the channel's videos include titled such as 'FROZEN ELSA HUGE SNOT', 'NAKED HULK LOSES HIS PANTS' and 'BLOODY ELSA: Frozen Elsa's Arm is Broken by Spiderman'.

Many of the videos feature graphic violence and toiler humour not appropriate for children.

"""
```
## example_output_explanation_id_1    
```
"""
  {
    "Country": "Worldwide", reasoning-> Youtube, including Youtube Kids, can be accessed in many countries. Though the incident is reported in the U.S., it doesn't mean the problem is limited to only the U.S..
    "State": "", reasoning-> The incident is nation-wide in the United States, not specific to one state, so leave blank.
    "City": "", reasoning-> The incident is nation-wide in the United States, not specific to one city, so leave blank.
    "Continent": "Worldwide", reasoning-> Youtube, including Youtube Kids, can be accessed in many countries. Though the incident is reported in the U.S., it doesn't mean the problem is limited to only the U.S.; therefore the result should be 'Worldwide' for continent.
    "Company": "Google LLC", reasoning-> Youtube is the company causing the issue in the article. Youtube is a subsidiary under Google, therefore the company is Google.
    "Company city": "Mountain View", reasoning-> Youtube is a subsidiary under Google and Google is headquartered in Mountain View.
    "Company state": "California", reasoning-> Mountain View is a city in the California state.
    "Affected population": ["Children on Youtube"], reasoning-> The incident affects children on youtube directly.
    "Number of people actually affected": "Unknown", reasoning-> There is no record of an actual number in the article text, we cannot know how many people are directly affected.
    "Number of people potentially affected": "Millions", reasoning-> There are millions of Youtube Kids subscribers at the time of the event. We estimate millions were affected.
    "Class of irresponsible AI use": "Disinformation", "Human Incompetence", "Mental Health", "Copyright Violation"], reasoning-> The classes in the taxonomy include "discrimination,human incompetence, psuedoscience, environmental impact, disinformation, copyright violation, mental health".
    We choose "Human Incompetence" because the engineers and administrators behind the platform have not well-regulated the videos, causing such an issue.
    "Mental Health" because the disturbing videos could potentially affect children's mental health.
    "Copyright Violation" because the videos use characters without permission such as Mickey Mouse and Elsa from Disney, and Peppa Pig fakes to portray disturbing acts in videos.
    "Subclasses": {
      "Human Incompetence":["Technical"], reasoning-> The subclasses of 'human incompetence' in the taxonomy example include 'technical' and 'administrative'. In this case it seems to be technical incomptence that allowed this type of inappropriate content to surface.
      "Mental Health":[], reasoning-> 'Mental health' doesn't have a subclass in the taxonomy, so it should be left empty.
      "Copyright Violation":[], reasoning-> 'Copyright Violation' doesn't have a subclass in the taxonomy, so it should be left empty.
    },
    "Sub-subclass": [], reasoning-> There are no sub-subclasses of the subclasses listed in the taxonomy, therefore this field should be left empty.
    "Area of AI Application": "content filtering", reasoning-> The area of AI application here is content filtering.
    "Online": "Yes", reasoning-> Youtube is an online platform, therefore this incident is in fact an online incident.
  },
"""
```

## example_output_id_1    
```
""" 
  {
    "Country": "Worldwide",
    "State": "",
    "City": "",
    "Continent": "Worldwide",
    "Company": "Google LLC",
    "Company city": "Mountain View",
    "Company state": "California",
    "Affected population": ["Children on Youtube"],
    "Number of people actually affected": "Unknown",
    "Number of people potentially affected": "Millions",
    "Class of irresponsible AI use": ["Human Incompetence", "Mental Health", "Copyright Violation"],
    "Subclasses": {
      "Human Incompetence":["Technical"]
    },
    "Sub-subclass": [],
    "Area of AI Application": "content filtering",
    "Online": "Yes"
  }
"""
```

## example_output    
```
"""
     "6": {
        "Country": "Worldwide", 
        "State": "", 
        "City": "", 
        "Continent": "Worldwide",
        "Company": "Microsoft", 
        "Company city": "Redmond",
        "Company state": "Washington",
        "Affected population": ["Twitter Users", "Online Community"],
        "Number of people actually affected": "Unknown",
        "Number of people potentially affected": "Millions",
        "Class of irresponsible AI use": [
            "Disinformation",
            "Discrimination",
        ],
        "Subclasses": {
            "Human Incompetence":["Technical"],
            "Disinformation":["Textual"],
            "Discrimination":["Data bias","Algorithmic bias"],
        },
        "Sub-subclass": {
        "Data bias":["gender","race","other"],
        "Algorithmic bias":["feedback loop", "optimization function", "other"]
        },
        "Area of AI Application": ["Chatbot"],
        "Online": "Yes"
    },
"""
```
