

# There and back again: Introducing Architectural Katas to my workplace environment

## Prologue

I am part of a 5 person team of developers who primarily work on a monolithic repository. Therefore, we do not often flex our architectural muscles. I could feel myself going flabby after the long break from the process that went into Katas 1 and 2 during my fall semester architecture course.

While working through the design process of a new piece of functionality for our EMR integration, I began to notice parallels between our Kata exercises last semester. 

1. We are building an architecture from the ground up, given a list of requirements. 
2. Questions about these requirements were asked to our project manager, who always tried to be as helpful as they could be, but would often provide vague or unhelpful answers.
3. The Cloud would start to come into play somewhere.

For better or worse, the need of having to make a business case for our functionality had been decided for us.

After work, I found myself aimlessly meandering through my files and organizing them, sipping an overpriced IPA from a local brewery in the process. It was then that I stumbled upon my Fall 2021 semester directory and found katas 1 and 2. A lightbulb went off.

> "I could still participate in Katas by bringing them to my work team!"

The Kata is probably my favorite assignment from the MSSE program. It is a wonderful thought exercise, combining concepts like system design, networking, data modeling,  cloud computing, and teamwork. I immediately started scheming how to bring them into my workspace.

## Act 1: The Proposition

I met with the Director of Technology for our 1 on 1 the next day and brought up Katas. It turns out he had participated in them at his most previous job. They were a great opportunity for the team to work together and talk about software architecture paradigms that they would not have otherwise. I got the nod of approval to bring it to the rest of the team.

I pitched architectural Katas at our next development team meeting. It was met with a warm reception. I looked forward to arguing over monolithic vs. microkernel architecture with my coworkers over drinks and set the date for our first meeting.

## Act 2: The first Kata

Everyone was interested in joining except for the director. He is in meetings for about 6 hours a day as it is, so that is understandable.  As I was the only person who had done a kata before, I realized I would need to be a product owner and exercise lead for our first Kata. 

