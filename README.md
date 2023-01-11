# Project 2: Book Sorting React App


## Description

This was my second project in the course. We were using React.js to create an app which allows users to retrieve information about a certain authors' works and publications. And also allows the users the ability to expand the view of a specific books.

## Deployment link

https://deft-tulumba-c73cf2.netlify.app/

## Getting Started/Code Installation

The project has 1 front end repo which can be accessed in the following link: 
https://github.com/Mohamed1419/book-sorting-updated

To run you need to have Node.js installed locally and you can find the instructions to that in the following link: 
https://nodejs.org/en/download/package-manager/

run 'npm install' or 'npm i' in the terminal to start the app


## Timeframe & Working Team (Solo/Pair/Group)

In this project I was working alongside Angeline Wang, you can visit her Github in the following link: 
https://github.com/angelinewang/book-sorting
We had 9 days from 30th August 2022 to 8th September 2022 which was the deadline.

## Technologies Used

Technologies used were: 
- React.js
- JavaScript
- CSS
- Open Library books API
- GIT

## Brief Instructions

Technical Requirements Your app must:

- Consume a public API – this could be anything but it must make sense for your project.
- The app should include a router - with several "pages".
- Include wireframes - that you designed before building the app.
- Have semantically clean HTML - you make sure you write HTML that makes structural sense rather than thinking about how it might look, which is the job of CSS.
- Be deployed online and accessible to the public.

Necessary Deliverables:

- A working application, hosted somewhere on the internet
- A link to your hosted working app in the URL section of your Github repo
- A git repository hosted on Github, with a link to your hosted project, and frequent commits dating back to the very beginning of the project
- A readme.md file with:
    - Explanations of the technologies used
    - A couple of paragraphs about the general approach you took
    - Installation instructions for any dependencies
    - Link to your wireframes – sketches of major views / interfaces in your application
    - Descriptions of any unsolved problems or major hurdles your team had to overcome

## Planning

The first thing me and my partner done in the planning stage was discuss an app we would like to make which would meet all the requirements of the brief and allow us to achieve the deliverables in the brief. We discussed at length what we would want over a Zoom call and payed attention to future problems which may occur and cause us to waste precious time. At the same time we wanted to create an app which challenged us both and allowed us to use the skills we learnt in the preceding weeks. An important factor in that determining process was choosing an API which allowed us to carry out the necessary deliverables and wasn't all extremely poorly constructed. 

We decided on a book sorting app which consumed an API from The Open Library. We then drew out our plan on how thr app will look, the pages it will contain, and how it will work on an framework designing application called Excalidraw. The link to the plan is seen below:
https://excalidraw.com/#room=7c811d46bdc6ea7cc2e7,GL4RIIV6gssaegorE_eAJA

Once the framework was drawn out we started breaking the project down into its functional components and decided on who will do what. We broke the project down into four main chunks being: sorting, pagination, routing, and consuming the API. We decided to split this between us and I focused on consuming the API and the routing of the app. At the same time whenever someone was undergoing some difficulty we would help each other out whenever possible. Following this we decided to open up a Trello board and used a Kanban template in order to manage the process of building the app. We would constantly update the Trello board whenever we completed a task. The link to the Trellow board can be accessed below: 
https://trello.com/b/0PoTgDjM/project-2-react


## Build/Code Process and Challenges

```js
let params = useParams();
let [extras, setExtras] = useState([])
useEffect(() => {
    async function getExtras() {
    const res = await fetch(`https://openlibrary.org/works/${params.id}.json`)
    const extrasData = await res.json();
    setExtras(extrasData)
    }
