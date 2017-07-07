# Developing Software in Thin, Valuable Increments
Developing anything larger than a moderate-sized tool can be tricky business.
Larger-scope requirements are more difficult to partition and implement,
integrations between large-scale components can become unwieldy to reason
about, and managing interpersonal or inter-team dependencies on a large project
is tricky.

This note hypothesizes that developing and releasing thin, valuable increments
is a critical tool in producing large-scale software. This note then posits a
few practical suggestions aimed at changing a team's culture to cultivate a
mindset of developing thin, valuable increments.

## Motivating Story
### Overpromising...
Several months back, I was tasked with an important project to migrate one of
our key components to a new vendor. The project was an interesting challenge
with ample business and technical ambiguity, and I was eager to prove myself.

I had grand plans. I immediately started by envisioning a new RESTful service
vending out the data consumed by our other systems. I excitedly jumped to a POC,
writing it in Clojure and publishing Atom feeds of vendor updates. Never mind
that it took 2-3 weeks of my 3-6 month estimate; this was a quality idea and any
time spent on a POC would be time saved in later development.

### ... and Underdelivering...
After spending three weeks on developing my very bare-bones POC, I presented my
idea to my team. I was so confident in my approach that I skipped the typical
requirements/possible solutions document and instead presented them with a
printed copy of a `README.md`.

My team's response was tepid. There was widespread confusion about what problem
I was trying to solve, why I was introducing unusual technology choices, and why
anybody should spend time on the project at that time. I walked away having
failed to convince my team about what I then considered a key component of my
project.

### ... and More Underdelivering
I tried salvaging my design and POC. I spent precious hours reading about
domain-driven design and in deep philosophical discussions about the fundamental
essence of our problem space.

After a week or two of this, I finally made a correct decision: I realized that
the POC I was so focused on was an ancillary part of my solution. I decided tha
I needed to create business value *now*. I could still improve the system as I
went but I needed to focus completing this project above all else.

Unfortunately, I made another critical mistake while executing on my new focus:
I was still so convinced about the soundness of my earlier design and POC that I
continuously distracted myself by rewriting major sections of code in
anticipation of a future launch of my super-awesome POC. Where I previously
resolved to do what it took to get this project done, I now repeatedly deluded
myself with, "It'll just be a day or two extra to rewrite this code to be
cleaner and work better with my super-awesome POC. It'll be time well spent."

### Faulty Assumptions, Ballooning Estimates, and Questionable Business Value
Everything fell apart while I was on leave five months into the project. I had
handed off my progress to two other devs on the team, meaning I dumped on them a
dozen lengthy CRs (with great commit messages!). The entire time I was on leave,
I couldn't overcome the nagging bother that my project had still not launched.

When I returned, not only had the project not launched but the delivery estimate
had been pushed back by an additional two to three months. It turned out that I
based all of my work on an assumption that was later rejected by our
stakeholders. I knew that I made this assumption; I had even mentioned it (in
passing) to a senior manager on an occasion or two. I knew that the rejection of
this assumption could seriously imperil my implementation, but rather than
challenge that assumption, I consciously doubled-down on it.

As my two poor teammates worked through the consequences of that assumption
being invalidated, an even more critical assumption was looking shaky: The data
they collected in their shadow testing indicated that the entire project did not
produce the business value expected. I want to repeat that for emphasis: *Their
data indicated that the anticipated business value --- the hoped-for benefit
that justified my paycheck --- might not actually happen.* Their data was only
preliminary and further refinements might actually deliver the promised value
but the possibility shocked me.

## Incremental Delivery
When I say incremental delivery, I mean producing value in phases. I mean
finding ways to release your work in such a way that you produce new business
or technical value every few weeks. I mean integrating your work into the
broader ecosystem every few weeks rather than waiting months to integrate.

Whether you write shrink-wrap software or cloud-based SaaS services, incremental
delivery provides valuable benefits. You can more quickly identify if your
project is not delivering the expected value. You eagerly integrate your work
into the broader ecosystem rather than postponing integration and the many
problems that inevitably come with it. You still provide some value even if your
project is cancelled partway though. You provide concrete deliverables that your
stakeholders or customers can immediately use and give early feedback.

Incremental delivery is hard. I have found that my brain likes to plan projects
in reverse of incremental delivery, progressing layer by layer through our stack
rather than considering units of business value. And some projects are more
difficult to dissect: I recently challenged a teammate to break a few of his
lengthy CRs into smaller increments. He explained that because of the way this
legacy code was structured, there was no smaller unit of value that he could
release; his lengthy CRs represented the most atomic unit of value he could
conceive.

