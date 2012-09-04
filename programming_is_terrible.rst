==============================================================
 programming is terrible. lessons learned from a life wasted.
==============================================================
:Author: tef

..
	outline

	introduction
	good and bad programmers
	how culture dictates code
	how we destroy learners
	learning to be good
	


Introduction
============

SLIDE:: intro slide, name, talk title

Hello. I am tef, and I am a bad programmer. 

I started programming because of a desire to take things apart and see how they worked. The more I learn about programming the more I am surprised *that* things work.

I am not a very good programmer. I forget to write tests, my documentation is sparse, and i'm pretty apologetic at any code review. I also write bugs. Lots of bugs. I have pretty high standards in the naïve belief that it is possible to write software that sucks much, much less than what we put up with.


SLIDE::
	good and bad programmers
	how culture dictates projects
	indoctrinating vs learning
	being successful vs being good

In as much as I'm here to complain, I am also offering survival tips and hope. 

I'm here to talk to you about mistakes I've made, mistakes other people make, and some of the mythology around programming. It's much more about the people than the code. I'll be taking questions at the end.

A standard disclaimer applies. This is my opinion and doesn't represent my employer, or reality.

SLIDE:: YMMV. HTH. HAND.

Some people have found my opinions useful, but for me they normally get me into trouble.

I'm also wrong a lot of the time. That didn't seem to be a roadblock for the majority of people who write about programming on the internet.

Let's begin with people being wrong on the internet. It's a good place to start.


Good and Bad Programmers
------------------------

..
	me/not me, language choice, political choice, 10x myth, penis having
	make mistakes, optimism, pebkac

SLIDE:: my code is better than your code (sing it)

Many blogs claim to elcuidate a dichotomy of programmers - good and bad. Upon careful inspection, most of them turn out to actually dictate the following types:

SLIDE::

    A. Programmers who are like me. 
    B. Programmers who are not like me.


The assertion is that if you cargo cult their personality, you too can be a successful programmer. Sometimes it is more veiled

SLIDE::

    A. Programmers who use my favourite language
    B. Programmers who do not use my favourite language

You may have heard this as 'the blub paradox'. 

