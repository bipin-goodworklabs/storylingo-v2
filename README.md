# Storylingo (ekstep)

## Introduction

This project aims to revolutionize language learning for children by leveraging the power of Artificial Intelligence (AI). Designed to be engaging and educational, the project focuses on helping children learn a new language and improve their pronunciation through interactive reading exercises and AI-driven feedback.
```markdown
Key Features

    Interactive Reading Exercises:
        Children read words, phrases, or sentences displayed on the screen.
        The AI listens to their reading and provides immediate feedback.

    AI-Powered Pronunciation Detection:
        The AI detects correct and incorrect pronunciations.
        It scores the child's reading based on accuracy and fluency.

    Real-Time Feedback:

      During practice sessions, words that are not pronounced correctly are highlighted.
      This helps children identify and correct their mistakes in real-time.

    Assessment Mode:

      A game-like assessment where children read sentences displayed on the screen.
      The game includes limited lives, making it more challenging and fun.
      Each incorrect pronunciation costs one life.
      The objective is to complete the game by reading all sentences correctly without losing all lives.

    Engaging Gameplay:

      The game structure motivates children to improve their pronunciation to progress.
      It provides a fun and competitive environment to reinforce learning.

```


## Getting Started

### Prerequisites

- Node.js >= 20.x
- @mui/material
- [TheAll ai](https://theall.ai/)
- npm or yarn

### Installation

1. Clone the repository:
   ```bash
    git clone https://github.com/bipin-goodworklabs/storylingo-v2.git
    cd storylingo-v2


- npm install / yarn install
- npm run / yarn run dev


### Project Structure
Explain the structure of your project, including directories and their purposes.

```markdown
## Project Structure

   - src/                  # Source code
     - assets/             # Contains images and logos.
     - Badwords/           # contains the list of badword/cusswords which act as a filter.
     - components/         # Components for common element
     - config/             # (optional) for S3 bucket, and API constants
     - mechanicsComponent/ # component to display words with record and start button
     - routes/             # file defining different routes.
     - services/           # folder defining telemetry services. 
     - store/              # folder defining store for managing state
     - ui-components/      # common component for repetitive use.
     - utils/              # utility functions defined here.
     - views/              # folder for the component defining the pages.
     
     - App.jsx             # Main App component
     - index.js            # Entry point
   
   - package.json          # Project dependencies and scripts

```

markdown
## Configuration

1. **Project SetUp**:
   - Go to [Github](https://github.com/bipin-goodworklabs/storylingo-v2.git) 
   - change directory to storylingo-v2



### Running the Project

To start the development server:
```bash
npm start
# or
yarn run dev
```

#### Deployment
Instructions for deploying the project to a local environment.

  - You need to add these properties to the local storage manually
  -  token: 
```bash
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJlbWlzX3VzZXJuYW1lIjoiMTAxNDQwMDc4MyIsInN0dWRlbnRfbmFtZSI6InByYW5hdjEyMzQiLCJzY2hvb2xfbmFtZSI6IkNIU1MgS09ZQU1CRURVIiwic2VjdGlvbiI6IkIiLCJlbWlzX3VzZXJ0eXBlIjoiMTciLCJzdHVkZW50X2lkIjoiMTQ0MDA3ODMiLCJlbWlzX3VzZXJ0eXBlMSI6IjMxOTMiLCJzY2hvb2xfaWQiOiIzMTkzIiwiZW1haWwiOm51bGwsIm1vYmlsZSI6bnVsbCwidWRpc2VfY29kZSI6IjMzMDIwNTAwODA0IiwiY2xhc3Nfc3R1ZHlpbmdfaWQiOiI0IiwibWVkaXVtX2lkIjoiMTYiLCJncm91cF9pZCI6IjgwNyIsInN0YXR1cyI6IkFjdGl2ZSIsIm5ld3NjaGwiOm51bGwsImlhdCI6MTcxMTY5MDk4NywiZXhwIjoxNzE0MjgyOTg3fQ.sJC8wyif5PijCKZ_Epu8hhT-BD49NO8TC7xTiv2yRF8
```
Note: You can change the student_name property in the token using https://jwt.io/ for creating a new user.
  - lang: en
  - contentSessionId: 
```jsx 
once you will add the upper two fields in localstorage go to homepage and do a refresh after this open network tab you will get virtualID from generateVirtualID API then  `${usernameDetails.data.virtualID}${Date.now()}`; use this formula to create a contentSessionId and manually paste this in localstorage.
```

1. **Telemetry Service**:
   - Describe how to set up telemetry service.
   - Example:
```javascript
     export const initialize = ({ did }) => {
      if (!CsTelemetryModule.instance.isInitialised) {
      CsTelemetryModule.instance.init({});
      const telemetryConfig = {
        config: {
          pdata: {
            id: process.env.REACT_APP_ID,
            ver: process.env.REACT_APP_VER,
            pid: process.env.REACT_APP_PID,
          },
          env: process.env.REACT_APP_ENV,
          channel: process.env.REACT_APP_CHANNEL,
          did: did,
          authtoken: '',
          uid: 'anonymous',
          sid: '',
          batchsize: 1,
          mode: '',
          host: process.env.REACT_APP_BASE_URL,
          apislug: process.env.REACT_APP_API_SLUG,
          endpoint: process.env.REACT_APP_ENDPOINT,
          tags: [],
          cdata: [
            { id: '', type: 'ContentSession' },
            { id: '', type: 'PlaySession' },
          ]
          // ,
          // dispatcher : {
          //   dispatch: function (event) {
          //     console.log('Event', event);
          //   }
          // }
        },
        userOrgDetails: {},
      };
  
      CsTelemetryModule.instance.telemetryService.initTelemetry(telemetryConfig);
    }
  };
```


## Components Documentation

### Assesment

This component allows you to choose the language to start the assesment part.

Here's a detailed breakdown of what the component does:

#### Initialization and State Management
- Token and User Details:

      Retrieves the JWT token from local storage.
      Decodes the token to extract user details, specifically the student_name.
      Sets the profileName in local storage.
- React State Hooks:

      searchParams: Manages URL search parameters.
      profileName: Stores the profile name.
      openMessageDialog: Manages the state of a message dialog.
      level: Stores the user's current level.
      openLangModal: Manages the state of the language selection modal.
      lang: Stores the current language.
      points: Stores the user's points.
- Side Effects with useEffect

      Initial Setup:

      Sets the lang in local storage.
      Dispatches an action to set the virtual ID in the Redux store.
      Retrieves contentSessionId from local storage and sets sessionId.
      Conditional API Calls:

      If discoverStart, username, and no virtualId in local storage:
      Fetches virtual ID and milestone details for the user.
      Updates local storage and component state with fetched data.
      Generates a unique session ID if not already present.
      Fetches and sets the user's total language points.
      If virtualId is present:
      Fetches milestone details and points for the user.
      Redux and Navigation
      Uses useDispatch to dispatch actions to the Redux store.
      Uses useSelector to retrieve virtualId from the Redux store.
      Uses useNavigate from react-router-dom for navigation.

**Props**:
- no props needed

**Example**:
```jsx
import Assesment from '../../components/Assesment/Assesment';

<Assesment />;
```
### Assesment-end

The AssesmentEnd component in this code is responsible for displaying the end screen of an assessment in a learning application. Here's a detailed breakdown of what it does:

**Importing Modules and Assets**

- Layouts and Components: 
It imports various components such as MainLayout, ProfileHeader, and utility functions from different files.
Assets: It imports images, audio, and other assets like assessmentBackground, homeBackground, LevelCompleteAudio, etc.


- Component State Management

  shake: A boolean state to control the shaking effect.

  level: A string state to store the current level.

  previousLevel: A string state to store the previous level.

  points: A number state to store the total points earned.

- Side Effects with useEffect
Audio Playback: It plays the LevelCompleteAudio when the component mounts.

Fetching Data: It makes asynchronous HTTP requests to fetch milestone details and pointers (points) for the user.

Milestone Details: Fetches milestone details using the virtualId and lang from local storage and updates the level state.

Pointers Details: Fetches pointer details using virtualId and sessionId from local storage and updates the points state.

Local Storage Management: It retrieves and sets various data points in local storage, such as virtualId, lang, previous_level, and sessionId.

**Props**:
- no props required

**Example**:
```jsx
import AssesmentEnd from '../../components/Assesment/AssesmentEnd'

<AssesmentEnd/>

```
### DiscoverEnd

The SpeakSentenceComponent component in this code is designed to provide a celebratory end screen, likely after a user completes a language assessment or activity. Here’s a detailed breakdown of its functionality:

**Importing Modules and Assets**

- UI Components: 
External Libraries: It imports Confetti for a visual effect and axios for making HTTP requests.

Routing: It uses useNavigate from react-router-dom for navigation.

Custom Components: It imports a BackButton component and a LetsStart component.

**Component State Management**

- State Variables:

  shake: A boolean state to control the shaking effect.

  level: A string state to store the current milestone level.

- Side Effects with useEffect

  Audio Playback: It plays the LevelCompleteAudio when the component mounts.

  Fetching Milestone Data: It makes an asynchronous HTTP request to fetch milestone details for the user using virtualId and lang from local storage and updates the level state.

  Local Storage Management: It retrieves and sets various data points in local storage, such as virtualId and lang.

**Props**:
- no props required.

**Example**:
```jsx
import DiscoverEnd from '../../components/DiscoverEnd/DiscoverEnd'

<DiscoverEnd/>
```

### MainLayout

The MainLayout component is a React functional component that serves as a layout wrapper for various levels of a game or application. 

Here's a breakdown of what this component is doing:

**Props**:
- `level`
- `handleNext`
- `enableNext`
- `showNext`
- `showTimer`
- `showScore`
- `nextLessonAndHome`
- `cardBackground`
- `backgroundImage`
- `points`
- `progressData`
- `showProgress`
- `setOpenLangModal`
- `lang`
- `handleBack`
- `disableScreen`
- `isShowCase`
- `startShowCase`
- `contentType`
- `percentage`
- `fluency`
- `setStartShowCase`
- `livesData`
- `gameOverData`
- `loading`
- `children`

**Progress and Lives** 

The component calculates the current practice step and progress from progressData.

It determines how many lives to display using the livesData prop.

`**Example**:
```jsx
import MainLayout from "../Layouts.jsx/MainLayout";

<MainLayout
  showNext={false}
  showTimer={false}
  cardBackground={assessmentBackground}
  backgroundImage={practicebg}
  {...{
    setOpenLangModal,
    lang,
    points,
  }}
>
{props.children}
</MainLayout>

```
### Practice

The Practice component is a comprehensive React functional component designed for a language learning or assessment application.

- State Variables

    The component manages a significant number of state variables using the useState hook, which are used to track various aspects of the practice session:

- Page & Navigation

    page, setPage: Current page being displayed.

    navigate: Function to navigate between different routes.

    state: Location state for navigation.

- Audio Handling

    recordedAudio, setRecordedAudio: Stores the recorded audio data.

    temp_audio, set_temp_audio: Temporary audio object for playback.

    audioPlayFlag, setAudioPlayFlag: Flag to manage audio playback state.

- Story and Voice Interaction

    Story, setStory: Array to store the story data.

    voiceText, setVoiceText: Text from the voice input.

    storyLine, setStoryLine: Index of the current story line.

    voiceAnimate, setVoiceAnimate: Flag to animate voice input.

- Question Handling

    currentQuestion, setCurrentQuestion: Index of the current question.

    questions, setQuestions: Array of questions.

    enableNext, setEnableNext: Flag to enable the next button.

- Game and Assessment Data

    assessmentResponse, setAssessmentResponse: Stores assessment response data.

    currentContentType, setCurrentContentType: Type of current content (e.g., word, sentence).

    currentCollectionId, setCurrentCollectionId: ID of the current content collection.

    points, setPoints: Points scored by the user.

    sentencePassedCounter, setSentencePassedCounter: Counter for sentences passed.

    progressData, setProgressData: Data about the user's progress.

    level, setLevel: Current level of the user.

    isShowCase, setIsShowCase: Flag to indicate if the current session is a showcase.

    startShowCase, setStartShowCase: Flag to start the showcase.

    disableScreen, setDisableScreen: Flag to disable the screen interactions.

    mechanism, setMechanism: Mechanism or type of the current practice.

    livesData, setLivesData: Data about the lives left for the user.

    gameOverData, setGameOverData: Data when the game is over.

    loading, setLoading: Loading state.

    openMessageDialog, setOpenMessageDialog: Message dialog state.

    totalSyllableCount, setTotalSyllableCount: Total syllable count for content.

    percentage, setPercentage: Percentage of progress or completion.

    fluency, setFluency: Fluency score.


- Constants

    LIVES, TARGETS_PERCENTAGE, limit: Constants used in the component logic.

- Functions

    Game Over Handling: gameOver function to handle the game over logic and update state accordingly.

    Confetti and Sound: callConfettiAndPlay function to play a sound and trigger confetti animation.

    Content Fetching and Initialization: fetchDetails function to fetch initial data and set up the practice session.

    Next Question Handling: handleNext function to proceed to the next question, update points, and check for game over conditions.

    Back Handling: handleBack function to navigate back to the previous step or page.

    Audio Playback: Functions learnAudio, playAudio, playTeacherAudio to handle audio playback.

- useEffect Hooks

    useEffect hooks are used to handle side effects:

    Initial data fetching when the component mounts.

    Updating lives data.

    Responding to changes in voiceText to handle voice recognition errors or success.

    Setting up showcase or practice progress.

    Playing audio when temp_audio changes.



### SnackBar

This component is used to diplay customizable SnackBar notification

The CustomizedSnackbars function defines the component.

- State and Dispatch

    useDispatch: Initializes dispatch, which allows the component to send actions to the Redux store.

    useSelector: Fetches the following pieces of state from the Redux store:
    open, message, type from the snackbar slice of the state.

    virtualId from the user slice of the state.

- Event Handlers

    handleClose: A function to handle the closing of the snackbar. It checks if the reason for closing is a clickaway and, if not, dispatches the hideSnackBar action.

## Contributing

We welcome contributions! Please follow these guidelines:
```bash
1. Fork the repository.
2. Create a new branch (`git checkout -b feature-name`).
3. Make your changes.
4. Commit your changes (`git commit -m 'Add feature'`).
5. Push to the branch (`git push origin feature-name`).
6. Create a pull request.
```

## License

This project is licensed under. See the [LICENSE](./LICENSE) file for more details.