Perhaps, then, the scope of an increment depends on the project. Some projects
can deliver early value by a simple rule change; others require more substantial
effort. Whatever the scope, teams should take the time to determine increments
that be delivered independent of each other.

## Thin, Valuable Increments
I first heard this concept called "thin vertical slices." I prefer the phrase
*thin, vertical increments*. I already explained what I mean by *increments*:
increments are discrete units of business or technical value.

*Thin* refers to the scope of the increment: making increments so small that
they are indivisible.

*Valuable* duplicates the definition of increment as "unit of business *value*,"
using repetition as a mnemonic device to emphasize that each increment should
add value to the system.

Put together, *thin, valuable increments* represents what I described in the
previous section: small chunks of business value that can be launched and
provide benefit independent of later work.

## Ordering of Increments
The order in which you work your increments is also important. In my motivating
story, my problem wasn't just that I didn't deliver value in small increments; I
also failed to adequately challenge the major assumptions on which my project
was based. My efforts to improve our code were highly commendable but
incorrectly timed: I could have more successfully met my deadline, earned the
trust of our stakeholders, *and* cleaned up our code if I had first completed
the job, gathered data on my critical assumptions, and *then* refactored the
code if my solution were deemed appropriate.

This isn't a new idea. I highly recommend *The Lean Startup* as an excellent
discussion of challenging your most critical assumptions first and failing fast
if those assumptions are invalidated. *The Lean Startup* argues that any work
that does not deliver value is waste; the key to avoiding work that does not
deliver value is to find out as soon as possible and to stop doing the worthless
work. The book talks of repeatedly iterating through a *build-measure-learn*
loop: *Build* the component that provides value, *measure* the impact of that
component, and *learn* if that component is still appropriate. (This is a gross
oversimplification.) But while you execute the loop in that direction, you must
*plan* the loop in the opposite direction: decide what you need to learn,
determine what data is necessary to learn that thing, and that plan what you
need to build to gather that data.

[![The Lean Startup describes a build-measure-learn loop through which you
should rapidly and repeatedly iterate.](http://theleanstartup.com/images/methodology_diagram.jpg
"Build-Measure-Learn Loop from The Lean Startup")](http://theleanstartup.com/principles)

So what should you try to learn? *The Lean Startup* says --- and I agree!
--- that you should first seek to learn if your foundational assumptions are
correct because getting those wrong could lead you to do worthless work. In my
motivating story, I should have started by challenging the project's most
foundational assumption, that the project would add business value. To learn
that, I needed to know what real-world business value was possible with the
project --- which meant that I needed to build the stupid thing and measure its
impact. As illustrated by the adage
[Make it Work, Make it Right, Make it Fast](http://wiki.c2.com/?MakeItWorkMakeItRightMakeItFast),
I should have first made the project work. It didn't have to be pretty or even
particularly robust: I just needed to be able to run a shadow test and gather
the real-world business value of the vendor migration. If the shadow test
confirmed the desired business value, then I could move on to the second step of
"Make it Right" by refactoring and adding new features.

To summarize this section: Deliver your thin, valuable increments in the order
that gives you the most valuable knowledge first, especially if that valuable
knowledge is foundational like "Will this project provide value?" or "Will this
approach satisfy the requirements?"

## Practical Suggestions for Individuals and Teams
These suggestions are all conjectures. I don't have enough experience to claim
that they will work; I hypothesize that these suggestions will help individuals
and teams to better deliver value by developing thin, valuable increments.

1. Explicitly encourage your team to focus on incremental delivery. You will
never be able to change a culture alone without getting members of your society
on board.
2. For every project you discuss, design you review, and story you groom, make
sure you understand the foundational assumptions on which that project, design,
or story is based. Assumptions are generally unstated, you may need to dig to
uncover and understand them. (Adapt the following questions for designs and
stories as well.)
   * "Why are we doing this project?"
   * "What is the success criteria of this project?*
   * "What might make this project fail?"
   * "What have you assumed in proposing this project?"
   * "Are there any uncertainties still in the project?"
2. For every project, design, or story, push yourself and your team to identify
the first, smallest, most indivisible unit of business value that will help you
challenge the biggest, most foundational assumption of the project, design, or
story. This is the
[minimal viable product](http://theleanstartup.com/principles) of *The Lean
Startup*. This suggestion is just a restatement of the *build-measure-learn*
loop mentioned in the previous section: Decide what you need to learn ("Is my
most foundational assumption true?"), decide what data you need to collect to
learn that thing, and then decide the smallest, quickest thing you can build to
gather the necessary data. Then move on to the next most critical assumption.
