# COMPSCI705/SOFTENG702 HCI Project

This is the implementation built to support Group 14's research on project D2: Visualising and supporting uncertainty in emotion recognition displays. This project is supervised by Dr. Danielle Lottridge and supported by Dr. Gerald Weber. 

Web app is currently deployed at [hci.etinaude.dev](https://hci.etinaude.dev). Use ID '56' when prompted.

The purpose of our project is to provide a greater understanding of how the display of machine uncertainty affects a human user's response toward the classification of human emotion in written text. The approach we have when doing this is comparing the accuracy of classification of emotion in written text by providing different displays of uncertainty. 

We are currently designating two different focus groups. One will be presented with the emotion that a machine thinks is most prominent in the passage. The other group will receive information about various emotions and the certainty the machine has for each of them.
<br />
<br />
<br />
## Experimental Design

<p align="center">
  <img src="https://i.imgur.com/arjidk6.png" />
</p>

1. As the user enters the experiment, they will be asked to read the instructions and enter the user ID that was provided to them. They will then be asked to provide their consent to take part in the research experiment, clicking 'Agree and Proceed' if they consent.

2. When the user begins the experiment, a [GPT-3](https://openai.com/api/) machine generated text will be displayed to them.

3. A machine will then classify the emotion of this same text and display it to the user. This varies depending on the group in which the user is in. Group A is the treatment group, where emotion classification and machine uncertainties are displayed to the user, while Group B is the control, where only the emotion that the machine thinks is being displayed in the text is shown.

4. Following this, the user is given a custom text field to type what emotion they think was being portrayed in the text.

5. Next, the user will select from a finite list of emotions the emotion they think was being portrayed in the text - joy, love, surprise, anger, sadness, fear. 

6. The user will next fill out a custom text field explaining why they made their classifications.

7. Finally, the user will be asked to enter the confidence that they had in their answers on a slider. 0% for not confident at all and 100% for very confident.

8. After submitting, the user will do the same for 9 more stories - a total of 10.

<p align="center">
  <img src="https://i.imgur.com/knvoCdH.png" />
  Group A: Only machine classified emotion shown
  <br> </br>
  
   <img src="https://i.imgur.com/gBZrR2e.png" />
  Group B: Machine classified emotions and uncertainties shown
</p>

The results from all users from both groups will then be analysed. The effect of a display of machine uncertainty to users and how it affects whether or not they classified the given emotion from a written text correctly, and their confidence will be looked at and with findings compiled in a report.
<br />

## Experimental Preparations
### Research Question
To determine the direction of research, research gaps from the literature review were summarised. Multiple rounds of discussions were conducted within the team and with the supervisor. Initially, the team wanted to investigate the impact of a variety of different displays of machine uncertainty on human’s ability to classify emotions. After discussing with the supervisor, the team realised the necessity of controlling variables, and thus only two different kinds of display were chosen in the final experiment. Our research therefore looks at understanding
>How the display of machine uncertainty affects a human user's response and uncertainty toward the classification of human emotion in written text

Relevant Literature: 
- [Evaluation of Normal Model Visualization for Anomaly Detection in Maritime Traffic](https://www.researchgate.net/publication/261959138_Evaluation_of_Normal_Model_Visualization_for_Anomaly_Detection_in_Maritime_Traffic)
- [Recent advances and challenges in uncertainty visualization: a survey](https://www.researchgate.net/profile/Parashar-Dhakal/publication/353050061_Recent_advances_and_challenges_in_uncertainty_visualization_a_survey/links/60e867341c28af3458594a24/Recent-advances-and-challenges-in-uncertainty-visualization-a-survey.pdf)

### Implementation
Text emotion classification is the centre of this research project, to obtain text data the team utilised the Generative Pre-trained Transformer 3 ([GPT3](https://openai.com/api/)) to generate stories with emotions. Furthermore, to show machine emotion classification uncertainty, a hugging face emotion classification model [bert-base-uncased-emotion](https://huggingface.co/bhadresh-savani/bert-base-uncased-emotion) was used to generate six different emotion classifications with percentages. A web app was created for experiment participants to read stories and uncertainty displays and enter their emotion classification results. To reduce the waiting time for users, stories and machine classification results were pre-generated and stored on Firebase.

### Project Plan Discrepancies
As there is a slight difference between what was presented in the Project Plan Presentation and what was actually executed. There were three changes that were made.

<p align="center">
   <img src="https://i.imgur.com/jv4XFGS.png" />
  Initial project plan
</p>

Firstly, as described in the Research Question section, as there was a change to look at machine uncertainty and a human user's response to it in human emotion in written text, implementation had to change in order to match that. This meant that we were no longer showing to the user what the 'topic' of a story was, but rather showing what another machine that had classified the story thought. The second change that was made was to the user input. Rather than just selecting from a finite list of emotions, we include both a way for the user to write a custom emotion and a user input to show their own confidence/uncertainty in their answer. Finally, in the initial plan there was the option to see how the participant did compared to other users. As we did not want the results of one participant to affect another, this was removed from the implementation in order to keep testing valid and fair.

### Instructions and Consent
Detailed instructions and a Research Consent Form are included in the web app for users to agree to proceed with the experiment. The instructions include the time required for the participants to complete the entire experiment, the content of the experiment tasks, how the experimental data was generated, and how they should interact with the web app. In the consent form, participants agreed to statements such as to take part in this research and that they are able to withdraw their participation at any time and to withdraw any data traceable.

### Organising Test Subjects
Around 30 participants were recruited to complete the experiment. All participants are friends or family members of one of the team members. Participants were informed of the task, the time required, the research topic, and other relevant information in the Research Consent Form, and they only proceeded with the experiment if they agreed with the consent. 

### Testing
Participants were randomly allocated into two groups, control and treatment groups. Each participant is randomly assigned a positive integer from 0 to 100 as their user ID, participants with a user ID less than 50 are assigned to the control group, and the rest are assigned to the treatment group. To investigate the impact of the display of machine uncertainty, the control group is shown one emotion classification label (e.g. Happy) generated by the machine (the label with the highest percentage from the list of labels). In contrast, the treatment group is shown with a list of labels with percentages (uncertainty information). 

### Results
User-generated data is collected through the web app and directly stored in the Firebase database. No personal information is collected. Each participant was asked to provide three pieces of data for each question, the custom answer collected from a short answer input text box, the emotion label selected from a finite list of emotions provided collected from a multi-select drop-down list, and the confidence level percentage collected from a slider from 0% to 100%. To complete the experiment, each participant was required to complete 10 questions, in total, 30 data points were collected for each participant.

### Data Analysis
These are the following ways we can measure the uncertainty in emotional response.
1) By comparing the responses from various participants on each question.
Example: if we would like to understand which story has the most uncertain responses? We can consider the voting approach and count the emotion category in each question. Then apply statistical techniques to analyse the uncertainty. Example in following Responses, the story2 got less standard deviation than story1. We can conclude that story2 has more uncertain response. 

<p align="center">
   <img src="https://i.imgur.com/ei7GvwF.png" />
<img src="https://i.imgur.com/vcdPc97.png" />
</p>

Standard deviation of story1 responses is: 17.54

Standard deviation of story2 responses is: 15.34

Lesser the standard deviation, lesser the variations in responses. 

2) Comparing how far the user responses are from the machine learning based emotion classifier score.
3) How much the responses on each story deviated from Group A to group B.

![image](https://user-images.githubusercontent.com/64719560/195040480-b007fd71-d749-4995-b1a2-3c854e4455e7.png)



<br />
<br />

## Installation

1. Install node.js and npm then run:

```bash
npm install
```

2. Request keys from a dev and place the keys dir in `src/keys`.

3. Once you've created a project and installed dependencies with `npm install`, start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

4. To create a production version of our app:

```bash
npm run build
```

## Implementation Decisions
For implementation, we wanted to carry out the experiment with a large amount of people in a short time frame to an effective quality, as so opted for a lightweight tech stack.

- [Svelte](https://svelte.dev/)

Svelte was used because of its familiarity and lightweight nature in creating a highly functioning web application.

- [Firebase](https://firebase.google.com/)

A simple Firebase database was used in order to store the data from participant experiments as well as GTP-3 generated stories. Calls to the database are fast and efficient.

- [Netlify](https://www.netlify.com/)

The web application was hosted on Netlify. Simple and easy.

- [Cloudflare](https://www.cloudflare.com/)

DNS. Security and protection :)

- [GitHub](https://github.com)

Github is the most familiar and well-used version control used by the group and so was selected.

## Forms
All UAHPEC certificates can be found [here](https://github.com/etinaude/gpt3-hci-research/blob/main/Certificates.pdf):

<br />

## Developers

| Dev           | GitHub                                  |
| ------------- | --------------------------------------- |
| Etienne Naude  | [etinaude](https://github.com/etinaude) |
| Raina Song       | [rainasong](https://github.com/rainasong)  |
| Henry Gann      | [4hgann](https://github.com/4hgann) |
| Lance Zhang     | [lancelancezhang](https://github.com/lancelancezhang) |
| Yuwei Shen       | [alieevee](https://github.com/alieevee) |
| Balaram Panda |   [BalaramUOA](github.com/BalaramUOA) |


