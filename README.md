## Engine for the emoji whisperer npm package
Building a search engine for emojis

## Implementation
The inverse word frequency ($iwf$) is calculated as:

$$
iwf(e, W) = \log \frac{{|W|}}{{|\{w \in W: e \in w\}|}}$$

where $|W|$ is the total number of words, and $|\{w \in W: e \in w\}|$
is the number of words where the emoji $e$ appears.

The median frequency ($mf$) is the median distance between a word an the
emoji.

The emoji-word frequency ($ewf$) is calculated as:

$$
ewf(e, w) = \frac{{\textit{{count of emoji }} e \textit{{ for word }} w}}{{\textit{{total number of emojis}}}}$$

where $f_{e, w}$ is the frequency of emoji $e$ given word $w$.

Finally, the score is computed as:

$$
score(e, w, W) = \frac{{iwf(e, W)}}{{mf + ewf(e, w)}}$$

$e$ corresponds to an emoji, $w$ corresponds to a word in the query, and
$W$ corresponds to the entire corpus from which the index was built.

Given an input query $Q$, the resulting emoji is calculated as:

$$
score(e, Q, W) = \sum_{{w \in Q}} \frac{{\textit{{iwf}}(e, W)}}{{\textit{{mf}}_w + \textit{{ewf}}(e, w)}}
$$

$$
\textit{{topEmojis}}(Q, W, n) = \textit{{top }} n \textit{{ emojis }} e \textit{{ sorted by }} \textit{{score}}(e, Q, W)
$$

See repository https://github.com/MagnusCardell/emoji-whisperer for an implementation of index in node.js
## Results
example input sentence and output 5 top scoring emoji groups
```
Who else is excited for the new Avengers movie? #MarvelFan,"😙👌, ✨, 🤝, 😂🤣, 🤷‍♂️🙏"
Can't believe how beautiful the sunset was today. #NaturePhotography,"💖, 😙👌🏼, 🔋, 😔🙏, 👌🏼👌🏼"
Dinner at my favorite sushi place #Foodie,"😭, 🙌🙌🙌, 🤞🏽, 👏🏻, 👏"
Throwback to my trip to Paris last summer #TravelDiaries,"😎🤙🏽, 🤘🏽, 🐝✊, 🙌🌅, 😎😂👍"
Feeling so blessed to have such amazing people in my life #Blessed,"😂🙌🏼, 🔥, ❤️🙏🏾💯, 😐✋🏼, 🇸🇴"
That was the best concert ever!,"😩👌, 👌🏽, 🤩🙌, 🤏🏼, 🤚🏼"
I'm scared of spiders.,"🙈, ✨🤞🏼, 😔🤚, 😃👋, 😁✌️"
My heart is broken.,"💙, ❤, 🍃, 🙏🏽😩, 🥰👍"
I can't wait for my birthday.,"💎🙌, ✨, 💪🏾🔥, 🔥🔥🔥🙌🙌🙌, 🇬🇹"
angry,"👺, 💢, 🗯, 😖, 😣"
love,"🙏🏽😃, 💘, ♥, ❣, 🏩"
hate,"👈🏽💯👁, 🙄👎🏼, 😈👌🏻🔥, ✋🏼🙄, 💪🏾💖"
food,"🌭, 🌮, 🌯, 🌶, 🌽"
hungry,"😭🖕, 😔🤚🏽, 😂😂😂😭, 😊👍👍❤️👍, 👍😭"
tired,"😫, 🛀, 🛁, 🛏, 😪"
excited,"🤑👏🏼👏🏼, 😭🙌🏻, 😩🙌🏼, 🤩🙌🏻👏🏻, 🤪🙌🏻"
work,"👏🏼👍🏼, ⌨, 🏢, 💻, 💼"
home,"🏴󠁧󠁢󠁥󠁮󠁧󠁿✌️, 👠👠👠, ✈️, 🏘, 🏠"
play,"▶, 🎴, 😂😂😂👏🏽👏🏽👏🏽, 💯🙌🏽, 😎👍😂😂"
game,"😎👍👍🇸🇻, ♠, ♣, ♥, ♦"
sports,"⚽, ⚾, ⛷, ⛸, 🎱"
music,"👏🏾👏🏾🥺, 🎙, 🎚, 🎛, 🎵"
movie,"🎞, 🎟, 🎥, 🎦, 🎫"
book,"📖, 📔, 📕, 📗, 📘"
travel,"⛩, ⛰, ⛱, ⛲, ⛴"
adventure,"🙏🏽🏈, 🙏🏾👍🏾😎, 🙌🙌🙌💙💙💙🔥🔥🔥, 😎🤙🏼, 😃🙏🏽"
family,"👨‍👩‍👦, 👨‍👨‍👦, 👨‍👨‍👦‍👦, 👨‍👨‍👧, 👨‍👨‍👧‍👦"
party,"🍷, 🍾, 🎁, 🎆, 🎇"
```

## Notes
Building index:
1. collect documents (sentences with emojis)
2. tokenize the documents
3. preprocess the tokens. lowercase, cleanup, english
4. Index documents with inverted index