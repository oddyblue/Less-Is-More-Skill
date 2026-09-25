# Editing this repo

`skills/less-is-more/SKILL.md` is the skill and its only copy. Keep `agents/openai.yaml` beside it, and the README's summary and always-on rule, consistent with it.

When changing the skill:

- It is a way of working that lets agents delete boldly once they have checked, not a list of bans.
- It applies in full to any change whenever it is invoked; never make it depend on words the user has to say.
- Keep a sentence only if it changes what a strong model would otherwise do.
- Use plain words; agents repeat the skill's vocabulary in their replies.
- Apply it to itself: an edit should not make it longer unless new evidence earns the words.
- Keep the header valid for strict parsers: no colon followed by a space inside the description.
