# Okta Workflows How-To: Customize your MS Teams messages
##### By [Bryan Barrows](https://www.linkedin.com/in/bbarrows89/)
---
Okta Workflows makes it easy to build automations that notify or alert your teams with connectors to services like Slack and MS Teams.

Someone recently asked, _"Why can't I add line-breaks to my MS Teams messages?"_

As it turns out, we need to leverage the Custom API Action card so that we can specify that our content is HTML, rather than text. 

With the default `Send Message to Channel` card, our content is sent as text and line-breaks are ignored. Writing our message in HTML allows us to include line-breaks, lists, headers, style our text with fonts & colors, and more.

---
We can use the `Text - Compose` card to write our HTML message.

![Text - Compose card with HTML message](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pk4ntvdyv0ci543er1mc.png)

We can use a pair of `Object - Construct` cards to construct our request payload. We create a message object that contains our message `content` and specifies our `contentType` as `html`. We then nest the message object in an object called `body`. 

![POST to your Teams endpoint](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0uciai24t7xmujxar87l.png)

The payload should look something like:

```
{
  "body": {
    "contentType": "html",
    "content": "<h1 style=\"color:#FF0000;font-weight:bold\">Attention!</h1> <p>Thanks for reading! &#127867</p>"
  }
}
```

Finally, we use the `Custom API Action` card to
```
POST /teams/{team-id}/channels/{channel-id}/messages
```

![Teams message result](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/l3hyoe23qmmlsgnoje30.png)

---

Additional Resources:

- [Teams API doc](https://learn.microsoft.com/en-us/graph/api/chatmessage-post?view=graph-rest-1.0&tabs=http)
- [How To Fetch The Teams ID And Channel ID For Microsoft Teams](https://www.c-sharpcorner.com/blogs/how-to-fetch-the-teams-id-and-channel-id-for-microsoft-teams)

---

Feel free to [download](https://github.com/bbarrows89/oktaworkflows/blob/main/guides/MSTeamsCAPIA/msTeamsHtmlCapia.flow) my example, [import it](https://help.okta.com/wf/en-us/Content/Topics/Workflows/build/export-import-flows.htm) and try it out - just update the Relative URL in the Custom API Action to point at your own Team and Channel. 
**_Download steps:_** 
* _right click "download" link above_ 
* _click "Save Link As"_
* _be sure the filename ends in `.flow`!_

---

Hope this helps! Find me on [LinkedIn](https://www.linkedin.com/in/bbarrows89/) or shoot me an [email](mailto:bryan.barrows@okta.com) if you have any questions. 

You can also join us at a [Community Office Hours](https://calendly.com/oktaworkflows) session to work through problems and ask questions - I'd love to see you there. 
