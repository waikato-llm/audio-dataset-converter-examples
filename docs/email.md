Whilst most readers and writers are file-based, it is also possible to
retrieve and send emails using the following:

* `get-email` - retrieve emails from an IMAP folder, FROM and SUBJECT can be stored in placeholders
* `send-email` - send emails via SMTP, the from/to/subject/body options automatically expand placeholders

The connection parameters are obtained through environment variables that are stored
in [.env](https://github.com/theskumar/python-dotenv) files.

The following pipeline uses the `get-email` reader to poll the `audio` folder 
for new messages with WAV attachments every 5 seconds. These audio files get 
downloaded and then forwarded to the `send-email` writer that attaches
the audio files and then sends an email to the specified email address:

```bash
adc-convert -l INFO \
  get-email \
    -l INFO \
    -f audio \
    -o {TMP} \
    -r ".*\.(wav|WAV)" \
    -w 5 \
    --only_unseen \
    --mark_as_read \
    --from_placeholder FROM \
    --subject_placeholder SUBJECT \
  send-email \
    -l INFO \
    -f from@example.com \
    -t someone@anotherexample.com \
    -s {SUBJECT} \
    -b "Message from: {FROM}"
```
