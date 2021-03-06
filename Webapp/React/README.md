 <br>
 <h1 align="center">Chapter Three</h1>
 <h2 align="center">Building Frontend using React.</h2>

 <p align="center">
    <a href="https://circleci.com/gh/huggingface/transformers">
        <img alt="Build" src="https://img.shields.io/badge/React-17.0.1-brightgreen?logo=React">
    </a>
    <a href="https://circleci.com/gh/huggingface/transformers">
        <img alt="Build" src="https://img.shields.io/badge/git-2.29.2-brightgreen?logo=git">
    </a>
    <a href="https://circleci.com/gh/huggingface/transformers">
        <img alt="Heroku" src="http://img.shields.io/static/v1?label=react-router-dom&message=5.2.0&color=brightgreen&logo=ReactRouter">
    </a>
    <a href="https://circleci.com/gh/huggingface/transformers">
        <img alt="Heroku" src="http://img.shields.io/static/v1?label=React-Bootstrap&message=1.4.0&color=brightgreen&logo=Bootstrap">
    </a>
    <a href="https://circleci.com/gh/huggingface/transformers">
        <img alt="Heroku" src="http://img.shields.io/static/v1?label=Build&message=pass&color=brightgreen">
    </a>
    <a href="https://circleci.com/gh/huggingface/transformers">
        <img alt="Heroku" src="http://img.shields.io/static/v1?label=Heroku&message=Deployed&color=brightgreen&logo=Heroku">
    </a>
</p>
 <br>
 
