---
title: Five separate approaches for documenting code
permalink: /docapis_code_strategies.html
keywords:
course: "Documenting REST APIs"
weight: 7
sidebar: docapis
section: docapiscode
path1: /doccode.html
published: false
---

In this section, we'll dive into approaches for actually documenting code. There are a number of approaches people take here, and I've covered five of them with examples and commentary.

* TOC
{:toc}

## Approach 1: Inline comments for *how*, conceptual code explanations for *why*

After reading the intro to this section ([When code is too complex to understand](docapiscode.html), one reader shared her approach to  documenting code. [Morgan Craft said](https://www.linkedin.com/feed/update/urn:li:activity:6561978466751913985?commentUrn=urn%3Ali%3Acomment%3A%28activity%3A6561978466751913985%2C6562329276002127872%29),

> I tend to split my documentation up into the 'how' (inline comments) and the 'why' (external markdown docs).

I think this general division and arrangement of of code comments makes sense. Separate out your explanations into two general categories: how and why. Then insert the *how* comments inline with the code (every 5-10 lines or so). In contrast, put the *why* comments into sections before or after the code.

This approach is insightful for a few reasons. First, it prompts you to consider the why. As technical writers documenting code (that others wrote), we might fail to consider the "why" behind the choices made. In fact, it might be difficult to even see what "why" questions exist. Why use this class instead of another? Why approach it like this? There tend to be many different ways to accomplish a similar end, so why go down this path rather than some other.

When you interview developers about the code samples, include a few "why" questions here:

* Are there other approaches that you rejected here? Why?
* Are users free to implement some other approach, or do we specifically want them to follow this method? Why?
* Why use this language/tool/framework/library rather than some other?

As for inserting comments regarding how, this tends to be somewhat controversial. If you're just explaining what the code is doing, it can be redundant to someone who reads the language. As discussed in [What research tells us about documenting code](docapiscode_research_on_documenting_code.html), some developers feel that some code (especially simple code) documents itself &mdash; its meaning is clear to those who read the language, without the need for explanation. However, this statement tends to cater to advanced users and doesn't cover complex code.

## Approach 2: Juxtaposed commentary in a third column

One huge challenge in writing code documentation is figuring out how to juxtapose your explanation of what's going on in the code with the code itself. Best practices for documentation in general involve placing helpful instruction next to the area of confusion, and here the common practice is to add inline comments peppered throughout code. But suppose you want a longer running commentary about what's going on in the code (because the level of complexity can't be relayed in a one or two line informal comment). How do you juxtapose the conceptual/explanatory information next to the code?

If your commentary dwarfs the code, you risk making the code unreadable. If you arrange the commentary in sections that come long after the code, you risk creating a chasm between the explanation and the code, such that readers won't know what parts of the code your explanation refers to.

One technique is to create an additional, third column in your layout. You devote the middle column to your conceptual explanation and your right column to the code. This way the code and the narration are juxtaposed such that readers can glance at the code while reading your conceptual explanations &mdash; in other words, the third column maintains the needed context between the code and explanations. Here's an example from Twilio showing this juxtaposed approach:

{% include course_image.html border="true" url="https://www.twilio.com/docs/authy/tutorials/account-verification-java-servlets?code-language=Java&code-sample=code-verify-an-authy-code-7&code-sdk-version=default#sending-a-token-on-account-creation" size="750px" filename="twiliocodedocexample1" ext_print="png" ext_web="png" alt="Twilio code documentation" caption="Twilio code documentation" %}

In this example, the conceptual content and steps appears in the middle column, with the code on the right, with a dark background behind the code to create visual contrast.

Some of Twilio's screens actually blur out the irrelevant code, allowing you to focus your attention on the right parts being articulated in the conceptual area, like this:

{% include course_image.html border="true" url="https://www.twilio.com/docs/authy/tutorials/account-verification-java-servlets?code-language=Java&code-sample=code-verify-an-authy-code-7&code-sdk-version=default#configuring-authy" size="750px" filename="twiliocodedocblurirrelevant" ext_print="png" ext_web="png" alt="Blurring out irrelevant code" caption="Blurring out irrelevant code" %}

One challenge with this juxtaposed approach is screen space. To pull off a third-column design, you need to occupy the whole screen, without margins. I'm surprised Twilio doesn't include a switch to collapse the left-side navigation, which would give more space for the code.

As is, the code is only partially visible. The code extends horizontally with an option to scroll right, but surely the designers must have cringed in developing a UI that involves a healthy dose of back-and-forth horizontal scrolling.

Additionally, implementing blur and focus views based on the point the user is at in the tutorial must be technically challenging and somewhat cumbersome.

Another challenge is that the code and explanations of the code rarely line up horizontally all the way down. Suppose you have one method in the code that occupies just a single line, but explaining this method occupies 30 lines of conceptual explanation. By the time the user reaches the bottom of the conceptual explanation, the referenced code is no longer juxtaposed. Now you not only have horizontal scrolling for the user to see the code, but you have to scroll up and down the column to locate the relevant code. Designing a UI to accommodate all of these moving parts not only seems challenging, but also puts more burden on the user as well.

Another challenge with this juxtaposed design is that code is often spread out across multiple files. The view on the design column doesn't indicate whether all the code appears in the same Java file or whether we're seeing code from multiple Java files.

## Approach 3: The Lego approach

Another approach is to build the code from the ground up level by level, which I'm calling the Lego approach. For an example of the Lego approach, take a look at this example from the eBay Shopping API: [Searching By Seller: Reviewing Information About A Seller](https://developer.ebay.com/DevZone/shopping/docs/HowTo/PHP_Shopping/PHP_FIA_GUP_Interm_NV_XML/PHP_FIA_GUP_Interm_NV_XML.html#step1).

{% include course_image.html url="https://developer.ebay.com/DevZone/shopping/docs/HowTo/PHP_Shopping/PHP_FIA_GUP_Interm_NV_XML/PHP_FIA_GUP_Interm_NV_XML.html#step1" size="750px" filename="ebayshoppingapiexample" ext_print="png" ext_web="png" alt="Lego approach shown through eBay Shopping API" caption="Lego approach shown through eBay Shopping API" %}

Their tutorial contains five steps:

> * Step 1: Set up basic files and folders
> * Step 2: Add code for making the GetUserProfile call and displaying the results
> * Step 3: Add code for making the FindItemsAdvanced call and displaying the results
> * Step 4: Add HTML and Javascript for the user interface
> * Step 5: Run the code

You start with a blank file. Then with each step, you add more and more code until you have a fully working example. The problem with this approach is that as a technical writer, you likely won't have the build-up logic that the developer followed. Developers will more likely just send you the finished piece of code to document, and then you might end up approaching it like I described in the [intro to this section](docapis_code_difficulty.html), where I divided my explanations of the code section by section. Tackling code explanations section by section won't necessarily match the Lego build order of the code, since code is non-linear. The code that appears at the top might have been like the icing on the cake for the developer's task &mdash; abstracting more complicated lines into variables that he or she chooses to use to reduce the code's complexity or to reuse parts more efficiently. Finished code often has logic that is abstracted away into variables or other referenced functions so that the final code remains cleaner and more concise, but also more opaque. Finished code is often too messy and confusing to document in any teachable way.

If you want to teach someone how to understand code, you have to start simple and work your way up. The next technique explains this approach through the metaphor of the nautilus.

## Approach 4: The nautilus approach

The nautilus approach is similar to the Lego approach, but rather than describing chunks of work that are tackled one by one into an assembly order, you describe the core, simple patterns that users need to know. You start with the simplest code and then let the project grow larger and larger as needed, like the growing spiral pattern of the nautilus' shell.

In a blog post explaining this approach, Paul Gustafson, who co-manages a technical writing staffing company in the Bay area called [Expert Support](http://expertsupport.com/), says that the nautilus provides a good metaphor for technical communication. The nautilus follows a spiral pattern (Fibonacci sequence) that allows it to start small and gradually grow larger and larger as needed:

{% include course_image.html url="https://commons.wikimedia.org/wiki/File:NautilusCutawayLogarithmicSpiral.jpg" border="true" filename="1920px-NautilusCutawayLogarithmicSpiral" ext_print="jpg" ext_web="jpg" alt="Nautilus" caption="Nautilus" %}

Paul writes:

> Fostering understanding, which is what technical communications is all about, happens most efficiently by following a similar pattern....
>
> When your understanding is small, you learn best when the first lesson imparts information for a small, simple task with traits importantly akin to the first nautilus chambers.
>
> ... The good news for the nautilus is that the small chambers follow the same basic plan as the bigger chambers. If the first tasks a learner masters are fundamentally similar to more complex tasks farther down the syllabus, the student begins to understand and apply those patterns. The sooner newbies learn to “think about things the right way,” the sooner they “get it,” which is exactly what both the instructor and the student want. ([Lessons from a cephalopod](http://expertsupport.com/2018/09/lessons-from-a-cephalopod/))

Following the nautilus approach, you start with the simple, core patterns and then build up more and more code around it gradually as needed. You don't start by describing the complex finished work from the get-go. That finished work likely involves all kinds of code abstractions and rearrangements for a clean, finished product. Instead, you start with the basic patterns, and then let users build out more complex code from those simple patterns.

I like this approach. The problem is that we often want to explain how the finished code works, taking a user through it all from start to end. We might have 500 lines of code that we want to articulate, but the nautilus approach would have us explain just several small pieces of that code. Hence there's an A to Z type of problem. We describe A (the simplest core pattern), but the end product is Z. How exactly do you get from A to Z? How do you get from the simple patterns that maybe occupy 20 lines of code to the monstrously complex code that spans 200 lines?

Here's the conundrum: To the technical writer looking at the finalized code, there's no clear sense of how the developer got there. We often can't decouple the Nautilus-like logic that the developer started with, which led him or her toward this more complex end. All we see is this complex end. How do you decompile the code to reconstruct the logic that the developer started with? How do you know what these initial nautilus patterns were that started the whole process? If you didn't develop the code, nor are you a developer, it will be nearly impossible to reconstruct the nautilus pattern behind the code.

As an analogy, consider a painting. Suppose your task is to describe a painting to a would-be painter.

{% include course_image.html url="https://en.wikipedia.org/wiki/Painting#/media/File:Mona_Lisa,_by_Leonardo_da_Vinci,_from_C2RMF_retouched.jpg" size="" border="true" filename="mona_lisa_painting" ext_print="jpg" ext_web="jpg" alt="How would you document the process of producing a painting?" caption="How would you document the process of producing a painting?" %}

Would you start at the top and work your way to the bottom? No, that would be ludicrous. Most likely you would start by creating ovals for the head. Then maybe some general sketches for the eyes, and so on. Maybe you sketch our perspective lines and other basic shapes first. You wouldn't get to the colors and lighting and shadows until later, right? Same with code. You start with the foundation and then work your way towards more of the finishing detail.

However, if you're not a painter, how would you know how to describing the process of creating a painting? You would need to know the painter's logic &mdash; where to start. If you instead just started at the end, the tutorial would likely seem insanely complex.

To illustrate this point more clearly, let me provide a code example. Although I'm not an engineer, I'm handy with Jekyll and theming, and the other day I set about creating a template that would take a content export from a ticketing tool (like JIRA) and render it as a documentation report.

My finished template looks like this:

```
{% raw %}
<div class="sprintDuration">{{page.duration}}</div>

{% assign sprintYamlFile = page.sprint_yaml_file %}

<div class="metaReportInfo" markdown="span">
Tech writers: {% for member in page.team_members %}<a href="https://somesite.company.com/users/{{member}}">{{member}}</a>{% unless forloop.last %}, {% endunless %}{% endfor %}<br/>
Team: <a href="https://ourteamsite.company.com/">DevComm</a><br/>
Sprint: <a href="{{page.sprint_link}}">Link</a>
</div>

<div id="top"></div>
<div class="all-items">

<h2 id="high-level-summary">High-level Summary</h2>

{{page.high_level_summary}}

{% include sprintdisplaylogic.html %}

{% assign sprintYamlFileOpen = page.sprint_yaml_file_open %}

<h2>Open Issues</h2>
<p>ACME project has <b>{{page.open_items_acme}}</b> open issues. Beta project has has <b>{{page.open_items_beta}}</b> open issues.</p>

{% include sprintdisplaylogic_open.html %}

{% include sprintstylesandscripts.html %}
{% endraw %}
```

This code looks kind of like gibberish, really. I have some "include" files where I've abstracted away the logic because I'll be repeating it from report to report. I don't want the scripts and styles showing here, as they'll clutter up the logic, so I've abstracted this away into include files as well.

Imagine trying to document this code. If you started from the top and worked your way to the bottom, it would be a real mess. The lengthy explanation would also be hard to read and understand for users. It's just confusing and like a ball of yarn. It doesn't help that I put this together in haste, without much thought for a clean, elegant solution. I needed to get this report out fast, so I hacked together the template as quickly as I could. Developers building applications often implement similar hacks and other quick-fixes using ["duct tape and WD-40"](https://www.joelonsoftware.com/2009/09/23/the-duct-tape-programmer/), as Joel Spolsky says, to get a working solution shipped to meet a deadline.

For example, in this code I couldn't get the usual table of contents tag that kramdown Markdown provides working:

```
{% raw %}
* TOC
{:toc}
{% endraw %}
```

So I just googled "TOC generator" and copied in some code I found online that worked on the first try. Unfortunately, the TOC generator only looks at a single level (such as `h2` tags), so nesting additional levels wouldn't be reflected in the TOC. Not a problem in my current template for the existing needs of the report, so I just noted the limitation in a code comment and moved on.

This kind of finalized code, with all of its quick hacks, is not instructive to someone looking to build their own report template. Instead, it would be more useful if I started from scratch with the core pattern. That pattern involves looping through a JSON file (the ticketing export) and pulling out the key values that I want to display. This key logic is available in the `sprintdisplaylogic.html` include above. Here's the contents of that include:

```liquid
{% raw %}
{% assign shortIdList = page.short_ids %}
{% for item in shortIdList %}
{% assign sprintItems = site.data.sprints[sprintYamlFile]  | where_exp:"entry",
"entry.ShortId contains item" %}

<h2 id="{{item}}">{{item}} Resolved Doc Issues</h2>
{% for entry in sprintItems %}
<div class="entryTitle">{{entry.Title}}</div>
<div class="entryIssueUrl"><a href="{{entry.IssueUrl}}">{{entry.ShortId}}</a></div>
<blockquote>{{entry.Description | markdownify }}</blockquote>
{% endfor %}
<small><a href="#top">↑ Back to top</a></small>
{% endfor %}
{% endraw %}
```

Even this is confusing, as I have some weird stuff going on here with variables inserted as brackets in YAML file references.

To really pare this down into the core logic, this is what developers would start with:

```
{% raw %}
{% assign sprintItems = site.data.sprints.someyamlfile %}
{% for entry in sprintItems %}
* {{entry.Title}}
* {{entry.Description }}
* {{entry.IssueUrl}}
{% endfor %}
{% endraw %}
```

This is the core logic of the report. It uses a `for` loop to look through items in a data file (accessed through `site.data.sprints.someyamlfile`), and Jekyll then prints them out with tags like `{{entry.Description}}`. Once you understand that, you can start building up more and more complex logic.

But if you didn't develop the code, it would be extremely difficult to pinpoint the core, simple logic that is the basic pattern of the code. Where did the developer start? What is the essential pattern to learn?

To gather this information, you need to interview the developer. And when you interview the developer, you need to understand the language and explanations he or she communicates. Alternatively, you can try to steer the developer towards this documentation approach through templates or other guidance.

Once users learn these core patterns, they can build on them to create more complex solutions, such as inserting variables into the loop so that you can repeat the looping without duplicating the loop for every report category manually.

As I said, the problem with the nautilus approach is that your documentation will teach the user the A, B, C parts of the code (the simple patterns), while mostly leaving the finalized code unarticulated. The documentation won't detail how we go to the X, Y, Z parts (the more advanced, finalized product). In that sense, there's more of a gap between your documentation and the code samples. But the documentation will likely be a lot more helpful and instructive.

You could start with these simple patterns and work your way toward the more finished code, but it will likely mean your documentation will be a lot longer and more extensive. Admittedly, this kind of documentation is more like a learning tutorial. A lot of times, your documentation will assume that the user is already familiar with these simpler core patterns.

### Decompiling the logic of the code

I've argued that documenting code requires you to peel back the finalized code to focus instead on the simpler logic that the developer started with. But if you're just receiving finalized chunks of code, how do you unravel the build logic that the developer proceeded through to get to that finished endpoint?

There are a couple of approaches. First, you could argue that all code in documentation should be simple, focused, and plain. There might not be a compelling argument for finalized, complex chunks of code in documentation in the first place. Save that more advanced code for sample apps.

But suppose there are good reasons for including lengthy advanced chunks of code in documentation. You could ask the developer to walk through how he or she built up to the code. If you follow this approach, chances are developers will quickly slip into advanced explanations and jargon and become impatient that you're unable to follow the logic. If basic concepts are totally unfamiliar, it is unrealistic for a beginning to simply soak in the explanation.

I highly recommend recording interviews where you ask an engineer to explain anything. This will allow you to go back and listen to the explanations in slow motion, hitting stop and rewind as much as you want. If the engineer mentions an unfamiliar concept, you could use that as a springboard for your own study. This will give you a map of a relevant list of topics to learn (rather than some course that might never get around to addressing the specific code you actually need to learn).

### What needs explanation and what doesn't

As you decompile the logic of the code to the simplest pattern, you will face another challenge: where to draw the line about what you explain and assume needs no explanation. This again is nearly impossible to answer without better understanding your audience, and chances are the engineer won't have any better sense of the audience than you, so the engineer will likely make the same assumption as technical writers often do &mdash; imagining a user not too unlike ourselves.


## Approach 5: Interactive browser experiences

With the shift toward teaching core patterns, I said this situates the documentation more as a tutorial or a learning module. Related to this is a category of coding interfaces that are executable in the browser. These browser executable UIs also have as their goal the aim to help users better understand the results of inputs and outputs so they can see for themselves through a more hands-on, try-it-for-yourself approach how the code works.

The most common example of interactive documentation for APIs is with Swagger UI, which I have already covered at length in [Introduction to OpenAPI and Swagger](pubapis_swagger_intro.html) and shown in the [Swagger UI Demo](pubapis_swagger_demo.html):

{% include course_image.html url="pubapis_swagger_demo.html" size="750px" filename="swagger-try-it-out-example" ext_print="png" ext_web="png" alt="Try it out button in Swagger's interactive REST API interface" caption="Try it out button in Swagger's interactive REST API interface" %}

Swagger provides an ingenious blending of documentation and try-it-out interactions that help users learn (by both reading and doing). But making requests with REST API endpoints tends to be somewhat simple. More extensive code tutorials will be harder to make interactive in the browser. Even so, some "Notebooks" (as they're often called) allow you to run code, specifically [Jupyter Notebooks](https://jupyter.org/). Jupyter explains:

> The Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations and narrative text. Uses include: data cleaning and transformation, numerical simulation, statistical modeling, data visualization, machine learning, and much more.

Google has some collaborative notebook options with TensorFlow documentation, which has operations that you can execute using Google Notebooks. In the following screenshot, you can see an option to "Run code now":

{% include course_image.html url="https://www.tensorflow.org/tutorials" size="750px" filename="tensorflowruncodenow" ext_print="png" ext_web="png" alt="Interactive code examples from TensorFlow" caption="Interactive code examples from TensorFlow" %}

Clicking "Run code now" takes you to Google's interactive notebooks that actually run the code in the browser:

{% include course_image.html url="https://colab.research.google.com/github/tensorflow/docs/blob/master/site/en/tutorials/_index.ipynb" size="750px" filename="tensorflowexperimentasyougo" ext_print="png" ext_web="png" alt="Google's interactive notebooks lets you run the code in the browser" caption="Google's interactive notebooks lets you run the code in the browser" %}

Although interactive notebooks look cool, they seem like a lot of work for something that could more easily be accomplished with a sample app. Instead of figuring out how you can compile Java code or some other language in the browser, why not just provide a sample app that users can download and then proceed through locally, using their own compiling tools and setup?

Sure, users might need to have some utilities and frameworks installed on their computer to make the sample apps run, as well as an IDE, but making code run in the browser might not fully inform users about all the required setup that will eventually be necessarily for them to make the code run locally. Browsers tend to be somewhat stiff and formal in what they can do &mdash; you often can't play around with the code too much. From what I've seen with the interactive notebooks, they mostly offer a "Run" button.


{% comment %}
## inline comments

https://hackaday.com/2019/03/05/good-code-documents-itself-and-other-hilarious-jokes-you-shouldnt-tell-yourself/

https://www.freecodecamp.org/news/code-comments-the-good-the-bad-and-the-ugly-be9cc65fbf83/

https://hackernoon.com/write-good-documentation-6caffb9082b4

https://medium.com/@andrewgoldis/how-to-document-source-code-responsibly-2b2f303aa525

https://hackernoon.com/write-good-documentation-6caffb9082b4 (what versus why)

links within code



scrolling focus

pop-ups

placemarkers [1]

diagrams (that screenshot)

layers approach. https://developer.ebay.com/DevZone/shopping/docs/HowTo/PHP_Shopping/PHP_FIA_GUP_Interm_NV_XML/PHP_FIA_GUP_Interm_NV_XML.html

split out files into tabs. https://stripe.com/docs/stripe-js


challenge is that any marker you put in the code can't be rendered as code itself. tricky from a tools perspective.


* **Formatting the code properly, and referring to various lines, is also a challenge.** You want to apply code syntax highlighting based on the code language but also based on code formatting for that language following standard conventions in that language (e.g., where to insert line breaks, spaces, capitalization, etc.). If you have 50-100 lines of code, referring to different aspects of the code is also challenging &mdash; you could conceivably refer to line numbers, if your samples have them, but that approach also has its problems. Do you wrap code or let the user scroll horizontally? How much do you pepper code with inline comments, writing for that opportunistic, experiential programmer rather than the systematic programmer who starts from page one?

*you need to use code syntax highlighting correctly to make the code readable.*
 *you have to use proper style formatting with white space and such*
*Is there any way to collapse the comments or to provide a way to expand the comments?*
With span or div comments, doesn’t this remove the ability to comment in the code. I think you’d need to give up your syntax highlighting, or maybe you … I’m not sure.*
- What if you could somehow provide an easy way to provide documentation right next to code?* *Like twilio? The dual pane, with code in focus.* *There is this paradox that the more you document, the more you interfere with the readability of the code.*
*there are lots of innovative things people are doing with code that wasn’t really possible before.*
What are some innovative techniques around code?*strip sample:* [Stripe.js and Elements | Stripe Payments](https://stripe.com/docs/stripe-js)
 What if code scrolls horizontally? Should you implement horizontal scrolling?*
 What is a Jupiter notebook?*[Project Jupyter | Home](http://jupyter.org/) [The evolution of Jupyter Notebook: Jupyter Lab – Mohtadi Ben Fraj – Medium](https://medium.com/@mohtedibf/the-evolution-of-jupyter-notebook-jupyter-lab-704f3e93230c)

 *Can you give people real-time feedback through validators, like Swagger Editor?*
 *Are line numbers really useful? Do people reference them?*

*should you highlight the code as a different color?*

*Here’s an example from eBay:* [Getting Started with Search: Specifying XML Results in a Shopping API GET Request](https://developer.ebay.com/DevZone/shopping/docs/HowTo/PHP_Shopping/PHP_FIA_GUP_Interm_NV_XML/PHP_FIA_GUP_Interm_NV_XML.html)

*How do you highlight or denote the parts of the code that a user needs to customize? What conventions or patterns are common with that?


How much height do you allow for code samples before you cut it off? Seems like it’s fairly common to cut it off at like 800px or so.*
3. *Here’s a key article:
2. *How do you dynamically insert API keys or other stuff into sample calls to make them more copy and pastable?*

 *When should you show scroll bars with code? A limit on the vertical horizon, on the horizontal axis? Should you shrink code so that it becomes smaller and smaller in the responsive view? Or like stripe should you make it not shrink so small but rather be a fixed width? Should writers about any need for horizontal scrolling, or is this okay? I don’t get any scroll bars on* stripe: [IBAN Element Quickstart | Stripe Elements](https://stripe.com/docs/stripe-js/elements/iban)

How do you allow users to navigate among comments in your code? Would the scrollto plugin really be a good idea?*
11. *How do you annotate code? Here’s an example:*
*This is from Android Programming for Beginners. Exploring the project's Java code and the main layout's XML code. This chapter provides a really interesting way to describe and document code. It walks you through more or less section by section. But the numbers allow you to expand with more depth. There are multiple layers here. Do you explain what packages are, and classes? We assume the user has this knowledge, right? But you have to understand what knowledge the user already has versus what knowledge the user needs. What does the user need to know? It is not readily apparent. There is no immediate task, or is there?*

 *Is the 3 column design an effort to try to provide narration of code separate from the code, to keep the two separated and easily scannable? Yes, this is a key point that you want to emphasize. How do you create a running commentary about code without interfering with the code itself. This is what has led to the 3 column display.*
2. *Are gists something you should be using?*
*Check out* [The Golden Rules of Code Documentation – Java, SQL and jOOQ.](https://blog.jooq.org/2013/02/26/the-golden-rules-of-code-documentation/)

*How could you implement the side by side scrolling technique with more regularity? I really think this might be the way to go. Problem is width, but maybe this is all right? Also, how to do code syntax highlighting while also having markers in the code that indicate narrative points?*

- it's hard to reference the code. you might want to refer to different parts of the code during conceptual explanations.  It could be useful to have some line numbers to reference this, but it might not be so wise to count on this for maintainability.

 {% endcomment %}