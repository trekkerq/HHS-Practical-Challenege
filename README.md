# HHS-Practical-Challenge
Hendall React Frontend Practical Exercise - VideoList Code Test

In this practical exercise for the React Frontend Developer code challenge.

<strong>Project Task Question for this React Code Challenge:</strong><br/>
Look at this page https://eclkc.ohs.acf.hhs.gov/playlist/highly-individualized-practices-series where each video is a node in Drupal 8 that includes a description and may include attachments and additional resources. Describe, providing as much technical detail as possible, how would you build the playlist functionality that appears on the page.

Main concepts in React include: 
- React JSX Components
- Project Structuring
- Lifecycle Methods
- State Management
- Props (parent-child) components
- Making API requests in fetching HHS Head Start videos via Drupal/Node model used for this project challenge. 

In this React Project, I will use the Google API/Youtube for real world testing of this concepts to use live fetched data from the Health & Human Services Channel, a link to test will available on my TrekkerQ Netlify hosted sandbox for review of this entire functional amazing app. 

Project Concept: Building a Video List React.js Component (parent-child) Video List item component to fetch live video from stored videos on the HHS drupal CMS SSR/node ecosystem, which will allow users to preview video playlist items stored in ReactJS state management utilizing the powerful React Hooks (UseState, SetState) to manage the current state (videoListItem) component will hold the current video until users trigger new selections video playlist items which will be handled by the UseState/SetState hooks to make the new search playlist item display in the HHS interface for viewing by end user. 

In my concept I will create a ReactJS application with several components:
VideoPlayListItem.js -  This JSX Component loads the single video playlist item.
VideoPlaylist.js - This JSX Component will load a predefined video list of HHS content videos for the end users to review each video content playlist item.
VideoPlaylistDetails.js - This JSX Component passing data (destructing properties include: videolist.id, videolist.details, videlist.item) props (videoplaylist details) to the useState([]) in a empty array structure, and setState([node:drupal stored array of videos in HHS playlist]).

Optional Structural Features: only a concept for the app inspired by this pratical code challenge.
-PlaylistSearch.js - Allows HHS users to perform search of videos in drupal cms content files, in the app I created it will fetch live video from many different API sources including SSR Drupal CMS, Public video platforms availablle via the web.


ReactJS setup, installation and build.
Setup - create-react-app {HHS-Videoplaylist-app}
With the Node Package Manager - npm i -g create-react-app (global install) allow for more reactjs structured components to run in the VirtualDom/ReactDom.
- install global for more apps
- Create-react-app ./ in file directory (documenting each set of instructions to ensure complete success is my best practice).
- Dependencies include Axios which is powerful set of fetch API functionality to streamline the API request with Promises/Async/Await
- Additional includes @material-ui/core, @material-ui/icons make the interface more immersive for the UX/UI experience for this concept only.
- Material UI is a React Components library for builidng components faster for web, mobile development allowing the developer to design their own system with Material Design guideline.


