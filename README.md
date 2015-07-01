JSON FB Message Saver
========================

A python script to download the a conversation in FB.  The data Facebook provides in their version is limited. The output is in the a JSON format, separated  into individual parts.

Setup
=============

Run for both `message.py` and `all_messages.py`

1. In Chrome, open [facebook.com/messages](https://www.facebook.com/messages/) and open the chat history you would like to save.
2. In Chrome Developer tools, open the network tab.
3. Scroll up in the conversation until the page attempts to load previous messages
4. Look for the POST request to [thread\_info.php](https://www.facebook.com/ajax/mercury/thread_info.php)
5. You need to input certain parameters from this request into the python script to complete the setup:
  1. Set the `cookie` value to the value you see in Chrome under `Request Headers`
  2. Set the `__user` value to the value you see in Chrome under `Form Data` 
  3. Set the `__a` value to the value you see in Chrome under `Form Data`
  4. Set the `__dyn` value to the value you see in Chrome under `Form Data`
  5. Set the `__req` value to the value you see in Chrome under `Form Data`
  6. Set the `fb_dtsg` value to the value you see in Chrome under `Form Data`
  7. Set the `ttstamp` value to the value you see in Chrome under `Form Data`
  8. Set the `__rev` value to the value you see in Chrome under `Form Data`

Now downloading messages can proceed.

Downloading Messages
====================

1. Acquire conversation ID by opening [http://graph.facebook.com/{username-of-chat-partner}](http://graph.facebook.com/{username_of_chat_partner})
2. Copy the `id` value from there
3. For group conversations, the ID can be retrieved from the messages tab, as part of the URL. You must use `all_messages.py` instead.
4. Run the command `python message.py {id} 2000`, and put the value you retrieved for ID earlier

Messages are saved by default to `Messages/{id}/`

Known Issues
============

The script can have some trouble with very large conversations (>50k messages). Facebook seems to rate limit this, and returns empty responses. In such cases, the script will retry every 30s until it gets a valid response.

Occasionally, it may take the script several tries to get a valid response.

