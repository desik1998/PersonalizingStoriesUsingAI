# Personalizing Stories Using AI

This project/experiment attempts to personalize a story for a user based on their cultural settings. For example, if there is an original story in an American or Russian setting, we retain the core message of the story and apply it to a different setting such as Indian or European. Although sometimes, it might not be possible to adapt the original story to different cultural context, as part of this project, we've taken stories which have universal human values across different cultural contexts such as American/Russian/Irish/Swedish and applied them to an Indian setting. 

**This project also showcases the remarkable capabilities of o1, illustrating its ability to tackle complex use cases like story personalization and effortlessly generating a well-tailored personalized story with minimal user input. Also with many questioning how o1 can be leveraged for commercial purposes, this project introduces a compelling use case that people can utilize to generate money**

Here are our personalized stories (All of these stories are < 2000 words and can be read in <= 10 mins):
1. Indian Adaptation of the story [Hearts and Hands](https://americanliterature.com/author/o-henry/short-story/hearts-and-hands/) by American author O'Henry
2. Indian Adaptation of the story [Vanka](https://americanliterature.com/author/anton-chekhov/short-story/vanka/) by Russian author Anton Chekhov
3. Indian Adaptation of the story [Seflish Giant](https://americanliterature.com/author/oscar-wilde/short-story/the-selfish-giant/) by Irish author Oscar Wilde
4. Indian Adaptation of [Little Match Girl](https://americanliterature.com/author/hans-christian-andersen/short-story/the-little-match-girl/) by Swedish author Hans Christian Andresen

**What is actually being personalizated?** 

The characters/names/cities/festivals/climate/food/language-tone in the personalized version are all adapted/changed to local settings while maintaining the overall crux of the original stories. 

For example, here are the personalizations done as part of Vanka: The name of the protaganist is changed from Zhukov to Chotu, The festival setting is changed from Christmas to Diwali, The Food is changed from Bread to Roti and Sometimes within the story, conversations include Hindi words (written in English) to add emotional depth and authenticity. This is all done while preserving the core values of the original story such as child innocence, abuse, hope

### Benefits:
1. Personalized story has more relatable characters, settings and situations which helps readers relate and connect deeper to the story
2. **Reduced cognitive load for readers:** We've showed our [personalized stories](https://github.com/desik1998/PersonalizingStoriesUsingAI/tree/main/PersonalizedStories) to multiple people and they've said that it's easier to read the personalized story than the original story because of the familiarity of the names/settings in the personalized story.

### How was this done?

Most of the heavy lifting was done by the o1 model and that too using very simple prompting techniques. Steps:
1. Give the whole original story to the model and ask how to personalize for a cultural context. Ask the model to explore all the different possible choices for personalization, compare each of them and get the best one. For now, we ask the model to avoid generating the whole personalized story for now and let it use it up all the tokens for deciding what all things are reqd for doing the personalization.
Prompt:
```
Personalize this story for Indian audience with below details in mind:
1. The personalization should relate/sell to a vast majority of Indians
2. Adjust content to reflect Indian culture, language style, and simplicity, ensuring the result is easy for an average Indian reader to understand
3. Avoid any "woke" tones or modern political correctness that deviates from the story’s essence

Identify all the aspects which can be personalized then as while you think, think through all the different combinations of personalizations, come up with different possible stories and then give the best story. Make sure to not miss details as part of the final story. Don't generate story for now and just give the best adaptation. We'll generare the story later
```
2. Now ask the model to generate the personalized story
3. If the story is not good enough, just tell the model that it's not good enough and ask it to adapt more for the local culture. (Surprisingly, it does it without much prompt effort)
4. Some minor manual changes if we want to make


Here is the detailed conversations which we've had with o1 model for generating each of the personalized stories [[1](https://chatgpt.com/share/6762e3f7-0994-8011-853b-1b1553bc7f82), [2](https://chatgpt.com/share/676bd09b-12d4-8011-9102-da7defbff2b9), [3](https://chatgpt.com/share/6762e40a-21e8-8011-b32d-7865f5e53814), [4](https://chatgpt.com/share/676c0aca-04a0-8011-b81a-e6577126e1b9)]

### Other approaches tried (Not great results):
1. Directly prompting a non reasoning model to give the whole personalized story doesn't give good outputs
2. Transliteration based approach for non reasoning model:

   2.1 We give the whole story to LLM and ask it how to personalize on a high level

   2.2 We then go through each para of the original story and ask the LLM to personalize the current para. And as part of this step, we also give ```the whole original story, personalized story generated till current para and the high level personalizations which we got from 2.1 for the overall story```

   2.3  We append each of the personalized paras to get the final personalized story

   But The main problem with this approach is:
   1. We've to heavily prompt the model and these prompts might change based on story as well
   2. The model temperature needs to be changed for different stories
   3. The cost is very high because we've to give the whole original story, personalized story for each part of the para personalization
   4. The story generated is also not very great and the model often goes in a tangential way

   **From this experiment, we can conclude that prompting alone a non reasoning model might not be sufficient and additional training by manually curating story datasets might be reqd**. Given this is a manual task, we can distill the stories from o1 to a smaller non reasoning model and see how well it does.

   [Here](https://github.com/desik1998/PersonalizingStoriesUsingAI/blob/main/OtherApproachesCode/Personalized_Novel_Generation_POC_draft.ipynb) is the overall code for this approach and [here is the personalized story generated using this approach for "Gifts of The Magi"](https://raw.githubusercontent.com/desik1998/PersonalizingStoriesUsingAI/refs/heads/main/OtherApproachesCode/Gifts%20of%20Selfless%20Love.txt) which doesn't meet the expectations

### Next Steps:
1. Come up with approach for long novels. Currently the stories are no more than 2000 words
2. Making this work with smaller LLMs': Gather Dataset for different languages by hitting o1 model and then distill that to smaller model.
   * This requires dataset for Non Indian settings as well. So request people to submit a PR as well
3. The current work is at a macro grain (a country level personalization). Further work needs to be done to understand how to do it at Individual level and their independent preferences
4. The Step 3 as part of the Algo might require some manual intervention and additionally we need to make some minor changes post o1 gives the final output. We can evaluate if there are mechanisms to automate everything

### How did this start?
Last year (9 months back), we were working on creating a novel with the Subject ["What would happen if the Founding Fathers came back to modern times"](https://github.com/desik1998/NovelWithLLMs). Although we were able to [generate a story, it wasn't upto the mark](https://github.com/desik1998/NovelWithLLMs/blob/main/Novel.md). We later posted a post (currently deleted) in Andrej Karpathy's LLM101 Repo to build something on these lines. Andrej took the same Idea and few days back tried it with o1 and [got decent results](https://x.com/karpathy/status/1868903650451767322). Additionally, a few months back, we got feeback that writing a complete story from scratch might be difficult for an LLM so instead try on Personalization using existing story. After trying many approaches, each of the approach falls short but it turns out o1 model excels in doing this easily. Given there are a lot of existing stories on the internet, we believe people can now use the approach above or tweak it to create new novels personalized for their own settings and if possible, even sell it

### LICENSE
MIT - **We're open sourcing our work and everyone is encouraged to use these learnings to personalize non licensed stories into their own cultural context for commercial purposes as well 🙂**
