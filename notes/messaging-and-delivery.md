# Messaging and delivery

## A send can report failure after it was delivered

- **Mistake:** Treating an error or timeout from a send as proof the message did not go out, and sending it again.
- **Symptom:** The owner received the same message twice.
- **Root cause:** The message was delivered, but the confirmation was lost or arrived late, so the send was reported as failed.
- **Fix:** Before resending, read back the conversation to check whether the first message landed.
- **Rule:** Never resend on a reported failure without checking the thread first. A duplicate costs more than a short check.

## Email to the owner's inbox bounced

- **Mistake:** Emailing build artifacts (packages, zipped extensions) to the owner's personal inbox from a sending address the inbox did not know.
- **Symptom:** Repeated bounces. The artifact never arrived.
- **Root cause:** The receiving mail provider rejected the unfamiliar sender.
- **Fix:** Push the artifact to a repository and send the link instead. Separately, the owner can add the sending address to their contacts.
- **Rule:** Deliver files as links to a permanent location. Treat email attachments as a fallback, and check the delivery result.

## Chat apps will not carry every file type

- **Mistake:** Planning to send a zip over chat.
- **Symptom:** The file could not be attached.
- **Fix:** Put it in the project repo, as a release asset or a file in `dist/`, and send the link.
- **Rule:** Check what the channel accepts before promising a file over it.

## Deliveries need proof, not just a claim

- **Rule:** A delivery message is a short summary, the permanent link, and at least one real frame of the live build. See [qa-and-verification.md](qa-and-verification.md).