ASIDE::
 
	the programmer who wrote this, left such a mess of lisp code that the
	company he sold its product to, switched to perl. they couldn't find anyone
	that could maintain his code.

	yes. perl was more maintainable.

	(he also claimed that if planes worked like lisp, 2001-09-11 wouldn't happen)

	(I am not making this up, he really said this)


Sometimes they just *imply* good and bad, without saying it outright.

SLIDE::

    A. Programmers who share my political beliefs
    B. Programmers who do not share my political beliefs

This one was spectacularly notable. It mashed everything into a simplified left/right view of politics.
And now programmers who don't understand programming are using political terms they don't understand
too. 

Why do we do this?  It’s easy and gets blog hits. Everyone loves a simple answer to a complex problem. Especially
when the two choices are emotionally charged. 

SLIDE:: 

	10x

Better still, when the good programmers  have magical super powers. You'll hear terms 
like rockstar, ninja, founder, entrepreneur, all used in the same pre-pubecsent machoism that our industrying
is drowning in.

Unfortunately, it's total bollocks. The 'some programmers are crazily more productive than others' comes
from a study, on batch processing vs interactive programming, in 1960.  On twelve people. In a half hour session.

We've been repeating this myth endlessly. it's destructive. it's either repeated by idiots who believe
they have nothing to learn from others, or repeated by learners to explain why they shouldn't try to learn.

*pause*

Really, when managers talk about 'A programmers' they mean people who will work long hours for little to no pay. 

*pause*

The worst sort of dichotomy is this

SLIDE::

	A. Programmers with a penis
	
	B. Programmers without a penis.

If any of you think this. Kill yourself now. This is not a joke. Just fuck off and die.


Studies (CITE) have shown, when you tell a group there is a genetic component to ability, the performance
goes down. People use this as a reason to avoid trying to improve, on both sides. 

If you believe in this divide in any way, it is highly likely that you are not only a terrible programmer, you are a terrible
person too.

I think that once we move past the issues like race, gender, within programming  we might have a chance
of handling tabs vs spaces.

*pause*

so, are there two types of programmers? Probably not, but if I was to try, i'd say::

SLIDE::

    A. Programmers who know they will make mistakes
    B. Programmers who think they will not make mistakes

I'm a little of column A an d a little of column B.  Sometimes I refuse to try, and sometimes I refuse to learn.

Really, the biggest mistake I make in programming is optimism.

SLIDE:: 'you would think that'

Optimism is the classic mistake programmers make, but it is often necessary because the task is so daunting.

 I am yet to meet a programmer who didn't chronically underestimate the time it takes to work.


Programmers like to complain, often starting “You would think that...” — Underlying this is the optimism that things can be better (Some like to think that they could have done better). Call me a cynic, but after years of fixing the bugs in software we are still no closer to fixing the behaviours in humans that propagate them.

SLIDE:: PEBKAC

The mistakes we make are in part due to the environments we work in. It is just as important to find out why the bug got written as well as how to fix it, if we are to have any hope of learning from our mistakes.

Software defects aren't endemic, they're systematic.


Culture Dictates Code
=====================


SLIDE::  quote Melvin Conway:

	    ...organizations which design systems ... are constrained to produce designs which are copies of the communication structures of these organizations

Essentially the software reflects the social structures of the teams that built it. If you need service orientated architecture, your teams should be structured around providing services to other teams, as opposed to delivering software or code. 

This raises its head in other ways - ‘God’ objects are often caused by ‘God’ programmers. People on the team who hoard responsibility for parts of the code and amass them into a lump. Frequently other programmers make small offerings to the object, and ensure that their code worships at its feet. 


It's not just individuals, sometimes, we make mistakes as a group, too.


SLIDE:: The Bike Shed

At a design meeting for a nuclear power plant, more time will be spent discussing the colour of the bike shed, than the technical details of the plant. 
The bike shed example first appeared in ‘Parkinson's Law’, under the ‘Law of Triviality’:

To be able to contribute to the techincal discussion, domain expertise is a requirement. To contribute to the bike shed, little or no expertise is required. No matter how well designed the bike shed, someone will always have a change in mind, and arguments will ensue.

The bike shed example first appeared in ‘Parkinson's Law’, under the ‘Law of Triviality’:

SLIDE:: “The time spent on any item of the agenda will be in inverse proportion to the sum involved.”

People love to contribute and feel that they have taken part in a discussion. As the barrier to entry lowers, more and more strive to take part in the discussion. Bikeshedding is the process of arguing over trivia, and how informed discussion is drowned in opinion. When everyone can contribute, nothing gets decided. 


SLIDE: The classic ‘Group Project‘

You have a group of friends. You all want to do something *together*. Everyone pools their ideas and then we'll all work on it.

Except if any of the ideas were motivating enough, someone would be working on them already. Effectively you're collating all the ideas that people think would be cool if someone else did it for them.

With no real individual desire to work, the project flounders. Collaboration tends to happen when someone leads by example. 

Leading by example doesn't mean coming up with ideas.  Ideas are cheap, plentiful and worthless. Ideas stand as a multiplier of work put in. Only with effort do ideas bring value. Even not so great ideas are successful with enough work. 

Sometimes, ideas is all the group has, and then you get...

SLIDE: Goon Project

Enthusiasm didn't get us to the moon, but we've got 18 logos and a wiki. A fatal group project popluated by idea guys and all discussions revolve around the colour of the bike shed.

When a lot of people want to solve a problem and don't know how, much of the bad ideas above surface and not much else. The most common cause of this is video games. Everyone has played them and not very many people have written them. A lot of enthusiasm goes a long way. Mostly "What should we call it", and "I can make a better logo"


SLIDE:: waterfall

It isn't just the individuls, and  structures within teams, the way in which we approach software developmet causes faults too. The Waterfall methodology was introduced as a strawman, and taken seriously and still used today. Mostly because it is easier to bill clients for than actually a good way to bill software.
Project Management is often an attempt to control reality rather than observe it, and react to it. Milestones are handed down upon high with little room for error, because maybe we'll get it right *this time*.


SLIDE:: Manhole cover

It is also evident in  how the company acquires workers. We struggle with finding good
programmers Often, companies resort to brainteases. I am asked ' What should I do when I am confronted with a brainteaser question in an interview?'

SLIDE:: CYA LATER SHITLORDS

Leave

ASIDE::

	There are a couple of experiments that show the context and framing of a problem have a massive effect on how people try and solve it (Wasson Selection Task). Brainteasers are not very effective at determining your ability beyond brainteasers. 

	Unless you’ve being hired as a quiz show host, brainteasers in an interview are mostly to make the candidate panic and see how willing you are to put up with bizzare or ludricrous requests.

	I’ve heard people justify them on this basis alone, because the job often involves bizzare or ludricrous requests from management, and they don’t like hearing “no”. 

	People tell me it happens at Facebook, they read it in some tech journalism.  The same articles were written about Google. Before then it was Microsoft.  Brainteasers make for an easy filler article, and so it’s quite a popular urban myth.

	It is a very effective warning sign of a terrible job. 


SLIDE:: cultists/occultism ?

Programming is not a science or an art, it’s rituals and cargo-culting at best. Our best practices amount to old wives tales from people who learned to program on punch cards, and we barely test our software, let alone our precious methodologies. At best, It's a craft.

Programming by and large is learned from maintaing existing software — fixing, testing, and adapting it, not creating it. That it not to deny the value of experimental programming, the adage ‘Top Down the second time’ still rings true. Often a prototype is needed to explore the idea, and understand the consequences of it. It is from maintaining this protoype you learn new approaches.

We don't just write bad code, we manage it badly and teach it badly.


teaching
--------

SLIDE::  teaching

Two largest influences on how programming is taught today are: nostalgia, and the way in which the teacher learns best. It’s a cargo cult approximation to education - do what I do and you will learn what I did.
	

Much of the discussion of education focuses heavily on “what students must know”, rather than more obviously “What do students want to learn, and how do they learn?”. A vital skill of the employed programmer is a willingness to learn on their own, and to explore. We need to encourage this from the outset, instead of dictating their course.

That said, a little guidance and help goes a long way.

This is more obvious in adult education - a teacher knows best attitude rarely earns you the respect of the pupils. I’ve learned much of what I know about programming by helping others gain an understanding. The teacher needs to cater to the pupils needs.
	
For a start, I’d like to see more appreciation for learning styles - the notion that some people prefer exercises to books, and some prefer talking to pictures. Many believe that the way in which you learn is the best way for everyone to learn. Most teachers will only teach in the way that they prefer, rather than teaching in a way that helps the students.
	

If someone asks you to teach them to program, ask them what they want to create, and then point them in the right direction.


SLIDE::
	learning through play

I encourage people to find a sandbox to play in. Be it a 2d environment with a turtle drawing pictures, or a musical environent, somewhere you can add elements and program them, as well as experiment or change existing programs quickly.

I try to focus on getting them to explain things to me and asking questions, rather than the drudgery of rote exercises. The computer should be a tool for learning and exploration, driven by the student.

I must confess that I too am tainted with a nostalgia — one of my earliest experiences of programming was in logo and I had fun.


SLIDE::	
	Seymour Papert and turtle

Logo was built by Seymour Papert to create a sort of ‘math world’.His idea was to give people an environment in which to construct their own rules and problems, and try to solve them, rather than a predefined course or structure to work through. Turtle graphics are the canonical example of the ‘math world’. A 2d box to draw in and play.

I’ve seen a similar idea espoused in math education. Currently it is treated as a death march through formulae to be inscribed into your brain, rather than actually trying to solve problems. Learning is more fun and rewarding when you get to be creative about how you go about it.

The other influence for me beyond Papert is ‘view-source’. I learned well from copying others and changing things. Fill in the blank exercises are boring to me, as are stepping through a problem in tiny chunks. I enjoyed taking something and tweaking it and manipulaing it to change the behaviour.

I learned a lot from reading other peoples code and changing it, more than I’ve learned from my own code. Learners need to be able to share and reuse examples easily. Programming is not just explaining things to the computer but working out how things work.


SLIDE::
	my first language

I would start with a relatively useful language from the outset, and by that I mean something::
    - that they can do something useful or fun within an afternoon. 
    - their friends know and can help them with. 
    - relatively easy to install and run.
    - that doesn’t require navigating an IDE.
    - that is general purpose.

I would advocate any popular scripting language - Python, Ruby, JavaScript, Lua.

Don’t worry about objects and classes too much. Worry about data structures and algorithms. Get simple functions working to make things happen.

Learning a language should be a side effect of some larger and more interesting goal. People rarely learn languages for their own merits.


SLIDE::
	REAL MEN USE C


C is a useful language. Many languages are implemented it it. Much of the libraries and operating system is implemented in it. Unless C is the only option for the project desired, I wouldn’t advocate it as a first language.

I don’t advocate it because it is hard to do anything immediately useful with it, in a small amount of time. Advocates seem to argue that “C is character building”. Great job! Suffering is such a great learning experience!

I would advocate *any* scripting language over C first. Even in the grizzly macho world of unix, people learn shell before they learn C. Using C effectively requires much more knowledge of the operating system.


SLIDE::
	Industry Standards.

Using C# and Java are difficult for vastly different reasons to C. For each of those languages, a simpler scripting language is available on the runtime, with access to the same libraries. 

Understanding Object Orientation requires a good understanding of procedural programming first. Focus on the basics before moving on to developing classes and objects.

Java, C# make better second languages.

People approach learning with caution, and they generalise on the initial experience. Often they learn with a predisposition for giving up - looking for an excuse to move on to something else. You see this all the time on forums - “Hi I am unconfident about my approach and I don’t want to find out the hard way”.


SLIDE::

	MATHS EH EH EH

Well, I’d say maths and programming are actually quite related, and the ignorance thereof is where we get things like floating point misconceptions. You need to understand as much mathematics as your program demands, which varies wildly. Not many programs have a high demand of math skills beyond counting. If you can use a spreadsheet, you probably know more than enough to start.

Part of programming is mathematical, not to say that differential geometry is somehow going to be useful, but reasoning about your program requires the same discipline of thought found in mathematics. I’m not saying that programers need to be mathematicians, but /are/ mathematicians (a class of). proofs are programs, innit.

Programming is ultimately an interdisciplinary set of skills: Programmers need to be able to write fluently, have critical reasoning skills, engineering dicipline as well as mathematical reasoning. Often overlooked is one of the most vital skills; Domain experience of the problem you are trying to solve. 



SLIDE::
	How do I become a successful programmer?

I'm not qualified to answer this question — I tend to burn out in jobs — but many other programmers I have met have managed to sustain employment and increase pay. I will share with your their winning strategies.

Although you will be forced to document your software, don't be afraid to write ugly prose, and ensure you leave out failure cases, or data types or arguments. Hopefully you will always be too busy to document and test the code. You have important bugs to fix.

Write lots of code. Lots of code. Autocomplete Helps. Use your own ad-hoc naming scheme. Write your own wrappers around standard library functions. Reinvent liberally. Learn to use the advanced features of your ide and language and use them everywhere. Don't be afraid to seperate everything out into modules that only make sense when combined.

Fix problems by creating new ones. Ensure that if you close the bug for now, someone new will re-open it. You can create an equilibrium by constantly shifting the problem around.

Ensure your tests only pass some of the time. Better if only on your machine with some elaborate setup. Become the central point of failure for the development — those who aren’t will be passed over or lose their job.

Job security comes from constant creation of work only you can do. If you act like you are the only programmer and this is the only bug you have, you will go far and be rewarded for your solipsist heroics of sabotaging the product.


SLIDE::
	How about being a good one?

Read code every day. Read other peoples code, in order to learn from someone elses mistakes.

To start with a terrible metaphor - if you met a professional writer you would expect them to be well read — the few I have encountered have a intimidating collection of books.  Before you are expected to write a novel, you should have read some novels. Same goes for code bases.

Yet with programming, much of the education and resources goes into the practice of writing code for the first time, and little towards analysis, debugging or maintenance.  

Programmers often complain that ‘we have to estimate things we’ve never done before’, I cannot help what part of this is due to our institutionalised ignorance of other peoples code and projects.


The only other advice I can relay is that you should write code as if it were mistaken, and you will have to change it, again and again. because you will.

Fail fast and repeatedly. It is easier to get something right by getting wrong a couple of times. It is easier to get it wrong a couple of times if you don't write so much code from the outset.

Try and think a little more about how the code will be called than how it works. It is far easier to change implementation over interface.

Don’t be an artist. Don't labour over the ‘right’ way to do things, but don't paint yourself into a corner.  Write code that is easy to replace, rather than extend. 

Bear in mind: It is OK to write ugly code. As long as the things using it don't have to write uglier code to use it.


As you get further in programming, you will understand the biggest problems are social, not technical. 


SLIDE:
	A final warning

the software industry is terrible, so is every other industry. retraining won’t help you escape people.

Thank you. Any questions?


