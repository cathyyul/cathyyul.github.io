---
layout: single
title:  Lean startup notes (part 3)
categories: Reading-notes
tag:
- Reading notes
- lean startup
- book
---

The part 3 of lean startup talks about "accelerate", which is about systematic approaches for most quickly, i.e. with the least amount of efforts, improving the efficiency and driving out resource waste for value creating activities. The acceleration aims at helping a startup to answer the following questions asap:

- What products do customers really want
- How will our business grow?
- Who is our customer?
- Which customer should we listen to and which should we ignore?

Part 3 mostly covers the acceleration techniques:

- Chapter 9: small batches — Lean startups practice just-in-time scalability
    - Conducting experiments without making massive up front investments in planning and design
- Chapter 10: metrics to understand growth model
    - By identifying engine of growth a startup is using, it can direct energy where it will be most effective in growing the business
- Chapter 11: how to build an adaptive organization — five whys

Part 3 of the book also covers tips for developing a sustainable company, but I will keep the notes of this aspect in the next post.

## Batch

- It is important to work in small batches so that quality problems can be identified sooner
    - Design, develop, and ship one feature at a time
    - Conduct one experiment with one feature at a time
    - Batch size = how much work moves from one stage to the next at a time

- A startup should go through the whole cycle on one feature at a time. The goal of a lean startup is to learn as soon as possible to build a sustainable business — not to build or produce more efficiently.
    - Check for defects immediately, preventing much bigger problems later

- Techniques
    - Automated tests
    - Continuous deployment — Immune system is programmed to detect business consequences (instead of just functional tests) and automatically invoke Andon Cord. Example:
      - The defective change is removed immediately and automatically
      - Everyone on the relevant team is notified
      - The team is blocked from introducing any further changes until the root cause of the problem is found and fixed
    - Pull, don’t push, i.e. the famous Kanban idea
      - The key is we should not unlimitedly push to the queue, i.e. reduce work-in-progress (WIP)
      - Each queue should be limited and only when a hole is produced, i.e. some task is consumed, new ones can be pulled to fill it.
      - For startups, the requests in queue should be in the form of experiments that need to be run
        - Once we formulate a hypothesis, engineer to design and run experiment as quickly as possible using the smallest batch size that will get the job done
        - It is not the customer, but our hypothesis about the customer, that pulls work from product development and other functions
- Almost all lean startup technique works in two ways
    - By converting push methods to pull
    - Reducing batch size

## The engines of growth

- The engine of growth = the mechanism that startups use to achieve sustainable growth
    - Definition of sustainable growth: New customers come from the actions of past customer, i.e. not an one-time growth
- 3 types of engines of growth
    - Sticky engine of growth — rely on high retention and repeat usage
        - Churn rate: fraction of customers in any period who fail to remain engaged with the company’s product
        - Growth is defined based on
            - The rate of compounding = customer acquisition rate - churn rate
        - For sticky engine of growth, a startup should focus on engaging existing customer if acquisition rate is high enough
    - Viral engine of growth -- rely on person to person transmission as a necessary consequence of normal product use
        - Viral loop — speed is determined by
            - Viral coefficient = how many new customers will use a product as a consequence of each new customer who signs up
            - Viral coefficient > 1 means growing exponentially
        - For viral engine of growth, a startup can focus development efforts on things that might affect customer behavior and safely ignore others
          - Many viral products do not charge customers directly and rely on indirect sources of revenue because they cannot afford to have any friction impede the process of signing customers up and recruiting their friends
    - Paid engine of growth -- the revenue from past sales is used to acquire new customers, e.g. by advertising or hiring sales people
        - Customer lifetime value (LTV) = money a customer pays over his lifetime of using the product - costs
        - Cost per acquisition (CPA)
        - The key of growth: LTV > CPA
        - Note that usually CPA will increase due to competition over time. The ability to grow in the long term requires a differentiated ability to monetize a certain set of customers
- More than one engine of growth can operate in a business at a time

- Lean startup in the engine of growth aspect
    - Should focus on one engine at a time for startups
        - Only after pursuing one engine thoroughly should a startup consider a pivot to others
    - If you are still asking if you achieved product/market fit, you’re not there yet
    - A startup can evaluate whether it is getting closer to product/market fit as it tunes its engine by evaluating each Build-Measure-Learn cycle using innovation accounting.
        - What matters is the direction and degree of progress of the numbers, i.e. the trend.
- All engines eventually run out of gas — enterprises must adapt

## Adapt

- The goal is to build an adaptive organization so that the the organization can adjust its process and performance to current conditions
- Startup needs speed regulators to find optimal pace of work to balance between the tradeoff between quality and time

- Five whys method
    - Tie investments directly to the prevention of the most problematic symptoms
    - Make incremental investments and evolve a startup’s processes gradually
    - Step 1: Repeating why 5 times help uncover the root problem and correct it, e.g.

          1. Why did the machine stop? A: Overload and the fuse blew
          2. Why was there an overload? A: The bearing was not sufficiently lubricated
          3. Why was it not lubricated sufficiently? A: The lubrication pump was not pumping sufficiently
          4. Why was it not pumping sufficiently? A: The shaft of the pump was worn and rattling
          5. Why was the shaft worn out? A: There was no strainer attached and metal scrap got in

    - Step 2: Make proportional investment
        - Principle: the investment will be smaller when the symptom is minor and larger when the symptom is major
        - We make incremental improvements to the process constantly directly addressing the five issues uncovered. Each time reaping incremental benefits. Naturally if the problem is encountered again we invest more to the solution to the same issue
    - The five whys requires an environment of mutual trust and empowerment.
        - Be tolerant of all mistakes the first time
        - Never allow the same mistake to be made twice
        - Start small and be specific
            - Starting with narrowly targeted class of symptoms only when new problems come up
            - Keep the meetings short and pick relatively simple changes at each of the five levels of the inquiry
            - Everyone relevant to a problem needs to be at the session
            - Explain the process and how it works for people new to the process
            - Appoint a Five Whys master for each area which the method is used
              - The five whys master is the point person in terms of accountability and is responsible for assessing how well the meetings are going and whether the prevention investments made are paying off
