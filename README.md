# PersonalizingStoriesUsingAI

This project/experiment attempts to personalize a story for a user based on their likely preferences. For example, if there is an original story in an American or Russian setting, we can retain the message of the story and apply it to a different setting for example Indian or European. Sometimes, it might not be possible to adapt the original story to different cultural context. But as part of this project, we've taken stories which have universal human values across different cultural contexts such as American/Russian/Irish and applied them to an Indian setting. 

### Benefits:
1. Personalized story has more relatable characters, settings and situations. This helps readers connect deeper to the story
2. We've showed our [personalized stories](https://github.com/desik1998/PersonalizingStoriesUsingAI/tree/main/PersonalizedStories) to multiple people and they've said that it's easier to read for the personalized story than the original story because of the familiarity of the names etc in the personalized story.

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

Here are our personalized stories:
1. Indian Adaptation of the story [Hearts and Hands](https://americanliterature.com/author/o-henry/short-story/hearts-and-hands/) by American author O'Henry
2. Indian Adaptation of the story [Vanka](https://americanliterature.com/author/anton-chekhov/short-story/vanka/) by Russian author Anton Chekhov
3. Indian Adaptation of the story [Selish Giant](https://americanliterature.com/author/oscar-wilde/short-story/the-selfish-giant/) by Irish author Oscar Wilde
4. Indian Adaptation of [Little Match Girl](https://americanliterature.com/author/hans-christian-andersen/short-story/the-little-match-girl/) by Swedish author Hans Christian Andresen 

Here is the detailed conversations which we've had with o1 model for generating each of the personalized stories [[1](https://chatgpt.com/share/6762e3f7-0994-8011-853b-1b1553bc7f82), [2](https://chatgpt.com/share/676bd09b-12d4-8011-9102-da7defbff2b9), [3](https://chatgpt.com/share/6762e40a-21e8-8011-b32d-7865f5e53814), [4](https://chatgpt.com/share/676c0aca-04a0-8011-b81a-e6577126e1b9)]

**This work also showcases a good usecase to use o1 model abilities for commercialization**

### Other approaches tried (Not great results):
1. Directly prompting a non reasoning model to give the whole personalized story doesn't give good outputs
2. Transliteration based approach for non reasoning model:

   2.1 We give the whole story to LLM and ask it how to personalize on a high level

   2.2 We then go through each para and ask the LLM to personalize the current para. As part of this step, we also give the whole original story, personalized story generated till current para and the high level personalizations which we got from 2.1 for the overall story. We then append each of the personalized paras to get the final personalized story

The main problem with this approach is:
1. We've to heavily prompt the model and these prompts might change based on story as well
2. The model temperature needs to be changed for different stories
3. The cost is very high because we've to give the whole original story, personalized story for each part of the para personalization

Prompting alone a non reasoning model might not be sufficient and additional training by manually curating story datasets might be reqd

TODO: Here is the overall code for this approach and here is a story generated which doesn't meet the expectations

### Next Steps:
1. Come up with approach for long novels. Currently the stories are no more than 1500 words
2. Gather Dataset for different languages by hitting o1 model and then distill that to smaller model.
   * This requires dataset for Non Indian settings as well. So request people to submit a PR as well
3. The current work is at a macro grain (a country level personalization). Further work needs to be done to understand how to do it at Individual level and their preferences
4. The Step 3 as part of the Algo might require some manual intervention and additionally we need to make some minor changes post o1 gives the final output. We can evaluate if there are mechanisms to automate everything

### LICENSE
MIT - **We're open sourcing our work and everyone is encouraged to use these learnings to personalize non licensed stories into their own cultural context for commercial purposes as well 🙂**
