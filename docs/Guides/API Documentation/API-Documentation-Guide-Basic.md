# API Documentation Guide Basic


## Create Comprehensive API Documentation
Can an API even be used without documentation? While technically possible, it’s through good API documentation that developers first experience an API and get to know its functionality. Whether your API is meant for internal use, exposed to partners, or fully public, developers will need complete and accurate documentation to best complete their integrations.

In this guide, we’ll cover the basics of documentation and the different types you’ll want for the comprehensive coverage developers require. We’ll also cover and look into API description documents as well as API description examples.

## What is API documentation?
API docs are the collection of references, tutorials, and examples that help developers use your API.

Your documentation is the primary resource for explaining what is possible with your API and how to get started. It also serves as a place for developers to return with questions about syntax or functionality. Your API docs have these answers.

Typically, documentation is hosted in a special section of your website, or its own API-focused portal. The content should be as widely accessible as it can be for your audience. If only developers within your own company use your API, its documentation is likely also internal. However, it should be easily discoverable. You shouldn’t have to know who to ask.

For APIs used outside your organization, make your documentation public. Even if you whitelist certain partners to the API, developers like to see what’s possible before discussing partnerships.

Once you’ve determined where these API docs will reside, you need to ensure they cover the needs of developers who will use them.

## Three Types of API Documentation
Your API documentation will have several types of content. Some is meant to show what’s possible to a developer considering an integration. Others will get those developers started quickly. And yet, good & simple API documentation should remain useful when that developer is deep into their work.

Your documentation must completely describe the API’s functionality, be accurate, educational, and inspire usage. It’s a big job that can roughly be broken down into three types:

- Reference and functionality
- Guides and tutorials
- Examples and use cases
We’ll discuss these in detail, but you can think of them as moving on a continuum of facts to context. A reference describes the endpoints of an API, it lays out all the pieces. Guides take some of those pieces and start to put them together, explaining why you’d use those parts. Finally, examples offer up a very specific solution, solving a common problem.

As you’ll see, the best API documentation nails all three of these types of content.

## Best REST API Documentation
Now that we know what types of documentation to look for, let’s look at some examples of great REST API documentation. For many years, two names continue to come up when discussing API docs: Stripe and Twilio.

Your API’s audience may not be as wide as either of these companies. You may only have internal developers or a few select partners. It’s still worth learning from the best, even if you won’t implement everything they have done. Stripe and Twilio have based their entire companies on developers successfully integrating, so they’ve placed a lot of attention on their documentation.

[Stripe’s API reference](https://stripe.com/docs/api/) has nearly become a standard for its completeness and browsability.

Each operation on an endpoint is described in human-friendly terms, along with the arguments developers pass to Stripe. Finally, a copy-paste request is shown, with an example response provided below.

![Image](../../../assets/images/APIDocumentationBasic-Stripe.png)


[Twilio’s guides](https://www.twilio.com/docs/quickstart) are notable for both their programming language coverage and how they walk you through step by step.

![Image](../../../assets/images/APIDocumentationBasic-Twilio.png)

Twilio keeps the code visible while you read the description of what’s happening and how to customize it for your needs. You can click through a step at a time or browse the code samples, which are described the way a developer would use them.

[Heroku’s examples](https://devcenter.heroku.com/start) are not an API, but worth mentioning for how well they cover the cloud platform’s supported programming languages.

![Image](../../../assets/images/APIDocumentationBasic-Heroku.png)

Each example is also accompanied by a guide, but what’s notable is Heroku walks you through cloning a git repository. By helping developers start with a complete app in their chosen language, Heroku quickly points would-be customers to a quick success.

One of the most important jobs of documentation is to help someone completely unfamiliar with your API. At the same time, you want it to remain useful for the developer who has already used your API. Of the three types of documentation, the reference most needs to remain relevant throughout a developer’s interaction with your API.