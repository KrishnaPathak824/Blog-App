# Frontend

**This codebase is a blog platform which is used to create and view blog posts. It uses react-router-dom for routing and clerk for authentication. It also uses material-ui for styling in the application.**

---

The index.html is the entry point of the react application and the in the main.tsx file with DOM manipulation the root element is accessed and it is used to render App component inside the root.

![filestructure](/materials/Task2/frontend.png)

In the App.tsx, ClerkProvider wraps the component which handles the authentication in the application.
It uses the VITE_CLERK_PUBLISHABLE_KEY from .env for api calls.

![filestructure](/materials/Task2/env.png)

The react-router handles routing in our application.

- Router is the top-level component that keeps track of the browser’s URL.

- Routes is a container for all your Route definitions.

- Each Route maps a URL path to a component.

---

### 1. Navigating to root (/) will automatically redirect to the blogs listing.

### 2. Displays all blog posts at route(/blogs) and shows the AllBlogs Component.

### 3. For route (/blog/create) it checks for authentication.

- If signed in it shows the CreateBlog component

- If not signed in it show a custom modal login prompt with Google Sign-In.

### 4. For route (/blog/:id) it gives the SingleBlog component of that id.

- Dynamic route to display a single blog post.

---

## AllBlogs Component

When the user reaches to the /blogs the AllBlogs component is rendered.

The AllBlogs Component uses a custom hook useAllBlogs to get the blogs data.

The custom hook:

- Fetches data from http://localhost:3001/api/blogs using axios using the useEffect hook where it only runs when the component mounts.

- Stores blog data in blogs state using the useState hsook.

- Handles loading and error states.

The blogs data array is mapped using key into single blog with the blogs attributes.

---

## SingleBlog Component

When the user reaches to the /blogs/:id route, the SingleBlog component is rendered.

The SingleBlog Component uses custom hooks useBlog, useBlogComments, and useUserById to get the blog data, comments, and user info.

The custom hooks:

useBlog(id):

- Fetches data from http://localhost:3001/api/blogs/:id using axios inside a useEffect hook that runs when the component mounts or id changes.
- Stores blog data in blog state using the useState hook.
- Handles loading and error states.

useBlogComments(id):

- Fetches blog comments from http://localhost:3001/api/comments/:id using axios in a useEffect hook triggered on mount or id change.
- Stores comment data in comments state using useState.
- Handles loading and error states.

useUserById(userId):

- Checks if the Clerk-authenticated user exists in the backend user table by fetching data from http://localhost:3001/api/users/:id.
- Stores user data in user state.
- Handles loading state.

The blog is displayed with its title, author, created date, and content. Comments are listed below with support for adding a new comment if the user is authenticated and exists in the backend.

---

## CreateBlog Component

When the user reaches the /create-blog route, the CreateBlog component is rendered.

The CreateBlog component checks if the authenticated Clerk user exists in the backend and allows them to create a blog post.

The component:

- Uses useEffect to check if the Clerk-authenticated user exists in the backend (http://localhost:3000/api/users) by sending a GET request with the Clerk token.

- If the user does not exist, it shows a form to complete the profile by providing first name and last name.

- Handles the profile creation with a POST request to the same API, storing user data in the backend.

- If the user exists, it displays a form to create a blog by entering a title and writing content using a rich text editor.

- Uses axios to send a POST request to http://localhost:3001/api/blogs with the blog title and content, along with the Clerk token.

- Stores title, content, loading, and error states using the useState hook.

---

The flow of the application starts from the index.html where the app component is rendered and inside the app component routing is used to navigate to different routes as react is a single page application. The different routes render different components.
