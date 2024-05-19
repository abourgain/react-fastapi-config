# FastAPI-Uvicorn--React-Vite-Mantine Project

This repository is structured to create a web application using FastAPI for the backend and React with Vite and TailwindCSS for the frontend. Here's how you can set up and run the project on your local machine.

## Project Structure

The project is divided into two main directories:
```markdown
/fastapi-react-vite-tailwind
|-- /backend
|-- /frontend
|-- README.md
```

### Backend Setup (FastAPI)

#### Prerequisites

- Python 3.8+
- pip

#### Steps

1. **Navigate to the Backend Directory**

   ```bash
   cd backend
   ```

2. **Create and Activate a Virtual Environment**

  ```bash
  python -m venv venv
  source venv/bin/activate  # On Windows use `venv\Scripts\activate`
  ```
or
  ```bash
  conda create -n name-env python=3.10
  conda activate quote-env
  conda install fastapi uvicorn
  ```

3. **Install Dependencies**
   
  ```bash
  pip install fastapi uvicorn
  ```
or 
  ```bash
  conda install fastapi uvicorn
  ```

4. **Run the Application**
   
Create a main.py file with the following content:
  ```python
  import uvicorn
   from fastapi import FastAPI
   from fastapi.middleware.cors import CORSMiddleware
   
   from core.routers import router
   
   app = FastAPI(
       title="quote",
   )
   
   app.add_middleware(
       CORSMiddleware,
       allow_origins=["*"],
       allow_credentials=True,
       allow_methods=["*"],
       allow_headers=["*"],
   )
   
   
   @app.get("/")
   async def read_root():
       """
       Root route
       """
       return {"Hello": "World"}
   
   
   # Inclure les routes définies dans le dossier routers de core
   app.include_router(
       router,
       prefix="",
   )
   
   if __name__ == "__main__":
       uvicorn.run("main:app", host="0.0.0.0", reload=True, port=8000)

  ```

Then, start the server with:
  ```bash
  python3 main.py --no-cache
  ```

### Frontend Setup (React with Vite and TailwindCSS)

#### Prerequisites
- Node.js 14+
- npm

#### Steps

1. **Create a React Application with Vite**
   
Start by creating a new Vite project if you don’t have one set up already. The most common approach is to use Create Vite. Use the guidelines from the following [website](https://tailwindcss.com/docs/guides/vite):

  ```bash
  npm create vite@latest frontend -- --template react
  cd frontend
  ```

2. **Install Mantine**
   
Install tailwindcss and its peer dependencies, then generate your tailwind.config.js and postcss.config.js files:

  ```bash
  npm install @mantine/core @mantine/hooks
  ```

3. **PostCSS setup**

Install PostCSS plugins and postcss-preset-mantine:
   
  ```bash
  npm install --save-dev postcss postcss-preset-mantine postcss-simple-vars
  ```

Create `postcss.config.js` file at the root of your application with the following content:

   ```javascript
   export default {
     plugins: {
       "postcss-preset-mantine": {},
       "postcss-simple-vars": {
         variables: {
           "mantine-breakpoint-xs": "36em",
           "mantine-breakpoint-sm": "48em",
           "mantine-breakpoint-md": "62em",
           "mantine-breakpoint-lg": "75em",
           "mantine-breakpoint-xl": "88em",
         },
       },
     },
   };
  ```

4. **Setup**

Add styles imports and MantineProvider to your application root component (usually `main.jsx`):

  ```javascript
  import React from 'react'
  import ReactDOM from 'react-dom/client'
  import App from './App.jsx'
  import './index.css'

  import '@mantine/core/styles.css'

  import { MantineProvider } from '@mantine/core'

  ReactDOM.createRoot(document.getElementById('root')).render(
    <React.StrictMode>
      <MantineProvider>
        <App />
      </MantineProvider>
    </React.StrictMode>,
  )
  ```

5. **Start the build process**
   
Run your build process with npm run dev.

  ```bash
  npm run dev
  ```

This command will start the Vite development server and you should be able to access your React application at http://localhost:3000.

### Troubleshooting

If you encounter permission issues while running Vite, try modifying the permissions of your project directory:
  ```bash
  sudo chown -R $USER:[Your-Group] [Path-to-Your-Project]
  ```

Or give read/write access to the project folder:

  ```bash
  chmod -R 755 [Path-to-Your-Project]
  ```

Ensure your tailwind.config.js has correct paths set under the content key to detect Tailwind classes in your project files.
