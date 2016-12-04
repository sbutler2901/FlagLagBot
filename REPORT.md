##Presentation [40%]

Please click on the link to access our demo on YouTube:

Draft Version:

<a href="http://www.youtube.com/watch?feature=player_embedded&v=58RUjCtPUo8
" target="_blank">
<img src="http://img.youtube.com/vi/58RUjCtPUo8/0.jpg" alt="Demo Video" width="300" height="180" border="10" />
</a>

Final Version:



## Report [10%]
### Problem that is Solved

Feature flags can be a powerful continuous deployment tool for controlling features at run-time. There are many feature flag management systems, such as LaunchDarkly, that provide a nice web interface for toggling features. However, there is nothing to connect the management system to the code that uses the feature flags. Once feature flags are introduced in the code they can be hard to keep track of, and can cause problems if they are not removed properly when the feature is fully released. 

The FlagLagBot aims to bridge the gap between Launch Darkly and the code base that uses it. Our bot lives on a slack. A user can manage feature flags present on LaunchDarkly dashboard directly from the slack channel. Some of the actions requested by the user results in changes to the code on the GitHub repository 

### Primary Features and Screenshots
A user can request the FlagLagBot to perform an action by issuing a command.  The primary features of our bot can be summarized by the list the commands and their description found below:

* List flags: `list flags`
  * List all the flags that are visible on Launch Darkly Dashboard

* Create flags: `create flag <flag-key>`
  * Creates a new feature flag key on the LaunchDarkly Dashboard that can be used on the code base

* Delete flags: `delete flag <flag-key>`
  * Deletes a flag on the LaunchDarkly Dashboard. Triggers an alert for the user on the slack channel if they want to discard or integrate the feature flag code 

* Toggle flags – ON/ OFF:  `turn on <flag-key>` or `turn off <flag-key>`
  * Turn a feature flag on or off on the dashboard. A turned on feature means that code is visible to the users and is executed. A turned off feature means the code for the feature exists but is not executed. 

* Integrate Feature Flag: `integrate feature <flag-key>`
  * Removes reference to the flag and merges the code of the new feature into the original code base so it is part of the project

* Discard Feature Flag: `discard flag <flag-key>`
  * Removes reference to the flag and also deletes the code related to the new feature from the original code base permanently.

Additionally, there are two triggers that the bot presents to the users based on the webbooks that the server receives from LaunchDarkly.

* If a feature flag is turned on for too long, it sends a notification message on the slack channel
  * From here, the user can choose to integrate the feature into mainline code if they are interested or dismiss the alert.

* If a feature flag has been deleted on LaunchDarkly, the bot sends a notification message on the slack channel
 * From here, the user can choose to integrate the feature or discard the feature in order to avoid dead feature flag code and eliminate a dangling reference.

### Refelction on the Development process and Project

This project was a semester long project and tied in well with the material we covered in class. Having the project broken down into phases using the different milestones definitely helped in making the development process more manageable. It would have been a challenge if we did not have these milestones as a guiding reference points. We had a chance to go through a complete cycle – starting from design phase and all the way to the deployment phase in a systematic way.

**Milestone Design** – In the very beginning, as a team we were a struggling to come up with an idea that seemed to fit the criteria of a bot. The suggested topics on the course website was our starting point. We ended up choosing feature flags. It took a good amount of research to identify and understand one of the pain points that feature flags presented. However, we were glad that we invested time in understanding our area at this phase as it defined our project for the rest of the semester.  

Coming up with architecture design, a wireframe and storyboards for our bot had directly forced us to have a pretty good vision about where we were headed. 
 
**Milestone Bot** – In this phase on the biggest challenges was identifying the components and setting them up. We did have a good idea from the design phase. But when it came to setting the components up, we had to eliminate, redefine and specify them to exactly meet our requirements. For instance, we decided that we did not a database to maintain our webhooks information. Also, we had to set up a NodeJS server on one of the member’s raspberry pi in order to listen to the LaunchDarkly POSTS. Setting up our server and connecting to API provided by LaunchDarkly took some time. We had to request LaunchDarkly for permission since it was not available for our free trial. They responded quickly and extended our free trial privileges. 

