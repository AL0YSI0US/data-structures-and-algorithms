> seattle-code-301n21/class-06]/**demo**/[jokes](https://github.com/codefellows/seattle-code-301n21/tree/main/class-06/demo)

App.js

````javascript
import React from 'react';
import axios from 'axios';

class App extends React.Component {
  constructor(props){
    super(props);
    this.state={
      jokes:[],
      randomJoke:''
    }
  }

  getJokes = async () => {
    const API = 'https://api.chucknorris.io/jokes/search?query=chuck';
    const jokes = await axios.get(API);
    this.setState({ jokes });
  }

  render() {
    return(
      <>
      <button onClick={this.getJokes}>Get Jokes</button>
      {this.state.jokes.length && this.state.jokes.map((joke, idx) => (
        <div key={idx}>
          {joke.value}
        </div>
      ))}
      </>
    )
  }
}

export default App;
````

index.js

````javascript
import React from 'react';
import ReactDOM from 'react-dom';
import App from './app';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
````
