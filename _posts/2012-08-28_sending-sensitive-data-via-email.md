[title: Sending sensitive data via email]: /
[alias: /2012/08/28/sending-sensitive-data-via-email/]: /
[date: 2012-08-28]: /

# Sending sensitive data via email  ###
A new site has come to my attention for sending sensitive data to another user. Assuming the site actually does what it says, this can be very useful.


<a href="https://noplaintext.com/" title="NoPlaintext" target="_blank">https://noplaintext.com/</a> takes a message, and provides a URL. They say the text is encrypted on your own machine, and then uploaded to their servers.

You then email the link to the recipient. They can click on the link <em>once</em> to see the contents. NoPlaintext then deletes the payload, so the link can only be used once.

The basic idea is they generate a hash. The hash is used for encryption locally, and also appears in the link. They claim they make no record of the hash.

The recipient also has the hash, so can run the decrypt to see the text.

Seems like a much better way to send passwords or other sensitive data through email. 

