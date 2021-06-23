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

Run the App
npm start

Steps breakdown for Challenge
1. Create React.js app
2. Inspect Package.json - Install dependencies 
                          a.(@material-ui/core, 
                          b. @material-ui/icons(optional), 
                          c. Axios.js(Fetching API, Video content files 
                          (Drupal CMS) node.js instance SSR
 3. App.js - create Class Component(state) instead of dummy function component (no state)
                          a. Created individual components to handle the over UI, which is React.js powerful features <Component (props)/> 
                          b. props: onSubmit(), passing video palylist to the main UI
                          c. map(videos in playlist) create new Item props, rendering listed videos
                          
  4. State management - using the Class component intial state={videos, videoplaylist, selection of videos in playlist} current/ user event listeners functions(event.target.value) Using setState({create object to hold response.data.playlist.items}) loading new video playlist
  5. Async/Await in Axios.js - Optional create separate JSX Elements/Components to handle the Drupal/Node instances SSR video playlist files.
  6. Events - onClick, HandleSubmit, onFormSubmit
  7. Lifecycle methods: Ensure the app loads properly one the Class component load is in ReactDOM.
  8. Playlist UI - fetching the data from src(Drupal) for this practical exercise I used my owm YT channel, SSR video content files to ensure resources, video content loaded fast and minimize any buffering issues. none discovered.
  9. Mapping through VideoPlayList Component (

    const VideoList = ({ videos, videoSelected }) //using arrown functions => {
      const listOfVideos //in playlist = videos.map((video, node) => //Arrow Functions loops through video playlist <VideoItem key={id}//required videos={video object}> )
    }
    return listOfVideos//UI Material design optional (Grid, Paper, Typography, Icons) //endless design solutions in the MD systems.
    
    App.js Class Component
    ---------------------
    
    //state
    state = {
        //Video array empty []
        videos: [],
        selectedVideo: null,
    }
    //Adding Lifecycle methods (ComponentDIMount()) to ensure the component loads after Class component loads properly / use to load search terms relating to HHS
    componentDidMount(){
        this.handleSubmit('Scholastic Donates Books to Winners of HHS Early Head Start Partnership Grants')

    }

    //Create function to select video / Class allow for data to pass to the current state
    onVideoSelect = (video) => {
        //Create object to fetch the data and the data pushed to current setState in playlist item selected video JSX Element
        this.setState({ selectedVideo: video});

    }

    //handleSubmit(searchTerm) props being passed (fetch data from YT APIv3) for demo only (replace with Drupal CMS node SSR) in async/await
    handleSubmit = async (searchTerm) => {
        //Await the response from YT API with Axios instance of the Fetch API (search {params: {q:searchTerm}} destructuring)
        //const response = await hhs_drupal.get('search', { params: { q: searchTerm }}); 
        //see what data response structure ()
        //console.log(response);

        //ne way
        const response = await hhs_drupal.get('search', {
            params: {
                part: 'snippet',
                maxResults: 5,
                key: 'API Key' optional,
                q: searchTerm,
        
            }

        });

        //console.log(response.data.items);
        //Now this.setState({videos: response}) destructuring the response{array[0]}
        this.setState({ videos: response.data.items, selectedVideo: response.data.items[0] });

    }
    ---------------------
    
    Mapping over Playlist Videos
    ---------------------
    const videoList = ({ videos, onVideoSelect }) => {
     //map through the list of videos
    const listOfVideos = videos.map((video, id) => <VideoItem onVideoSelect={onVideoSelect} key={id} video={video} /> )

    return (

        <Grid container spacing={10}>
        {listOfVideos}
        </Grid>        
        
        )  

}
-------------------------------

VideoPlayListDetail.js UI

const VideoDetail = ({ video }) => {
    if(!video) return <div>Loading...</div>

    //console.log(video.id.videoId);
    console.log(video);

    //Create dynamic data with back ticks `${}`
    const videoSrc = `https://www.hhs_drupal/node_instance/${video.id.videoId}`

    //conditional statement to check for video in playlist, if not return an empty <div>
    return (
        <React.Fragment>
            <Paper elevation={6} style={{ height: '70%' }}>
            <iframe  frameBorder="0" height="100%" width="100%" title="Video PlayList App" src={videoSrc}/>
            </Paper>
            <Paper elevation={6} style={{ padding: '15px' }}>
            {/* Fetching data (video.snippet.title, video.snippet.channelTitle, video.snippet.description) */}
            <Typography variant="h4">{video.snippet.title} - {video.snippet.HHs_Title}</Typography>
            <Typography variant="subtitle1">{video.playlistVideoTitle}</Typography>
            <Typography variant="subtitle2">{video.description}</Typography>
            </Paper>          
        </React.Fragment>
    )
}
-------------------------------

VideoListItem.js

   const VideoItem = ({ video, onVideoSelect }) => {
    return (
        <Grid item xs={12}>
            {/* //Arrow function onClick event  allow user select and play video in playlist*/} 
            <Paper style={{ display: 'flex', alignItems: 'center', cursor: 'pointer'}} onClick={() => onVideoSelect(video)}>
                <img style={{ marginRight: '20px'}} alt="thumbnail" src={video.drupal.url} />
                <Typography variant="subtitle1"><b>{video.hhstitle}</b></Typography>
            </Paper>

        </Grid>
    )
} 

PlayListVideoSearch.js
    ---------------------
      //Managing state of the searchbar
    state = {
        searchTerm: '',
        //Use state modifiers based on state components
    }

    //Bind to scope to class in Arrow Function workaround (accepts one value (e) event) (implicit)
    handleChange = (event) => 
        //this will refer to the class component -setState above for the state = {current state of searchTerm} in state=[]
        //setState(searchTerm) change at the current view state
        //console log the search term value being passed to the event listener(event.target.value)
        //console.log(event.target.value);
        //This will update the state and pass the value of the SearchTerm input onChange(lifecycle input methods)
        this.setState({ searchTerm: event.target.value});
    //HandleSubmit Arrow Function when form is TextField input passed search term (fetch SearchTerm) from the state
    //Destructuring ES6 (searchTerm) / onFormSubmit this.props
    handleSubmit = (event) => {
        const { searchTerm } = this.state;
        const { onFormSubmit } = this.props;
        //pass the props the searchTerm
        //. providing data to the onFormSubmit()
        onFormSubmit(searchTerm);
        //no refresh the the search bar input field

      
        //const { searchTerm, value, value1 } = this.state;
        //console.log(searchTerm, value, value1)
        //otherwise if not destructuring would be before ES6
        //console.log(this.state.searchTerm, this.state.value, this.state.value1);
        //console.log(this.state.value1);
        event.preventDefault();
    }
    
    --------------------
    
    
10. Wrap up:
            In this Practical Code execise demo components create included;
            App.js - Class Component(intial state functionality
            VideoPlayList.js - Displays the list of videos in Playlist
            VideoDetail.js - Displays the video content details (Drupal CMS instances will load own endpoints/file path mappings)
            VideoPlayListItem.js - Separating the components in modular best practices is the powerful and makes reactive frameworks so easy to troubleshoot and make changes instead large codebases.
            
Conclusion: I really like the this project, it gave me a chance to create more React.js experience in thinking, documenting, and I decided to create GitHub repository for the great opportunity to showcase my JS framework skills and growing my approach to a more modern JS framework world. Thank you, Ty "Humble Developer"            
              





