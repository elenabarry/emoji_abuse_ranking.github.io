# Emoji Abuse Scores 

Inspired by the work of Novak et al. [1] who created the first emoji sentiment lexicon denoted as the [Emoji Sentiment Ranking](http://kt.ijs.si/data/Emoji_sentiment_ranking/). I have created the first [Emoji Abuse Ranking](https://elenabarry.github.io/emoji_abuse_ranking.github.io/), an emoji abuse lexicon which provides abuse scores for the 334 most frequently used emojis.

![Screenshot 2021-05-02 at 11 06 47](https://user-images.githubusercontent.com/53048127/116809577-8ef5f700-ab36-11eb-914c-770536b6a07a.png)

## Process
I used the corresponding dataset from the paper ‘Large Scale Crowdsourcing and Characterization of Twitter Abusive Behavior’ [2]. Each tweet is labelled as abusive/hateful/spam/normal by 5 CrowdFlower workers. Founta et al. [2] My focus was cyberbullying; therefore, I only included abusive, hateful, and normal tweets, and tweets labelled as ‘spam’ were removed.

To find out the underlying emotions of abusive tweets that used emojis, I calculated the probabilities of each emoji in the dataset to be in either an abusive, hateful, or normal context. 

I have followed Novak et al. process and calculated 334 new abuse scores of emojis from -1 and 1 on whether the emoji is present in a normal, hateful, or abusive context. 

I split the dataset into three equal sizes of abusive, hateful and normal tweets. After duplicates were removed, this resulted in 3000 tweets for abusive and normal categories and then a multiplier was used for the hateful category to upsample it. Emojis with at least 5 occurrences are included, resulting in a lexicon of 334 emojis. The abuse scores for the emojis with fewer than 5 occurrences are not very reliable.

Abuse labels can take one of three values: abusive ≺ hateful ≺ normal. Which correspond to a discrete, 3-valued variable c ∈ {−1, 0, +1}.

For each emoji, I was able to use these three labels to form a discrete probability distribution. The distribution components, p−, p0, and p+ denote the abusiveness, hatefulness, and normality of the emoji, respectively.

The number of occurrences N, of each emoji to appear in each label, c, allows a probability, pc, to be estimated. Multiple emojis in a tweet are counted.

The mean of the distribution gives an emoji it’s abuse score.

## A Worked Example

### Face with Tears of Joy 😂

I divided the dataset into equal 3000 parts of abusive, hateful and normal labels.

Number of the Face with Tears of Joy emoji 😂 in the dataset: 

* 😂 in abusive dataset = 2078
* 😂 in hateful dataset = 2376
* 😂 in normal dataset = 540

Total number of 😂 in all datasets = 4994

Then in order to find the probability of the emoji to appear in an abusive, hateful or normal context, I calculated the probability of each set: pc = N(c)/N

* Pabusive = 2078/4994 = 0.416
* Phateful = 2376/4994 = 0.476
* Pnormal = 540/4994 = 0.178

To create the abuse score I needed to find the mean of the discrete probability distribution: discrete probability distribution = P+ - P-

S = 0.178 - 0.416 = -0.238

## References 
   
[1]P.  Kralj Novak, J.  Smailović, B.  Sluban and I.  Mozetič, "Sentiment of Emojis", PLOS ONE, vol. 10, no. 12, p. e0144296, 2015. Available: 10.1371/journal.pone.0144296.

[2]A.  Founta et al., "Large Scale Crowdsourcing and Characterization of Twitter Abusive Behavior", 12th International Conference on Web and Social Media, ICWSM 2018, 2018. [Accessed 10 October 2020].

[3]"tutsplus/tablesorter", GitHub, 2021. [Online]. Available: https://github.com/tutsplus/tablesorter. [Accessed: 30- Apr- 2021].