## Introduction
In this tutorial we will build a simple React App which will use the API we developed in the [Flask tutorial](https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Webapp/Flask/README.md).
> The complete code for this part can be found here: https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/tree/main/Webapp/React
## What is React?
React is javascript framework developed by Facebook developers. React is a declarative, efficient, and flexible JavaScript library for building user interfaces. It lets you compose complex UIs from small and isolated pieces of code called “components”[[ref]](https://reactjs.org/tutorial/tutorial.html). It uses virtual DOM (JavaScript object), which improves the performance of the app. The JavaScript virtual DOM is faster than the regular DOM. Its modeular we can write code for individual component and manage it saparetly. We can use ReactJS on the client and server-side as well as with other frameworks.

## Contents of this Section
* [Pre-Requisites for the section](#prerequisite)
* [Getting Started](#started)
* [File Structure](#file)
* [Components: React](#component)
* [Prediction Component](#pred)
* [Example Component](#example)
* [Main Component](#main)
* [Deploy on Heroku](#deploy)
* [Conclusions & Summary](#summary)

## <a name="prerequisite">Pre-Requisities</a>
We assume you are familiar with these concepts- 
* HTML- [Learn here](https://www.w3schools.com/html/)
* CSS- [Learn here](https://www.w3schools.com/css/)
* JavaScript- [Learn here](https://www.w3schools.com/js/DEFAULT.asp)
 

### <a name="stared">Getting started</a> 
* Before we start writing we need to setup a development environment for this you need to have `node>=8.10` and `npm>=6.5` installed. 
To create new project write the following code in terminal of a directory of your choice.
```bash
  npx create-react-app react-app
```
* To run this initial project `cd` (change directory) in to `react-app` directory and enter `npm start` in the terminal.
> It will pop up new tab in your browser serving on `Localhost 3000`
<p align="center">
    <kbd>
  <img  src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/first.png">
  </kbd>
</p> 

* Now we need to download some packages which we will use in our project.
```bash
  npm install react-router-dom
  npm install react-bootstrap
  npm install axios
  npm install http-proxy-middleware
  
      OR
  
  npm install axios http-proxy-middleware react-router-dom react-bootstrap
```
> We will look into the understanding of each package we installed later in this tutorial.

### <a name="file">File System</a> 
We need to have a clean flie structure which will help us to manage our code and easy to resolves bugs.
* We remove a few files- `logo.svg, App.css, App.test.js, index.css, favicon.ico, setupTests.js`.
* Also we add some files and folder.
    `component folder` where we store all our component files.
<table>
<tr>
<th>Initial file structure</th>
<th>Our projetc file structure</th>
</tr>
<tr>
<td>
<pre>
    react-app
    ├── README.md
    ├── node_modules
    ├── package.json
    ├── .gitignore
    ├── public
    │   ├── favicon.ico
    │   ├── index.html
    │   └── manifest.json
    └── src
        ├── App.css
        ├── App.js
        ├── App.test.js
        ├── index.css
        ├── index.js
        ├── logo.svg
        └── serviceWorker.js
        └── setupTests.js
</pre>
</td>
<td>

<pre>
    react-app
    ├── README.md
    ├── node_modules
    ├── package.json
    ├── .gitignore
    ├── public
    │   ├── index.html
    │   └── manifest.json
    └── src
        └── components  ----- (Component Folder)
        │   ├── example.js
        │   ├── main.js
        │   └── prediction.js
        ├── App.js
        ├── index.js
        ├── setupProxy.js --- To set proxy as we use external API.(Explained later in this tutorial)
        └── serviceWorker.js
</pre>
</td>
</tr>
</table>

### Before we start building our project let's talk about `react-router-dom` pacakage we have installed.
```
Many modern websites are actually made up of a single page, they just look like 
multiple pages because they contain components which render like separate pages. 
These are usually referred to as SPAs - single-page applications. At its core, 
what React Router does is conditionally render certain components to display 
depending on the route being used in the URL (/ for the home page, /about for the about page, etc.).

For example, we can use React Router to connect www.knit-with-scrimba.com/ 
to www.knit-with-scrimba.com/about or www.knit-with-scrimba.com/shop 
```
[REF](https://www.freecodecamp.org/news/react-router-in-5-minutes/)

* Although we are using only use one route for our project, it is good to learn something extra here.
  * You can read about react-router-dom here - https://reactrouter.com/web/guides/quick-start

### <a name="component">Our component structure</a> 
 * In `app.js` file we define our main component `App` and we use `react-router-dom` to access different component based on route. In our case only one `\`.
 <details> 
    <summary>See Code</summary>
    <h3 style="display:inline-block"><summary>All this code to be written in <u><i>App.js</i></u> fie. </summary></h3>
    
```js
import main from "./components/main"; // Importing MAIN component
import {
  BrowserRouter as Router,
  Route
} from "react-router-dom";

function App() {
  return (
    <div className="App">
      <Router>
          <Route exact path="/" component={main} />
      </Router>
    </div>
  );
}

export default App;


```
    
</details>

 <p align="center">
    <kbd>
  <img  src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/app.png">
  </kbd>
</p> 

 * For route `\`, we create a component `Main.js` in `components folder`. 
 * Further we divide our `MAIN` component in two parts `Prediction` and `Example`. **We can see the beauty of React here that we can modularize our frontend project and manage them individually.**
 
## <a name="pred">Prediction component</a>
* This piece code has to be written in `component/prediction.js` file.
<details> 
    <summary>See Code</summary>
    <h3 style="display:inline-block"><summary>All this code to be written in <u><i>component/prediction.js</i></u> fie. </summary></h3>
    
```js
import React, { Component} from "react";

import {
    Badge,
    Button,
    InputGroup,
    Form
  } from "react-bootstrap";
  
import axios from "axios";

class PREDICTION extends Component {
    constructor(props) {
        super(props);
        this.state = {
            review:null,
            result:null
        };
        this.onChange = this.onChange.bind(this)
        this.onSubmit = this.onSubmit.bind(this)
    }


    onChange(e) {
        this.setState({ [e.target.name]: e.target.value })
      }
  
      onSubmit(e) {
        this.setState({result: null})
          e.preventDefault()
          let data ={
              "review": this.state.review
          }
          axios.post(`/predict`, data).then(res => {
            console.log(res, "result");
            this.setState({result: res.data})
                });
      }

  render() {
    return (
          <div style={{padding:"50px", background:"#c4ffe6", height:"100%"}}>
            <h3 style={{margin:"auto", marginBottom:"20px"}}>Enter movie review here to predict positive or negative(min 200 Character).</h3>
            
            <InputGroup size="lg" style={{width:"100%"}}>
            <Form onSubmit={this.onSubmit} style={{width:"100%"}}>
                    <Form.Group >
                        <Form.Control 
                        style={{width:"100%"}}
                        size="lg"
                        as="textarea" 
                        placeholder="Enter movie review... " 
                        type="text"
                        name="review"
                        value={this.state.review}
                        onChange={this.onChange}
                        />
                        </Form.Group>
                        <Button variant="primary" type="submit" style={{marginBottom:"10px"}}>
                            Predict
                        </Button>
                </Form>
            </InputGroup>
            {this.state.review == null ? " " : <p><h4>Entered review - </h4> {this.state.review}"</p>}
            {this.state.result == null ? " " : <h4>Predicted value - <Badge variant="primary">{this.state.result.toUpperCase()}</Badge></h4>}
            
          </div>
    );
  }
}

export default PREDICTION;

```
    
</details>

* We will use this component to take input for the model and also display the result.
* To send `POST` request to the API we have created in Flask blog we use a package called `axios`.
 <p align="center">
    <kbd>
  <img  src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/axios.png">
  </kbd>
</p> 

* We define two state variable with null values.
 <p align="center">
    <kbd>
  <img  src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/state.png">
  </kbd>
</p> 

* We create a Form using `react-bootstrap` and add a `onSubmit` callback to the form. 
 * `onChange`, `onSubmit`, etc are called hooks in React, you can learn about them [here](https://reactjs.org/docs/hooks-intro.html).
 
  <p align="center">
    <kbd>
  <img  src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/hook.png">
  </kbd>
</p> 

* We define our `onSubmit` function in our `PREDICTION` component in the way given above.
* When the user clicks on submit button, the onSubmit function is executed which takes `input review` from the state varible, and changes whenever any change occurs in `Input area.`
* The above function returns the result which will be stored in the `result` variable defined in `state` and the result will be diplayed.
 
## <a name="example">Example component</a>
* This code goes into the `components/example.js` file.
<details> 
    <summary>See Code</summary>
    <h3 style="display:inline-block"><summary>All this code is to be written in <u><i>components/example.js</i></u> fie. </summary></h3>
    
```js
import React, { Component} from "react";

import {
  Badge,
  ListGroup
} from "react-bootstrap";

class EXAMPLE extends Component {

  render() {
    return (
      <div style={{padding:"50px", height:"100%"}}>
            <h3 style={{alignContent:"center"}}>Sample review to test model.</h3>
            <ListGroup>
            <ListGroup.Item variant="info">
            <h4 style={{marginBottom:"0"}}>Example 1</h4>
            <p style={{margin:"0"}}>No one expects the Star Trek movies to be high art, but the fans do expect a movie that is as good as some of the best episodes. Unfortunately, this movie had a muddled, 
            implausible plot that just left me cringing - this is by far the worst of the nine (so far) movies. Even the chance to watch the well known characters interact in another movie can't save this 
            movie - including the goofy scenes with Kirk, Spock and McCoy at Yosemite. I would say this movie is not worth a rental, 
            and hardly worth watching, however for the True Fan who needs to see all the movies, renting this movie is about the only way you'll see it - even the cable channels avoid this movie.</p>
            </ListGroup.Item>
            <ListGroup.Item variant="info">
            <h4 style={{marginBottom:"0"}}>Example 2</h4>
            <p style={{margin:"0"}}>Encouraged by the positive comments about this film on here I was looking forward to watching this film. Bad mistake. I've seen 950+ films and this is 
              truly one of the worst of them - it's awful in almost every way: editing, pacing, storyline, 'acting,' soundtrack (the film's only song - a lame country 
              tune - is played no less than four times). The film looks cheap and nasty and is boring in the extreme. Rarely have I been so happy to see the end credits
               of a film. The only thing that prevents me giving this a 1-score is Harvey Keitel - while this is far from his best performance he at least 
               seems to be making a bit of an effort. One for Keitel obsessives only.</p>
               </ListGroup.Item>
            <ListGroup.Item variant="info">
            <h4 style={{marginBottom:"0"}}>Example 3</h4>
            <p style={{margin:"0"}}>If you like original gut wrenching laughter you will like this movie. If you are young or old then you will love this movie, hell even my mom liked it.Great Camp!!!</p>
            </ListGroup.Item>
            <ListGroup.Item variant="info">
            <h4 style={{marginBottom:"0"}}>Example 4</h4>
            <p style={{margin:"0"}}>I saw this movie when I was about 12 when it came out. I recall the scariest scene was the big bird eating men dangling helplessly from parachutes 
              right out of the air. The horror. The horror.As a young kid going to these cheesy B films on Saturday afternoons, I still was tired of the 
              formula for these monster type movies that usually included the hero, a beautiful woman who might be the daughter of a professor and a happy resolution 
              when the monster died in the end. I didn't care much for the romantic angle as a 12 year old and the predictable plots. I love them now for the 
              unintentional humor.But, about a year or so later, I saw Psycho when it came out and I loved that the star, Janet Leigh, was bumped off 
              early in the film. I sat up and took notice at that point. Since screenwriters are making up the story, make it up to be as scary as possible and not 
              from a well-worn formula. There are no rules.</p>
              </ListGroup.Item>
              </ListGroup>
          </div>
    );
  }
}

export default EXAMPLE;

```
    
</details>

* This component is straight forward, we add simple text which user can copy and test our model on the fly.

## <a name="main">Main Component</a>
* In this component we combine the components we created in above section.
<details> 
    <summary>See Code</summary>
    <h3 style="display:inline-block"><summary>All this code to be written in <u><i>components/main.js</i></u> fie. </summary></h3>
    
```js
import React, { Component } from "react";
import PREDICTION from "./prediction";
import EXAMPLE from "./example";

import {
  Navbar,
  NavDropdown,
  Nav
  } from "react-bootstrap";

class Main extends Component {

  render() {
    return (
      <div>
          <Navbar collapseOnSelect expand="lg" bg="dark" variant="dark">
            <Navbar.Brand href="#home">Senti-review</Navbar.Brand>
            <Navbar.Toggle aria-controls="responsive-navbar-nav" />
            <Navbar.Collapse id="responsive-navbar-nav">
              <Nav className="mr-auto">
                <Nav.Link href="#">Jupyter Notebook</Nav.Link>
                <NavDropdown title="Tutorial Chapters" id="collasible-nav-dropdown">
                  <NavDropdown.Item href="#">Ch-1</NavDropdown.Item>
                  <NavDropdown.Item href="#">Ch-2</NavDropdown.Item>
                  <NavDropdown.Item href="#">Ch-3</NavDropdown.Item>
                </NavDropdown>
              </Nav>
              <Nav>
              <Nav.Link href="https://www.imdb.com/">Best Movies review</Nav.Link>
                <Nav.Link eventKey={2} href="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask">
                  Github
                </Nav.Link>
              </Nav>
            </Navbar.Collapse>
          </Navbar>
      
        <div style={{display:"flex",justifyContent:"center", flexDirection:"row", padding:"10px", height:"auto", width:"auto", background:"#B3E5FC"}}>
          
            <div style={{width:"50%"}}>
                <PREDICTION></PREDICTION>
            </div>
            <div style={{width:"50%"}}>
                <EXAMPLE></EXAMPLE>
            </div>
        </div>
        </div>
    );
  }
}

export default Main;

```
    
</details>

* We first import the components and combine them in a single `div`. As given below.
<p align="center">
    <kbd>
  <img  src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/main.png">
  </kbd>
</p> 


### http-proxy-middleware `Important`
Remenber downloading `http-proxy-middleware`, let's understand why we need a Http proxy middleware.  
If did not add proxy middleware then we will get error every time we make `POST` request to our Flask API.
> Error
<p align="center">
    <kbd>
  <img  src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/error.png">
  </kbd>
</p> 

> `Brief Explanation`If you don’t control the server your frontend JavaScript code is sending a request to, and the problem with the response from that server is just the lack of the necessary Access-Control-Allow-Origin header.
Read more about this issue [here](https://stackoverflow.com/questions/43871637/no-access-control-allow-origin-header-is-present-on-the-requested-resource-whe)

* **To solve this problem we use http-proxy-middleware package**.
 1. For this we have created a file `setupProxy.js` in main directory.
 2. Add the code written below, this code helps to create proxy for our `POST` request.
 ```js
 const { createProxyMiddleware } = require('http-proxy-middleware');

module.exports = function(app) {
  app.use("/predict",
    createProxyMiddleware( { target: "YOUR_FLASK_URL" ,changeOrigin: true})
  );
};

 ```

# <a name="deploy">Deployment on Heroku.</a>
We expect you have GitHub account and the knowledge of how to create repository. If not, [learn here](https://guides.github.com/activities/hello-world/)
> For React you need not to add any `Heroku` specific file as Heroku can automatically build your app.

1. **Now create a repository and push all code on github repository. If you don't know how to do that, learn it [here](https://www.datacamp.com/community/tutorials/git-push-pull)**

2. **Create New App.**
    <details> 
        <summary>Detail Screenshot</summary>
        <p align="center">
            <kbd>
              <img src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/1.png">
                </kbd>
        </p>
    </details>

3. **Choose App name and region.**
    <details> 
        <summary>Detail Screenshot</summary>
        <p align="center">
            <kbd>
              <img src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/2.png">
                </kbd>
        </p>
    </details>

4. **Link your Github account with Heroku, search your repository where you have pushed all your code and `connect`.**
    <details> 
        <summary>Detail Screenshot</summary>
        <p align="center">
            <kbd>
              <img src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/3.png">
                </kbd>
        </p>
    </details>

5. **Choose branch, `Enable automatic deploy` so that it can automatically build your app when you push any changes to your repository and hit `Deploy Branch`.**
    <details> 
        <summary>Detail Screenshot</summary>
        <p align="center">
            <kbd>
              <img src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/4.png">
                </kbd>
        </p>
    </details>

6. **You can see App Build log. It will display any errors if occurs.**
    <details> 
        <summary>Detail Screenshot</summary>
        <p align="center">
            <kbd>
              <img src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/5.png">
                </kbd>
        </p>
    </details> 
    
7. **Finally after successful build you can launch your app by clicking `View`**
    <details> 
        <summary>Detail Screenshot</summary>
        <p align="center">
            <kbd>
              <img src="https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/blob/main/Images/react/6.png">
                </kbd>
        </p>
    </details> 
    
    
***
## <a name="summary">Summary and Conclusion</a>
In this section of the blog we created a basic Frontend that uses the Flask API created in the [previous section](https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask/tree/main/Webapp/Flask). By now, we assume that you have learnt how to create a basic/ advanced text classifier, create a Flask Application and deploy it on Heroku to get an API, and incorporate a React Frontend project with this created API, and deploy the complete project on Heroku. You can now create your own text classification application and host it using Heroku. In case of any difficulties, feel free to contact us on the contact details mentioned at the end of [Section One](https://github.com/ahmadkhan242/Transfer-Learning-Model-hosted-on-Heroku-using-React-Flask).

***
### Refrence
* https://reactjs.org/tutorial/tutorial.html
* https://www.freecodecamp.org/news/react-router-in-5-minutes/
* https://stackoverflow.com/questions/43871637/no-access-control-allow-origin-header-is-present-on-the-requested-resource-whe
*** 