The slack bot workshop, selenium testing workshop and mocking workshop materials were our resources to help us meet the requirements of this milestone. 
 
**Milestone Service** – By this phase, we had to have our three main use cases implemented.  The previous milestone covered one of the challenging aspects of the project. Since we had components identified and set up, our main challenge here was to connecting them. Connecting the components was important in order to define the work flow of any action. 

We were able to get the required 3 use cases completed on time. In addition we also had 2 more done. In the previous phase, we had outlined 8 use cases, so we had a lot to cover. By the end of this milestone, we had finished 5/8 successfully. The other 3 use cases defined, relied on the parser and the server notification to be working. There were members delegated to be working on specific parts on the project – Parser.js was started. We were using ESPRIMA to build an AST tree. However, the library we were relying on for the first couple of weeks did not work as we intended. The documentation was not specific. We had to explore into another option. This issue is documented in service.md. Also, the timer notification about a flag being turned on for too long was not yet working.  

**Milestone Deploy** – For this milestone, we had to not only finish the 3 use cases from the previous milestone, but also write scripts to pull and push changes to GitHub repo when a use case calls on the parser to make changes to code. Automating the script – without being prompted for credentials took some research. We also had to set up a public test repo and create credentials that we could use on the scripts.  Once we had the scripts in place, we had to test the use case that allowed the users to make changes to the code.
Another challenge in this phase as we were trying to wrap up the last 3 use cases was when we were trying to handle the flow – the promise and call back between components. The use cases that relied on changes being made in the code and being pushed required careful consideration. 

A part of our team was dedicated to deploying our project on the amazon ec2 server and writing the playbook, while another part was trying to finish the left over requirements from the previous milestone. Homework 5 and the workshop on ansible and vagrant were extremely helpful. This phase was very demanding as we had new issues crop up regularly and thus required us to spend a good amount of debugging. 

**Milestone Report** – Having a draft version of the demo ready for class helped us outline our presentation well. We took some time in adding effects and improving the flow for the final demo linked in this report. 

As we worked our way into a milestone’s requirements, we realized we were making significant progress towards the final project by taking calculated steps.  The project was a comprehensive experience and was tied in well with workshops/ material covered in the class throughout the semester.

During the development process, we used the GitHub Issue Tracker for setting up the use cases, assigning them and tracking our progress. As a part of every milestone requirement, we were updating the worksheet.md. However, the task list in there was more of an afterthought and thus did not help in planning our work ahead.  

We used slack as the main form of communication for setting up meetings, delegating tasks, checking on progress and debugging and posting when issues arise.  It was easier to delegate action items for bot, service, and deploy milestones compared to the design and report milestone were documentation was significant. For the most part, there were sections of the project we could divide and tasks to delegate, however, we had to meet and collaborate when we were putting them together. Our full team meetings usually happened in the last week before a milestone is due. This meant all of our schedules two days before the milestone deadline seemed loaded with work. 


### Limitations and Future work
Keeping in mind that we only have a semester and this is a three credit hour class, we were limited by the time we could spend on this project. If we had more time on this project, we could invest some to improve/ extend this project as follows:

We spent a good amount of time trying to explore the slack API for creating and using interactive buttons. We were successful in making them show up on our channel. Since we were running short on time, we could not invest any in trying to see how the click event will connect back our program’s control flow. Because we were using simple slack api from the beginning, using buttons meant we had to change other things as well. Switching to slack api would also make our code cleaner, but again time was our constraint. 

Currently FlagLagBot supports users to integrate feature flag code into mainline or discard feature flag code from the repository for java script files only. Some of LaunchDarkly SDK’s include: Go | iOS | Java | JavaScript | PHP | Python | .NET | Ruby. In the future, we could extend the bot to support code base written in other languages.  

## Peer Evaluations [50%]
All team members must individually submit a peer evaluation report.
