# Secret handling

## A token pasted into chat stays readable there

- **Mistake:** A personal access token was pasted into a chat conversation.
- **Symptom:** The token remained visible in the chat history.
- **Root cause:** Chat is not a secret store, and only the sender can delete a message for everyone.
- **Fix:** Store the credential in a proper secret store, ask the owner to delete the message for everyone, and rotate the token: mint the new one, switch everything to it, confirm it works, then revoke the old one, in that order so nothing breaks.
- **Rule:** Never ask for a secret in chat, never echo one back, never reuse a secret that has been exposed. Collect secrets through a secure form.

## Keep tokens out of files, logs and commits

- **Rule:** A token is filled into memory at the moment of use and cleared afterwards. It never goes into a file, a commit, a log line, a report or a screenshot. Run a secret scan before every push.

## One-time codes and sign-in prompts

- **Rule:** Only trigger a sign-in when the owner started or approved it. Tell them exactly which site and account it is for, and that the code expires in minutes. Never ask for a code for an account they did not choose to connect.

## Delete old credentials only when you are sure

- **Rule:** After a rotation, delete only the entry proven to be the old credential. Leave anything whose purpose is uncertain and flag it.
