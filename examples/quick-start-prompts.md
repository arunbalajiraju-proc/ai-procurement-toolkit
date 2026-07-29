# Quick Start Prompts

Paste the relevant skill file into your assistant first, then use one of these below it. Replace the details with your own and remove anything identifying.

## Routing an incoming request

```
Run the AI buy routing diagnostic on this request.

A business unit wants to buy [what the vendor calls it]. The vendor
says it [what it does].

Data going in: [what the tool will receive, including what users are
likely to paste in without being told to]

What the output is used for: [who reads it and what decision it feeds]

We [do / do not] have an existing cloud commitment. This vendor
[is / is not] already under contract with us for something else.
```

## Routing AI that arrived without a purchase

```
Run the AI buy routing diagnostic on this.

One of our existing applications has enabled AI features through a
terms update. Nobody procured this. It is already live.

The application holds [type of data]. The AI features [what they do].

I need to know what route this is, what governance is now triggered,
and where our leverage is.
```

## Checking whether a request is really software

```
Run the AI buy routing diagnostic.

This came to us logged as a software purchase and I think it has been
mislabelled. [Describe what the vendor is selling.]

Tell me whether this is a software buy or an AI buy, and what changes
if it is the latter.
```

## Testing your own classification

```
I have run the routing diagnostic and classified this as
[route] at data tier [n], decision level [n].

Here is the situation: [description]

Challenge my classification. Tell me specifically where I may have
understated the data tier or the decision level, and what the
consequence would be if I have.
```

The last one is worth using more than it sounds. Understating the decision level is the most common error in this whole process, and it is the one a regulator asks about.

## Preparing questions for a vendor

```
Using the routing result below, give me the ten questions I should put
to this vendor in writing before we go further, ordered by what would
most change our position if the answer is bad.

[paste the routing output]
```

## A note on input quality

Every one of these gets better if you describe what the tool actually does rather than what the vendor calls it. Vendor naming is marketing. "Intelligent talent matching" and "resume ranking" are the same product with very different governance consequences, and only one of those phrasings will route correctly.