getExtras()
}, [params.id])
```

In this code snippet I made, I had to communicate with a completely separate API from The Open Library. This is because in the original API which we used to extract the information for the books, it did not contain links to the actual cover page that we needed. Therefore I figured out that I needed to communicate with another different API but I had to use the ID of the specific book which was clicked on to extract the cover page ID. 

```js
if (specificBook) {
return (
<>
<div className="heading">
    <Link to="/">
      <button>Back</button>
    </Link>
    <div>Title: {specificBook.title}</div>
    <div>Author: {specificBook.author_name}</div>
    <div>Page count: {specificBook.number_of_pages_median ? specificBook.number_of_pages_median : "N/A"}</div>
    <div>Publish Date: {specificBook.first_publish_year}</div>
</div>
{specificBook.cover_i ?  (
  <img
  src={`https://covers.openlibrary.org/b/id/${specificBook.cover_i}-L.jpg`}
  alt={specificBook.title}
  /> 
) : <h1>No image available</h1>}
```

In this code snippet I made, I designed the page for the specific book which was clicked on from the homepage. This dynamically changed depending on what book the user clicks on and expands the details of the book utilizing the params feature and the route construction i made. I came into a problem because it turned out that not all books in the API contained a cover page, therefore i needed to cater for this and made some text which acted as a placeholder if there was no picture available for the cover. 

```js
useEffect(() => {
async function getData() {
  Promise.all([
    fetch("https://openlibrary.org/search.json?author=jrr+tolkien"),
    fetch("https://openlibrary.org/search.json?author=leo+tolstoy"),
    fetch("https://openlibrary.org/search.json?author=dan+brown"),
    fetch("https://openlibrary.org/search.json?author=jk+rowling"),
  ])
    .then((responses) =>
      Promise.all(responses.map((response) => response.json()))
    )
    .then((values) => setBooks(values));
}
getData();
}, []);
```

In this code snippet I made, we decided to only keep the app to 4 authors and extracted all their publications only. This is because the API contains a very heavy load of information for each author and the apps performance speed would be drastically affected if we decided to fetch the information for all the authors in The Open Library API. And since we did not need every author to meet our deliverables, we decided on just using these four. 

```js
return (
<Router>
  <Routes>
    <Route path="/" element={<Home books={books} />} />
    <Route path="/details/:id" element={<BookDetails books={books} />} />
  </Routes>
</Router>
);
```

In this code snippet this is where I made the routing for the application. I came across many roadblocks trying to figure out why the BookDetails component was not working (the props i wanted to pass though was not going through). I thought it was sufficient to simply include the props in the Book.js component but later when i was testing and constantly console.logging to find the problem i eventually realised after playing around with the route system that i had setup that i need to pass the proms through the route. I also worked on thsi problem together with my partner and we used liveshare on VSCode to carry out our testing.


## Wins, Bugs, and Future Improvements

- We were able to effectively use GIT to distribute work and efficiently build the app. We constantly made use of git checkout and git merge and got familiar with resolving conflicts when we merging. 
- We were able to meet all deliverables and meet the deadline date with a deployed app that we could present. 
- We worked smoothly with one another displaying strong communication skills and we knew what was going on at all times and felt comfortable with the work distribution. 
- One bug that is still in the app is that when you refresh the app on a specific books page, the whole app breaks and must be restarted.
- To enhance the app i would like to add a searchbar feature as i think that is something which will make the user experience on the app much better
- I would also like to make the app more mobile friendly because in its current state i do not think mobile users will have the most smooth and fluid experience
- I also would like to make the design of the app more modern and cutting edge as i think it is currently very old fashion looking. 

## Key Learnings/Takeaways

- In this project i very much strengthened by GIT skills, especially when it comes to using GIT with more than just myself, but rather, in a team. I familiarized myself a lot with branches and using the git checkout feature and git merge as well
- I learnt a lot about how to work alongside other engineers utilizing tools which allowed multiple people to work on alongside one another like Excalidraw, Trello, VSCode Liveshare feature, GitHub. Moreover, how to manage the project and distribute work in order to streamline the development process. 
- I learnt about using APIs in my code, and that not all APIs are exactly what you want them to be and that sometimes you need to figure out ways that are not so straightforward in order to get what you need from an API
- I learnt about deploying applications on apps like Netlify