Our team comprised 3 back-end developers, including myself and the team lead, a front-end developer, and our cloud engineer. We began working through the [Make the Grade](http://nealford.com/katas/kata?id=MakeTheGrade) kata. Immediately, the team started to talk about how they would work on the data model, what AWS components we should use, and even the Python and Javascript frameworks that would be a good fit. I quickly and gently gave the team a hint: "I bet we can look at this prompt and figure out a bunch of questions that we have about the system for our product owner."

It was also an opportunity for me to see how team members interacted with each other. It quickly became obvious that there was some contention between our team lead and our front end developer. I overlooked this but kept it in mind moving forward.

The team started looking at the prompt critically. It wasn't long before they came up with a list of questions for their product owner. Here are a select few:

<u>Them</u>: "Will students take the exam on tablets or a traditional computer?" <u>Me</u>: "Both."

<u>Them</u>: "Can administrators be graders as well?" <u>Me</u>: "Yes."

<u>Them</u>: "How do we notify the parents of their student's standardized test results?" <u>Me</u>: "They can be alerted via email, SMS, or postal mail."

<u>Them</u>: "Does the district have on-premises requirements?" <u>Me</u>: "Define on premise." <u>Them</u>: "Does data need to be stored on a local server?" <u>Me</u>: "Yes. There is a large Oracle Database with records dating back to the 90s that lives in the basement of the district headquarters."

This went on for the first session and part of the second. We then started deriving use stories:

##### Institution Administrator

- Aggregate and submit student results for state reporting
- Add/Remove teachers or students
- Revisions of scale (answer correction)
- Can produce a PDF of the results for any given test and subset of students.
- Generate and print student test access "ticket"
- (re)Schedules instances of test occurrence
  - number of students
  - who are the proctors
  - date
  - location
  - communication
    - initial scheduling
    - new test location/date (if reschedule)

##### Teacher

- View results for their own students
- View students that haven't taken the test
- Grade essay
- Grade short answer
- As proctor:
  - generate/gather one time login codes for students

##### Student

- Take a test
  - Log into system
  - View questions
  - Submit essay
  - Submit short answer
  - Submit multiple choice

##### Testing Company

- Defend budget
  - Monitor costs of system and development

##### Test Maker

- Import test
- Create a test
  - Make essay question
  - Make short answer question
  - Create multiple choice questions and answers
    - Text and pictures in the answers and questions.

In conjunction with the user stories, the team derived the following assumptions:

- Administrators would have control over student hardware
- No control over grader hardware.
- Students may be registered ahead of time or the day of the the exam
- Administrator == IT Admin
- School system utilizes SSO via existing LDAP system.
- All systems are accessed via web browser and are optimized for mobile viewing.
- Role based access control teacher/admin have roles.
- Student does not have a role.
- A hosting center (from Additional context) is where the exams are taken, NOT a data center
- Test grades will be primarily sent via email, but with SMS and postal mail as an alternative.

It was at the end of our fourth meeting, and the team was ready to discuss using a microkernel as an architecture. 

*We have core functionality and (at least) 2 distinct systems (plugins) that will rely on some core functionality that will remain largely static after implementation (For the Make the Grade kata). We derive this assumption based on the fact that the requirements outline what the tests will do, and additional context dictates.*

> “A change approval processes involving three different government agencies is required for changes to the way student grades are kept to ensure security.”

*Once the core functionality is built, this thing will probably not change all too often.* - Me in Slack. 

I then linked to the [Microkernel chapter](https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/ch03.html) of Mark Richard's book and an [ADR Template](https://github.com/pmerson/ADR-template).

We decided to take a week off from Katas to focus on an upcoming software release. I was excited to see my small R&D project blossom into an exercise that my team could use when planning out new systems in the future.

## Act 3: The Tragedy

It was during that week that I found out that Neal Ford would be hosting an [Architectural Kata](https://www.oreilly.com/attend/architectural-katas/0636920054100/0636920054099/) event. It was perfect timing as it was difficult for me to play product owner and team member at the same time. I decided to bring up the opportunity at our weekly developer team meeting. 

> Sometimes, at the height of our revelries, when our joy is at its zenith, when all is most right with the world, the most unthinkable disasters descend upon us. - Darren McGavin, *A Christmas Story*

During our weekly developer team meeting, our team lead made an announcement. His last day with the company would be 2 weeks from that day. 

The next week, our front-end developer made an announcement. His last day with the company would be 2 weeks from that day. 

The remaining back-end developer would take the next week off to move to Seattle. 

With 2/5ths of the team leaving (and 1/3rd of the team being temporarily in dispose) we suddenly needed to pivot toward focusing on ensuring a smooth exit and transition.  

With many projects being put on hold briefly or indefinitely and quickly changing priorities, I chose not to schedule our next kata session. It would be difficult to do an R&D activity with so much else going on.

## Act 4: The Redemption

I took a day to help our remaining backend developer move. After helping him move a couch out of his living room full of moving boxes (and some terrible docker/Kubernetes jokes about all the moving boxes), I found myself sitting on the floor of his and his wife's now empty flat, drinking some beer that had been sitting in the office fridge since the pre-COVID times. 

He lamented to me about how he wished that we could have continued the kata and how hard it would be to rope the new team members into the process. A little later, we started talking about interview questions. Again, a lightbulb went off.

> "What if we used a Kata question in the interview process for our new team members!"

It would be a great way to gauge how well candidates could build and understand a system from the ground up. The only challenge would be timeboxing and making the exercise accessible. What world event could we possibly use that has demanded critical and adept thinking that a developer we have never met could relate to during the summer of 2021?

### The Pandemic Kata

A dangerous global pandemic has begun and is raging across the globe. To aid in early detection efforts to contain the spread, our company is creating virus test result-delivering software.

- Users: 
  - Billions of diverse end users.
  - Millions of diverse lab personnel.

- Requirements:
  - End users will be able to view their test results via Email. Phone, SMS, or within the app.
  - End users will be alerted via Email, Phone, App Notification, or SMS when their results are ready
  - If the Google/Apple Contact tracing Bluetooth system is enabled on their device, end users can utilize the [Exposure Notification System](https://www.google.com/covid19/exposurenotifications/) to alert others at risk.
  - End users can also share their results manually.
  - Lab personnel can upload thousands of test results to the system at once.
  - Integration with existing Lab Information Management Systems (LIMS) is critical.
- Additional context:
  - Users will access the application from anywhere on the planet.
  - We are dealing with Patient Health Information (PHI), so privacy is critical.
  - The Gates Foundation, Apple, Google, WHO, CDC,  and the European Union have contributed significant resources to the project. Budget and personnel bandwidth are of no concern.

## Act 5: The interview

We plan to give this prompt to interview candidates during the interview. This way, we can see their process from start to finish.

Obviously, we will need to emphasize that they do not need to build the entire system in an hour, but they must be able to build at least part of it and defend their choices. Ideally, we are looking for a candidate who has a strong understanding of what goes into building a software system, and the cloud infrastructure behind it, and knows what questions to ask. This means that my co-workers and I will work to steer the conversation, poking holes in the design and prompting explanations where appropriate.

## Act 6: Conclusion

Beyond the interview, I hope to bring Katas back to my dev team. Part of me wishes I stuck with my school group as it would have been less administrative work, but I feel like I have set things up nicely to continue doing Katas in the future. One thing that will come of using the Kata in an interview is that the new developers who join our team will have shown adeptness for them!

